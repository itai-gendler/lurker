---
references:
- kind: code
  role: implementation
  target: server/db/ignoredMasks.ts
- kind: code
  role: implementation
  target: server/services/ignoreRulesService.ts
---

# Ignore rule

An account’s matching ignore or exception rule, including scope, levels and expiry.

## Information kept

- **Mask** — The supported sender mask.
- **Pattern** — The supported message pattern.
- **Matching kind** — The configured supported matching method.
- **Network scope** — The optional owned-network scope.
- **Levels** — The ignore levels controlling display, unread, highlight or notification handling.
- **Exception status** — Whether this matching rule is an exception.
- **Expires at** — Optional rule expiry after which the matching rule no longer applies and is eligible for cleanup.
