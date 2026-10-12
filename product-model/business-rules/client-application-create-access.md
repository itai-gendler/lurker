---
appliesTo:
- type: entity
  id: client-application
  effect: creates
permits:
- actors:
  - client-application
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
---

# Client application creation requires the stated owner or bound entry authority

Create: valid standalone public registration and limits. Read: disclosed metadata. Change: cookie-authorized First approval. Remove: unattended unused-registration expiry.
