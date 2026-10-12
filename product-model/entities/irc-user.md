---
references:
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
- kind: code
  role: implementation
  target: server/services/verbs/listMembers.ts
---

# IRC user

Partial, volatile observations of an IRC peer, rather than a complete persistent profile.

## Information kept

- **Nick** — The nick identifying the scoped peer or annotation.
- **Membership status** — The peer’s observed membership information.
- **Presence** — Partial observed presence information.
- **Profile information** — Observed WHOIS/profile fields, which may be absent or incomplete.
