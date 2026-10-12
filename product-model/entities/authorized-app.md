---
relations:
- entity: web-push-subscription
  verb: has-registration
  cardinality: one-to-many
- entity: native-push-device
  verb: has-registration
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
---

# Authorized app

An account’s approval of a registered application and the access issued under that association.

## Information kept

- **Approval** — The account’s recorded application approval and authorization time, derived from its earliest still-retained application access token. This is distinct from the application’s first approval across all accounts.
- **Issued access** — Access tokens and associated authorization-code issuance under the application association.
- **Last used at** — Most recently recorded credential or authorization use.

## States

### Approved

An account’s approval of a registered application and the access issued under that association.
