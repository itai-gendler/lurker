---
type: api
actors:
- user
- administrator
references:
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: docs/CLIENT_PROTOCOL.md
entryPoints:
- api: /api/config
- api: /ws
---

# Client API

The documented REST and WebSocket client contract exposes supported account operations. Its qualified administration contract is for administrator tools; availability does not imply native interface parity.
