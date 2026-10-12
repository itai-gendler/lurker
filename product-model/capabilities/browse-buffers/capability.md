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
  target: server/services/verbs/listBuffers.ts
---

# Browse buffers

Surface-specific enumeration of owned conversation subjects.

Web/API hydration enumerates owned subjects. MCP aggregates message-bearing channel/DM targets, excluding server/system/DCC subjects and without filtering closed status. Bouncer control/attachment contracts differ.
