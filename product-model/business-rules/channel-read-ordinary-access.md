---
appliesTo:
- type: entity
  id: channel
  effect: reads
  facts:
  - Target
  - Visibility
  - Joined status
  - Autojoin
  - Channel key
  - Topic
  - Members
  - Modes
  - Read boundary
  - Clear boundary
  - Unread counts
  - Retention override
  - Notification override
  - Encryption status
  - Events
permits:
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
  configuredBy: account
- related:
  - verb: contains
    entity: network
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
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
  target: server/services/verbs/listBuffers.ts
- kind: code
  role: implementation
  target: server/services/verbs/getTopic.ts
- kind: code
  role: implementation
  target: server/services/verbs/listMembers.ts
- kind: code
  role: implementation
  target: server/services/verbs/recentMessages.ts
- kind: code
  role: implementation
  target: server/services/verbs/searchMessages.ts
- kind: code
  role: implementation
  target: server/services/verbs/joinChannel.ts
- kind: code
  role: implementation
  target: server/services/verbs/setChannelModes.ts
- kind: code
  role: implementation
  target: server/services/retentionSweeper.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts#foldTargetFor
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

# Only the owning account and its matched delegation read Channel observations

HTTP and WebSocket reads resolve the channel through the authenticated owner’s network and folded target. Paused reads remain available. Bouncer playback/query observations concern the registered account’s bound network, negotiated support and requester routing. This ordinary selector does not authorize the separately governed live mode-list query.

The Account-configured human grants resolve the actual authenticated personal account, not merely an account related to the target. HTTP uses the valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer; ordinary sessions must exist and be unexpired (30-day issuance), and OAuth access must still exist. WebSocket upgrade uses a valid signed session cookie or accepted session/OAuth bearer and binds later commands to that socket’s account. Later commands retain the inspected socket pause guard and OAuth-revocation closure; this is not a promise that ordinary logout reauthenticates or terminates every open socket. API tokens do not authenticate ordinary REST/WebSocket requests.

Where this Rule covers the bouncer, admission is standalone PASS/SASL PLAIN with the selected username’s password or the exact matching active read-write API token owned by that same account. OAuth and ordinary-session tokens are not bouncer passwords. Registration checks the account still exists and is unpaused, connection limits and an eligible owned binding. Subsequent operations use that registered account and bound network; token revocation, pause, recovery or account removal close affected attachments. Control-mode discovery/away does not confer arbitrary network creation, configuration, removal or post-registration rebinding.

A User or Administrator acts only for that personal account. An AI grant’s related path reaches that same accountable person and then the initiating AI agent. The delegation is not a persisted harness roster, global one-to-one binding or grant to all agents.

The API-token-configured alternative applies only to an MCP request whose presented Bearer hashes to that exact retained, nonrevoked API token and whose token owner resolves to the current authenticated account. It evaluates that matched token’s current Scope; it never chooses another token merely because the account owns it. API tokens have no mapped automatic expiry.

The Authorized-app-configured alternative applies only to the OAuth fallback when the presented Bearer did not match an active API token. The presented access token’s hash must match a currently retained Issued access under the actual approved application association, and its account must still exist. The authenticated account and application association are those of that exact token, not any other approved application. Deleting the token/authorization removes this authority. OAuth access has read-write MCP authority, no automatic expiry and no refresh-token contract; it does not inherit API-token scope fields.

For either alternative, effective scope is reduced to read when the authenticated account is paused. A read operation admits effective read or read-write; an outbound or local write operation requires effective read-write and the current account unpaused. The requested tool determines the required scope even when it returns information. Each supplied network selection must be a positive integer owned by that authenticated account; omitted selections walk only that account’s networks where the tool explicitly supports omission. Subject lookup, folded target and record ownership stay within those networks. Neither configured alternative enlarges personal ownership or opens the selected operation on another Interface.

The permitted MCP operations affecting this selector are:

| Operation | Required effective scope | Selected behavior |
|---|---|---|
| list_buffers | read | message-bearing target/kind/time enumeration, without a closed-state filter |
| get_topic | read | current or last-known topic from the owned connection’s observed channel |
| list_members | read | current or last-known channel members, modes and away observations |
| recent_messages | read | retained channel activity for the owned network and requested target |
| search_messages | read | matching owned retained activity |
| join_channel | read-write | consult the selected channel’s stored key for the requested join |
| set_channel_modes | read-write | consult observed mode support and stored -k key for the requested mode change |

Eligible closed-buffer maintenance may read current visibility to avoid collecting a reopened subject.

Bouncer disclosure follows the requested registered command: BOUNCER discovery requires its supported negotiated extension and exposes only network wire attributes; CHATHISTORY requires the supported history contract and a bound network, then validates its timestamp and 0–1000 limit parameters. TARGETS filters closed subjects and excludes server/system/DCC targets. These commands do not admit the web/API unread-count, preset or connection-preference projections merely because the same owner is authenticated.
