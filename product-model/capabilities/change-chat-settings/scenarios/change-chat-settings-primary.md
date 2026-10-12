---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change chat settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::chat-settings
    client:
      place: client-api::personal
  actor: user
- text: Chat preferences change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Chat settings
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
---

# Change chat settings

## Trigger

The User invokes change chat settings.

## Outcome

Chat preferences change

Validated overrides in the chat section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
