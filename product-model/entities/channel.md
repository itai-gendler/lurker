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

# Channel

An IRC channel subject with independently kept visibility, membership, join intent, history view state and upstream observations.

## Information kept

- **Target** — The network-folded IRC target identifying the subject.
- **Visibility** — Whether the retained conversation is open or closed in the personal view.
- **Joined status** — Confirmed observed channel membership, independent of visibility and requested join intent.
- **Autojoin** — Persisted intent to rejoin the channel.
- **Channel key** — The retained channel join key where supported.
- **Topic** — The current or last-known observed channel topic.
- **Members** — Observed channel membership and supported role information.
- **Modes** — Observed channel modes.
- **Mode lists** — Results of supported live IRC list-mode queries.
- **Read boundary** — The monotonic personal read pointer in this subject’s own sequence.
- **Clear boundary** — The reversible display-clear boundary; it neither deletes history nor advances the read pointer.
- **Unread counts** — The bounded derived unread and highlight counts under the subject’s actual counting rules.
- **Retention override** — The conversation’s retention override or inheritance, bounded by effective instance ceilings.
- **Notification override** — The channel’s supported notification override.
- **Encryption status** — The observed enabled encrypted-channel transport status; stored decrypted history can remain plaintext.
- **Events** — Recorded conversation activity presented with the conversation.

## States

### Open

The conversation is visible in the personal view.

### Closed

The retained conversation is hidden from that view.
