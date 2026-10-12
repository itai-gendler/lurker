---
appliesTo:
- type: entity
  id: irc-client
  effect: changes
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
- unattended: true
  when:
  - entity: instance-settings
    fact: Edition
    is: standalone
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# IRC client changes require the stated owner or bound entry authority

The authenticated attachment negotiates its own extensions and preregistration binding and reports its own presence. Post-registration rebinding is forbidden. The attachment’s credentials and bound network determine the acting account; control mode is not an arbitrary writable network.

Unattended permission is limited to the attributable received event, expiry, delivery-health update or eligible maintenance/parent cleanup described for this operation; it does not authorize arbitrary scheduled account mutation.

The Account-configured owner grant selects the person’s actual validated registration or already registered attachment and its retained account/binding, not an arbitrary account named in a later command. Pre-registration BIND remains constrained to eligible owned networks; CAP and presence changes apply only to this attachment. A later command cannot change its registered account or network.
