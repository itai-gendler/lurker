---
appliesTo:
- type: entity
  id: data-export
  effect: reads
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
- unattended: true
references:
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/routes/exports.ts
---

# Data export disclosure requires the stated owner or bound entry authority

Only the authenticated owner reads progress or downloads the owned ready/present artifact. Permitted paused reads remain allowed; readiness/expiry/missing artifact checks still apply.

Unattended retention maintenance consults in-flight archive progress solely to enforce deferral.
