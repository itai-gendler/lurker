---
kind: system
acts: external
relations:
- entity: authorized-app
  verb: has-authorization
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
---

# Client application

A registered public OAuth application identified by a client ID. Registration does not authenticate the application.

## Information kept

- **Name** — The name displayed for this subject.
- **Website** — The optional application website shown during approval.
- **Return locations** — Registered return locations accepted by the OAuth redirect policy.
- **Registration time** — When the application registration was created.
- **First approval** — When this registration first gained account approval; approved registrations escape unused-registration expiry.

## States

### Registered

A registered public OAuth application identified by a client ID. Registration does not authenticate the application.
