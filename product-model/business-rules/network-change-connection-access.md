---
appliesTo:
- type: entity
  id: network
  effect: changes
  contexts:
  - place: web::personal
  - place: client-api::personal
  - place: irc-bouncer::personal
  - place: mcp
  facts:
  - Connection state
  - Current nick
  - Away state
  - CASEMAPPING
permits:
- related:
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
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/services/verbs/connectNetwork.ts
- kind: code
  role: implementation
  target: server/services/verbs/disconnectNetwork.ts
- kind: code
  role: implementation
  target: server/services/verbs/setNick.ts
- kind: code
  role: implementation
  target: server/services/verbs/setAway.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendRaw.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts#connectGate
- kind: code
  role: implementation
  target: server/services/ircManager.ts#setAway
- kind: code
  role: implementation
  target: server/services/wsHub.ts#handleClientMessage
- kind: code
  role: implementation
  target: server/services/bouncerLogin.ts#verifyBouncerLogin
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

# Only an account-bound writer or attributable Product event changes Network connection state

HTTP connect, disconnect and reconnect require the authenticated owner’s unpaused account. WebSocket raw/nick/away/back paths require the socket’s account not to be paused. Bouncer requests use their registered account and bound network; control AWAY applies to that account’s network set. Starting or retrying a connection additionally requires the current host policy and usable configured proxy. No personal request can change another account’s network.

The Account-configured human grants resolve the actual authenticated personal account, not merely an account related to the target. HTTP uses the valid signed ordinary-session cookie first, then an accepted ordinary-session or OAuth bearer; ordinary sessions must exist and be unexpired (30-day issuance), and OAuth access must still exist. WebSocket upgrade uses a valid signed session cookie or accepted session/OAuth bearer and binds later commands to that socket’s account. Later commands retain the inspected socket pause guard and OAuth-revocation closure; this is not a promise that ordinary logout reauthenticates or terminates every open socket. API tokens do not authenticate ordinary REST/WebSocket requests.

Where this Rule covers the bouncer, admission is standalone PASS/SASL PLAIN with the selected username’s password or the exact matching active read-write API token owned by that same account. OAuth and ordinary-session tokens are not bouncer passwords. Registration checks the account still exists and is unpaused, connection limits and an eligible owned binding. Subsequent operations use that registered account and bound network; token revocation, pause, recovery or account removal close affected attachments. Control-mode discovery/away does not confer arbitrary network creation, configuration, removal or post-registration rebinding.

A User or Administrator acts only for that personal account. An AI grant’s related path reaches that same accountable person and then the initiating AI agent. The delegation is not a persisted harness roster, global one-to-one binding or grant to all agents.

The API-token-configured alternative applies only to an MCP request whose presented Bearer hashes to that exact retained, nonrevoked API token and whose token owner resolves to the current authenticated account. It evaluates that matched token’s current Scope; it never chooses another token merely because the account owns it. API tokens have no mapped automatic expiry.

The Authorized-app-configured alternative applies only to the OAuth fallback when the presented Bearer did not match an active API token. The presented access token’s hash must match a currently retained Issued access under the actual approved application association, and its account must still exist. The authenticated account and application association are those of that exact token, not any other approved application. Deleting the token/authorization removes this authority. OAuth access has read-write MCP authority, no automatic expiry and no refresh-token contract; it does not inherit API-token scope fields.

For either alternative, effective scope is reduced to read when the authenticated account is paused. A read operation admits effective read or read-write; an outbound or local write operation requires effective read-write and the current account unpaused. The requested tool determines the required scope even when it returns information. Each supplied network selection must be a positive integer owned by that authenticated account; omitted selections walk only that account’s networks where the tool explicitly supports omission. Subject lookup, folded target and record ownership stay within those networks. Neither configured alternative enlarges personal ownership or opens the selected operation on another Interface.

The permitted MCP operations affecting this selector are:

| Operation | Required effective scope | Selected behavior |
|---|---|---|
| connect_network | read-write | owned start or force-restart; host policy checked before force disposes the old connection |
| disconnect_network | read-write | owned stop; already-offline stop is a no-op |
| set_nick | read-write | owned connected upstream; result is only acknowledgement |
| set_away | read-write | selected owned network, or all of the authenticated account’s networks when omitted |
| send_raw | read-write | supported raw traffic on the owned connected upstream; no automatic configuration or removal authority |

Attributable upstream connection/nick/CASEMAPPING observations and the account’s eligible reconnect/automatic-away policy may update state. Automatic away never replaces manual away. A requested dial or IRC command is not confirmation of its upstream outcome.
