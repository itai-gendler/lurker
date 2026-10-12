---
availability:
- place: oauth
references:
- kind: code
  role: implementation
  target: server/db/oauth.ts#purgeOAuth
- kind: code
  role: implementation
  target: server/services/oauth.ts
---

# Expire app registration

Unapproved expired registration removed unattended.

Boot/hourly cleanup removes unused registrations older than one hour; a first approval preserves the registration.
