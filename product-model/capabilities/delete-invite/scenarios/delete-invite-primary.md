---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes delete invite.
  kind: actor
  entities:
  - entity: invite
    as: invite-available
    effect: reads
    facts: []
  - entity: invite
    as: invite-consumed
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::invites
    admin-client:
      place: client-api::administration
  actor: administrator
- text: The Product removes the selected invitation in its current available or consumed state.
  kind: product
  entities:
  - entity: invite
    effect: removes
    from: Available
    as: invite-available
  - entity: invite
    effect: removes
    from: Consumed
    as: invite-consumed
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
---

# Delete invite

## Trigger

The Administrator invokes delete invite.

## Outcome

Invitation removed

Removing an invitation does not remove the admitted member or revive a consumed proof.

Only the selected invitation is removed; the state-specific aliases denote the applicable retained row, not two deletions.
