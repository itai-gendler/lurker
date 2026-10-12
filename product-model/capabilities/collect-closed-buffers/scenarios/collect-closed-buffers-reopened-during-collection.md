---
kind: exception
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The closed-subject maintenance schedule examines old closed conversations.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::buffers
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  unattended: true
- text: Reopening prevents otherwise pending unattended collection
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Visibility
  - entity: direct-message
    effect: reads
    facts:
    - Visibility
  contexts: *id001
references:
- kind: code
  role: implementation
  target: server/services/retentionSweeper.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
---

# Collect closed buffers reopened during collection

## Trigger

The Product observes an otherwise eligible closed subject reopen before collection completes.

## Outcome

Reopening prevents otherwise pending unattended collection
