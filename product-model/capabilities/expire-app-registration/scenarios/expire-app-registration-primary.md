---
kind: primary
routes:
  application: OAuth application
steps:
- text: Unused application registration reaches its expiry.
  kind: condition
  entities: []
  contexts: &id001
    application:
      place: oauth
  unattended: true
- text: Unapproved expired registration removed unattended
  kind: product
  entities:
  - entity: client-application
    effect: removes
    from: Registered
  contexts: *id001
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts#purgeOAuth
- kind: code
  role: implementation
  target: server/services/oauth.ts
---

# Expire app registration

## Trigger

Unused application registration reaches its expiry.

## Outcome

Unapproved expired registration removed unattended

Boot/hourly cleanup removes unused registrations older than one hour; a first approval preserves the registration.
