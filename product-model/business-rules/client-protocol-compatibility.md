---
appliesTo:
- type: context
  context:
    place: client-api::personal
references:
- kind: code
  role: implementation
  target: server/routes/config.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/protocol.ts
- kind: code
  role: implementation
  target: docs/CLIENT_PROTOCOL.md
---

# Client protocol compatibility

The supported client protocol keeps its documented additive compatibility contract: existing field meanings/types remain stable and unknown additions are not fatal. This does not establish native implementation parity or release compatibility outside this checkout.
