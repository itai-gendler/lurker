---
references:
- kind: code
  role: implementation
  target: server/db/reactions.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Reaction

A reaction to eligible upstream-identified content, including a retained withdrawal timestamp.

## Information kept

- **Value** — The reaction value.
- **Reacting identity** — The upstream identity that reacted.
- **Self attribution** — Whether the recorded item or reaction is attributed to this account’s upstream identity.
- **Reacted at** — When the active reaction was recorded.
- **Removed at** — The withdrawal timestamp retained as a tombstone against stale replay.

## States

### Active

The attributable reaction stands at its retained maximum add timestamp, without a later withdrawal.

### Withdrawn

The withdrawal timestamp remains recorded.
