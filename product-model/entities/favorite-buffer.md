---
references:
- kind: code
  role: implementation
  target: server/db/favoriteBuffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Favorite buffer

An account’s independently ordered favorite of a conversation across networks.

## Information kept

- **Position** — The retained relative order within this association’s applicable list.
