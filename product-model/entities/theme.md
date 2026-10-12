---
references:
- kind: code
  role: implementation
  target: server/db/themes.ts
- kind: code
  role: implementation
  target: server/services/themesService.ts
---

# Theme

An individually saved named theme snapshot. Built-in themes are shipped choices rather than saved instances.

## Information kept

- **Name** — The name displayed for this subject.
- **Values** — Validated saved theme values.
- **Created at** — When this saved subject was created.
- **Updated at** — When the retained values were last changed.
