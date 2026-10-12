---
appliesTo:
- type: entity
  id: personal-uploader
- type: entity
  id: instance-uploader
references:
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/uploaders.ts
- kind: code
  role: implementation
  target: server/routes/adminUploaders.ts
- kind: code
  role: implementation
  target: server/db/exportSchema.ts
- kind: code
  role: implementation
  target: server/services/exportService.ts
---

# Uploader secret disclosure

Configuration responses omit secret values and disclose secret-presence status; omitted replacement secrets preserve prior values. Managed rows may redact configuration too. Execution reads configured secrets, and qualified owned archives can contain sensitive owned configuration. Response redaction is not a server-blindness guarantee.

Personal-uploader credentials are excluded from export and must be re-entered after import. Portable network/channel secrets are a distinct archive path; this does not imply export of instance uploader credentials.
