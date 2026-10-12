---
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# IRC client

A live downstream IRC attachment authenticated to one account, in control mode or bound to an owned network.

## Information kept

- **Registration** — Registered credential or downstream registration information appropriate to this subject.
- **Network binding** — The owned network selected before registration completes, or control mode without a bound network.
- **Negotiated extensions** — The IRC extensions negotiated for this downstream client.
- **Credential association** — The supported credential through which this attachment authenticated.
- **Presence contribution** — Whether this attachment contributes counted presence for automatic away.

## States

### Registering

Downstream registration is in progress.

### Attached

The downstream client is registered in its chosen binding.
