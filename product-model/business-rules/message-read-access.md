---
appliesTo:
- type: entity
  id: message
  effect: reads
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
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/services/verbs/recentMessages.ts
- kind: code
  role: implementation
  target: server/services/verbs/searchMessages.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendMessage.ts
- kind: code
  role: implementation
  target: server/db/messages.ts#searchMessagesSql
- kind: code
  role: implementation
  target: server/db/messages.ts#replySendMsgid
- kind: code
  role: implementation
  target: server/services/bouncer.ts#playbackLines
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
- kind: code
  role: implementation
  target: server/db/index.ts
---

# Only the owning account and its matched delegation read retained Messages

HTTP/WebSocket history, search, activity, bookmarked history and reply lookups are restricted to the authenticated account and owned subject. Bouncer playback uses its registered account and bound network under the negotiated history representation. Stored offline history remains readable; Administrator has no private-history bypass.

The Account-configured human grants resolve the actual authenticated personal account, not merely an account related to the target. HTTP uses the valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer; ordinary sessions must exist and be unexpired (30-day issuance), and OAuth access must still exist. WebSocket upgrade uses a valid signed session cookie or accepted session/OAuth bearer and binds later commands to that socket’s account. Later commands retain the inspected socket pause guard and OAuth-revocation closure; this is not a promise that ordinary logout reauthenticates or terminates every open socket. API tokens do not authenticate ordinary REST/WebSocket requests.

Where this Rule covers the bouncer, admission is standalone PASS/SASL PLAIN with the selected username’s password or the exact matching active read-write API token owned by that same account. OAuth and ordinary-session tokens are not bouncer passwords. Registration checks the account still exists and is unpaused, connection limits and an eligible owned binding. Subsequent operations use that registered account and bound network; token revocation, pause, recovery or account removal close affected attachments. Control-mode discovery/away does not confer arbitrary network creation, configuration, removal or post-registration rebinding.

A User or Administrator acts only for that personal account. An AI grant’s related path reaches that same accountable person and then the initiating AI agent. The delegation is not a persisted harness roster, global one-to-one binding or grant to all agents.

The API-token-configured alternative applies only to an MCP request whose presented Bearer hashes to that exact retained, nonrevoked API token and whose token owner resolves to the current authenticated account. It evaluates that matched token’s current Scope; it never chooses another token merely because the account owns it. API tokens have no mapped automatic expiry.

The Authorized-app-configured alternative applies only to the OAuth fallback when the presented Bearer did not match an active API token. The presented access token’s hash must match a currently retained Issued access under the actual approved application association, and its account must still exist. The authenticated account and application association are those of that exact token, not any other approved application. Deleting the token/authorization removes this authority. OAuth access has read-write MCP authority, no automatic expiry and no refresh-token contract; it does not inherit API-token scope fields.

For either alternative, effective scope is reduced to read when the authenticated account is paused. A read operation admits effective read or read-write; an outbound or local write operation requires effective read-write and the current account unpaused. The requested tool determines the required scope even when it returns information. Each supplied network selection must be a positive integer owned by that authenticated account; omitted selections walk only that account’s networks where the tool explicitly supports omission. Subject lookup, folded target and record ownership stay within those networks. Neither configured alternative enlarges personal ownership or opens the selected operation on another Interface.

The permitted MCP operations affecting this selector are:

| Operation | Required effective scope | Selected behavior |
|---|---|---|
| recent_messages | read | owned network and target, including the explicitly named server target |
| search_messages | read | SQL ownership restriction across that account’s networks |
| send_message | read-write | eligible reply lookup must match the acting account, network and buffer |

Unattended reads deliver only eligible recorded content to the recipient account’s configured notification destinations or bounded playback to its authenticated attachment. They do not disclose arbitrary private history.

The selected retained Message belongs directly to its Network, whether its target is a Channel, Direct message or server output. The same account and matched-credential restrictions apply to every such target.

Bouncer disclosure follows the requested registered command: BOUNCER discovery requires its supported negotiated extension and exposes only network wire attributes; CHATHISTORY requires the supported history contract and a bound network, then validates its timestamp and 0–1000 limit parameters. TARGETS filters closed subjects and excludes server/system/DCC targets. These commands do not admit the web/API unread-count, preset or connection-preference projections merely because the same owner is authenticated.
