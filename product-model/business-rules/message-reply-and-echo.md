---
appliesTo:
- type: entity
  id: message
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Message reply and echo

Reply tags require an eligible owned same-buffer upstream identity and supported negotiation; otherwise submission follows the established fallback. Native multiline batching or splitting follows negotiation. Echo-capable paths adopt observed self echo; no-echo paths record supported local self content. A send acknowledgement does not prove recipient delivery.
