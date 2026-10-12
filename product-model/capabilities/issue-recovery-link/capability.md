---
availability:
- place: web::administration
- place: client-api::administration
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
domain: administration-users
---

# Issue recovery link

New single-use recovery link issued.

Standalone issuance creates a 24-hour recovery proof, supersedes earlier access links and returns the URL for administrator hand-off.
