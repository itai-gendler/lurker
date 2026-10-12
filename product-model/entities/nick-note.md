---
references:
- kind: code
  role: implementation
  target: server/db/nickNotes.ts
- kind: code
  role: implementation
  target: server/services/verbs/setNickNote.ts
---

# Nick note

A private note for a network-scoped nick, independent of the peer’s public IRC profile.

## Information kept

- **Nick** — The nick identifying the scoped peer or annotation.
- **Text** — The saved private note or unsent composition text.
- **Updated at** — When the retained values were last changed.
