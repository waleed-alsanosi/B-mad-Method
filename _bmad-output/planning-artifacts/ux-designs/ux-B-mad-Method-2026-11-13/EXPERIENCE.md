---
name: Rebat
status: final
sources:
  - _bmad-output/planning-artifacts/prds/prd-B-mad-Method-2026-11-13/prd.md
  - user-stories-student.md
  - user-stories-driver.md
  - user-stories-admin.md
updated: 2026-11-13
---

# Rebat — Experience Spine

> Documents the existing, built design (Figma file "Rebat-Project", 185+ screens read screen-by-screen across three audits) rather than proposing new UX — per explicit product decision. Paired with `DESIGN.md` for visual identity. Where source docs mark a behavior "Unconfirmed," this spine says so rather than inventing a resolution — see the Open Questions carried in the PRD (§9).

## Foundation

Three surfaces, one backend:

- **Student app** — mobile, Flutter, iPhone + Android (iPhone-only device family per the driver doc's iOS readiness notes; no tablet layout found). Arabic RTL primary, English LTR secondary (first-release inclusion unconfirmed — PRD §9 item 12).
- **Driver app** — mobile, Flutter, same platform/RTL posture as Student.
- **Admin console** — desktop web, React 19 + Vite + Tailwind v4, fixed 1440×900 frame with a 256px sidebar; no sub-desktop layout found in the design file (see `DESIGN.md` → Layout & Spacing).

No named external UI system (shadcn/MUI/etc.) — Rebat ships its own token-based design system (`DESIGN.md`), built and versioned directly in the Figma file (visible `__VERSION__`, `__REGISTRY__`, `__KIT__` metadata nodes) rather than inherited from a library. `DESIGN.md` is the visual identity reference for every token and component named below.

## Information Architecture

### Student app

| Section | Reached from | Purpose |
|---|---|---|
| A · Onboarding & Sign-in | Cold open | Splash, 3-slide onboarding, phone+OTP auth, university/pickup setup |
| B · Subscribe & Pay | Bottom nav "Plan" | Plan selection, trip-direction pricing, Moyasar payment, 4 payment-state sheets, subscription status (active/searching/team-contacting), day-by-day schedule |
| C · Daily Trip | Bottom nav "Home" / "Trips" | Home trip card, live tracking, trip details, rating, incident report, skip/apology sheet, SOS |
| D · Chat & Support | Bottom nav "Chats" | Driver chat (numbers masked), support tickets, notifications, announcements, help FAQ |
| E · Account & Settings | Bottom nav "Account" | Profile, university/pickup editing, lecture schedule, trusted contacts, notification prefs, language, account deletion |

Bottom nav: Home / Plan / Trips / Chats / Account (`BottomNav` component, RTL/LTR variants).

### Driver app

| Section | Reached from | Purpose |
|---|---|---|
| A · Onboarding & Registration | Cold open | Splash, onboarding, phone+OTP, 6-step application (personal info, documents, face check, vehicle, availability, review), pending-review status |
| B · Run a Route | Bottom nav "Home" / "Routes" | Availability toggle, tomorrow's-rides confirmation, route list, 6-state active-trip machine, start/end trip sheets, reorder stops, reassignment request |
| C · Requests & Offers | Bottom nav "Routes" (Requests tab) | Subscription offers, cover requests, single-trip pool, decline-reason sheet |
| D · Earnings & Settlements | Bottom nav "Earnings" | Per-trip income, commission tier, weekly settlement cycles, dispute flow |
| E · Account & Compliance | Bottom nav "Account" | Profile, vehicle, documents/verification, Wasl standing, face re-verification, availability windows, account deletion |
| F · Support & Chats | Account → Support | Ticket list, rider chat, notifications |

Bottom nav: Home / Routes / Earnings / Account (`DriverNav`, RTL/LTR variants) — one fewer tab than Student (no dedicated Chats tab; chat is reached through a route/trip context).

### Admin console

| Section | Reached from | Purpose |
|---|---|---|
| A · Login & Dashboard | Cold open | Auth, KPI dashboard, global search, notifications |
| B · Driver Onboarding Review | Sidebar "Drivers" | Verification queue, application review, driver records, commission overrides |
| C · Trip Operations | Sidebar "Live Trips" / "Generated Routes" | Live trip monitoring, route generation, trip ratings moderation |
| D · Money Operations | Sidebar "Subscriptions" / "Transactions" / "Settlements" | Moyasar transactions, refunds, settlements, plans/pricing, coupons, ads |
| E · Students & Support | Sidebar "Students" / "Support" | Student records, periodic re-verification, tickets, notification templates, reports |
| F · Settings & Permissions | Sidebar "Settings" | Universities/pickup points, regions/pricing, admins & RBAC, account-deletion approval |
| G · Trip Management & Dispatch | Sidebar "Trip Management" | The Day Board — live dispatch console, manual driver assignment, cover-request handling |

Sidebar nav is sectioned (Operations / Student App / Driver App / Communication & Growth / Settings), `AdminSidebar` component, dark/`surface-inverse` background.

→ Composition reference: none rendered to `mockups/` for this pass (documenting existing Figma, not generating new mocks) — the Figma file itself (`ZNXBS4ibE5L8cqeZym6egZ`) is the authoritative screen reference. Spine wins on conflict with any future mock.

## Voice and Tone

Microcopy. Brand voice and aesthetic posture live in `DESIGN.md` → Brand & Style.

| Do | Don't | Observed example |
|---|---|---|
| State the mechanism plainly, even for sensitive topics | Vague reassurance | "There is no password. Sign-in uses a one-time verification code; email is for recovery only." |
| Name the actual privacy guarantee | Generic "your data is safe" | "Numbers masked on both sides. Communication is in-app only and archived." |
| Explain consequences before confirming a destructive action | Bare "Are you sure?" | "The account is deleted automatically on the scheduled date. Deleting now only brings that forward." |
| Give a specific, actionable reason for a block | Generic error | "Your pickup point is 46 km from the selected campus, and the service area reaches 40 km. Choose a closer point or another university." |
| Name the actual safety consequence of an action | Soft confirmation copy | "They will no longer receive SOS alerts or arrival notifications." (deleting a trusted contact) |
| Short, declarative sentences even for compliance/legal content | Legalese | "We keep trip, payment, invoice and rating records without your personal details, because Saudi regulations require us to retain them." |

Rebat's voice is **transparent before it is warm** — nearly every screen that could get away with a vague reassurance instead states the actual mechanism, number, or consequence. This is a deliberate, consistent pattern across all three surfaces (student privacy copy, driver payment-transparency copy, admin consequence-before-confirm copy) and should be treated as load-bearing brand voice, not incidental.

## Component Patterns

Behavioral. Visual specs live in `DESIGN.md.Components`.

| Component | Use | Behavioral rules |
|---|---|---|
| Button | Every primary/secondary/destructive action, all 3 surfaces | Primary (solid navy) is the single committing action per screen — never two Primary buttons side by side. Danger/DangerOutline reserved for destructive confirmations (delete account, cancel trip, void invoice) and always paired with consequence copy (see Voice and Tone), never used alone to signal destructiveness. Ghost/Muted/Outline are secondary/tertiary actions beside a Primary (e.g. "Cancel" beside "Confirm"). No long-press behavior observed on any button — tap-only (see Interaction Primitives). |
| TextField | Every form input, all 3 surfaces | White fill on `surface-default` pages, grey fill when nested inside an already-white card (contrast against the container, not the page). Hint state shows format guidance inline (e.g. phone format) rather than only on error. |
| AppCard | List rows — driver cards, trip cards, subscription cards | Entire card is tappable to the detail view unless it contains its own inline actions (e.g. a trip card with Track/Chat/Skip buttons), in which case the card background is not independently tappable to avoid conflicting hit targets. |
| AppBar / TabHeader | Screen header, all 3 surfaces | Back action always top-leading (RTL: visually right; LTR: visually left) per the Icon/arrow-left / arrow-right pair; title centered; optional overflow ("Actions=More") variant for a secondary menu — see the SOS-reachability open question in Flow 2 for why what lives behind "More" vs. persistently visible matters. |
| BottomNav / DriverNav | Primary navigation, Student/Driver | Persistent across all IA sections for that app; active tab indicated by icon + label color (`primary-default`), not icon shape change. No badge-count pattern observed on nav icons. |
| AdminSidebar / AdminTopbar | Primary navigation, Admin | Sidebar is always-expanded (no collapse control found) with grouped sections (Operations / Student App / Driver App / Communication & Growth / Settings); Topbar carries global search + notifications + account menu, persistent on every Admin screen. |
| Avatar | Driver/student identity, list rows and detail views | Size 32 in dense list rows, 44 in standard rows, 56 in profile/detail headers — no behavior beyond display; no tap-to-expand or upload affordance observed outside the dedicated photo-upload flows in onboarding. |
| Switch | Boolean settings (notification toggles, availability online/offline) | Immediate effect on toggle — no separate "Save" step observed for any Switch in the audited screens. Off state for a gating toggle (e.g. driver "Available") can be blocked with an inline reason rather than silently reverting (see State Patterns — WASL-ineligible block). |
| Logo/lockup | Splash, auth headers | Navy tone on light/`surface-default` backgrounds, inverse (white) tone on `surface-inverse`/dark backgrounds (splash gradient) — never navy-on-dark or inverse-on-light. |
| Bottom sheet | Confirmations, payment states, cancellation reasons, SOS | Every destructive or state-changing sheet states the consequence in its body copy before the action button — see Voice and Tone. Visual spec: `DESIGN.md` → Components. |
| Reason-capture field | Rejections, cancellations, disputes | Structured dropdown + free text is the established pattern (reassignment reasons, decline-offer reasons, dispute reasons); plain free-text-only fields (e.g. Driver "Can't drive") are the exception, not the rule — treat free-text-only as a gap to close, not a style choice. Visual spec: `DESIGN.md` → Components. |
| Day-board action menu (Admin) | Per-trip dispatch intervention | Riders / Change driver / Confirm on behalf / Remind / Open cover / Cancel trip — destructive item (Cancel trip) always last and visually distinct. **Accessibility gap, not yet resolved:** "visually distinct" has no stated programmatic/ARIA counterpart for screen-reader users — see Accessibility Floor. |

## State Patterns

| State | Surface | Treatment |
|---|---|---|
| Payment processing | Student — Subscribe & Pay | Dedicated sheet: "Complete the payment on the secure page, then come back here — we'll confirm it automatically." Distinct from... |
| Payment delayed confirmation | Student — Subscribe & Pay | "...Confirmation is taking a little longer. Track your subscription status from the subscription tab." (visually near-identical to Processing — flagged as a real confusion risk in the original audit) |
| Payment failed | Student — Subscribe & Pay | "Payment failed. The payment didn't go through. You can retry now or later." + Retry action. |
| Resume existing payment | Student — Subscribe & Pay | "You have a payment in progress... Resume it here instead of starting a new one." |
| Subscription searching for driver | Student — My Plan | "Finding your driver" state, distinct from "Rebat team is contacting you" escalation state. |
| Day confirmed / unconfirmed / no-driver-yet / driver-assigned | Student — Scheduled rides | Four distinct day-level states shown as a list; cancel action available on every state with no visible differentiation in consequence copy between them (open item — see Component Patterns on structured reason fields). |
| Driver application under review | Driver — Pending Review | 3-step progress: Application received → Document matching → Account approval, each Done/In progress/Waiting; "Refresh status" manual recheck. |
| Face check — optional vs. overdue | Driver — Account / Home | Optional periodic recheck has a "Later" deferral option and no visible due-date; overdue recheck hard-blocks route assignment and shows the missed due date. Two distinct severities, same underlying check. |
| Driver commission tier | Driver — Earnings | Tenure-based auto-tiering (12% → 18% → 25%, per the driver doc's defaults) with a visible countdown to the next tier change; admin override exists and suppresses auto-tiering. |
| Settlement cycle | Driver — Earnings / Admin — Settlements | Accruing → Ready for payout → Disbursed, or → Failed (with per-line retry, idempotent). |
| Trip reassignment mid-dispatch | Admin — Day Board | Driver ranked list with an expandable "Why?" score breakdown; ineligible drivers shown separately with their specific disqualifying reason, never silently omitted. |
| Account deletion pending | Student / Driver — Account | Persistent banner on the main Account screen for the full grace period, not just at the moment of request — the pending state is never allowed to be forgotten. |
| OTP entry — wrong/expired code | Student / Driver — Onboarding & Sign-in | Inline error on the code field; "Resend in N seconds" countdown, then "Resend" becomes active. **Not independently covered beyond this** — resend-exhausted (what happens after repeated failed resends) was not found in the audited screens; treat as unconfirmed, not as "no limit." |
| Driver active-trip, 6 states | Driver — Run a Route | Enumerated from the original Figma audit: (1) en route to first pickup, (2) at pickup point, (3) en route to destination, (4) trip completed / arrived at campus, (5) return-leg active, (6) gate-arrival status on return. Each state changes the primary action button and the live-tracking map annotation; full button-label detail lives in the driver user-story doc §6. |
| Empty chat thread / no tickets yet | Student — Chats; Driver — Support & Chats | **Gap, not covered in the original audit** — both IA sections exist (Student "D," Driver "F") but no empty-state, send-failure, or offline-chat copy was captured from the Figma screens. Flag for a follow-up pass rather than assuming a default empty state. |
| Admin dashboard cold-load / empty verification queue | Admin — A Login & Dashboard, B Driver Onboarding Review | **Gap, not covered in the original audit** — only Trip Operations (C/G) and Money Operations (D) states were captured in depth. A near-certain loading/zero-state exists for the KPI dashboard and the verification queue; treat as unconfirmed until checked against the live console. |

## Interaction Primitives

- Tap-driven throughout; no swipe gestures observed in the audited screens (no swipe-to-delete, no swipe-to-refresh beyond standard pull-to-refresh on list screens).
- Pull-to-refresh on list/feed screens (Student home announcements, trip lists).
- Countdown timers are a recurring primitive for time-boxed decisions: OTP resend, payment-offer expiry, cover-request response window, single-trip offer expiry — always rendered as live `mm:ss` or `N minutes` text, never a silent timeout.
- Confirmation-before-destructive is universal: every delete/cancel/void/reject action in the entire product routes through a sheet stating the consequence (see Voice and Tone) — no inline destructive action without a confirmation step was found anywhere.
- Drag-to-reorder: the one exception to tap-only, used solely for the Driver "Reorder stops" screen, rate-limited to 2 edits per route with an explicit remaining-count indicator.

## Accessibility Floor

Behavioral. Visual contrast lives in `DESIGN.md`.

- RTL/LTR is a first-class design concern, not a runtime mirror — every navigation and chrome component ships both variants in the token file itself (see `DESIGN.md` → Components). **Caveat:** this claim describes the design system's component inventory, not a confirmed shipping surface — English/LTR's first-release inclusion is itself unconfirmed (PRD §9 item 12). A QA pass should verify, at minimum: RTL mirroring of directional icons (back-chevrons, progress indicators), VoiceOver/TalkBack reading order in RTL, and correct bidi handling of mixed Arabic/Latin/numeral strings (phone numbers, SAR amounts).
- Status is never color-only: every `StatusBadge` pairs its color with text (e.g. "Verified," "Under review"), and destructive actions pair `danger` color with explicit consequence copy, not just a red button. **This guarantees a text alternative, not sufficient contrast** — see `DESIGN.md` → Colors for two confirmed WCAG AA contrast failures (`status-badge-brand` at 2.08:1, `status-badge-negative` at 4.28:1) found by computing actual ratios from the token hex values. A full contrast-ratio pass across every soft/strong token pairing is a named follow-up, not yet done.
- **Unconfirmed, not verified in this pass:** touch target sizing, screen-reader labeling, and dynamic-type/font-scaling behavior were not independently audited against a platform standard (44pt iOS / 48dp Android) — the original audits reviewed static Figma frames, which cannot surface this. Flag for a dedicated accessibility pass before treating this floor as met.
- **SOS reachability is a safety-critical accessibility requirement, not just a UX preference** (see Key Flows, Flow 2): if the SOS control sits behind an overflow menu rather than being persistently visible during an active trip, that is a motor-impairment and time-critical-use failure independent of labeling or contrast. When Flow 2's reachability question is resolved upstream, "persistent, not nested" should be the accessibility bar, not a design nice-to-have.
- **Drag-to-reorder has no documented non-gesture alternative** (see Interaction Primitives) — the Driver "Reorder stops" screen's drag gesture needs a keyboard/screen-reader-accessible equivalent (e.g. move-up/move-down controls); none was found in the audited screens. Confirm against the live build before assuming one exists.
- **Countdown timers have no stated timeout-extension mechanism** (OTP resend, cover-request 30-minute window, single-trip offer expiry) — satisfies WCAG's "no silent timeout" but not necessarily 2.2.1 Timing Adjustable. Cover-request and single-trip windows carry real consequences on lapse (a trip goes uncovered); whether either can be extended for a user who needs more time is unconfirmed and may be a backend/business-rule decision, not a pure UX one.
- **Bottom-sheet focus management is unaddressed** — every destructive sheet states its consequence in text (good), but whether focus moves into the sheet on open and returns to the triggering control on dismiss (a standard screen-reader modal requirement) was not captured from static Figma frames and needs a dedicated pass.
- **Day Board destructive-action distinction may rely on styling alone for assistive tech** — "Cancel trip always last and visually distinct" has a text label (not color-only), but no semantic/ARIA distinction is specified; a non-sighted admin navigating the action menu may not get the same "pause before acting" signal a sighted admin gets from the visual treatment.
- **Pull-to-refresh has no confirmed non-gesture alternative on most screens it appears on** — a manual "Refresh status" button is documented for one Driver screen (Pending Review) but not confirmed present on the Student home/trip-list screens that also rely on pull-to-refresh. Motor-impaired users need an equivalent tappable control everywhere the gesture is the primary refresh path.
- **Admin Day Board keyboard operability is unaddressed** — a dense, interaction-heavy desktop surface (ranked driver lists, expandable rows, inline action menus) is exactly the pattern that commonly fails keyboard-navigation audits even with solid visual/mouse design. Name this explicitly for the dedicated accessibility pass alongside the Day-board action menu's ARIA gap above.

## Responsive & Platform

Triggered: genuinely multi-surface (2 mobile, 1 desktop-only web).

- Student and Driver apps: single-column mobile layout, 375×812 base frame, no tablet or foldable layout found.
- Admin console: fixed 1440×900 desktop frame with a non-collapsing 256px sidebar. No responsive/mobile admin layout exists in the design file — an admin on a smaller screen is undesigned territory, not a tested-and-degraded experience.
- No dark-mode token set found for any surface (a `Theme=Dark` StatusBar symbol exists in the token file, suggesting dark mode was considered for system-chrome purposes, but no corresponding dark-mode color tokens exist in `DESIGN.md`'s source — treat as unimplemented, not hidden).

## Key Flows

### Flow 1 — Ride-alone notice and consent (Lama, evening return leg)

Full narrative in PRD §4a; numbered here for a walkable sequence.

**What's designed** (per the 7 Nov 2026 product decision):
1. Lama's return-leg trip reaches a point where she is the only remaining rider — the other students on the route have already been dropped off.
2. The assigned driver is male.
3. Before the trip proceeds with just Lama aboard, she receives an in-app notice naming the driver and stating she is the only rider.
4. She taps Accept or Decline.
5. **Climax:** her choice directly gates dispatch — Accept continues the trip as normal; Decline stops it short of departing with her alone.
6. **Failure/alternate path:** on Decline, another rider is found, the trip is covered by another driver, or the ride doesn't happen that leg (exact resolution mechanism not specified upstream).

**What's confirmed shipped:** nothing yet, per the student user-story doc ("Unconfirmed: implementation status in the app"). The driver doc separately notes the code "only warns at trip start" today rather than hard-blocking — whether Decline in step 4 is enforced or merely advisory is the open question carried in PRD §9 item 2.

### Flow 2 — Emergency during a trip (Sarah, SOS)

**What's designed:**
1. Sarah is mid-trip (tracking active, "Start Trip" already fired).
2. She opens the SOS control.
3. Confirmation sheet: "Send SOS now" — an explicit secondary step, not a single accidental tap.
4. On send: "The operations team and your trusted contacts will be alerted immediately with your current location."
5. **Climax, as designed:** a confirmation notice to Sarah that the SOS was received and is being handled.

**What's confirmed shipped vs. not:**
- Operations-team alert: assumed to fire (no contrary evidence found).
- Trusted-contacts alert: **confirmed NOT implemented** (REBAT-189, not started as of every source checked) — step 4's promise is only half true today.
- SOS control reachability in step 2 (persistent vs. behind an overflow menu): **unconfirmed** — not just a UX open item but an accessibility one (see Accessibility Floor).

**Failure:** if SOS is buried behind a menu or the trusted-contacts alert silently fails, Sarah has no visible indication that help beyond ops wasn't actually requested — no in-app signal of partial failure was found for this flow.

### Flow 3 — Driver cover request (Hind, can't confirm a scheduled trip)

1. 18:00 (default): Hind is asked to confirm tomorrow's rides; 21:00 cutoff.
2. Hind taps "Can't drive," gives a free-text reason (3–200 characters — the one place in the product that breaks from the structured-reason pattern, see Component Patterns).
3. System opens a cover request to up to 3 other eligible drivers in parallel, 30-minute response window each (driver doc §5.4).
4. **Climax:** another driver accepts — trips move to them immediately, riders notified.
5. **Failure:** if uncovered ~90 minutes before the earliest start, the trip cancels back to the open pool and "the Rebat team follows up" (manual, not automated resolution).
6. Admin side: the Day Board surfaces this exact state live (Cover open / Uncovered counts in the KPI strip), with an "Open cover" manual-intervention action available at any point in the cycle, not only after automatic escalation.

### Flow 4 — Manual driver assignment (Abdullah, an admin, placing an unplaced rider)

1. Route generation or the daily roster leaves a rider unplaced, with a named reason ("No driver available," "Pickup out of range").
2. Abdullah opens "Choose a driver" for that rider.
3. Every eligible driver is shown ranked by score with an expandable "Why?" breakdown (distance, window coverage, round-trip pairing, recent-driver history, preferred-driver flag, rating, load balancing).
4. Ineligible drivers are shown separately with their specific disqualifying reason — never silently hidden.
5. **Climax:** Abdullah can override the coverage rule with a typed reason for a genuine exception, rather than being stuck when the automatic ranking has no clean match.
6. **Failure:** if no driver is eligible even with an override and none is manually assigned, the rider remains in the "Unplaced riders" panel — the flow has no further automated escalation beyond this screen.

This is the flow that makes the whole automated-matching system trustworthy to operate, because it never dead-ends short of a human decision.
