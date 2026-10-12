---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes browse messages.
  kind: actor
  entities:
  - entity: message
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Retained owned history read through the applicable paging/search contract
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

# Browse messages

## Trigger

The User invokes browse messages.

## Outcome

Retained owned history read through the applicable paging/search contract

Retained owned history supports bounded latest/before/after/around slices, search, activity and bookmarks. It is readable while the upstream is offline. Hydration does not JOIN or reopen a closed subject.

## Edge cases

- WS limits are 1–500; around can return 2×limit+1. Continuous scanning is bounded. Request tokens reject stale web responses.
- Search terms use whitespace AND matching with supported sender, conversation and network scopes, newest first.
- Bouncer CHATHISTORY uses timestamps rather than msgid selectors, exclusive bounds and bounded 0–1000 requests; malformed requests are rejected, not silently clamped.
- Bouncer playback preserves ignored senders and can expose persisted decrypted plaintext without original upstream identity/reply tags. Live raw delivery has a different representation.
