---
singleton: true
relations:
- entity: network-preset
  verb: offers
  cardinality: one-to-many
- entity: instance-uploader
  verb: offers
  cardinality: one-to-many
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
---

# Instance settings

The singleton effective edition, feature and policy configuration, with instance-reported operational information.

## Information kept

- **Edition** — The standalone or managed-node edition.
- **Feature availability** — The public and authenticated feature availability advertised by this instance.
- **Setup status** — Whether initial account setup remains available.
- **Sign-in availability** — The aggregate sign-in methods advertised by the instance.
- **Network policy** — Effective host and proxy restrictions and preset continuity policy.
- **Uploader policy** — Effective destination offerings, default and personal-creation policy.
- **Retention ceilings** — Instance ceilings constraining account and conversation retention.
- **Notification transports** — Configured sender availability and supported delivery transports.
- **Relay opt-in** — Administrative opt-in for relay registration and delivery.
- **Relay status** — Reported relay subscription/status-check information, guarded against superseded results.
- **Bouncer connection details** — Authenticated downstream IRC address, port and connection guidance.
- **Storage measurements** — Reported storage attribution and retained-history measurements.
- **Versions** — Reported application and optional engine versions, which can be unknown.
- **Login policy** — Effective sign-in throttle and backoff policy.
- **Blocked sign-ins** — Currently blocked addresses; subthreshold failure budgets are retained separately by the policy.
