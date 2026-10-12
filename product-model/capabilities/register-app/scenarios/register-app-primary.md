---
kind: primary
routes:
  application: OAuth application
steps:
- text: The Client application invokes register app.
  kind: actor
  entities: []
  contexts: &id001
    application:
      place: oauth
  actor: client-application
- text: Valid public-client metadata produces a registration
  kind: product
  entities:
  - entity: client-application
    effect: creates
    facts:
    - Name
    - Website
    - Return locations
    - Registration time
    - First approval
    to: Registered
  contexts: *id001
  actor: client-application
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/services/oauth.ts
---

# Register app

## Trigger

The Client application invokes register app.

## Outcome

Valid public-client metadata produces a registration

Valid public-client metadata produces a client ID. Redirects follow the supported HTTPS, loopback, reverse-domain scheme or out-of-band policy.

## Edge cases

- Registration is limited to five requests in ten minutes per throttle key and at most 1000 pending registrations; unused registrations expire after one hour.
