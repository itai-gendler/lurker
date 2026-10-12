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
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
---

# User

A person using their own Lurker account to keep IRC connections, conversations and preferences.
