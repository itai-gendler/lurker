---
references:
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/routes/exports.ts
---

# Data export

An account’s background archive job, whose progress and temporary downloadable artifact have their own lifecycle.

## Information kept

- **Requested contents** — The selected archive contents, including qualified owned configuration and optional history.
- **Progress** — The export’s reported build progress.
- **Counts** — Counts reported for the export.
- **Artifact** — The temporary downloadable archive, or its absence before readiness or after expiry.
- **Error** — The recorded export failure information.
- **Expires at** — The artifact’s temporary availability cutoff; expiration and cleanup do not remove the account’s source history.
- **Downloaded at** — When the artifact was downloaded.

## States

### Pending

An archive job awaits execution.

### Running

The archive build is in progress.

### Ready

The temporary artifact is available for download.

### Failed

The archive job records a build or interruption failure.
