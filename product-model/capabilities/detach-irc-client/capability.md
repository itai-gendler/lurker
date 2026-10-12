---
availability:
- place: irc-bouncer::personal
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Detach irc client

Downstream attachment ends while upstream remains.

The downstream client departs; shared upstream connections and retained history remain.
