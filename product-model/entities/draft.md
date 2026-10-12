---
references:
- kind: code
  role: implementation
  target: server/db/drafts.ts
- kind: code
  role: implementation
  target: server/routes/drafts.ts
---

# Draft

An account’s synchronized unsent text and optional reply reference for a conversation.

## Information kept

- **Text** — The saved private note or unsent composition text.
- **Reply reference** — The draft’s optional owned eligible reply reference, corrected when invalid.
- **Updated at** — When the retained values were last changed.
