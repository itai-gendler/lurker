---
relations:
- entity: account
  verb: admits
  cardinality: one-to-one
references:
- kind: code
  role: implementation
  target: server/db/invites.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Invite

An expiring, single-use invitation issued by an administrator to admit an account.

## Information kept

- **Expires at** — The cutoff after which the invitation proof cannot be redeemed; expiry is checked together with consumption.
- **Redeemed at** — When the invitation was consumed.
- **Validity** — Whether the entry proof is still usable, considering consumption, expiry, supersession or revocation.

## States

### Available

The invitation has not been consumed. Its expiry and Validity separately decide whether that unconsumed proof can be redeemed.

### Consumed

The invitation has been successfully redeemed.
