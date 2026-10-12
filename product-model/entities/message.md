---
relations:
- entity: reaction
  verb: has-association
  cardinality: one-to-many
- entity: bookmark
  verb: has-association
  cardinality: one-to-many
- entity: draft
  verb: has-association
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Message

A recorded conversation item, including ordinary messages, actions and notices, retaining sender, time and contextual annotations.

## Information kept

- **Sender** — Recorded sender attribution, before any relay display interpretation.
- **Content** — The retained content; supported encrypted transport can still persist decrypted plaintext here.
- **Kind** — The recorded conversation item kind, including message, action and notice.
- **Time** — Upstream server time when supplied, otherwise receive time.
- **Self attribution** — Whether the recorded item or reaction is attributed to this account’s upstream identity.
- **Upstream identity** — The upstream message identity when available; encrypted storage and playback can lack original wire tags.
- **Reply context** — Eligible contextual reference to earlier content, bounded by retained history and upstream support.
- **Highlight information** — The highlight and reply-to-self annotations computed when the item is recorded.
- **Ignore information** — The ignore annotations stamped at record time; removing an ignore rule does not rewrite old stamps.
- **Encryption indication** — Whether the recorded content followed the encrypted messaging path.

## States

### Recorded

A recorded conversation item, including ordinary messages, actions and notices, retaining sender, time and contextual annotations.
