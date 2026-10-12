---
entities:
- entity: network
  shows:
  - Name
  - Connection configuration
  - Authentication
  - Connection preferences
  - Startup channels
  - Preferred nick
  - Current nick
  - Connection state
  - Away state
  collects:
  - Name
  - Connection configuration
  - Authentication
  - Connection preferences
  - Startup channels
  - Preferred nick
- entity: network-certificate
  shows:
  - Certificate description
  collects:
  - Certificate
  - Private credential
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
---

# Network

Owned Network configuration and certificate description. Collects edits, secrets and certificate input.
