# Forbidden Apple Tavern SillyTavern Theme Preview

This repository contains a Forbidden Apple Tavern visual theme package for SillyTavern-style chat previews.

## Main demo

Open:

```text
forbidden-apple-tavern-full-demo.html
```

The demo uses hosted image URLs from GitHub raw so it can act like a real image-hosted theme preview.

## Hosted frame assets

The six v5 three-slice PNG assets are stored in:

```text
chat-frame-assets/generated-three-slice-v5/
```

External image URLs are recorded in:

```text
chat-frame-assets/hosted-three-slice-v5-urls.json
```

## CSS snippets

- `forbidden-apple-chat-frame-three-slice-hosted.css`: three-slice hosted-image version.
- `forbidden-apple-chat-frame-stretchable.css`: older Catbox whole-frame border-image experiment.
- `forbidden-apple-tavern-beautified-overrides.css`: general SillyTavern beautification pass.
- `forbidden-apple-tavern-catbox-icon-overrides.css`: hosted icon override pass.

## Notes

Catbox upload was attempted for the v5 three-slice PNG files, but catbox.moe reset the upload connection from this environment. The complete demo therefore uses GitHub raw URLs as the image host.
