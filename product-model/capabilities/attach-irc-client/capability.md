---
availability:
- place: irc-bouncer::public
- place: irc-bouncer::personal
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Attach irc client

Credentials establish account-bound control or network mode.

Standalone registration establishes account control mode or a preselected owned-network binding. A successful completion sets the attachment to Attached and may request an upstream connection.
