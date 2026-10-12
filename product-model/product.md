---
id: lurker
summary: Self-hosted, always-on IRC conversations with retained history, a web client, supported client API, IRC
  bouncer and authorized agent access.
category: communication
authors:
- name: Brad Root
  url: https://github.com/amiantos
license: MPL-2.0
languages:
- en
limitations:
- Upstream IRC servers decide accepted membership, nick, topic and mode changes.
- History is subject to configured retention and account or network removal.
- Encrypted channel transport can persist decrypted plaintext on the Lurker server.
- Ordinary logout does not guarantee termination of every already-authenticated connection.
references:
- kind: doc
  role: context
  target: README.md
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Lurker

Lurker keeps account-owned IRC connections and retained conversations available across reconnecting clients. People read and participate through the web client, supported client protocol and built-in IRC bouncer. An account owner can delegate scoped MCP access to an AI agent or approve a registered OAuth application.

## Intent

Keep personal IRC history and connection state together while allowing each supported client contract to expose its own established representation.
