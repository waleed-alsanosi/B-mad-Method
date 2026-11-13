---
name: Rebat
description: رباط — subscription university transport for Saudi students. Trustworthy, calm, official-feeling without being cold; Arabic-first RTL with a parallel English/LTR track.
status: draft
updated: 2026-11-13
colors:
  primary-default: '#063354'
  primary-hover: '#052e4c'
  primary-active: '#05263f'
  primary-muted: '#19456b'
  primary-soft: '#f8f1f1'
  primary-soft-hover: '#efeaea'
  primary-inverse: '#16c79a'
  accent-default: '#16c79a'
  accent-soft: '#f3fcfa'
  content-default: '#03192a'
  content-strong: '#4c4a4a'
  content-subtle: '#666363'
  content-muted: '#615f5f'
  content-inverse: '#ffffff'
  surface-default: '#f8f1f1'
  surface-raised: '#ffffff'
  surface-sunken: '#f8f1f1'
  surface-sunken-soft: '#f8f1f1'
  surface-inverse: '#03192a'
  surface-inverse-raised: '#05263f'
  line-default: '#e5e3e3'
  line-soft: '#efeaea'
  line-strong: '#c4c2c2'
  muted-default: '#4c4a4a'
  muted-soft: '#efeaea'
  muted-solid: '#c4c2c2'
  danger-default: '#e11d48'
  danger-strong: '#be123c'
  danger-muted: '#f43f5e'
  danger-soft: '#fff1f2'
  danger-soft-strong: '#ffe4e6'
  danger-line: '#fecdd3'
  danger-line-strong: '#fda4af'
  warning-default: '#b45309'
  warning-strong: '#92400e'
  warning-soft: '#fffbeb'
  warning-soft-strong: '#fef3c7'
  warning-line: '#fde68a'
  warning-line-strong: '#fcd34d'
  success-default: '#0d775c'
  success-solid: '#16c79a'
  success-soft: '#f3fcfa'
  info-default: '#2563eb'
  info-soft: '#eff6ff'
  rating: '#f59e0b'
  focus: '#063354'
  scrim: '#02101a'
  hover-wash: 'rgba(3,25,42,0.05)'
  gradient-from: '#19456b'
  gradient-via: '#063354'
  gradient-to: '#041f33'
  on-primary: '#ffffff'
  on-primary-inverse: '#03192a'
  on-accent: '#03192a'
  on-danger: '#ffffff'
  on-success: '#03192a'
typography:
  display:
    fontFamily: Tajawal
    note: 'Logo lockup and splash tagline only — see Brand & Style'
  heading:
    fontFamily: Tajawal
    fontWeight: 700
  body:
    fontFamily: Tajawal
    fontWeight: 400
  label:
    fontFamily: Tajawal
    fontSize: 10.5px
    note: 'Smallest observed size, used for design-token captions and the tightest badge text'
rounded:
  sm: 8px
  md: 12px
  lg: 16px
  full: 9999px
spacing:
  '1': 4px
  '2': 8px
  '3': 12px
  '4': 16px
  '5': 24px
  '6': 32px
components:
  button-primary:
    background: '{colors.primary-default}'
    text: '{colors.on-primary}'
    radius: '{rounded.full}'
    hover: '{colors.primary-hover}'
    active: '{colors.primary-active}'
  button-danger:
    background: '{colors.danger-default}'
    text: '{colors.on-danger}'
    radius: '{rounded.full}'
  button-danger-outline:
    background: transparent
    border: '{colors.danger-line}'
    text: '{colors.danger-default}'
    radius: '{rounded.full}'
  button-outline:
    background: transparent
    border: '{colors.line-default}'
    text: '{colors.content-default}'
    radius: '{rounded.full}'
  button-ghost:
    background: transparent
    text: '{colors.primary-default}'
    radius: '{rounded.full}'
  status-badge-positive:
    background: '{colors.success-soft}'
    text: '{colors.success-default}'
    radius: '{rounded.full}'
  status-badge-negative:
    background: '{colors.danger-soft}'
    text: '{colors.danger-default}'
    radius: '{rounded.full}'
  status-badge-warning:
    background: '{colors.warning-soft}'
    text: '{colors.warning-default}'
    radius: '{rounded.full}'
  status-badge-neutral:
    background: '{colors.muted-soft}'
    text: '{colors.muted-default}'
    radius: '{rounded.full}'
  status-badge-info:
    background: '{colors.info-soft}'
    text: '{colors.info-default}'
    radius: '{rounded.full}'
  status-badge-brand:
    background: '{colors.accent-soft}'
    text: '{colors.accent-default}'
    radius: '{rounded.full}'
  choice-pill-selected:
    background: '{colors.primary-default}'
    text: '{colors.on-primary}'
    radius: '{rounded.full}'
  choice-pill-idle:
    background: '{colors.surface-raised}'
    border: '{colors.line-default}'
    text: '{colors.content-default}'
    radius: '{rounded.full}'
  app-card:
    background: '{colors.surface-raised}'
    radius: '{rounded.md}'
    border: '{colors.line-soft}'
  info-banner:
    background: '{colors.primary-soft}'
    text: '{colors.primary-default}'
    radius: '{rounded.sm}'
  text-field:
    background-white: '{colors.surface-raised}'
    background-grey: '{colors.surface-sunken}'
    radius: '{rounded.sm}'
    border: '{colors.line-default}'
  bottom-nav:
    background: '{colors.surface-raised}'
    active-icon: '{colors.primary-default}'
    inactive-icon: '{colors.content-muted}'
  admin-sidebar:
    background: '{colors.surface-inverse}'
    active-item: '{colors.primary-muted}'
    text: '{colors.content-inverse}'
