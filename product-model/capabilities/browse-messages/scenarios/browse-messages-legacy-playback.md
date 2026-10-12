---
kind: path
routes:
  irc: IRC bouncer
steps:
- text: The established presence or startup condition is observed.
  kind: condition
  entities: []
  contexts: &id001
    irc:
      place: irc-bouncer::personal
  unattended: true
- text: Attachment triggers bounded automatic playback when the history extension is absent. No downstream
    actor initiates a separate request in this path.
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
  contexts: *id001
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

# Browse messages legacy playback

## Trigger

The User attaches an IRC client without the on-demand history extension.

## Outcome

Attachment triggers bounded automatic playback when the history extension is absent. No downstream actor initiates a separate request in this path.
