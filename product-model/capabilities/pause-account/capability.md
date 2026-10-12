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
domain: administration-users
---

# Pause account

Target paused; live IRC/bouncer access stopped.

Standalone pause stops target IRC/bouncer access and retains data. Existing WebSocket connections can remain under their exact operation guards.
