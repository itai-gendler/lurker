---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes edit nick note.
  kind: actor
  entities:
  - entity: nick-note
    effect: reads
    facts: []
    as: existing-nick-note
  contexts: &id001
    web:
      place: web::personal::nick-note
    client:
      place: client-api::personal
  actor: user
- text: When no scoped note exists, the Product saves trimmed private text and its update time.
  kind: product
  entities:
  - entity: nick-note
    effect: creates
    facts:
    - Nick
    - Text
    - Updated at
    as: new-nick-note
  contexts: *id001
  actor: user
- text: For the existing scoped note, the Product replaces private text and update time and synchronizes the result.
  kind: product
  entities:
  - entity: nick-note
    effect: changes
    facts:
    - Text
    - Updated at
    as: existing-nick-note
  contexts:
    web:
      place: web::personal::nick-note
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
  target: server/services/verbs/setNickNote.ts
---

# Edit nick note

## Trigger

The User invokes edit nick note.

## Outcome

Private note saved/changed

A network-scoped nick note is saved, trimmed and synchronized. Absent notes are created; text is limited to 4096 characters.

## Decision points

### Existing selected record

Does the selected record already exist?

- Absent record → create it with its supported initial/default values.
- Existing record → update that same selected record; no independent duplicate is created.
