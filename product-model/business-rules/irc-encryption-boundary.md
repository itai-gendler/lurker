---
appliesTo:
- type: entity
  id: channel
- type: entity
  id: message
- type: entity
  id: reaction
references:
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/db/messages.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/reactions.ts
---

# IRC encryption boundary

Supported ordinary channel-message transport encrypts before upstream send, while server history can retain plaintext. Encryption failure never sends plaintext fallback. Action/notice/reaction have distinct refusal boundaries; manager action/notice refusal can return success with an app warning, so MCP can return {ok:true} without the send. MCP raw encrypted PRIVMSG is guarded, unlike the mapped WS raw path. Bouncer live traffic relays ciphertext, playback can reveal retained decrypted plaintext, and original upstream identity/reply tags can be absent.
