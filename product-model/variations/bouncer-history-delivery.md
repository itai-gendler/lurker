---
kind: version
of: capability-scenario
discriminator:
  entity: irc-client
  fact: Negotiated extensions
takesEffect: The negotiated history contract is selected before attachment playback or a supported history request.
  Reattachment reevaluates attachment behavior.
stability: Attach-time playback is not retrospectively repeated after extension changes. Subsequent explicit requests
  follow the current negotiated contract.
alternatives:
- id: browse-messages-timestamp-history
  label: draft/chathistory
  selectedWhen: The downstream client negotiated draft/chathistory and sends a supported timestamp request.
- id: browse-messages-legacy-playback
  label: legacy playback
  selectedWhen: The history extension is absent at attachment; bounded automatic legacy playback applies.
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Bouncer history delivery

The downstream negotiated extension selects explicit timestamp history requests or bounded automatic attachment playback.
