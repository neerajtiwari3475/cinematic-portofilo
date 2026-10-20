# The build briefs — how this portfolio was directed

A record of the creative direction each scene was built from, in the order it
arrived. Every brief came with reference assets (images/videos in the project
root), and every brief carried the same standing rules:

- **The supplied reference is the pixel-level source of truth.** Replicate it
  as closely as technically possible; never generate replacement assets —
  anything needed is extracted from the references themselves.
- **Entrances are choreographed, never plain fades**: darkness → light →
  atmosphere → elements → settle → subtle continuous life (~2s reveals).
- **Card sets appear as ONE coordinated event**, never one-by-one.
- **The person is the main character** and layers IN FRONT where the brief
  says so.
- **Strict palette discipline per scene**; premium and restrained, not flashy.
- **Portrait recomposes intelligently** — never just shrinks desktop.

## Scene 1 — Cinematic hero opening
Black screen → the walking man (video 1, white backdrop removed, no visible
rectangle) enters centre → the giant red distressed PSYCHO2.9 rises from below,
dissolving and sharpening in → WELCOME TO MY WORLD drops in front → chips,
arrows and dots fly in → header reveals → settled hero with subtle motion and
mouse parallax. Mid-build corrections: videos 2 & 3 removed entirely; the
top-left dot cluster removed; final layering fixed as background → PSYCHO2.9 →
walking person IN FRONT → labels → header, with the animated reveal kept.

## Scene 2 — The creative universe
All twelve tool cards materialise TOGETHER, rise bottom-to-top as one event,
settle, then float; red energy lines draw and travel; central circle alive.
Superseded by direction: play the supplied reference film itself as the
section ("i just want to see the section 2 video"), then "add text on the
video" — the chapter title now sits over the footage; the loop seam hides
behind a breathing veil.

## Scene 3 — A journey through time
Match the reference: giant clock whose hand is driven by the cursor mapped
intelligently to the years 2021–2026 (projection onto the timeline, not raw
mouse X), smooth inertia, active-year cards, curved rail, rotating floor
rings, warm amber/red grading. Final corrections: person slightly left and
BROUGHT IN FRONT of the cards (his own layer over the deck), visible via
reference lighting (warm pool, wraparound rim, floor bounce — not brightened),
clock rebuilt to the reference (ball pivot, divider-pose hands, ornate screw
ornament, beam projecting light into the active year), year labels dark and
warm rather than white pills.

## Scene 4 — The project universe
Replicate the reference inch-for-inch: the amphitheatre of twelve project
screens around the creator. Built by cutting the reference apart — every card
becomes a sprite of the reference's own pixels, the emptied room becomes the
plate the shader stages and re-lights (ring, floor-circle ignition, wet
shimmer). Cards rise as one system with pop-overshoot and dephased floating;
pointer moves the whole universe by depth; hover lifts a card while its
siblings ease back; scroll dollies in.

## Scene 5 — Certifications (built, then removed)
A man walks out of darkness into a cyan world; five glass plaques summoned as
one event. Required a black-void matte preset (subject brighter than the
backdrop, detached smoke kept, silhouette solidify with a tracked soft
corridor, luminance-shaped smoke translucency). The section was later deleted
at the client's direction; its tools remain in `tools/` for regeneration.

## Finale — the closing shot (footer)
Replicate `Footer image.jpg` exactly: the reference itself is split into
layers — the smoking man GrabCut-matted out of the artwork, everything else
(wordmark + red fog) becoming a plate staged by a luminance-gated reveal (the
title surfaces through the fog and sharpens). Captions return as live DOM;
a whispering functional row carries contact/socials/copyright. A later brief
added a SECOND frame: past the settled scene, extra scroll slides the
supplied Ferrari still in from the left — damped progress, blur-to-sharp,
leading-edge shadow — the film's last cut.

## Contact links from environment variables (replaces the owner dashboard)

The earlier owner-dashboard brief is **removed completely**: no dashboard, no
login, no database, no one-time codes, no email/SMS provider, no sessions, no
secret encryption. The only things the owner ever needs to change are four
contact destinations (Telegram account, Telegram channel, YouTube channel,
email), and those live in the hosting platform's environment variables.

**Hard rule: this is purely additive.** The public site's visuals, layout,
sizes, type, colours and timings do not change except where the *Theme and
responsive layout* section below explicitly says so.

