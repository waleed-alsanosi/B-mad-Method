# Spine Pair Review — Rebat

## Overall verdict

The pair is a credible, well-disciplined extraction of an already-built product: DESIGN.md's token layer resolves completely with no broken references, section order is canonical, and the voice/state documentation is unusually honest about what's unconfirmed rather than inventing resolutions. The main downstream risk is a two-way component-catalog mismatch between the files (several visually-specified components have no behavioral entry and vice versa) plus thin-to-absent state coverage on Chat/Support and most Admin surfaces — a consumer building those screens would have to go back to the Figma file or invent behavior, which is exactly what this pass was meant to avoid.

## 1. Flow coverage — adequate

Climax beats are present and well-marked in all four Key Flows, and failure/alternate branches exist in substance (payment retry logic lives elsewhere in State Patterns; Flow 3's uncovered-trip branch; Flow 4's override branch). But format discipline slips against the calibration examples (Quill/Drift always: named protagonist + numbered steps + a labeled `Failure:` line).

### Findings
- **Major** Flow 1 has no numbered steps (EXPERIENCE.md Key Flows, Flow 1) — it's prose pointing to PRD §4a rather than a walkable sequence. Every other flow in this file and in both calibration examples is numbered. A story-dev consumer has to open a second document to get the steps. Fix: give Flow 1 its own numbered sequence (even if short), keeping the PRD pointer as a citation, not a substitute.
- **Minor** Flows 2–4 name no protagonist, only a role ("student," "driver," "Admin") (EXPERIENCE.md Key Flows, Flows 2–4) — both examples name every protagonist (Mira, Sarah, Devon/Mara) even in a single-line setup. Downstream impact is low since the flows are otherwise concrete, but it's a consistent format deviation worth normalizing. Fix: borrow a name from the cited user-story docs, or state explicitly that the source docs don't name one.
- **Minor** No flow uses the examples' explicit `Failure:` label — alternate/failure paths are folded into numbered steps instead (Flow 3 step 4, Flow 4 step 4) or left as open questions (Flow 1, Flow 2). Content is present, format is inconsistent. Fix: pull the failure/escalation branch into its own labeled line per flow, matching the calibration pattern.

## 2. Token completeness — strong

Every frontmatter token and every `{path.to.token}` reference in DESIGN.md resolves cleanly; no missing hex values. EXPERIENCE.md uses no `{path}` syntax at all (it refers to colors/components by name in prose instead, e.g. "pairs `danger` color with explicit consequence copy"), which is consistent with how the spec allows plain-prose cross-references and doesn't break resolution — just less rigorous than it could be.

