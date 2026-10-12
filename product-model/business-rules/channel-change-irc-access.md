---
appliesTo:
- type: entity
  id: channel
  effect: changes
  contexts:
  - place: web::personal
  - place: client-api::personal
  - place: irc-bouncer::personal
  - place: mcp
  facts:
  - Visibility
  - Joined status
  - Autojoin
  - Channel key
  - Topic
  - Members
  - Modes
  - Encryption status
permits:
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: account
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: account
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  - verb: connects
    entity: ai-agent
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: api-token
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  - verb: connects
    entity: ai-agent
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: authorized-app
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  - verb: connects
    entity: ai-agent
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: api-token
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
  - verb: connects
    entity: ai-agent
  when:
  - entity: account
    fact: Pause status
    is: Active
  configuredBy: authorized-app
- unattended: true
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/verbs/joinChannel.ts
- kind: code
  role: implementation
  target: server/services/verbs/partChannel.ts
- kind: code
  role: implementation
  target: server/services/verbs/setTopic.ts
- kind: code
  role: implementation
  target: server/services/verbs/setChannelModes.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendRaw.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts#joinChannel
- kind: code
  role: implementation
  target: server/services/ircManager.ts#partChannel
- kind: code
  role: implementation
  target: server/services/ircConnection.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts#handleClientMessage
- kind: code
  role: implementation
  target: server/middleware/apiAuth.ts#requireApiAuth
- kind: code
  role: implementation
  target: server/services/mcpServer.ts
- kind: code
  role: implementation
  target: server/services/verbRegistry.ts#callVerb
- kind: code
  role: implementation
  target: server/db/apiTokens.ts#findActiveByHash
- kind: code
  role: implementation
  target: server/db/oauth.ts#findTokenByRaw
- kind: code
  role: implementation
  target: server/middleware/auth.ts#requireAuth
---

# Only an account-bound writer or attributable IRC observation changes Channel IRC state

Owner JOIN/PART, opening or closing that can affect join intent, raw IRC, topic Save and mode edits follow the inspected writable transport. HTTP mutations require the current authenticated account unpaused; WebSocket join/open/close/part/raw/topic/mode paths are pause-blocked. Bouncer commands act on its bound network and shared upstream identity. Topic or mode privilege remains the upstream server’s decision.

The Account-configured human grants resolve the actual authenticated personal account, not merely an account related to the target. HTTP uses the valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer; ordinary sessions must exist and be unexpired (30-day issuance), and OAuth access must still exist. WebSocket upgrade uses a valid signed session cookie or accepted session/OAuth bearer and binds later commands to that socket’s account. Later commands retain the inspected socket pause guard and OAuth-revocation closure; this is not a promise that ordinary logout reauthenticates or terminates every open socket. API tokens do not authenticate ordinary REST/WebSocket requests.

Where this Rule covers the bouncer, admission is standalone PASS/SASL PLAIN with the selected username’s password or the exact matching active read-write API token owned by that same account. OAuth and ordinary-session tokens are not bouncer passwords. Registration checks the account still exists and is unpaused, connection limits and an eligible owned binding. Subsequent operations use that registered account and bound network; token revocation, pause, recovery or account removal close affected attachments. Control-mode discovery/away does not confer arbitrary network creation, configuration, removal or post-registration rebinding.

A User or Administrator acts only for that personal account. An AI grant’s related path reaches that same accountable person and then the initiating AI agent. The delegation is not a persisted harness roster, global one-to-one binding or grant to all agents.

The API-token-configured alternative applies only to an MCP request whose presented Bearer hashes to that exact retained, nonrevoked API token and whose token owner resolves to the current authenticated account. It evaluates that matched token’s current Scope; it never chooses another token merely because the account owns it. API tokens have no mapped automatic expiry.

The Authorized-app-configured alternative applies only to the OAuth fallback when the presented Bearer did not match an active API token. The presented access token’s hash must match a currently retained Issued access under the actual approved application association, and its account must still exist. The authenticated account and application association are those of that exact token, not any other approved application. Deleting the token/authorization removes this authority. OAuth access has read-write MCP authority, no automatic expiry and no refresh-token contract; it does not inherit API-token scope fields.

For either alternative, effective scope is reduced to read when the authenticated account is paused. A read operation admits effective read or read-write; an outbound or local write operation requires effective read-write and the current account unpaused. The requested tool determines the required scope even when it returns information. Each supplied network selection must be a positive integer owned by that authenticated account; omitted selections walk only that account’s networks where the tool explicitly supports omission. Subject lookup, folded target and record ownership stay within those networks. Neither configured alternative enlarges personal ownership or opens the selected operation on another Interface.

The permitted MCP operations affecting this selector are:

| Operation | Required effective scope | Selected behavior |
|---|---|---|
| join_channel | read-write | owned writable connection and supported channel/key; persist only confirmed or already-joined intent |
| part_channel | read-write | owned writable connection; lower existing autojoin intent without creating an absent row |
| set_topic | read-write | owned writable connection; a required empty topic explicitly clears it |
| set_channel_modes | read-write | owned writable connection; advertised letters and parameter direction; upstream may still refuse |
| send_raw | read-write | guarded outbound raw path, with encryption-channel PRIVMSG refusal |

Confirmed joins, parts, membership, topics, modes and attributable encryption observations update only that owned subject. Observation is not arbitrary scheduled mutation, and acknowledgement alone does not establish successful membership or IRC privilege.
