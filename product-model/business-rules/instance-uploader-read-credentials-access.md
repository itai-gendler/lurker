---
appliesTo:
- type: entity
  id: instance-uploader
  effect: reads
  facts:
  - Secrets
permits:
- configuredBy: instance-settings
references:
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/adminUploaders.ts
---

# Instance uploader disclosure is limited to configured execution

Only configured upload execution reads provider secrets for the selected permitted destination. Human administration/configuration responses do not disclose secret values. Owned personal archives have their separately qualified owned configuration path.
