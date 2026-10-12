---
availability:
- place: oauth
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts
---

# Revoke app token

Matching application token revoked.

The registered client/token association governs revocation; an unknown or unmatched token does not revoke unrelated access.
