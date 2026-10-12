---
references:
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/routes/push.ts
---

# Native push device

An APNs or FCM installation registration with an opaque transport token and account association.

## Information kept

- **Transport** — The supported APNs or FCM delivery transport.
- **Installation token** — The opaque native installation token.
- **Device description** — The supplied or observed description of the registering browser or installation.
- **Enabled** — Whether this configured subject is enabled.
- **Last seen at** — Most recently recorded heartbeat, registration or successful delivery activity.
- **Delivery health** — Recorded failure streak and delivery status used for disable/removal policy.
- **Authorization association** — The optional OAuth access association whose revocation removes the registration.
