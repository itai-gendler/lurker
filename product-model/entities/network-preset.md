---
references:
- kind: code
  role: implementation
  target: server/routes/adminNetworks.ts
---

# Network preset

An independently editable offered network configuration used to guide connection setup.

## Information kept

- **Name** — The name displayed for this subject.
- **Host** — The offered IRC host.
- **Port** — The offered IRC port.
- **TLS** — The offered TLS preference.
- **Recommended channels** — The offered initial channels.
- **Authentication guidance** — The offered authentication guidance.
- **Enabled** — Whether this configured subject is enabled.
- **Position** — The retained relative order within this association’s applicable list.
