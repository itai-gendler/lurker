---
kind: path
routes:
  irc: IRC bouncer
steps:
- text: The User requests supported timestamp history after negotiating the history extension.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    irc:
      place: irc-bouncer::personal
  actor: user
- text: The supported BEFORE/AFTER/LATEST/AROUND/BETWEEN timestamp query returns oldest-first bounded playback.
    TARGETS excludes closed subjects even though their target history can still be read. Event/reaction playback
    follows negotiated extensions.
  kind: product
  entities:
  - entity: message
    effect: reads
    facts:
    - Sender
    - Content
    - Kind
    - Time
    - Self attribution
    - Upstream identity
    - Reply context
    - Highlight information
    - Ignore information
    - Encryption indication
  - entity: reaction
    effect: reads
    facts: []
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/routes/search.ts
- kind: code
  role: implementation
  target: server/routes/activity.ts
- kind: code
  role: implementation
  target: server/routes/bookmarks.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
- kind: code
  role: implementation
  target: server/services/verbs/recentMessages.ts
- kind: code
  role: implementation
  target: server/services/verbs/searchMessages.ts
- kind: code
  role: implementation
  target: vue_client/src/lib/historyPaging.ts
---

# Browse messages timestamp history

## Trigger

The User requests supported timestamp history after negotiating the history extension.

## Outcome

The supported BEFORE/AFTER/LATEST/AROUND/BETWEEN timestamp query returns oldest-first bounded playback. TARGETS excludes closed subjects even though their target history can still be read. Event/reaction playback follows negotiated extensions.
