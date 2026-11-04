# ai-training-updates

Compiled AI Trainer v3 updates. Application source and personal data are excluded.

## Latest release

[AI Trainer 3.1.55 — paced preview scheduling](https://github.com/xgt2010x-a11y/ai-training-updates/releases/tag/v3.1.55)

Open the app's **Updates** tab, check for updates and download. Choose **Install and restart** when ready. This is a complete cumulative update: you can skip earlier versions. A complete program ZIP is also available from the release.

### Complete paced preview scheduling

Version 3.1.55 gives ready pictures one paced UI scheduler instead of waiting solely on WPF rendering callbacks. Raw pictures and annotations share a short coalescing deadline. Only one UI callback can wait, and a stalled UI resumes with the latest image. The configured video rate and Windows composition rate limit preview work. A native waitable timer keeps the cadence without changing the system-wide timer resolution. Busy bitmap surfaces retry through this same scheduler.

This addresses the ready-frame waiting found in the 3.1.53 trace. In a controlled test with rendering callbacks withheld, the previous path did not present within an 80 ms observation window; the new path presented in 16.0 ms. A paired-arrival model produces 60 dispatches for 60 captures and 120 raw/analysis arrivals. An isolated native dispatcher test sustains approximately 60 updates/s. These establish scheduling behavior, not physical gameplay smoothness or zero delay.

AI color status also expires when capture stops producing previews. Its brief self-refresh ends when the freshness lease expires, without another full-picture upload.

The pixel-picker, same-frame annotations, yellow box switch, bounded bitmap pool, Stop/reset, retry and disposal checks pass, including 185 existing preview checks. New heartbeat measurements separate ready-frame waiting from submission duration. The yellow box still starts hidden and can be shown under Live details.

The complete 1,961-file cumulative update includes all earlier features. Capture, detector/model, shot calculations and controller transport are preserved. Each PC keeps its current profiles, pairing and recordings. Install from Updates when ready.

### Paced preview scheduling (3.1.54, superseded)

Version 3.1.54 gives ready pictures one paced UI scheduler instead of waiting solely on WPF rendering callbacks. Raw pictures and annotations share a short coalescing deadline. Only one UI callback can wait, and a stalled UI resumes with the latest image. The configured video rate and Windows composition rate limit preview work. A native waitable timer keeps the cadence without changing the system-wide timer resolution. Busy bitmap surfaces retry through this same scheduler.

This addresses the ready-frame waiting found in the 3.1.53 trace. In a controlled test with rendering callbacks withheld, the previous path did not present within an 80 ms observation window; the new path presented in about 8 ms. A paired-arrival model produces 60 dispatches for 60 captures and 120 raw/analysis arrivals. An isolated native dispatcher test sustains approximately 60 updates/s. These establish scheduling behavior, not physical gameplay smoothness or zero delay.

The pixel-picker, same-frame annotations, yellow box switch, bounded bitmap pool, Stop/reset, retry and disposal checks pass, including 185 existing preview checks. New heartbeat measurements separate ready-frame waiting from submission duration. The yellow box still starts hidden and can be shown under Live details.

The complete 1,961-file cumulative update includes all earlier features. Capture, detector/model, shot calculations and controller transport are preserved. Each PC keeps its current profiles, pairing and recordings. Install from Updates when ready.

### Live yellow search box control (3.1.53)

Version 3.1.53 starts with the yellow search outline and its label hidden. Expand **Live details** below the preview and use **Show yellow search box** to compare while video runs. No Apply or capture restart is needed. Detection keeps using your applied search area; A/B marks, meter history and shot timing are preserved. The view starts hidden again on the next launch.

When hidden, changes only to search-box geometry no longer upload the same captured picture again. Visible meter drawing changes still upload correctly. This retains the 3.1.52 pacing correction without adding a per-frame dispatcher or timer.

An isolated 1080p CPU test measured roughly 0.014 ms extra drawing time for the box and label. It does not measure GPU presentation or establish the cause of whole-picture stutter. Live smoothness still needs comparison after installation.

All 1,961 program files and previous features are included. Capture/analysis, meter models, shot calculations and controller transport are preserved. Each PC keeps its settings, pairing and recordings.

### Preview dispatch regression correction (3.1.52)

Version 3.1.52 removes the extra per-frame dispatcher path introduced in 3.1.51 and restores the render-paced preview used in 3.1.50. This corrects excess submissions: raw pictures and their annotations coalesce before the render tick.

The same controlled raw-plus-annotation case uploaded 24 pictures in 12 render ticks with 3.1.51, and 12 with this correction. Existing preview, pixel-picker, overlay, busy-surface, reset, resolution and runtime checks pass. This is a correction for the reported regression; the earlier occasional stutter and physical display latency remain under investigation. Visible smoothness after installation still needs comparison.

This complete cumulative update retains all 1,961 program files and prior features. Meter models, capture/analysis, shot calculations and controller transport are preserved. Each PC keeps its settings, pairing and recordings.

### Fresh-frame preview scheduling (3.1.51, superseded)

Version 3.1.51 lets a freshly prepared video frame request a UI update alongside the existing rendering callback. Only one request can wait at a time, and newer pictures replace the pending image. This addresses a scheduling weakness that can leave a ready picture waiting when a render tick is delayed.

The prior version reproduced that wait in a controlled test with rendering callbacks withheld. The updated version presents the newest frame and coalesces 120 prepared pictures into one pending UI request. Pixel sampling, overlays, busy-surface retry, Stop/reset and the existing preview regressions pass. Actual visible smoothness after installation still needs comparison; this does not promise zero delay or eliminate every possible stutter.

This complete update includes all 1,961 program files and earlier updates. Capture/analysis, meter models, shot calculations and controller transport are preserved. Updates keep this PC's saved settings, pairing and recordings.

### Stable preview image binding

Version 3.1.50 keeps one image source attached to the preview control while the existing three reusable pixel buffers rotate behind a retained drawing. It follows V1's stable image-binding approach while preserving the buffer handling introduced in 3.1.49. Resolution changes update the drawing bounds; Stop releases the drawing and buffers. Bug-log heartbeats include a source-rebind counter.

The controlled 12-frame comparison reduced preview-control Image.Source assignments from 12 to one. 204 focused and existing checks passed, covering actual WPF drawing colors, resolution changes, pixel sampling, busy-buffer handling and cleanup. This is a presentation experiment, not a measured live FPS improvement; smoothness must be compared after installation.

Capture source/pacing, meter detection/models, shot timing, controller input and settings remain unchanged. This cumulative update includes all earlier releases.

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
