---
appliesTo:
- type: entity
  id: ignore-rule
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
  target: server/db/ignoredMasks.ts
- kind: code
  role: implementation
  target: server/services/ignoreRulesService.ts
---

# Ignore rule removal requires the stated owner or bound entry authority

Owner through actual HTTP/WS guards, valid matching/scope fields; duplicate refresh and unattended expiry.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
