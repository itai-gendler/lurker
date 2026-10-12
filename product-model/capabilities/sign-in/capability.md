---
availability:
- place: web::public
- place: client-api::public
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
---

# Sign in

Valid supported credential issues an account session.

Supported password sign-in issues a fixed-lifetime ordinary session. Web uses its cookie; the client password-token endpoint returns a bearer session. Passkey sign-in uses the challenge-cookie ceremony.
