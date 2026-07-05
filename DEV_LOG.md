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

## Planned
- Enhance aesthetics with modern web design (richer gradients, micro-animations).
- Ensure SEO best practices.
- Add more visual showcases for the apps.
