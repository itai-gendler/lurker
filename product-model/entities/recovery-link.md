---
references:
- kind: code
  role: implementation
  target: server/db/accountRecovery.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
---

# Recovery link

An administrator-issued, expiring, single-use proof for replacing an account’s sign-in access.

## Information kept

- **Expires at** — The expiry recorded for this subject; expiry does not itself imply deletion of all live connections.
- **Validity** — Whether the entry proof is still usable, considering consumption, expiry, supersession or revocation.

## States

### Issued

An administrator-issued, expiring, single-use proof for replacing an account’s sign-in access.
