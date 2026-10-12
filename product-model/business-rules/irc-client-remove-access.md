---
appliesTo:
- type: entity
  id: irc-client
  effect: removes
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
  configuredBy: account
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
  configuredBy: account
- actors:
  - administrator
  configuredBy: account
  when:
  - &id001
    entity: instance-settings
    fact: Edition
    is: standalone
- actors:
  - user
  - administrator
  configuredBy: recovery-link
  when:
  - *id001
- unattended: true
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
---

# Registered departure, qualified administrative control or credential cleanup closes an IRC client

The Account-configured owner grant selects the actual registered attachment for departure, or the authenticated account’s exact token-revocation operation and the clients associated with that token. Departing the bouncer leaves the shared upstream and history in place. Ordinary session logout does not promise closure of every downstream attachment.

The separate Administrator grant selects the current authenticated, unpaused administrative caller and the actual permitted pause/deletion target. Pause cannot target that caller’s own account; deletion also retains the self/final-administrator protections. These authorized control operations close that target’s live bouncer clients without granting its private-history reads.

The Recovery-link-configured exception spends the exact live proof through successful credential replacement for its bound account and closes that recovered account’s prior bouncer clients, even if the target is paused. It grants no anonymous arbitrary attachment closure.

Unattended removal is limited to attachment disconnect/failure, eligible socket cleanup and targeted credential/account revocation callbacks. Every closure concerns the registered attachment or the independently authorized target; it grants no unrelated account control.
