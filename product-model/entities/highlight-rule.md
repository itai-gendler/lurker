---
references:
- kind: code
  role: implementation
  target: server/db/highlightRules.ts
- kind: code
  role: implementation
  target: server/services/highlightRulesService.ts
---

# Highlight rule

An account’s configurable matching rule, including automatically maintained nick rules with restricted personal editing.

## Information kept

- **Pattern** — The supported message pattern.
- **Mask** — The supported sender mask.
- **Matching kind** — The configured supported matching method.
- **Network scope** — The optional owned-network scope.
- **Channel scope** — The optional channel scope.
- **Case sensitivity** — Whether matching is case sensitive.
- **Enabled** — Whether this configured subject is enabled.
- **Automatic origin** — Whether the highlight rule is automatically maintained rather than personally editable.
