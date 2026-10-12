---
entities:
- entity: nick-note
  shows:
  - Nick
  - Text
  - Updated at
  collects:
  - Text
references:
- kind: code
  role: implementation
  target: server/services/verbs/getNickNote.ts
- kind: code
  role: implementation
  target: server/services/verbs/setNickNote.ts
---

# Nick note

Nick-note nick/text/time. Collects note text.
