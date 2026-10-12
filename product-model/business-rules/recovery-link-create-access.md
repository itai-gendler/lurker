---
appliesTo:
- type: entity
  id: recovery-link
  effect: creates
permits:
- actors:
  - administrator
  configuredBy: account
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
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

# Only the authenticated standalone Administrator issues a Recovery link

Select the actual current caller’s administrative Account authority and an existing target account. Issuance creates a fresh single-use link for that target and supersedes its previous outstanding link. Being the target account’s owner is not an issuance grant. The raw link is revealed only in the issuance response; subsequent metadata does not disclose its secret.

The Account-configured administrative grant selects the current caller’s actual authenticated account, using requireAuth’s valid signed ordinary-session cookie or accepted ordinary-session/OAuth bearer. The caller must hold the fixed Administrator identity. A mutating HTTP request additionally requires that caller’s current account unpaused; administrative GET/HEAD reads retain paused read access. The caller and targeted account are distinct inputs: this decision does not test the target’s Pause status in place of the caller’s. Edition, valid-target and protected-subject conditions remain conjunctive. This administrative alternative grants no private IRC-history access.
