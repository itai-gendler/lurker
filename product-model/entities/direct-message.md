---
relations:
- entity: message
  verb: contains
  cardinality: one-to-many
- entity: draft
  verb: contains
  cardinality: one-to-many
- entity: pin
  verb: contains
  cardinality: one-to-many
- entity: favorite-buffer
  verb: contains
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Direct message

A private-message subject on one network, with its own visibility, peer observations and retained history view state.

## Information kept

- **Target** — The network-folded IRC target identifying the subject.
- **Visibility** — Whether the retained conversation is open or closed in the personal view.
- **Peer presence** — Last observed peer presence for the direct-message subject.
- **Read boundary** — The monotonic personal read pointer in this subject’s own sequence.
- **Clear boundary** — The reversible display-clear boundary; it neither deletes history nor advances the read pointer.
- **Unread counts** — The bounded derived unread and highlight counts under the subject’s actual counting rules.
- **Retention override** — The conversation’s retention override or inheritance, bounded by effective instance ceilings.
- **Events** — Recorded conversation activity presented with the conversation.

## States

### Open

The conversation is visible in the personal view.

### Closed

The retained conversation is hidden from that view.
