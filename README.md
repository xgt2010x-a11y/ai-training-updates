# ai-training-updates

Compiled AI Trainer v3 updates. Application source and personal data are excluded.

## Latest release

[AI Trainer 3.1.49 — preview presentation repair](https://github.com/xgt2010x-a11y/ai-training-updates/releases/tag/v3.1.49)

Open the app's **Updates** tab, check for updates and download. Choose **Install and restart** when ready. This is a complete cumulative update: you can skip earlier versions. A complete program ZIP is also available from the release.

### Preview presentation repair

Version 3.1.49 addresses a display bottleneck observed after 3.1.48: capture/analysis delivered about 60 frames per second while the HUD preview stayed near 20 fps. The display now rotates three reusable bitmap surfaces so it can use an idle surface when the renderer retains a recent one. It keeps only the latest pending image rather than queuing old pictures.

A failed upload leaves the previous picture and original-pixel sample paired. Stop releases the reusable surfaces and pending pixel leases. Bug logs now include render callbacks, uploads, busy deferrals, rejected frames, surface count and graphics render tier to identify any remaining presentation bottleneck.

The same controlled two-callback busy-renderer case accepted 4 of 12 new frames before and 12 of 12 afterward. 197 focused/existing preview checks passed, along with the earlier scheduling/preview regression harness. This simulates bitmap availability; a live after-install FPS comparison is still needed. Capture source/pacing, meter detection/models, shot timing and controller code remain unchanged. This cumulative update includes all earlier releases.

### Video, laptop controller and installation improvements

Version 3.1.48 gives the existing capture, analysis and preview workers dedicated threads. The preview defers a busy bitmap upload and avoids copying identical image/drawing updates. These changes passed isolated scheduling and presentation checks; actual smoothness still depends on the capture setup and PC.

Slow SDL startup now has up to five seconds to produce its first controller reading. Once acquired, the existing 250 ms stale-input cutoff remains active. The ordered PS5 helper writer has its own thread so a busy shared worker pool cannot hold up forwarding. Button order, neutralization, explicit arming, controller mapping and 4 ms polling remain unchanged. Two failure reproductions and 194 connection checks passed; the reported laptop still needs checking after installation.

Future installations verify existing file hashes and back up/replace only changed program files, preserving full signed-package authentication, final installed-file verification and rollback. The controlled 1,961-file, 8 MB synthetic install-only test fell from about 49 seconds to 16 seconds. This is not a full restart benchmark. The older helper installs this release, so the full speed benefit applies to subsequent updates installed by 3.1.48.

Timing algorithms, meter detection/models and the 3.1.47 controller crash repair are preserved. This is cumulative and includes all earlier updates.

### Controller crash repair

Version 3.1.47 fixes a Windows input-resource leak introduced by the SDL integration in 3.1.46. The reader now services its own hidden Windows input window and clears unused SDL events. It does not pump the app's UI thread or add another controller reader. The original leak reproduced at about 250 USER objects per second; the repaired two-minute native DualSense test held at 6-7 objects across 28,302 controller updates and returned to 1 on shutdown.

If 3.1.46 keeps crashing, reopen it and go directly to **Updates** before turning on **Read controller**. Install 3.1.47 and restart when ready. Timing calculations, meter detection/models, input mapping, polling interval and previews are unchanged. The native test read the controller without capture or PS5 output; it does not prove every possible crash is resolved.

### Controller reader and previews

Version 3.1.46 brings V1's SDL physical-controller read and attachment-check sequence into V3. Dedicated polling requests a 4 ms interval, while physical-device qualification, neutral output on detach and explicit output arming remain in place. Local checks passed, including unplug/reconnect and an occupied worker pool. Laptop hardware and the actual console connection still need testing after installation.

The **Controller** tab shows the V1 PS5 controller image. A compact copy also stays visible below the game picture across tabs. Purple marks held buttons. Both views share the existing physical input snapshot; they do not open a second controller reader.

The compact UI uses buttons and small **!** controls for details. It retains the saved profile picker, setup cues, themes and pinned Timing controls. Shot timing calculations, meter detection and models are unchanged in 3.1.46.

### App performance and reliability

Version 3.1.45 reduces repeated setup-status work and unnecessary download-progress callbacks. Cancelled downloads no longer repaint obsolete progress, and cancelling GitHub setup keeps private uploads OFF even if an earlier access check completes later.

It also fixes upload queues that could be saved but fail to reload on restart. State reads and writes now share a bounded size limit; oversized writes preserve the previous file. Duplicate identifiers are checked with a set, and the existing 10,000-recording queue cap is enforced on startup.

Diagnostic line parsing uses chunks, with identical prepared bundle hashes in the comparison tests. Isolated parser measurements do not establish higher capture FPS or better shot accuracy. Timing, meter detection, models, controller polling and output behavior are unchanged.

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
