# ai-training-updates

Compiled AI Trainer v3 updates. Application source and personal data are excluded.

## Latest release

[AI Trainer 3.1.44 — Clearer setup, profiles and portable PS5 fixes](https://github.com/xgt2010x-a11y/ai-training-updates/releases/tag/v3.1.44)

Open the app's **Updates** tab, check for updates and download. Choose **Install and restart** when ready. This is a complete cumulative update: you can skip earlier versions. A complete program ZIP is also available from the release.

### Clearer setup

The header and stopped preview show one next-step action. Four status cues show the game picture, controller, PS5 connection and control forwarding. Timing keeps **Apply changes** and **Turn controls ON** fixed below its settings. Short hints, expandable help, clearer bug-log labels and both dark and light themes are included. These UI changes preserve the shot timing calculations, meter models and controller behavior.

### Saved profiles

Use **Profile** under AI Trainer to select a saved setup, or **+ Create** to copy the settings shown. Switching saves the current profile's edits and stops video and forwarding before loading the chosen setup. Start video and turn controls ON again when ready. The last selected profile returns at startup. Default starts with existing settings; PS5 pairing stays separate.

### PS5 fixes for other PCs

The package now includes required compiled Python modules that earlier portable packages omitted. The complete bundled PS5 runtime is checked without global Python before packaging. Pairing, Forget and changed-address operations preserve the saved list if encrypted storage cannot be written. Pair each PC separately, using that console's address, the correct PSN account ID and a fresh eight-digit pairing code. Encrypted pairing files cannot be transferred between Windows accounts.

Automated runtime, UI, profile and simulated connection checks passed. Network conditions and live console behavior still need checking on the actual setup; these checks do not establish live shot accuracy.

### Private bug-log uploads

In **Help & logs**, expand **Send bug logs to your private GitHub**. Connect GitHub once on each PC using an account with write access to the private diagnostics repository. New completed Record bug logs upload as private draft-release assets when enabled. Uploads wait while forwarding is armed, then resume when it is off or V3 reopens. Offline failures stay queued; original recordings stay local.

Bundles contain redacted diagnostics. Gameplay video, meter photos, historical recordings and account credentials are not automatically uploaded. GitHub authorization stays on each PC. This public repository contains program releases and public instructions only.

Each computer keeps its settings, device choices, PS5 pairings and recordings when updating. The update retains the mint A / white T branding, Neon Pulse and Frosted Studio themes, earlier Timing controls and private log uploads.
