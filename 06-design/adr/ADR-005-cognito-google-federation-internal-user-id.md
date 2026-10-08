# ADR-005: Sign-in with Google through Amazon Cognito; data keyed by an internal user id
Status        : Accepted
Date          : 2026-10-08
Deciders      : Product Owner, Architecture Lead (@abalas4)
Related       : THM01FTR01 HLD / LLD; THM01STR04, THM01STR05, THM01STR40; ADR-003, ADR-004

## Context
The MVP needs sign-in so data survives a reinstall or a phone change. The owner chose Google sign-in
first; email / password accounts may come later (RAID log, L-04) and must not force a data migration.
Mobile rule MA-04 requires the system browser for login, not an embedded web view.

## Options considered
1. **Amazon Cognito user pool (Lite tier) with Google as a federated identity provider**, OAuth 2.0
   Authorization Code + PKCE through the managed login — always free up to 10,000 monthly active users,
   social sign-in included; the app and API only ever see Cognito tokens.
2. Google Sign-In directly in the app, API validating Google ID tokens — adding native accounts later
   would change both the app and the API.
3. A self-built auth service — more code and risk for no benefit.

## Decision
**Phase A (MVP):** Cognito with Google federation only in `prod` (native sign-up disabled).
- Flow: app → system browser (PKCE, `identity_provider=Google`) → Cognito managed login → Google →
  Cognito `/oauth2/idpresponse` → code returned to the app → code + PKCE verifier exchanged for Cognito
  access / ID / refresh tokens → `Bearer <access token>` → API Gateway JWT authorizer → Lambda.
- Google side: a Google Cloud project, an External consent screen with only `openid email profile`
  (non-sensitive, no Google verification), an OAuth client of type Web application whose client is
  Cognito. The Google client secret is stored only in Cognito, read by OpenTofu from an SSM
  SecureString (state is encrypted, ADR-008) — never in the app or the repository.
- Cognito side: Lite tier pool, Google identity provider, attribute mapping (email, email_verified,
  name), a free Cognito domain prefix, a public app client (no secret, PKCE) with callback
  `com.jot.app://auth/callback`.
- **Identity design:** the API does **not** key data by the Cognito `sub`. On first sign-in it creates an
  internal `userId` (ULID) and an identity map item `IDENTITY#<sub> → userId`; all data is keyed
  `USER#<userId>`. Phase B can then link a Google user and a native user with the same verified email
  (pre-sign-up trigger, `AdminLinkProviderForUser`) without moving data. The `sub → userId` lookup is
  cached in Lambda memory.
- **Authorization:** the user id comes only from the verified token, never from the request; every key
  is scoped to the user, so another user's item returns 404 (OWASP API1). One "owner" role. Tokens in
  the Android Keystore (iOS Keychain). Sign-out revokes the refresh token at Cognito and cancels the
  phone's scheduled reminders.

**Phase B (backlog, L-04):** native email / password accounts with MFA on the same pool; no app or API
change.

## Consequences
- **Testing without Google:** Google blocks automated sign-ins, so test automation never drives the
  Google page. `local`: the dev token script signs JWTs with a local key the API trusts only when
  `ENV=local`. `dev` pool: native sign-in enabled only there, for admin-created test users (no self
  sign-up); their password lives in SSM / GitHub secrets. The Google flow is checked by hand on the
  emulator and once on Device Farm with a throwaway account. `prod`: Google only.
- Creating the Google OAuth client cannot be automated; it is an owner checklist step (README).
