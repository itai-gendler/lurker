---
availability:
- place: web::administration
- place: client-api::administration
references:
- kind: code
  role: implementation
  target: server/routes/adminPush.ts
- kind: code
  role: implementation
  target: server/services/push/relayStatus.ts
- kind: code
  role: implementation
  target: server/services/push/relay.ts
---

# Change instance notifications settings

Relay policy/status process completes.

Relay opt-in and explicit status checking use their supported administrative paths. An explicit check may contact the relay while delivery is disabled; superseded asynchronous results cannot overwrite newer policy.
