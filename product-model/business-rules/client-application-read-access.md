---
appliesTo:
- type: entity
  id: client-application
  effect: reads
permits:
- actors:
  - user
  - administrator
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
---

# Client application disclosure requires the stated owner or bound entry authority

Create: valid standalone public registration and limits. Read: disclosed metadata. Change: cookie-authorized First approval. Remove: unattended unused-registration expiry.
