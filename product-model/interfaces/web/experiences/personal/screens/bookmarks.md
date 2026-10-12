---
entities:
- entity: bookmark
  shows:
  - Saved at
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
  target: server/routes/bookmarks.ts
- kind: code
  role: implementation
  target: server/db/bookmarks.ts
---

# Bookmarks

Saved-message association, Saved at and Message facts. Collects supported filters.
