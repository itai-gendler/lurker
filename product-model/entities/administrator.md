---
kind: person
acts: external
relations:
- entity: account
  verb: has-account
  cardinality: one-to-one
- entity: ai-agent
  verb: connects
  cardinality: many-to-many
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
---

# Administrator

A person administering the Lurker instance and its accounts. Their own personal information belongs to their Account.
