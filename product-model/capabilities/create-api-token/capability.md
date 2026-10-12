---
availability:
- place: web::personal
references:
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
domain: api-tokens
---

# Create api token

Scoped token created; raw value revealed once.

Standalone token creation records read or read-write scope and reveals the raw token only in the creation result.
