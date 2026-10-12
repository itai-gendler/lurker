---
appliesTo:
- type: entity
  id: channel
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Channel join confirmation

JOIN acknowledgement/start is distinct from observed membership. Confirmed JOIN or the established already-joined path saves membership/key/autojoin intent and opens the subject; upstream refusal does not fabricate that state. PART lowers autojoin, while kicks and relevant upstream corrections update observed state.
