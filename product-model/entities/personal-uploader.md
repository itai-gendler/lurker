---
relations:
- entity: image-upload
  verb: stores
  cardinality: one-to-many
- entity: file-upload
  verb: stores
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/routes/uploaders.ts
---

# Personal uploader

An account-owned upload destination with retained configuration and secret-status disclosure.

## Information kept

- **Label** — The person’s displayed label for this saved subject.
- **Driver** — The configured upload-provider driver.
- **Configuration** — Supported nonsecret destination configuration; managed rows may redact this as well.
- **Secrets** — Retained provider credentials used by upload execution; configuration responses omit the values.
- **Secret status** — Whether each supported secret is present, without revealing its value.
- **Enabled** — Whether this configured subject is enabled.
