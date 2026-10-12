---
appliesTo:
- type: entity
  id: highlight-rule
  effect: creates
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: account
    fact: Pause status
    is: Active
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: account
    fact: Pause status
    is: Active
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/highlightRules.ts
- kind: code
  role: implementation
  target: server/services/highlightRulesService.ts
- kind: code
  role: implementation
  target: server/services/importService.ts
- kind: code
  role: implementation
  target: server/db/exportSchema.ts
---

# Highlight rule creation requires the stated owner or bound entry authority

HTTP Owner; personal editing/removal only for nonautomatic rules; unattended automatic nick-rule maintenance.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

Eligible archive restoration keeps its separate zero-network, archive-validation and replacement conditions; it does not infer that every restored row passes the interactive add form’s ceremony or creation-policy check.
