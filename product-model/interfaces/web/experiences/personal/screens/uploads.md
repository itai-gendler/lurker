---
entities:
- entity: image-upload
  shows:
  - Filename
  - URL
  - Content type
  - Byte size
  - Dimensions
  - Thumbnail
  - Favorite status
  - Removal status
- entity: file-upload
  shows:
  - Filename
  - URL
  - Content type
  - Byte size
  - Favorite status
  - Removal status
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
- kind: code
  role: implementation
  target: vue_client/src/components/settings-panes/UploadsPane.vue
---

# Uploads

Owned image/file history, favorites and removal status; excludes private deletion references from ordinary feeds.
