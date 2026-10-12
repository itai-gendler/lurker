---
appliesTo:
- type: entity
  id: session
- type: entity
  id: api-token
- type: entity
  id: authorized-app
- type: entity
  id: passkey
references:
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/webauthnCredentials.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
---

# Credential surface separation

Ordinary session cookies/bearers and OAuth access authenticate supported REST/WS paths; scoped API tokens authenticate MCP but are not ordinary REST/WS sessions. Bouncer supports its password/read-write API-token registration and not OAuth. HTTP FILEHOST Basic accepts its username/password, read-write API-token or OAuth fallback; its bearer path accepts ordinary session/OAuth credentials, not cookies. An ordinary session token is not accepted as a Basic password. Passkey setup/addition/entry retains signed challenge-cookie binding; human OAuth approval requires a cookie and approval-only displayed-account match. Public OAuth IDs identify rather than authenticate the app; code binding and PKCE are exchange proofs.
