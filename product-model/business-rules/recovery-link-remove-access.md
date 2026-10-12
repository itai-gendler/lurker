---
appliesTo:
- type: entity
  id: recovery-link
  effect: removes
permits:
- actors:
  - administrator
  configuredBy: account
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
- actors:
  - user
  - administrator
  configuredBy: recovery-link
- unattended: true
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
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAdmin
---

# Only administrative revocation, valid proof spending or eligible cleanup removes a Recovery link

The administrative alternative revokes only the outstanding link for the requested target under the current standalone Administrator’s authenticated write authority.

The proof alternative removes the exact presented, still-live link as successful supported password/passkey recovery spends it for its bound account. It requires the corresponding validated replacement method and, for passkey recovery, the signed challenge/link/account match and verification; it is not arbitrary owner deletion.

Unattended removal is limited to expired rows, supersession after authorized new issuance, and parent-account cleanup. Each uses the selected row’s actual expiry or authorized target; no cleanup invents a general anonymous revoke path.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
