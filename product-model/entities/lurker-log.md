---
references:
- kind: code
  role: implementation
  target: server/services/systemLog.ts
---

# Lurker log

The account’s view of global and private Lurker events, with a separate sequence and personal read boundary.

## Information kept

- **Entries** — The retained output or Product events visible in this log’s authorized view.
- **Read boundary** — The monotonic personal read pointer in this subject’s own sequence.
- **Unread counts** — The bounded derived unread and highlight counts under the subject’s actual counting rules.
