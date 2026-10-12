---
appliesTo:
- type: entity
  id: draft
references:
- kind: code
  role: implementation
  target: server/db/drafts.ts
- kind: code
  role: implementation
  target: server/routes/drafts.ts
---

# Draft last write

The last received text/reply replaces the draft and fans out. Empty text without a reply removes it. Invalid/unowned reply references are dropped while supported text remains; legacy omitted reply fields keep the established compatibility behavior.
