---
references:
- kind: code
  role: implementation
  target: server/db/relayBots.ts
- kind: code
  role: implementation
  target: server/services/verbs/setRelayBot.ts
---

# Relay bot

An account’s network-scoped nick and envelope-template mark used to interpret relayed display attribution.

## Information kept

- **Nick** — The nick identifying the scoped peer or annotation.
- **Envelope template** — The supported relay envelope template used to derive display attribution.
- **Created at** — When this saved subject was created.
