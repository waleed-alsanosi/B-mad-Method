---
name: Rebat
status: draft
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
| InfoBanner | Reassurance/trust copy | Appears at the moment a user might hesitate (sign-in, payment, chat) — never as decoration. |
| StatusBadge | Any status chip | Soft-background/strong-text pairing per tone; one badge per status, never stacked. |
| ChoicePill | Single-select filters, trip direction | Selected state inverts to solid; disabled state exists for ineligible options (shown with a reason nearby, not silently). |
| Bottom sheet (unnamed in token file, used throughout) | Confirmations, payment states, cancellation reasons, SOS | Every destructive or state-changing sheet states the consequence in its body copy before the action button — see Voice and Tone. |
| Reason-capture field | Rejections, cancellations, disputes | Structured dropdown + free text is the established pattern (reassignment reasons, decline-offer reasons, dispute reasons); plain free-text-only fields (e.g. Driver "Can't drive") are the exception, not the rule — treat free-text-only as a gap to close, not a style choice. |
| Day-board action menu (Admin) | Per-trip dispatch intervention | Riders / Change driver / Confirm on behalf / Remind / Open cover / Cancel trip — destructive item (Cancel trip) always last and visually distinct. |

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

## Interaction Primitives

- Tap-driven throughout; no swipe gestures observed in the audited screens (no swipe-to-delete, no swipe-to-refresh beyond standard pull-to-refresh on list screens).
- Pull-to-refresh on list/feed screens (Student home announcements, trip lists).
- Countdown timers are a recurring primitive for time-boxed decisions: OTP resend, payment-offer expiry, cover-request response window, single-trip offer expiry — always rendered as live `mm:ss` or `N minutes` text, never a silent timeout.
- Confirmation-before-destructive is universal: every delete/cancel/void/reject action in the entire product routes through a sheet stating the consequence (see Voice and Tone) — no inline destructive action without a confirmation step was found anywhere.
- Drag-to-reorder: the one exception to tap-only, used solely for the Driver "Reorder stops" screen, rate-limited to 2 edits per route with an explicit remaining-count indicator.

## Accessibility Floor

Behavioral. Visual contrast lives in `DESIGN.md`.

- RTL/LTR is a first-class design concern, not a runtime mirror — every navigation and chrome component ships both variants in the token file itself (see `DESIGN.md` → Components). Any new component should follow the same pattern rather than relying on automatic mirroring.
- **Unconfirmed, not verified in this pass:** touch target sizing, screen-reader labeling, and dynamic-type/font-scaling behavior were not independently audited against a platform standard (44pt iOS / 48dp Android) — the original audits reviewed static Figma frames, which cannot surface this. Flag for a dedicated accessibility pass before treating this floor as met.
- Status is never color-only: every `StatusBadge` pairs its color with text (e.g. "Verified," "Under review"), and destructive actions pair `danger` color with explicit consequence copy, not just a red button.

## Responsive & Platform

Triggered: genuinely multi-surface (2 mobile, 1 desktop-only web).

- Student and Driver apps: single-column mobile layout, 375×812 base frame, no tablet or foldable layout found.
- Admin console: fixed 1440×900 desktop frame with a non-collapsing 256px sidebar. No responsive/mobile admin layout exists in the design file — an admin on a smaller screen is undesigned territory, not a tested-and-degraded experience.
- No dark-mode token set found for any surface (a `Theme=Dark` StatusBar symbol exists in the token file, suggesting dark mode was considered for system-chrome purposes, but no corresponding dark-mode color tokens exist in `DESIGN.md`'s source — treat as unimplemented, not hidden).

## Key Flows

### Flow 1 — Ride-alone notice and consent (Lama, evening return leg)

See PRD §4a for the full narrative. Lama is the sole remaining rider on tonight's return leg with a male driver; she gets an in-app notice naming the driver and must accept or decline before the trip proceeds with her alone. **Climax:** her accept/decline choice gates whether the trip departs — this is the one flow in the whole product where a single student's in-the-moment decision directly controls dispatch behavior. **Unconfirmed:** whether this notice-and-consent step is actually implemented (student doc marks it so), and whether declining hard-blocks the trip or only logs a warning (driver doc's open question).

### Flow 2 — Emergency during a trip (student, SOS)

1. Student is mid-trip (tracking active, "Start Trip" already fired).
2. She opens the SOS control — **exact reachability during an active trip was not confirmed** in the original audit (persistent control vs. behind an overflow menu); this is a real open item, not a documented certainty.
3. Confirmation sheet: "Send SOS now" — explicit secondary step, not a single accidental tap.
4. On send: "The operations team and your trusted contacts will be alerted immediately with your current location."
5. **Known gap, not an assumption:** the trusted-contacts portion of step 4's promise is not actually implemented (REBAT-189, not started as of every source checked) — the operations-team alert is the only part confirmed to fire.
6. **Climax, as designed:** a confirmation notice to the student that the SOS was received and is being handled — but this closes the loop only for the ops-team half of the promise.

### Flow 3 — Driver cover request (a driver can't confirm a scheduled trip)

1. 18:00 (default): driver is asked to confirm tomorrow's rides; 21:00 cutoff.
2. Driver taps "Can't drive," gives a free-text reason (3–200 characters — the one place in the product that breaks from the structured-reason pattern, see Component Patterns).
3. System opens a cover request to up to 3 other eligible drivers in parallel, 30-minute response window each (driver doc §5.4).
4. **Climax:** either another driver accepts (trips move to them immediately, riders notified) or — if uncovered ~90 minutes before the earliest start — the trip cancels back to the open pool and "the Rebat team follows up."
5. Admin side: the Day Board surfaces this exact state live (Cover open / Uncovered counts in the KPI strip), with an "Open cover" manual-intervention action available at any point in the cycle, not only after automatic escalation.

### Flow 4 — Manual driver assignment (Admin, an unplaced rider)

1. Route generation or the daily roster leaves a rider unplaced, with a named reason ("No driver available," "Pickup out of range").
2. Admin opens "Choose a driver" for that rider.
3. Every eligible driver is shown ranked by score with an expandable "Why?" breakdown (distance, window coverage, round-trip pairing, recent-driver history, preferred-driver flag, rating, load balancing).
4. Ineligible drivers are shown separately with their specific disqualifying reason — never silently hidden.
5. **Climax:** admin can override the coverage rule with a typed reason for a genuine exception, rather than being stuck when the automatic ranking has no clean match — this is the flow that makes the whole automated-matching system trustworthy to operate, because it never dead-ends.
