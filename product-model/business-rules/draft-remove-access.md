---
appliesTo:
- type: entity
  id: draft
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
  target: server/db/drafts.ts
- kind: code
  role: implementation
  target: server/routes/drafts.ts
---

# Draft removal requires the stated owner or bound entry authority

Only the owner clears its draft, empty valid composition clears it, or authorized parent closure/removal cleans the association. Local WS and HTTP flush have their distinct pause guards.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
