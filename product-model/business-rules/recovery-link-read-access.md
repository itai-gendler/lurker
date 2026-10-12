---
appliesTo:
- type: entity
  id: recovery-link
  effect: reads
permits:
- actors:
  - administrator
  configuredBy: account
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

# Only administrative metadata authority or the exact valid proof reads a Recovery link

The administrative alternative reads only current expiry/target metadata for the authenticated Administrator’s roster; it never recovers the raw secret from storage.

The proof alternative selects the exact hash-matched presented link, requires it unexpired and still present, and discloses only the supported standalone recovery landing information for its target. Unknown, expired, spent and superseded proof is refused without showing that an old token existed. Mere ownership of the account is not a public recovery-proof bypass.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
