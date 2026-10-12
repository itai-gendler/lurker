---
type: api
actors:
- client-application
references:
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/routes/oauth.ts
entryPoints:
- api: /.well-known/oauth-authorization-server
---

# OAuth

The public-client OAuth contract supports registration, discovery, approval-code exchange and revocation. Client IDs identify applications; bound codes and PKCE govern exchange.
