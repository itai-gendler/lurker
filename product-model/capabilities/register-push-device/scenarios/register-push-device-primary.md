---
kind: primary
routes:
  client: Client API
steps:
- text: The User invokes register push device.
  kind: actor
  entities: []
  contexts: &id001
    client:
      place: client-api::personal
  actor: user
- text: For a new installation token, the Product records native transport, device description, enabled defaults,
    seen time, health and authorization association.
  kind: product
  entities:
  - entity: native-push-device
    effect: creates
    facts:
    - Transport
    - Installation token
    - Device description
    - Enabled
    - Last seen at
    - Delivery health
    - Authorization association
    as: new-native-push-device
  contexts: *id001
  actor: user
- text: For the same transport class, for the same installation token, the Product replaces native transport and
    the latest authorization association, preserves an omitted device description, enables delivery and resets health.
  kind: product
  entities:
  - entity: native-push-device
    effect: changes
    facts:
    - Transport
    - Device description
    - Enabled
    - Last seen at
    - Delivery health
    - Authorization association
    as: existing-native-push-device
  contexts:
    client:
      place: client-api::personal
  actor: user
- text: When a same-owner endpoint registration changes transport class, the Product replaces the predecessor’s
    transport-specific subject with the accepted incoming registration.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: removes
  - entity: native-push-device
    effect: creates
    facts:
    - Transport
    - Installation token
    - Device description
    - Enabled
    - Last seen at
    - Delivery health
    - Authorization association
    as: replacement-native-push-device
  contexts:
    client:
      place: client-api::personal
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/services/pushService.ts
- kind: code
  role: implementation
  target: server/services/push/index.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Register push device

## Trigger

The User invokes register push device.

## Outcome

Valid supported native installation registered

A validated installation token for a configured supported native sender is registered or rebound under the stored/incoming native transport checks.

## Edge cases

- Cross-account mixed native/browser collisions refuse registration. The latest registration replaces the authorization association and resets delivery health.

## Decision points

### Existing selected record

Does the selected record already exist?

- Absent record → create it with its supported initial/default values.
- Existing same-class record → update that selected record without an independent duplicate.
- Existing other-class record owned by this same account → overwrite the endpoint’s transport-specific registration using the validated incoming fields; this does not delete a provider endpoint.
