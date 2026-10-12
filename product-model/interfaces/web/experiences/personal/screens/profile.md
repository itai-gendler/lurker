---
entities:
- entity: irc-user
  shows:
  - Nick
  - Membership status
  - Presence
  - Profile information
- entity: nick-note
  shows:
  - Nick
  - Text
  - Updated at
  collects:
  - Text
- entity: relay-bot
  collects:
  - Nick
  - Envelope template
references:
- kind: code
  role: implementation
  target: vue_client/src/components/UserProfileModal.vue
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
---

# Profile

Observed IRC-user nick/presence/membership/profile facts and private Nick-note text/time.
