# Codicium Web - Development Log

## Project Goal
A portfolio website representing Codicium's philosophy of "extremely simple apps that just work."

## Status
- Core landing page implemented.
- Links to privacy policy and app descriptions.
- Recently updated with improved descriptions for Pomodoro Voice and Huge Clock.

## Latest Changes
- Design polish pass (2026-07-05): SVG data-URI favicon, meta description + Open Graph/Twitter card tags, real "Get it on Google Play" badges replacing plain text links, "Live" status badges on each app card, staggered card fade-in on load, "Built with Flutter" footer credit.
- Made the card status badge robust to any viewport width by taking it out of flex flow (absolute-positioned in the card's top-right corner) instead of relying on flex shrink/wrap, which was fragile at narrow widths. Verified via computed `getBoundingClientRect()` that the badge stays inside the card bounds.
- Fixed Pomodoro Voice card linking to shared `privacy.html` instead of its own `pomodoro-voice-privacy.html` (2026-07-05).
- Pull everything from git (2026-07-05): pulled `index.html` revamp, `privacy.html` split, new `pomodoro-voice-privacy.html`, app icons for Huge Clock and Pomodoro Voice.
- Verified fresh builds exist for both apps: Huge Clock (release AAB, debug APK) and Pomodoro Voice (release AAB, debug APK), both built 2026-07-05.
- Pull everything from git (2026-02-12).
- Consolidated privacy policy into `privacy.html`.

## 2026-07-08
- Added Breathe Voice and Volt Timer cards, following the Pomodoro Voice precedent: each gets its own dedicated privacy page (`breathe-voice-privacy.html`, `volt-timer-privacy.html`), not the shared `privacy.html`.
- Neither app is on Play Store yet, so cards show a "Soon" status tag (not "Live") and have no Play Store badge link — added when each ships.
- New accent colors: teal for Breathe Voice, green for Volt Timer (matches Volt Timer's own in-app accent). Card hover glows and link colors follow.
- Permissions listed in each privacy page were verified against that app's actual `AndroidManifest.xml`, not copied blind from the existing template — Volt Timer's includes `VIBRATE` (haptics), Breathe Voice's doesn't.
- App icons resized to the existing 640x640 convention from each app's source `icon.png`.

## 2026-07-13
- Added JSON-LD structured data (`Organization` + `SoftwareApplication` per app) to `index.html`. Researched first: `llms.txt` checked against 2026 evidence (Google explicit non-signal, 97% of files get zero AI-bot traffic per Ahrefs 137k-site study) — skipped, doesn't work. Schema.org markup does have evidence (2.5x higher AI-answer citation rate per 2025 study, confirmed read by Google/Microsoft/ChatGPT) — added instead. Breathe Voice/Volt Timer entries omit `offers`/Play URL since neither is published yet, no fabricated data.
- Committed (`7c1390b`) and **pushed directly from this session** — owner set up git auth in this environment (not `gh` CLI, some other credential helper/PAT), confirmed working via `git fetch`/`git push` both succeeding, live on `origin/main`. First time a Claude Code session in this workspace could push without a manual owner step.

## 2026-07-14
- **Real bug found and fixed**: `pomodoro-voice-privacy.html` was never actually customized after being split off from the shared `privacy.html` (`80c4acb`) — title/meta description still said "Codicium Apps"/"Pomodoro Voice and Huge Clock", and the app-list badge row still linked out to Huge Clock's Play listing instead of its own. Fixed: title/description/app-list now Pomodoro Voice-only. Permission list was already accurate (verified against `pomodoro_voice`'s manifest — matches exactly), left as-is.
- **Real bug found and fixed**: `privacy.html` (now effectively Huge Clock-only per `[[codicium_web]]` vault note) still listed Pomodoro Voice in its app badges, and its permission list (`WAKE_LOCK`, `POST_NOTIFICATIONS`, `SCHEDULE_EXACT_ALARM`, `RECEIVE_BOOT_COMPLETED`, `INTERNET`, `BILLING`) was a leftover from when the page covered both apps. Checked huge_clock's actual manifest + pubspec deps: only `WAKE_LOCK` (from `wakelock_plus`), `INTERNET` (from `google_mobile_ads`), and `BILLING` (from `in_app_purchase`) are real — `POST_NOTIFICATIONS`/`SCHEDULE_EXACT_ALARM`/`RECEIVE_BOOT_COMPLETED` belong to `flutter_local_notifications`/alarm-manager, which huge_clock doesn't use. Trimmed to the 3 real ones. Bumped both pages' "Last updated" to July 14, 2026 since permission/app-scope claims materially changed.
- SEO hygiene pass: added `robots.txt` + `sitemap.xml` (didn't exist before), `<link rel="canonical">` on all 6 pages, completed `index.html`'s social meta (`og:site_name`, `twitter:title`/`description`/`image` — card previously only had `twitter:card` with nothing else set).

- Generated `assets/apple-touch-icon.png` (180×180): no rasterizer available (no ImageMagick/Inkscape/rsvg-convert/cairosvg/sharp installed), so redrew the same brand mark natively with Pillow instead of trying to rasterize the SVG — solid `#111111` bg, white "C" in Georgia Bold, flattened to RGB (no alpha, per Apple's own guideline). Wired `<link rel="apple-touch-icon">` into all 5 pages.

- Removed `SCHEDULE_EXACT_ALARM`/`RECEIVE_BOOT_COMPLETED` from `pomodoro-voice-privacy.html`'s permission list — a `pomodoro_voice` dependency audit found `android_alarm_manager_plus` unused and removed it + the manifest permissions that existed only for it, so this page needed to follow to stay accurate.

## Planned
- Enhance aesthetics with modern web design (richer gradients, micro-animations).
- Swap "Soon" → "Live" + add Play Store badges once Breathe Voice / Volt Timer are published.
