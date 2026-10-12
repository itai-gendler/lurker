---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User marks this nick with a supported envelope template.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::profile
    client:
      place: client-api::personal
  actor: user
- text: For a previously unmarked nick, the Product records the relay-bot nick, envelope template and creation time.
  kind: product
  entities:
  - entity: relay-bot
    effect: creates
    facts:
    - Nick
    - Envelope template
    - Created at
    as: new-relay-bot
  contexts: *id001
  actor: user
- text: For an existing relay-bot nick, the Product replaces its trimmed envelope template.
  kind: product
  entities:
  - entity: relay-bot
    effect: changes
    facts:
    - Envelope template
    as: existing-relay-bot
  contexts:
    web:
      place: web::personal::profile
    client:
      place: client-api::personal
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/services/verbs/setRelayBot.ts
---

# Mark relay bot

## Trigger

The User invokes mark relay bot.

## Outcome

Nick/template mark saved

The network/nick envelope mark is saved or replaced. Supported templates unwrap display attribution with bounded nesting while retaining original content.

## Edge cases

- The mark does not prove the embedded sender’s identity. Invalid templates do not produce invented attribution.

## Decision points

### Existing selected record

Does the selected record already exist?

- Absent record → create it with its supported initial/default values.
- Existing record → update that same selected record; no independent duplicate is created.
