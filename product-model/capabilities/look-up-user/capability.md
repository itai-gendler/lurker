---
availability:
- place: web::personal
- place: client-api::personal
- place: irc-bouncer::personal
- place: mcp
references:
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/services/verbs/whois.ts
---

# Look up user

WHOIS requested; profile or asynchronous result exposed.

WHOIS requests observation. Web/profile results can be partial; MCP acknowledges the write-scope request and later output requires a separate history read.
