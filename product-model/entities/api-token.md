---
references:
- kind: code
  role: implementation
  target: server/db/apiTokens.ts
- kind: code
  role: implementation
  target: server/routes/apiTokens.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts#dropSessionsForApiToken
relations:
- entity: irc-client
  verb: authenticates
  cardinality: one-to-many
---

# API token

A named, scoped account credential for MCP and supported IRC authentication. Its raw value is revealed once.

## Information kept

- **Name** — The name displayed for this subject.
- **Scope** — Read or read-write API access scope; this is not an OAuth refresh or expiry policy.
- **Created at** — When this saved subject was created.
- **Last used at** — Most recently recorded credential or authorization use.
- **Revocation** — Whether the retained token has been revoked.

## States

### Active

The token is retained and not revoked; its current scope governs matched MCP authority and the supported read-write bouncer authentication path.

### Revoked

The retained token is revoked.

One API token may authenticate multiple downstream IRC clients. Each such client retains that exact token association so token revocation can close only its matching attachments. Password-authenticated clients have no API-token association.