---

## Brand & Style

Rebat reads as **official but warm** — the visual register of a service parents and students need to trust with a daily commute, not a consumer lifestyle app chasing engagement. The dominant mode is a deep navy (`primary-default`, `#063354`) paired with a single chromatic accent, a teal-green (`accent-default`, `#16c79a`) that also anchors the logomark. Everything else — surfaces, text, lines — sits in a restrained warm-neutral family (`surface-default` `#f8f1f1`, a soft rose-cream, not pure white) that keeps the product from feeling clinical or governmental despite its compliance-heavy subject matter (driver vetting, WASL/ELM, Absher).

The brand needs to hold three registers at once: a splash screen with ambient teal/navy gradient blooms (aspirational, calm), dense operational tables in the Admin console (functional, scannable), and safety-critical moments — SOS, incident reporting, account deletion — that must read as serious without becoming alarming. The palette is built for this: one accent carries all positive/brand moments, a dedicated `danger` family (distinct from `warning`) is reserved specifically for destructive and emergency actions, and `rating` (`#f59e0b`, amber) is scoped to star ratings only, never reused as a generic warning color.

Arabic-first, right-to-left; every surface has a mirrored LTR/English counterpart built into the component library itself (AppBar, BottomNav, TextField, TabHeader, AdminSidebar, AdminTopbar all ship RTL and LTR variants), not bolted on after the fact.

## Colors

The system is organized as semantic pairs (`default` / `soft` / `strong` / `line`), not a raw palette — every screen pulls meaning from the token name, not the hex value.

- **`primary` (navy family, anchored on `#063354`)** — the brand's authority color. Primary buttons, the Admin sidebar, headers, and the splash/onboarding gradient all draw from this family. `primary-soft` (`#f8f1f1`) doubles as the default page background across the whole product — it's warm enough to avoid looking like a form, cool enough to stay out of the way of content.
- **`accent` (teal, `#16c79a`)** — the one chromatic color allowed outside semantic states. Reserved for the logo, the splash tagline, success-adjacent brand moments, and anywhere the product wants to feel alive rather than official. Never used for destructive or warning states — those have their own families.
- **`danger` (rose-red, anchored on `#e11d48`)** — destructive actions and emergencies only: SOS, account deletion, void invoice, cancel trip, reject application. Distinct from `warning` (amber-brown, `#b45309`) which is reserved for "needs attention but not broken" states — overdue compliance checks, pending items, "due soon" flags.
- **`success` (`#0d775c` / solid `#16c79a`)** and **`info` (`#2563eb`)** are standard semantic states — payment succeeded, document verified, informational banners.
- **`rating` (`#f59e0b`, amber/gold)** is its own token, intentionally separate from `warning` even though both read as amber — ratings are never a negative signal and shouldn't borrow warning's connotation.
- **`surface` family** gives three depths: `surface-default` (`#f8f1f1`, page background), `surface-raised` (`#ffffff`, cards and sheets), `surface-inverse` (`#03192a`, the Admin sidebar and dark-ground moments like the splash screen).

Avoid: using `danger` for anything short of destructive/emergency (it dilutes the one signal that should make a user stop and read); reusing `accent` as a generic "positive" color where `success` is more precise; introducing a new chromatic color outside this set.

## Typography

**Tajawal** throughout, chosen for strong Arabic letterforms that also render cleanly in Latin for the English/LTR track — this is why there's one font family doing both jobs rather than a per-language pairing. Weight carries hierarchy more than size: headings and emphasis use Tajawal Bold (700), body text uses Tajawal Regular (400). The smallest observed size in the live file is 10.5px (design-token captions, the tightest badge text) — treat that as a practical floor, not a target; body copy throughout the audited screens reads comfortably larger.

