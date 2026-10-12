---
type: messaging
actors:
- user
- administrator
references:
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# IRC bouncer

The standalone IRC bouncer registers a downstream client to an account and an existing network or control mode. Attachments share the account’s upstream identity.
