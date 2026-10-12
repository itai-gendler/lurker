---
appliesTo:
- type: entity
  id: irc-client
  effect: creates
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
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: account
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
  - entity: account
    fact: Pause status
    is: Active
  - entity: api-token
    fact: Scope
    is: read-write
  configuredBy: api-token
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
  - entity: account
    fact: Pause status
    is: Active
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
  - entity: account
    fact: Pause status
    is: Active
  - entity: api-token
    fact: Scope
    is: read-write
  configuredBy: api-token
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
- kind: code
  role: implementation
  target: server/db/apiTokens.ts#findActiveByHash
- kind: code
  role: implementation
  target: server/db/users.ts
---

# Only matched standalone account credentials admit an IRC client

The Account-configured alternative selects the username actually supplied through supported PASS/SASL PLAIN and requires that account’s matching password proof. The API-token-configured alternative selects the exact presented token hash, requires it active/nonrevoked, read-write and owned by that same selected username’s account; an arbitrary other token owned by the account is never substituted. Ordinary sessions and OAuth tokens are not bouncer passwords. Both paths require that account unpaused, current connection limits respected and any preselected binding resolved to an eligible owned network before registration completes. A capability-aware unbound control connection and the supported sole-network fallback retain their explicit registration rules. The registered attachment retains its credential association for later targeted revocation.
