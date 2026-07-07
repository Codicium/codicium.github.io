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

## Planned
- Enhance aesthetics with modern web design (richer gradients, micro-animations).
- Ensure SEO best practices.
- Swap "Soon" → "Live" + add Play Store badges once Breathe Voice / Volt Timer are published.
