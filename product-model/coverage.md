---
scope: Broad account, IRC/history, supported client, bouncer, MCP/OAuth, upload, push, data and administration implementation
  at source commit 0cf180f44bd781d085d4e82f1b483763280b30d4.
method: Static tracked-source inspection, tracing handlers, persistence and client outcomes with documentation and
  tests as leads.
covered:
- description: Inbound application wiring and client protocol gates
  paths:
  - server/app.ts
  - server/protocol.ts
  - docs/CLIENT_PROTOCOL.md
- description: Account entry, sessions, passkeys, invitations and recovery code
  paths:
  - server/routes/auth.ts
  - server/middleware/auth.ts
  - server/db/users.ts
  - server/db/sessions.ts
  - server/db/webauthnCredentials.ts
  - server/db/invites.ts
  - server/db/accountRecovery.ts
  - server/services/webauthn.ts
- description: API-token and OAuth registration, approval, exchange and revocation code
  paths:
  - server/routes/apiTokens.ts
  - server/routes/oauth.ts
  - server/db/apiTokens.ts
  - server/db/oauth.ts
  - server/services/oauth.ts
- description: MCP transport, shared verbs, presented-credential scopes and ownership checks
  paths:
  - server/services/mcpServer.ts
  - server/services/verbRegistry.ts
  - server/services/verbs/
  - server/middleware/apiAuth.ts
- description: Personal network configuration, certificate and connection-state code
  paths:
  - server/routes/networks.ts
  - server/db/networks.ts
  - server/services/ircManager.ts
  - server/services/ircConnection.ts
- description: Buffer identity, history slices, search, activity, read markers and display boundaries
  paths:
  - server/db/buffers.ts
  - server/db/bufferReads.ts
  - server/db/bufferResolve.ts
  - server/db/casemapping.ts
  - server/db/messages.ts
  - server/services/wsHub.ts
  - server/routes/search.ts
  - server/routes/activity.ts
  - shared/channels.ts
- description: User-visible network and Product-event recording code
  paths:
  - server/services/systemLog.ts
  - server/db/messages.ts
- description: Web account-entry and chat hand-off code
  paths:
  - vue_client/src/views/InviteAccept.vue
  - vue_client/src/views/AccountRecovery.vue
  - vue_client/src/views/OAuthAuthorize.vue
  - vue_client/src/components/ChannelListModal.vue
- description: Web conversation hydration, paging, detached windows and local lifecycle code
  paths:
  - vue_client/src/stores/buffers.ts
  - vue_client/src/composables/useSocket.ts
  - vue_client/src/lib/historyPaging.ts
  - vue_client/src/lib/bufferLifecycle.ts
- description: Downstream IRC registration, shared sessions, query routing, playback and timestamp-marker code
  paths:
  - server/services/bouncer.ts
  - server/routes/bouncer.ts
- description: Private annotations, drafts, bookmarks, reactions and ordering persistence
  paths:
  - server/db/nickNotes.ts
  - server/db/relayBots.ts
  - server/db/drafts.ts
  - server/db/bookmarks.ts
  - server/db/reactions.ts
  - server/db/pinnedBuffers.ts
  - server/db/favoriteBuffers.ts
  - server/routes/drafts.ts
  - server/routes/bookmarks.ts
- description: Ignore, highlight, theme and registry-driven personal preference code
  paths:
  - server/services/ignoreRulesService.ts
  - server/services/highlightRulesService.ts
  - server/services/themesService.ts
  - server/db/ignoredMasks.ts
  - server/db/highlightRules.ts
  - server/db/themes.ts
  - server/routes/settings.ts
  - shared/settingsRegistry.ts
  - shared/themePresets.ts
- description: Observed encrypted send, receive, refusal and plaintext-persistence call sites
  paths:
  - server/services/ircManager.ts
  - server/services/e2e/manager.ts
  - server/services/verbs/sendRaw.ts
  - server/services/bouncer.ts
