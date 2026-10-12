---
appliesTo:
- type: entity
  id: data-export
  effect: removes
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
- unattended: true
references:
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/routes/exports.ts
---

# Data export removal requires the stated owner or bound entry authority

Active HTTP Owner starts; Owner reads/downloads, including permitted paused reads; unattended job progress; download attribution; expiry/cleanup removes.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
