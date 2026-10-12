---
availability:
- place: web::personal
- place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/sessions.ts
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/services/webauthn.ts
domain: account
---

# Add passkey

Valid cookie-backed ceremony registers a credential.

The signed challenge-cookie registration ceremony verifies the credential before saving it.