- description: Upload classification, processing, destination selection, history and HTTP FILEHOST code
  paths:
  - server/routes/uploads.ts
  - server/routes/filehost.ts
  - server/routes/uploaders.ts
  - server/services/uploadService.ts
  - server/services/uploadLimits.ts
  - server/db/uploadHistory.ts
  - server/db/uploaderConfig.ts
- description: Push registration, transport rebinding, health, relay opt-in and delivery-policy code
  paths:
  - server/routes/push.ts
  - server/db/pushSubscriptions.ts
  - server/services/push/relay.ts
  - server/services/push/relayOrigin.ts
  - server/services/push/relayStatus.ts
  - server/services/pushService.ts
  - server/services/push/index.ts
  - server/services/wsHub.ts
- description: Archive jobs, validated replacement import and web completion code
  paths:
  - server/routes/exports.ts
  - server/services/exportJobs.ts
  - server/services/importService.ts
  - vue_client/src/components/settings-panes/DataPane.vue
  - server/db/exportSchema.ts
  - server/services/exportService.ts
- description: Effective retention, bookmark/reply protection and closed-subject collection code
  paths:
  - server/services/retentionSweeper.ts
  - server/services/retentionLimits.ts
  - server/db/retention.ts
  - server/routes/retention.ts
- description: Account, invitation, offering, storage, relay and lockout administration code
  paths:
  - server/routes/admin.ts
  - server/routes/adminNetworks.ts
  - server/routes/adminUploaders.ts
  - server/routes/adminPush.ts
  - server/routes/adminStorage.ts
  - server/middleware/rateLimit.ts
- description: Authenticated feature/about/bouncer information code
  paths:
  - server/routes/config.ts
  - server/routes/about.ts
  - server/routes/bouncer.ts
- description: Observed engine socket adoption and bounded backlog reconciliation call sites
  paths:
  - server/services/ircManager.ts
  - server/services/ircConnection.ts
  - server/engine/lineBuffer.ts
exclusions:
- description: CI and deployment/build machinery
  paths:
  - .github/
  - deploy/
  - Dockerfile
- description: Style and static asset implementation
  paths:
  - vue_client/src/assets/
- description: Test harness and fixture machinery
  paths:
  - server/test-utils/
unmapped:
- description: DCC transfer lifecycle and client presentation implementation
  paths:
  - server/services/dcc.ts
  - server/routes/dcc.ts
- description: Encryption trust, identity, handshake, distribution and portability implementation beyond traced
    messaging calls
  paths:
  - server/services/e2e/
  - server/db/e2e.ts
- description: Link-preview decoder/provider/cache lifecycle
  paths:
  - server/services/linkPreview.ts
- description: Remaining IRC protocol events and slash-command breadth
  paths:
  - server/services/ircConnection.ts
  - vue_client/src/lib/commands/
- description: Detailed input recall, typing and presence-probe behavior
  paths:
  - server/services/wsHub.ts
- description: Complete destination-specific provider deletion and authorization contracts
  paths:
  - server/services/uploadProviders/
- description: Complete push-provider payload and retry contracts
  paths:
  - server/services/push/
- description: Independent autonotes integration code
  paths:
  - integrations/autonotes/
- description: Sheep interaction implementation
  paths:
  - vue_client/src/lib/sheep/
  - vue_client/src/lib/commands/sheep.ts
- description: Operator recovery, folding and maintenance workflows
  paths:
  - tools/
- description: Managed-node/fleet and external moderation contract
  paths:
  - server/middleware/nodeAuth.ts
  - server/app.ts
- description: Engine topology, administrative control and deployment lifecycle beyond observed continuity
  paths:
  - server/engine/
limitations:
- description: External IRC, upload and push response behavior cannot be established solely from local call sites
  paths:
  - server/services/ircConnection.ts
  - server/services/uploadProviders/
  - server/services/push/
- description: External relay, preview decoder and control-plane implementations are absent from the inspected dependency
    call sites
  paths:
  - server/services/push/relay.ts
  - server/services/linkPreview.ts
  - server/middleware/nodeAuth.ts
- description: Native implementation and UI parity cannot be established from the client contract documentation
  paths:
  - docs/CLIENT_PROTOCOL.md
---

# Coverage


