---
type: web
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
- web: /
---

# Web

The web client, including mobile web and PWA use, presents account entry, personal IRC conversations and instance administration.
