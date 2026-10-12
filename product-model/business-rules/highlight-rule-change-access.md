---
appliesTo:
- type: entity
  id: highlight-rule
  effect: changes
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
---

# Highlight rule changes require the stated owner or bound entry authority

Only the authenticated unpaused owner edits a personally editable rule. Automatic-origin rules cannot be personally edited; attributable nick changes maintain them.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
