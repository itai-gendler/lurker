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
  target: server/routes/adminUploaders.ts
---

# Instance uploader

An instance-provided upload destination, with protected default, managed and built-in configuration boundaries.

## Information kept

- **Label** — The person’s displayed label for this saved subject.
- **Driver** — The configured upload-provider driver.
- **Configuration** — Supported nonsecret destination configuration; managed rows may redact this as well.
- **Secrets** — Retained provider credentials used by upload execution; configuration responses omit the values.
- **Secret status** — Whether each supported secret is present, without revealing its value.
- **Enabled** — Whether this configured subject is enabled.
- **Offered to users** — Whether the instance destination is offered for permitted personal selection.
- **Default status** — Whether this is the protected instance default destination.
- **Managed status** — Whether external instance management locks this destination’s configuration.
- **Built-in status** — Whether this destination is built in and protected from removal.
