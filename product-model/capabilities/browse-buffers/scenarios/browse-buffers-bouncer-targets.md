---
kind: path
routes:
  irc: IRC bouncer
steps:
- text: The User requests CHATHISTORY TARGETS with supported timestamp bounds and a bounded limit on the registered
    network attachment.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  actor: user
  contexts:
    irc:
      place: irc-bouncer::personal
- text: The Product returns the eligible conversation targets and their latest activity timestamps within the requested
    window.
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts:
    - Target
    - Visibility
  - entity: direct-message
    effect: reads
    facts:
    - Target
    - Visibility
  - entity: message
    effect: reads
    facts:
    - Time
  actor: user
  contexts:
    irc:
      place: irc-bouncer::personal
references:
- kind: code
  role: implementation
  target: server/services/bouncer.ts#handleChatHistoryTargets
- kind: code
  role: implementation
  target: server/db/messages.ts#listActiveTargetsInWindow
---

# Browse conversation targets through bouncer history

## Trigger

The bound downstream client requests CHATHISTORY TARGETS.

## Outcome

The timestamp window returns eligible channel/private-message targets and latest activity times, with closed subjects excluded using the network’s case mapping. Event/reaction and self-message negotiation select the eligible activity. No unread counts or web buffer hydration payload is promised. Server/system/DCC targets remain excluded.

## Edge cases

- The bounded limit is validated from 0 through 1000; malformed bounds or limits produce the established FAIL response.
- A control connection has no bound history and receives INVALID_TARGET.
- Timestamp bounds are supported; msgid selectors are rejected.
- Batch framing follows negotiated support; target enumeration never joins or reopens a conversation.
