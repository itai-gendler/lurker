---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: Incoming IRC activity or available engine backlog arrives.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
  unattended: true
- text: The Product drops the unreadable encrypted chunk and emits the bounded transient hint when applicable;
    sender presence can still be observed.
  kind: product
  entities:
  - entity: irc-user
    effect: changes
    facts:
    - Presence
  contexts: *id001
references:
- kind: code
  role: implementation
  target: server/services/ircConnection.ts#surfaceE2eDecryptIssue
- kind: code
  role: implementation
  target: server/services/e2e/manager.ts#decryptIncoming
- kind: code
  role: implementation
  target: server/services/bouncer.ts#onRawUpstream
---

# Receive messages with failed decryption

## Trigger

The Product receives encrypted activity that it cannot decrypt.

## Outcome

Missing-key and rejected chunks produce the app’s bounded transient hint, with duplicate hints collapsed for five seconds. Replay outcomes are silent. The unreadable ciphertext is not persisted as a conversation item; observed sender presence can still update. Bouncer live delivery follows its raw ciphertext contract.

## Edge cases

- A missing key can initiate the rate-limited handshake and display an establishing-session hint.
- Off-channel or encryption-disabled content beginning with the wire prefix follows ordinary cleartext handling.
