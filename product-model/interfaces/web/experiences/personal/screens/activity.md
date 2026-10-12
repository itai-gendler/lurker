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
- entity: reaction
  shows:
  - Value
  - Reacting identity
  - Self attribution
  - Reacted at
  - Removed at
references:
- kind: code
  role: implementation
  target: server/routes/activity.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
---

# Activity

Message highlight and Reaction facts. Collects supported filters.