| Variable | Purpose | Example (placeholder) |
| --- | --- | --- |
| `PUBLIC_SITE_URL` | canonical origin used in meta tags, sitemap, Open Graph | `https://your-domain.example` |
| `TELEGRAM_PROFILE_URL` | where the "profile" contact action goes | `https://t.me/your_username` |
| `TELEGRAM_CHANNEL_URL` | where the "channel" contact action goes | `https://t.me/+invite_code` |
| `YOUTUBE_URL` | where the "YouTube" contact action goes | `https://www.youtube.com/@your_channel` |
| `CONTACT_EMAIL` | address the "Email" contact action opens | `you@example.com` |
| `GRIEVANCE_EMAIL` | public privacy/grievance address (see DPDP pass) | `privacy@example.com` |

- Ship an `.env.example` with placeholders only; `.env` and `.dev.vars` are
  git-ignored. Real values are entered in the host's dashboard.
- **Hiding the links:** the page never contains the Telegram URLs or the
  contact email. The footer's four contact links (Telegram, Channel, YouTube,
  Email) point to same-origin routes `/go/profile`, `/go/channel`, `/go/youtube`
  and `/go/email`; `functions/go/[target].js` reads the variable at request
  time and answers `302`. It accepts only `https://t.me/...`,
  `https://telegram.me/...` and YouTube hosts (no open redirects), turns the
  email into a `mailto:` redirect, sends `Referrer-Policy: no-referrer`, and
  uses `no-store`. The only contact actions are those four: no Instagram,
  Behance, LinkedIn or other social links.
- **Email:** `/go/email` redirects to `mailto:` + `CONTACT_EMAIL`, so the
  address is never printed in the markup. A copy-to-clipboard button is an
  optional later extra.
- **Changing a link later:** edit the variable in the host dashboard and
  redeploy (variables apply to the next deployment). Every visitor then gets the
  new destination. Nothing is stored anywhere else.
- Be honest in the README: hiding a URL deters casual viewing only; anyone who
  clicks still learns the destination.
- Use real brand logos (Telegram, YouTube, a mail icon) on contact actions, in the
  site's existing visual language.
- Target host: **Cloudflare Pages** (static files + Pages Functions). Keep the
  site itself static with no build step.

## Theme and responsive layout (new scope)

The site must follow the device on two axes, automatically.

**Automatic light / dark theme**

- Follow the operating system: `prefers-color-scheme`, no toggle button, live
  update when the OS setting changes (listen with `matchMedia(...).addEventListener`).
  Add `<meta name="color-scheme" content="dark light">` and two `theme-color`
  metas with `media` queries.
- **Dark stays the current look, pixel-for-pixel at 16:9.** Light is a new,
  deliberately designed theme: reuse the existing CSS custom properties and add
  light overrides; keep the brand red; paper-light ground, ink-dark type.
- The WebGL scenes and baked art (hero, finale plate, section images) are
  red-on-black. Decide and document one approach per scene: a shader-level
  treatment, or light-variant assets produced by the `tools/` pipeline from the
  supplied references (never invented art). State anything left dark by design.
- Contrast: body and caption text meet WCAG AA in both themes.

**Every screen shape**

- Phones in portrait (9:16, 9:19.5, 9:20), phones in landscape, tablets
  (3:4 / 4:3), laptops (16:10, 16:9), desktops (16:9), ultrawide (21:9, 32:9
  capped). The page must fill the viewport with no horizontal scroll and no
  letterboxing bars.
- The standing rule stands: **portrait recomposes intelligently, never just
  shrinks desktop.** Inventory what already exists (the finale already switches
  below an aspect of 0.75), then art-direct each aspect bucket: focal points,
  wordmark scale (never stretched), crop of the person, caption placement.
- Use `svh`/`dvh`/`lvh` and `env(safe-area-inset-*)` so mobile browser bars and
  notches do not break the pinned, scroll-driven scenes; no layout thrash on
  address-bar resize.
- Mobile performance: `playsinline muted` video, poster frames, lazy-load
  heavy media, lighter variants on small screens or `Save-Data`, and keep
  `prefers-reduced-motion` support.
- **Test matrix** (Playwright, screenshots committed to `shots/`):
  390×844, 360×800, 412×915, 844×390, 768×1024, 1024×768, 1366×768, 1440×900,
  1920×1080, 2560×1080, 3440×1440, in dark and light. Include a regression
  check that dark 1920×1080 matches the current build.

## Privacy and DPDP pass (scaled to what the site really collects)

