---
kind: validation
routes:
  irc-registration: IRC registration
steps:
- text: The User registers an downstream attachment with invalid credentials, a paused member identity, an
    exceeded attachment limit or an invalid configured upstream binding.
  kind: actor
  entities: []
  contexts: &id001
    irc-registration:
      place: irc-bouncer::public
  actor: user
- text: Invalid credentials, pause, limit or invalid binding refuses attachment
  kind: product
  entities: []
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Attach irc client refused

## Trigger

The User registers an IRC client with invalid credentials, a paused account, an exceeded attachment limit or an invalid network binding.

## Outcome

Invalid credentials, pause, limit or invalid binding refuses attachment
