---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User requests surrounding history for an anchor that is no longer available.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
  actor: user
- text: The established missing-anchor result/fallback is surfaced; unavailable retained context is not invented.
  kind: product
  entities: []
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

# Browse messages missing anchor

## Trigger

The User requests surrounding history for an anchor that is no longer available.

## Outcome

The established missing-anchor result/fallback is surfaced; unavailable retained context is not invented.