Work on branch `compliance/dpdp`. **Do not push.** Log every decision in
`DPDP_PROGRESS.md`. Nothing here is legal advice; mark all legal copy
**"FOR LEGAL REVIEW"**.

Context (checked October 2026): the DPDP Act 2023 and Rules 2025 are in force
in phases; the main obligations and penalties apply from about May 2027, with
some provisions earlier, and sources differ on a few dates. Maximum penalty is
up to **₹250 crore** (₹2,500 million) for failing to keep reasonable security
safeguards, up to ₹200 crore for failing to notify a breach.

**Pre-audit findings** (verified in this codebase; re-verify):
no forms or inputs, no cookies, no `localStorage`/`sessionStorage`, no
analytics or ad trackers, no third-party scripts, fonts self-hosted, no
external URLs; the only `fetch` calls load the site's own JSON, plus dev-only
screenshot hooks (`window.__shot*` → `/__shot`). The remaining personal data is
what the host and the `/go/*` functions log (IP addresses, user agents).

Do:

1. **Audit** collection points, trackers and third-party services, and record
   them in `DPDP_PROGRESS.md`. If a category is empty, say so and mark the
   dependent items below "not applicable — nothing to protect".
2. **Privacy Notice page** (`/privacy`): what data (none collected by the site
   itself; host/redirect logs), why, retention (as set by the hosting
   provider), third parties (hosting provider; Telegram once a visitor leaves),
   rights (access, correct, erase, withdraw), grievance contact. Match the
   existing visual language; link it from the footer without changing the
   footer's layout.
3. **Consent checkboxes** (unticked, per purpose, stored consent records) only
   where a data-entry point exists. There is none today; do not invent forms
   or a database to host consent.
4. **Trackers:** ship none. If analytics is ever added, it loads only after a
   consent banner and is documented in the notice.
5. **Grievance contact** in the footer and on the privacy page, using
   `GRIEVANCE_EMAIL` (a dedicated address, separate from the hidden
   `CONTACT_EMAIL`). Counsel decides whether plain text is required.
6. **Data-rights requests:** an email path to the grievance address with the
   response procedure written down; no form, no database.
7. **Terms page** with a data-protection clause (for legal review).
8. **`BREACH_RUNBOOK.md`:** intimation to affected users without delay, detailed
   report to the Data Protection Board within 72 hours, notice templates,
   evidence log, owner roles. Realistic scenarios for this site: host account
   takeover, leaked environment variable, domain hijack, tampered deployment.
   Note that CERT-In reporting may apply separately (counsel to confirm).
9. **Security gaps** to flag and fix: HTTPS and HSTS enforced; no secrets in
   client code; dev-only `__shot` hooks removed or limited to localhost;
   security headers (CSP, `X-Content-Type-Options`, `Referrer-Policy`,
   `Permissions-Policy`); report "unverified captcha" and "fail-open
   encryption" as not applicable unless those features are added.

Finish `DPDP_PROGRESS.md` with: what was built, what needs lawyer review, open
items.

## Discoverability and SEO (delivered; keep and extend)

Already in the project, do not remove: `robots.txt` (disallows `/go/`),
`sitemap.xml`, `llms.txt`, canonical URL, Open Graph and Twitter-card tags,
JSON-LD (`WebSite` + `Person`), a 1200×630 `public/og-image.jpg` and favicons
cut from the supplied reference art, and commented-out verification tags for
Google Search Console and Bing Webmaster Tools. Every absolute URL uses the
placeholder `https://YOUR-DOMAIN`, which `tools/build_site.sh` replaces with
`PUBLIC_SITE_URL` at deploy time and fails the build if any placeholder is
left. Never invent a domain, and never hand-edit the deployed copy.

When the DPDP pass adds `/privacy` and `/terms`, add them to `sitemap.xml` and
`llms.txt`. Be honest in the README that `llms.txt` is not a Google ranking
factor. Step-by-step launch order: `docs/LAUNCH_ROADMAP.md`.

## Cross-cutting passes
- **Background-removal fixes**: repeated briefs demanded frame-stable person
  isolation — no halos, no flicker, cigarette and natural smoke preserved,
  "filmed inside the environment" compositing (room-tinted smoke, rim light
  from each room's glow).
- **Final polish pass**: every section awakens on screen (reveal thresholds
  raised), ~2s reveal pacing, buttery easing, HD sprite sharpening, 60fps.

The technical companion to this document is the README, which explains how
each direction was implemented.
