---
appliesTo:
- type: entity
  id: highlight-rule
  effect: removes
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
---

# Highlight rule removal requires the stated owner or bound entry authority

Only the authenticated unpaused owner removes personally editable rules. Automatic-origin rules are not personally removable; automatic maintenance and authorized parent cleanup retain their own boundaries.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

An eligible authenticated import has a separate account-scoped replacement/failed-insertion cleanup path in importService. It removes the affected retained roots as that import’s replacement or reset requires; upload cleanup removes local history metadata and does not assert provider-byte deletion. This exception requires the current unpaused importing account, zero-network entry guard and the actual validated replacement attempt. It is not a general bypass of interactive deletion guards.