### Findings
- **Trivial** A meaningful share of frontmatter color tokens are defined but never referenced anywhere in prose or in the `components` map: `rating`, `scrim`, `focus`, `hover-wash`, `gradient-from/via/to`, `on-primary-inverse`, `on-accent`, `on-success`, `primary-inverse`, `success-solid`, and the `*-strong`/`*-soft-strong`/`*-line-strong` variants across danger/warning. None of these are wrong, but a consumer can't tell from the spine alone whether they're load-bearing (e.g. `rating` is explained in prose even though it's never used in a `components` entry) or dead weight carried over from the raw token export. Fix: either wire the used-but-unreferenced ones (`rating`, `scrim`) into a component entry, or note in Colors/Components that some tokens exist only for the raw palette and aren't yet assigned to a component.

## 3. Component coverage — thin

This is the pair's weakest mechanical category. The two files' component catalogs don't match in either direction.

### Findings
- **Major** DESIGN.md gives visual specs to `Button`, `AppCard`, `TextField`, the nav-chrome set (AppBar/BottomNav/DriverNav/AdminSidebar/AdminTopbar/TabHeader), `Avatar`, `Switch`, and `Logo/lockup`, but EXPERIENCE.md → Component Patterns has no row for any of them (EXPERIENCE.md "Component Patterns" table lists only InfoBanner, StatusBadge, ChoicePill, Bottom sheet, Reason-capture field, Day-board action menu). `Button` is explicitly called out in DESIGN.md as "load-bearing brand identity" with 11 named styles, yet has zero behavioral rules anywhere (when is Danger vs. DangerOutline used? does tap vs. long-press differ?). Fix: add Component Patterns rows at minimum for Button, TextField, and the nav set — these appear on every screen.
- **Major** The reverse gap: EXPERIENCE.md's `Bottom sheet`, `Reason-capture field`, and `Day-board action menu` have real behavioral rules but no corresponding DESIGN.md visual row — bottom sheets are described as "used throughout" (payment states, cancellation, SOS) yet have no anatomy, sizing, or scrim-behavior spec beyond the one `scrim` color mentioned in Elevation & Depth. A consumer implementing a new bottom sheet has behavior but no visual contract. Fix: add a `Components` entry (or at minimum a frontmatter `components` token block) for bottom sheet and reason-capture field.

## 4. State coverage — thin

Payment (Student B) and settlement/compliance (Driver D/E, Admin dispatch) states are genuinely thorough and specific. Coverage drops to near-zero on several IA surfaces.

### Findings
- **Major** Chat & Support has no state coverage on either mobile surface — Student "D · Chat & Support" (empty chat, no tickets yet, message-send failure, offline) and Driver "F · Support & Chats" are both listed in Information Architecture but have zero rows in State Patterns. Fix: add empty/error rows for ticket list and chat thread on both apps, or state explicitly that chat/support states weren't captured in the audit.
- **Moderate** Onboarding/auth has no error states — Student/Driver "A · Onboarding & Sign-in" covers OTP and application flow in IA, but State Patterns has no row for OTP failure/expiry, invalid phone, or resend-exhausted, despite "Countdown timers" for OTP resend being called out in Interaction Primitives. Fix: add at least an OTP-failure row.
- **Moderate** Admin surfaces A, B, E, F (Login & Dashboard, Driver Onboarding Review, Students & Support, Settings & Permissions) have no State Patterns rows at all — only Trip Operations (C/G) and Money Operations (D, partially) are covered. A dashboard cold-load/empty-queue state is a near-certainty in any admin console and isn't addressed. Fix: add at minimum a loading/empty-queue row for the verification queue (B) and dashboard (A).
- **Minor** The Driver "6-state active-trip machine" is named in Information Architecture (surface B) but never enumerated — neither State Patterns nor Interaction Primitives lists the six states. Fix: either enumerate the six states in State Patterns or point explicitly to the driver user-story doc section that defines them.

## 5. Visual reference coverage — strong (expected gap, not a miss)

EXPERIENCE.md's Information Architecture section explicitly states no mockups were rendered for this pass and names the Figma file (`ZNXBS4ibE5L8cqeZym6egZ`) as the authoritative screen reference, with "spine wins on conflict with any future mock." This matches the stated framing exactly — not a gap.

## 6. Bloat & overspecification — strong

No pixel-chasing where tokens already cover it (the one literal dimension, AppCard's 327×140, is cited as evidence from the token file rather than invented, and is load-bearing for "what size is this card" — appropriate). Prose carries real decisions throughout rather than decoration (e.g., flagging that Processing/Delayed payment sheets are "visually near-identical... flagged as a real confusion risk" is a judgment call, not filler). The PRD §4a/§9 restatements in Flows 1 and 2 are pointer-plus-summary rather than full restatement, which is reasonable given this is meant to be a readable spine, not a document that forces every reader back to the PRD.

### Findings
- **Trivial** Flow 2 (SOS) and Flow 1 (ride-alone) lean heavily on "Unconfirmed" / "Known gap" callouts stacked three deep in a few sentences, which is honest but makes the climax hard to parse on a skim. Fix: consider separating "what's designed" from "what's confirmed shipped" into two short lines per flow rather than interleaving.

## 7. Inheritance discipline — adequate

DESIGN.md token refs resolve 100% internally (verified programmatically — every `{colors.*}` and `{rounded.*}` used in the `components` map and in prose exists in frontmatter). EXPERIENCE.md's `sources` frontmatter cites the PRD (verified to exist and resolve: §4a and §9 citations both check out against the real document) plus three user-story docs not present in this workspace, so their content can't be verified — only that the spine's citations to them (REBAT-189, driver §5.4, driver §6.4, Student ST-11/12/17/22) are internally consistent and specific enough to be checkable later, which is the right posture for an unverifiable source. The real inheritance break is the component-name mismatch documented in §3 above — that's the one place where the two files don't actually share a vocabulary.

### Findings
- (see §3 — the component-name mismatch is the substantive inheritance-discipline finding; not repeated here to avoid double-counting.)

## 8. Shape fit — strong

DESIGN.md sections appear in exact canonical order: Brand & Style, Colors, Typography, Layout & Spacing, Elevation & Depth, Shapes, Components, Do's and Don'ts. EXPERIENCE.md has all required defaults in the example-established order (Foundation, IA, Voice and Tone, Component Patterns, State Patterns, Interaction Primitives, Accessibility Floor, Key Flows) plus the correctly-triggered Responsive & Platform section (justified: 2 mobile + 1 desktop-only surface), placed in the same slot the Drift example uses. "Inspiration & Anti-patterns" is omitted, which is allowed (optional in both examples) and arguably correct here since this pass documents an existing product rather than making new design choices to justify.

### Findings
- **Trivial** Accessibility Floor is present and in the right slot, but its content explicitly says touch-target sizing, screen-reader labeling, and dynamic-type behavior were "not independently audited" and are "Unconfirmed." The section exists (satisfies shape fit) but doesn't actually commit to a floor a consumer can build against — this is a completeness issue flagged honestly rather than a structural one, but downstream consumers should treat this section as a to-do, not a spec.

## Mechanical notes

- **Cross-reference check:** EXPERIENCE.md's PRD citations (§4a, §9 item 2, item 8/9, REBAT-189, REBAT-187, Student ST-11/12/17/22) were checked against `_bmad-output/planning-artifacts/prds/prd-B-mad-Method-2026-11-13/prd.md` and all resolve to real, matching sections — the ride-alone rule's three-revision history and the trusted-contacts/REBAT-189 gap are stated consistently in both documents.
- **Token resolution:** Every `{colors.*}` and `{rounded.*}` reference in DESIGN.md's `components` frontmatter map and body prose resolves to a defined frontmatter key (verified by extracting all `{...}` references and all `colors:`/`rounded:` keys and diffing them — zero unresolved references, zero missing hex values).
- **Name consistency:** Components are named identically where they do appear in both files (`InfoBanner`, `StatusBadge`, `ChoicePill` match exactly in casing and naming between DESIGN.md.Components and EXPERIENCE.md.Component Patterns). The gap is coverage, not naming drift — see §3.
- **User-story docs:** `user-stories-student.md`, `user-stories-driver.md`, `user-stories-admin.md` are cited in EXPERIENCE.md frontmatter `sources` but are not present in this workspace, confirming the task framing — their content can't be independently verified, only the internal consistency of what the spine attributes to them (e.g., driver §5.4's 30-minute cover window, driver §6.4 safety items).
- **No frontmatter type violations:** `colors` is a flat kebab-case object of hex strings per spec; `typography` uses platform-note-style fields appropriately (`fontFamily`/`fontWeight` for the two live-coded roles, `note` for `display`'s special-case usage); `rounded` and `spacing` are plain dimension maps. No type-rule violations against `design-md-spec.md`.
