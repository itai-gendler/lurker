---
references:
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Network log

The retained server and network output for one owned network, with its own read and display-clear boundaries.

## Information kept

- **Entries** — The retained output or Product events visible in this log’s authorized view.
- **Read boundary** — The monotonic personal read pointer in this subject’s own sequence.
- **Clear boundary** — The reversible display-clear boundary; it neither deletes history nor advances the read pointer.
- **Unread counts** — The bounded derived unread and highlight counts under the subject’s actual counting rules.
