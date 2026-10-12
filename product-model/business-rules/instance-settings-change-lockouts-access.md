---
appliesTo:
- type: entity
  id: instance-settings
  effect: changes
  contexts:
  - place: web::administration
  - place: client-api::administration
  facts:
  - Blocked sign-ins
permits:
- actors:
  - administrator
  configuredBy: account
references:
- kind: code
  role: implementation
  target: server/routes/config.ts
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/app.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAdmin
- kind: code
  role: implementation
  target: server/middleware/rateLimit.ts
---

# Only the authenticated Administrator clears current login lockouts

The current caller is selected by the Account-configured ordinary-session or accepted OAuth authentication path and must be an unpaused Administrator. DELETE /api/admin/login-lockouts clears currently blocked sign-ins. It preserves subthreshold failure budgets and does not change Login policy. GET returns the lockout roster and policy under the separate administrative read grant. The caller is distinct from the blocked account or address being listed.
