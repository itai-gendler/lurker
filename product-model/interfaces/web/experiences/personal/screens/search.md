---
entities:
- entity: message
  shows:
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
references:
- kind: code
  role: implementation
  target: server/routes/search.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
---

# Search

Matching Message and reply-context facts. Collects search terms and supported scope.
