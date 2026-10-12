---
kind: primary
routes:
  irc-registration: IRC registration
  irc: IRC bouncer
steps:
- text: The User invokes attach irc client.
  kind: actor
  entities:
  - entity: irc-client
    effect: reads
    facts: []
  contexts: &id001
    irc-registration:
      place: irc-bouncer::public
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Credentials establish account-bound control or network mode
  kind: product
  entities:
  - entity: irc-client
    effect: creates
    facts:
    - Registration
    - Network binding
    - Negotiated extensions
    - Credential association
    - Presence contribution
    to: Registering
  - entity: account
    effect: reads
    facts: []
  - entity: network
    effect: reads
    facts: []
  contexts: *id001
  actor: user
- text: The Product completes downstream registration in the selected binding.
  kind: product
  entities:
  - entity: irc-client
    effect: changes
    facts:
    - Registration
    - Network binding
    - Negotiated extensions
    - Presence contribution
    to: Attached
    from: Registering
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Attach irc client

## Trigger

The User invokes attach irc client.

## Outcome

Credentials establish account-bound control or network mode

Standalone registration establishes account control mode or a preselected owned-network binding. A successful completion sets the attachment to Attached and may request an upstream connection.

## Edge cases

- PASS and supported SASL PLAIN accept password or read-write API credentials, not OAuth. Sole-network selection and capability-aware control mode follow their established registration paths.
- Attachment limits, pause, invalid credentials or binding refuse registration. Binding cannot be changed after registration.
