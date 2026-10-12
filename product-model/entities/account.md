---
relations:
- entity: session
  verb: owns
  cardinality: one-to-many
- entity: passkey
  verb: owns
  cardinality: one-to-many
- entity: api-token
  verb: owns
  cardinality: one-to-many
- entity: authorized-app
  verb: owns
  cardinality: one-to-many
- entity: network
  verb: owns
  cardinality: one-to-many
- entity: nick-note
  verb: owns
  cardinality: one-to-many
- entity: relay-bot
  verb: owns
  cardinality: one-to-many
- entity: highlight-rule
  verb: owns
  cardinality: one-to-many
- entity: ignore-rule
  verb: owns
  cardinality: one-to-many
- entity: theme
  verb: owns
  cardinality: one-to-many
- entity: personal-uploader
  verb: owns
  cardinality: one-to-many
- entity: image-upload
  verb: owns
  cardinality: one-to-many
- entity: file-upload
  verb: owns
  cardinality: one-to-many
- entity: web-push-subscription
  verb: owns
  cardinality: one-to-many
- entity: native-push-device
  verb: owns
  cardinality: one-to-many
- entity: data-export
  verb: owns
  cardinality: one-to-many
- entity: bookmark
  verb: owns
  cardinality: one-to-many
- entity: draft
  verb: owns
  cardinality: one-to-many
- entity: pin
  verb: owns
  cardinality: one-to-many
- entity: favorite-buffer
  verb: owns
  cardinality: one-to-many
- entity: lurker-log
  verb: has-view
  cardinality: one-to-one
- entity: invite
  verb: issues
  cardinality: one-to-many
- entity: recovery-link
  verb: has-recovery
  cardinality: one-to-many
- entity: irc-client
  verb: owns
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: server/db/users.ts
- kind: code
  role: implementation
  target: server/routes/auth.ts
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
---

# Account

The personal identity, sign-in methods, preferences and pause status of a Lurker member.

## Information kept

- **Username** — The account name used for sign-in and IRC credential selection.
- **Sign-in methods** — The configured password and registered passkey methods; public availability is reported as an instance aggregate.
- **Pause status** — Whether administrative pause is in force; individual transport operations keep their own pause guards.
- **Ident** — The effective IRC ident and optional administrative override.
- **Appearance settings** — Appearance overrides, built-in or saved theme selection and theme-related preferences.
- **Chat settings** — Conversation display and behavior preferences in the Chat section.
- **Event settings** — Preferences controlling presentation of IRC conversation events.
- **Input bar settings** — Composition and input bar preferences.
- **Upload settings** — File-processing preferences and selected default upload destination.
- **Notification settings** — Personal notification eligibility, quiet-time and presentation preferences.
- **Away settings** — Automatic-away timing and applicable scope preferences.
- **Data settings** — Account retention and data preferences, subject to effective instance ceilings.
- **Retained history counts** — Reported retained-history counts used in account and storage administration.

## States

### Active

The account has no administrative pause; each operation still follows its transport-specific authorization.

### Paused

Administrative pause is in force.
