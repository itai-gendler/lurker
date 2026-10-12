---
relations:
- entity: network-certificate
  verb: uses-certificate
  cardinality: one-to-one
- entity: channel
  verb: contains
  cardinality: one-to-many
- entity: direct-message
  verb: contains
  cardinality: one-to-many
- entity: irc-user
  verb: contains
  cardinality: one-to-many
- entity: nick-note
  verb: contains
  cardinality: one-to-many
- entity: relay-bot
  verb: contains
  cardinality: one-to-many
- entity: network-log
  verb: has-output
  cardinality: one-to-one
- entity: message
  verb: contains
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/db/index.ts
---

# Network

An account-owned IRC connection configuration, observed upstream identity, connection state and cached directory.

## Information kept

- **Name** — The name displayed for this subject.
- **Connection configuration** — Host, port, TLS and other supported connection configuration.
- **Authentication** — Supported server, SASL and nick-service authentication preferences and credentials.
- **Position** — The retained relative position in the account’s personal network list.
- **Connection preferences** — Supported proxy, startup and auto-connect preferences.
- **Startup channels** — Configured startup join targets and their supported keys.
- **Preferred nick** — The configured desired nick.
- **Current nick** — The last observed nick of the shared upstream identity.
- **Connection state** — Observed connection progress or disconnection, distinct from an accepted start request.
- **Away state** — Manual or automatic away state and message, without overwriting existing manual away.
- **CASEMAPPING** — The IRC server’s case-folding contract used to match channel and nick targets.
- **Listed channels** — The cached upstream LIST directory entries.
- **Directory progress** — The state of a requested directory refresh and its accumulated results.
