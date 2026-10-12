---
appliesTo:
- type: capability
  id: look-up-user
- type: capability
  id: connect-network
- type: capability
  id: disconnect-network
- type: entity
  id: network-log
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Network output recorded

Established network/server output is recorded in the owned Network log and presented through its retained history and notable-count contract.

The Rule records only the established output/event emitted by these operations at their inspected logging call sites; it is not a guarantee that every request, refusal or underlying packet creates an entry.
