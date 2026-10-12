---
appliesTo:
- type: entity
  id: recovery-link
  effect: changes
permits:
- actors:
  - user
  - administrator
  configuredBy: recovery-link
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
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAdmin
---

# Only the exact valid recovery proof spends its Recovery link

Select the presented hash-matched, unexpired link and its bound account in standalone edition. Password recovery validates replacement input before atomically spending and setting it. Passkey recovery also requires the valid signed recovery-purpose challenge bound to that exact link/account and successful WebAuthn proof; the spend/enroll transaction preserves the established duplicate-credential rollback. A parallel, revoked or superseded link cannot win spending twice.

The proof is an authentication input. There is no personal-owner alternative that treats a missing or invalid presented link as valid.