## Layout & Spacing

Scale: 4 / 8 / 12 / 16 / 24 / 32px (`spacing.1`–`spacing.6`). Mobile screens (Student, Driver) are built on a 375×812 base frame — standard small-to-mid phone width, so layouts should assume no generous horizontal breathing room and lean on vertical rhythm instead. The Admin console is a fixed 1440×900 desktop frame with a 256px fixed sidebar (`AdminSidebar`) — not responsive by evidence in the file; treat sub-1440 breakpoints as undesigned rather than assuming adaptive behavior.

Bottom-anchored primary actions are the mobile convention throughout: CTAs pin to the bottom of the screen above a safe-area gutter rather than inline with content, consistent with the generous-empty-space-above-a-pinned-CTA pattern seen on sign-in, payment, and confirmation screens alike.

## Elevation & Depth

The system favors **flat, card-based separation** over shadow-driven elevation. `surface-raised` (white cards) against `surface-default` (cream page background) does the work that drop-shadows would do elsewhere — the tonal contrast between the two surface tokens, not a shadow, is what reads as "this is a distinct, tappable unit." Sheets and modals (the many bottom-sheet confirmations throughout the product — payment states, cancellation reasons, SOS) use a `scrim` (`#02101a`) backdrop rather than a shadow to separate from the page beneath.

## Shapes

Rounded corners throughout, scaling with surface size: `rounded.sm` (8px) for inputs, chips, and the design-token swatches themselves; `rounded.md` (12px) for cards; `rounded.full` (pill/9999px) for buttons, status badges, and choice pills. The full-pill button shape is load-bearing brand identity — it appears on every primary CTA across all three surfaces and is one of the most consistent visual signatures in the product. Nothing in the audited screens uses a sharp (0px) corner.

## Components

- **Button** — 11 named styles observed (Primary, Secondary, Outline, Subtle, PrimaryOutline, Danger, DangerSoft, Ghost, Inverse, Muted, DangerOutline), all pill-shaped (`rounded.full`). Primary is solid navy/`on-primary` text; Danger and DangerOutline are reserved for destructive confirmations (delete account, cancel trip, void invoice); Ghost/ Muted are used for secondary/tertiary actions like "Cancel" or "Skip" sitting beside a primary CTA.
- **StatusBadge** — 6 tones (positive, neutral, negative, warning, info, brand), always pill-shaped, soft-background + strong-text pairing (e.g. `success-soft` background with `success-default` text) rather than solid fills — this is the pattern behind every status chip seen throughout the audit (Verified/Under review/Suspended, Open/In progress/Resolved, Active/Expired/Pending).
- **ChoicePill** — 4 states (selected, idle, filled, disabled), used for single-choice selections like trip direction or region filters; selected state inverts to solid `primary-default`.
- **AppCard** — the base `surface-raised` container (327×140 in the token file) underlying list rows throughout — driver cards, trip cards, subscription cards.
- **TextField** — white or grey fill, hint or value state, full RTL/LTR pairing — the standard input across all three surfaces.
- **InfoBanner** — the `primary-soft` background callout used repeatedly for reassurance copy ("There is no password," "Numbers masked on both sides," privacy/trust statements) — this component is doing real brand work; see Voice and Tone in EXPERIENCE.md.
- **AppBar / BottomNav / DriverNav / AdminSidebar / AdminTopbar / TabHeader** — the full navigation chrome set, each with RTL and LTR variants built in rather than mirrored at runtime.
- **Avatar** (3 sizes: 32/44/56px) and **Switch** (on/off) — standard utility components appearing throughout settings and list rows.
- **Logo/lockup** — navy and inverse (white) tone variants, for use on light and dark/`surface-inverse` backgrounds respectively.

## Do's and Don'ts

- **Do** keep `danger` scoped to destructive/emergency actions only — SOS, delete account, cancel trip, void invoice, reject application. Diluting it into routine negative states (e.g., "Expired" badges) would blunt the one color meant to make users stop and read carefully.
- **Do** use the soft-background/strong-text badge pairing for all status chips — it's the established pattern and reads consistently across all three surfaces.
- **Do** build RTL and LTR as first-class variants of every navigation/chrome component, not as a runtime mirror — that's how the existing system is built and how it should stay.
- **Don't** introduce a new chromatic color outside `primary` / `accent` / `danger` / `warning` / `success` / `info` / `rating` — the restraint is deliberate and load-bearing for the "official but warm" brand read.
- **Don't** use sharp corners anywhere — the full-pill button and rounded-card language is a consistent brand signature across all three surfaces.
- **Don't** assume the Admin console adapts below 1440px — no sub-desktop layout was found in the design file; treat responsive admin behavior as undesigned, not just unconfirmed.
