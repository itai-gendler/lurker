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
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
---

# Recover account

Valid recovery replaces prior access and issues a fresh session.

Recovery consumes the single-use proof, replaces prior password/passkey access, invalidates ordinary sessions, revokes delegated access and closes associated live access. A separate completion step issues fresh access. Web success returns into chat.
