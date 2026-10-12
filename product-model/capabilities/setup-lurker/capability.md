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

# Setup lurker

Valid first setup creates the initial Administrator account and session.

The password setup path creates the first administrative account and its ordinary session. Web first setup has password input; the supported client API also exposes a passkey ceremony. The return destination is conditional.
