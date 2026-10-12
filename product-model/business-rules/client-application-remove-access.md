---
appliesTo:
- type: entity
  id: client-application
  effect: removes
permits:
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
---

# Client application removal follows unused-registration expiry

Create: valid standalone public registration and limits. Read: disclosed metadata. Change: cookie-authorized First approval. Remove: unattended unused-registration expiry.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.
