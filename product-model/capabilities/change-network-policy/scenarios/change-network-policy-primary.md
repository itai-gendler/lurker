---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator submits the instance host and proxy policy.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::networks
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Instance host policy changes
  kind: product
  entities:
  - entity: instance-settings
    effect: changes
    facts:
    - Network policy
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminNetworks.ts
---

# Change network policy

## Trigger

The Administrator invokes change network policy.

## Outcome

Instance host policy changes

Validated network offering/policy changes retain a usable enabled preset when lockdown requires it.

## Edge cases

- The actual policy constrains future creation/connect paths; it does not infer unrestricted fleet administration.
