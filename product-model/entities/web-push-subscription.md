---
references:
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/routes/push.ts
---

# Web Push subscription

A Web Push endpoint and delivery keys, including relay-device endpoints with the established rebinding exception.

## Information kept

- **Endpoint** — The registered Web Push delivery endpoint.
- **Delivery keys** — The Web Push encryption keys required for delivery; ordinary settings displays do not disclose them.
- **Device description** — The supplied or observed description of the registering browser or installation.
- **Enabled** — Whether this configured subject is enabled.
- **Last seen at** — Most recently recorded heartbeat, registration or successful delivery activity.
- **Delivery health** — Recorded failure streak and delivery status used for disable/removal policy.
- **Authorization association** — The optional OAuth access association whose revocation removes the registration.
