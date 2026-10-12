---
availability:
- place: oauth
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/services/oauth.ts
---

# Register app

Valid public-client metadata produces a registration.

Valid public-client metadata produces a client ID. Redirects follow the supported HTTPS, loopback, reverse-domain scheme or out-of-band policy.
