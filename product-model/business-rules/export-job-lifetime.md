---
appliesTo:
- type: entity
  id: data-export
references:
- kind: code
  role: implementation
  target: server/services/exportJobs.ts
- kind: code
  role: implementation
  target: server/routes/exports.ts
---

# Export job lifetime

Only one in-flight archive job is kept per account. Background progress reaches Ready or Failed; startup recovery fails interrupted running jobs. Artifacts expire after twenty-four hours, and ready download records attribution. Not-ready returns conflict; missing/expired artifacts fail distinctly. Paused HTTP POST is refused while permitted reads remain available.
