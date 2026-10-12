---
appliesTo:
- type: entity
  id: instance-settings
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
  target: server/middleware/rateLimit.ts
---

# Login throttling

Ten failures within fifteen minutes produce fifteen-minute backoff. Web and bouncer budgets keep their actual separate accounting. Clearing currently blocked addresses retains subthreshold failure budgets rather than deleting all recent attempts.
