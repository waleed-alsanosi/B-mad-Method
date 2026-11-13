---
title: Rebat Product Requirements Document
status: final
created: 2026-11-13
updated: 2026-11-13
---

# Product Requirements Document (PRD) — Rebat

**Last updated:** 13 Nov 2026.

**Sources, in order of authority:** `user-stories-driver.md` and `user-stories-student.md` (code-verified, 7–9 Nov 2026); the Plane delivery record and linked epics (workspace `vp`, 209 issues); two production release logs (2026-11-04, 2026-11-05); `user-stories-admin.md` (design + Plane only, not code-verified); the Figma file "Rebat-Project" (185 screens read across Student/Driver/Admin). This PRD replaces an earlier draft that described a parent-mediated, school-bus-fleet transport service — that draft does not match anything built, documented, or designed for this product, and should be treated as unrelated.

**How to read it:** every claim below is traceable to one of the sources above. Where sources disagree or a question has no settled answer, it's listed in §9 rather than asserted either way.

**A methodology note on Plane:** this project's Plane workspace has shown its "Done" state to be unreliable at least three times (REBAT-46, REBAT-104, REBAT-190 — the last since genuinely fixed per a later release log). Treat a Done state as a starting point to verify, not as proof.

**A note on citations:** the scope table in §6 cites each capability into one of three per-surface user-story docs. Student and Admin cite by discrete ID (ST-xx, OP-xx); the Driver doc is cited by section number (§x.x) because that's how it's structured — not a missing ID scheme. All three docs were read in full to build this PRD and their citations below have been confirmed to resolve.

---

## 1. Overview

Rebat (رباط) is a subscription-based university transport service for students in Saudi Arabia, connecting them with verified private-car drivers for scheduled, tracked rides between a fixed pickup point and their university. The system has three surfaces: a Student mobile app (rider self-service), a Driver mobile app (driver self-service), and an Admin console (operations, compliance, finance, dispatch). Pilot market: Jeddah. Arabic-first, right-to-left; the Figma design carries a parallel English/LTR track in both mobile apps, but **whether English ships in the first release is explicitly unconfirmed** (see §9).

The product is **past MVP and live in production** as of 2026-10-15 (backend, admin console, landing site), with signed Android builds in Google Play Closed Testing as of 2026-11-05. iOS has not been built as of the same date — see §9.

## 2. Problem

University students arranging daily transport have no centralized system for being matched with a vetted driver, knowing who's picking them up, tracking the ride in real time, or paying predictably. Drivers offering this kind of transport have no structured way to find consistent, scheduled work with transparent pay. Rebat replaces informal, ad hoc arrangements with a managed subscription, automated driver matching, live tracking, and named safety safeguards.

## 3. Objectives

- Run a subscription model where a student pays once for a period (week/month/semester/custom days) and is matched to a driver for the whole period, not booked per ride. *(Student ST-05–ST-07)*
- Match students to drivers automatically, ranked by distance, window coverage, seat availability, and continuity (same driver where possible) — with a human override always available from the Admin console. *(Driver §5.1; Admin OP-13–OP-15)*
- Deliver real-time ride tracking, scoped strictly to the active trip (tracking starts at "Start Trip," stops at "End trip"). *(Driver §7; Student ST-09 — see §9 item 6 on a code-level exception to this claim)*
- Operate named safety safeguards: trusted contacts, an SOS/emergency button, incident reporting, and a notice-and-consent flow when a student would otherwise ride alone with a male driver. *(Student ST-11, ST-12, ST-17, ST-22; §4a)*
- Run compliance against Saudi regulatory requirements (WASL/ELM vehicle and driver registration; Absher driver background checks) without blocking launch indefinitely on them. *(Driver §3.2; Admin OP-05, OP-09)*
- Give drivers transparent earnings: a visible, explained commission structure, GPS-sourced trip distance (not estimates), and a predictable weekly settlement cycle. *(Driver §8)*
- Give operations staff a single console to run daily dispatch, approve drivers, manage money, and handle support — without needing engineering involvement for routine interventions. **Not yet fully true today:** generic error states on at least one high-traffic operations screen gave no failure cause as of the original audit (since reported fixed under REBAT-158, not independently re-verified), and the SOS-alerts screen (OP-36) exists in production with no design-file counterpart — both are exactly the kind of thing that currently *does* need engineering to chase down.

## 4. Target Personas

### Student
- **Role:** Registers with a phone number (OTP, no password), selects a university and fixed pickup point, sets a weekly lecture schedule, subscribes to a plan, and rides.
- **Goal:** A safe, predictable, on-time ride to and from university without arranging transport herself/himself each day.
- **Note:** there is **no parent or guardian role anywhere in the product.** The student manages her/his own account, payment, and schedule directly. (See §9 on whether the service is restricted to female students only — unconfirmed.)

### Driver
- **Role:** Self-registers with a six-step application (personal info, documents, face check, vehicle info, availability, review), gets approved by an admin, then receives subscription offers and single-trip requests ranked to fit their availability and location.
- **Goal:** Consistent, scheduled income with transparent commission and a predictable weekly payout — not instant-dispatch gig work.

### Admin / Operations staff
- **Role:** Approves drivers, runs and monitors daily dispatch, manages money (subscriptions, refunds, settlements, pricing), handles support escalations, and administers compliance and account-deletion requests. Roles are scoped (Super Admin, Region Admin, Support Agent, Finance) with an audit log.
- **Goal:** Keep the service running reliably without needing engineering for routine operational decisions.

## 4a. Illustrative Journey — Ride-Alone Notice

This PRD deliberately carries no full set of user journeys (detail lives in the three per-surface docs), but the ride-alone flow is the one safety-relevant moment a reader should be able to picture without opening another document:

> Lama is the only remaining rider on tonight's return leg; the other two students on her route already got off. The assigned driver is male. Before the trip proceeds with just Lama aboard, she gets a notice in the app telling her she's the only rider and naming the driver, and she can accept or decline. If she accepts, the trip continues as normal. If she declines, the trip stops short of departing with her alone, and (per the current, still-unconfirmed rule — see §9 item 2) either another rider is found, the trip is covered by another driver, or the ride doesn't happen that leg.

**What's unconfirmed about this exact journey:** whether this notice-and-consent step is actually implemented in the shipped app (the student doc marks it "Unconfirmed: implementation status"), and whether declining hard-blocks the trip or merely logs a warning (the driver doc's open question). Treat the journey above as the *intended* behavior per the most recent product decision (7 Nov 2026), not as confirmed shipped behavior.

## 5. Constraints

- **WASL/ELM compliance is a named launch blocker (REBAT-6), not yet resolved.** The backend integration is fully built and deployed, but runs with `COMPLIANCE_PROVIDER=mock` until ELM issues client credentials (client-id/app-id/app-key). Deadline tracked as 2026-11-13 (estimate). Store listing copy currently claims WASL registration, which is not yet literally true — this needs resolving before store submission, not after.
- **Whether the Absher criminal-record check gates a brand-new driver's first trip is unconfirmed.** The design shows copy stating a driver "may drive meanwhile" the check is pending; no source consulted in this engagement — design, Plane, or either code-verified user-story doc — settles whether that's intended production behavior. This is the single most important open constraint to resolve directly (see §9).
- **A subscription route needs at least two riders, unless the sole rider consents to ride alone — except this rule has changed three times** (21 July 2026: hard minimum of two; Oct 2026: notice-and-consent for a solo female rider with a male driver; 7 Nov 2026, latest: no minimum at all, with the same notice-and-consent). Implementation status of the current (7 Nov) rule is explicitly unconfirmed in the student user-story doc. Whichever rule is live needs to be confirmed before being relied on anywhere, including in this document.
- **Store release is not complete.** Android: signed builds exist and are in Google Play Closed Testing (Alpha), pending Google's review as of 2026-11-05. iOS: not built as of the same date, per the most recent release log — this is a material gap if any stakeholder believes a TestFlight build already exists.
- Production payments currently run through Moyasar's **test account**, an accepted risk limited to closed testing (REBAT-84) — must switch to the live account before any wider release.
- Mandatory Saudi-market requirements: Arabic-first RTL UI, SAR currency, Hijri/Gregorian dual date handling for driver compliance fields, phone-number-only identity (no email/password for riders or drivers).

## 6. In Scope (Launch)

Grouped by the business-module taxonomy already in use in Plane (M01–M16), with the user-story doc that defines each in detail:

| Module | Capability | Primary doc |
|---|---|---|
| M01 Accounts & Access | Phone+OTP signup, sessions, account deletion (self-service + admin review) | Student ST-01, ST-28; Driver §1.1, §10.4; Admin OP-25 |
| M02 Student Profiles & Travel Needs | University selection, fixed pickup point, weekly lecture schedule | Student ST-02–ST-04 |
| M03 Drivers & Vehicles | Driver registration, documents, face verification, vehicle data, availability | Driver §1–§4; Admin OP-04–OP-09 |
| M04 Service Coverage & Universities | City/university/gate catalogue, location tooling, campus-request approval | Student ST-23; Admin OP-18–OP-19 |
| M05 Plans & Pricing | Plan definitions, per-km rates, fare calculation | Student ST-05; Admin OP-20 |
| M06 Subscriptions | Purchase, renewal, cancellation of an unpaid subscription | Student ST-06, ST-07, ST-15 |
| M07 Route Planning & Assignment | Automated ranking, manual assignment, reassignment, cover requests | Driver §5; Admin OP-13–OP-15, OP-32–OP-35 |
| M08 Trip Execution & Tracking | Start/End trip, pickup sequence, live tracking, no-show handling | Driver §6–§7; Student ST-09; Admin OP-10 |
| M09 Payments & Refunds | Moyasar checkout, refunds, invoice voiding, payment-state visibility | Student ST-06, ST-24; Admin OP-22 |
| M10 Driver Earnings & Settlements | Per-trip earnings, commission tiers, weekly settlement, payout | Driver §8; Admin OP-23 |
| M11 Safety & Incidents | SOS, trusted contacts, incident reporting, ride-alone notice | Student ST-11, ST-12, ST-17, ST-22; Driver §6.4; Admin OP-36 |
| M12 Communication & Notifications | In-app chat (numbers always masked), push/in-app notifications, preferences | Student ST-20, ST-27; Driver §9; Admin OP-27–OP-28 |
| M13 Support & Service Quality | Tickets, ratings, dispute handling | Student ST-13, ST-21; Driver §8.3, §10.2; Admin OP-16, OP-26 |
| M14 Promotions & Acquisition | Announcements, landing site, store listings — **coupons are admin-managed only; no redemption UI exists in the Student app** (confirmed gap, see §9) | Student ST-29, ST-30; Admin OP-12, OP-24 |
| M15 Compliance & Governance | WASL/ELM, consent, account-deletion review, audit logging | Admin OP-05, OP-09, OP-25, OP-30 |
| M16 Business Reporting | Admin dashboards and exportable reports | Admin OP-03, OP-29 |

*Note: Admin OP-25 appears under both M01 and M15 — it's one screen (account-deletion review) serving two workflows (the student/driver-initiated self-service request, and the admin's compliance review of it), not a duplicate.*

## 6a. Glossary

Terms used in §3 and §6 without a natural-language definition elsewhere, to keep usage consistent as the three source docs (and future documents) reuse them:

- **Subscription route** — a recurring, multi-day trip pattern tied to a student's paid subscription, as distinct from a one-off single-trip request.
- **Window coverage** — the % overlap between a subscription's required pickup/drop-off times and a driver's stated availability windows; one of the ranking factors in automated driver matching.
- **Continuity** (as a matching criterion) — preferring to re-assign the same driver a student already had, rather than optimizing purely on distance/score each time.
- **Cover request** — an operational workflow triggered when a driver can't confirm an already-assigned trip; up to 3 other eligible drivers are offered the trip in parallel, with a default 30-minute response window per the Driver doc (§5.4).
- **Notice-and-consent** (ride-alone) — the mechanism by which a student riding alone with a male driver (where normally two or more riders are expected) is shown a notice and must actively accept or decline before the trip proceeds. See §9 item 2 for its current, unsettled state.

## 7. Out of Scope (Launch)

- iOS App Store release (Android closed testing only is live; see §9 on current state).
- Live Moyasar production account (test account in use during closed testing).
- Any parent/guardian account type, school-bus fleet, or in-vehicle camera system — none of these appear in any source for this product. If a stakeholder needs these, it is a different product, not a gap in this one.
- Automated face-match verification for drivers (a human reviews the submitted photo; no machine matching exists in the code per the driver doc).
- Guaranteed unattended bank payout (currently admin-supervised; automatic payout rail is unconfirmed as live, per the driver doc).
- Instant/on-demand single trips beyond the existing "single-trip request" pool model (explicitly postponed per the 7 Nov 2026 product decision referenced in the student doc).

## 8. Success Metrics

No formally adopted launch-metric targets were found in any source for this engagement. The one earlier PRD draft that proposed targets (50+ drivers, 200+ subscriptions in 3 months, 90%+ on-time pickup) describes a different product and its numbers shouldn't be assumed to carry over. For reference, current production scale as shown on the Admin dashboard (not a target, a snapshot): ~86 verified drivers, ~1,248 active subscriptions, ~312 trips/day. If launch metrics are wanted, they need to be set deliberately against this baseline, not inherited from the unrelated draft.

**Metric categories to define** (no numbers invented — this scopes the gap rather than leaving it blank), each tied directly to the thesis in §2–§3:

- **Continuity rate** — % of subscription trips served by the same driver across the subscription period. This is the thesis's actual bet (managed subscription + continuity beats ad hoc arrangement); it should be measured even provisionally.
- **On-time / reliability rate** — % of trips with a confirmed driver by the 21:00 T-1 cutoff, and % completed without a no-show or late cancellation.
- **Settlement reliability** — % of weekly settlement cycles disbursed on schedule without a "Failed" status.
- **Safety-incident rate** — SOS alerts per 1,000 trips, and time-to-acknowledge on the Admin side (OP-36) — directly relevant given §9's open safety questions.

Counter-metric to watch: driver commission-tier churn (drivers leaving once they roll off the promotional 12% tier to 25%) shouldn't be masked by a rising driver count if new signups are backfilling attrition.

## 9. Open Questions & Risks

These are carried forward from every round of this engagement's audits and cross-checks, and remain unresolved as of this writing. Safety- and compliance-critical items carry an explicit owner and target date rather than none, per PM discipline — where no owner is actually known, that's stated honestly rather than left blank.

### Safety- and compliance-critical

1. **Does the Absher criminal-record check gate a new driver's first trip**, independent of the broader WASL/ELM mock status? Highest-priority open item — safety-relevant, and unresolved across design, Plane, and both code-verified user-story docs. **Owner: unassigned — needs a direct answer from whoever owns the WASL/ELM integration (REBAT-6). Target: before the 2026-11-13 ELM-credentials deadline, not after.**
2. **Which version of the "ride alone" rule is actually live** — hard minimum of two riders, notice-and-consent for a male-driver/solo-female pairing, or no minimum at all (the 7 Nov decision)? Student doc marks its own current understanding as unconfirmed in-app. The Driver doc adds a sharper question: the code only warns at trip start rather than hard-blocking — is a hard block actually wanted? **Owner: unassigned (decision history shows Waleed/Samah involved in prior revisions — confirm with them). Target: before relying on this rule in any other document.**
3. **Is the service restricted to female students only, or open to all students?** Listed as an explicit open question in the student user-story doc; not settled anywhere else either. **Owner: unassigned. Target: before any wider marketing or store-listing claim is made either way.**
### Release / platform state

4. **Does an iOS TestFlight build currently exist?** The most recent release log (2026-11-05) says iOS is not built; if any stakeholder believes otherwise, reconcile directly before this PRD is relied on for release planning.
5. **Is REBAT-46's 15-item driver-assignment bug list actually resolved?** Plane marks it Done; its own body text and an earlier delivery-record snapshot say it wasn't, as of their respective write dates; neither newer source confirms either way.
### Trust, scope and process

6. **The Driver app's "no tracking outside trips" privacy claim is contradicted by code** that sends idle location every 30 seconds while a driver is online but not on a trip (per the driver user-story doc). This is a stated trust claim users are relying on. **Owner: unassigned — needs a product decision on whether to fix the copy or the behavior. Target: before the claim is repeated in any store listing or onboarding copy.**
7. **No coupon/promo-code entry exists in the Student payment flow**, despite full coupon management existing in the Admin console. Confirmed independently against the Student app design.
8. **An Admin "SOS alerts" screen is live in production** (OP-36, per the 2026-11-04 release log under REBAT-187) **with no counterpart anywhere in the Figma design file.** Needs either a design-file update or a direct review of the live screen against the same safety questions raised for the mobile SOS flow. **Owner: unassigned — needs whoever owns the Admin design file plus whoever owns REBAT-189. Target: before the next design-file sync.**
9. **Does acknowledging or closing an SOS alert (OP-36) interact at all with the separately-tracked bug that trusted contacts aren't actually notified** (REBAT-189, not started as of every source checked)? Same owner/target as item 8.
10. **Which admin roles can see unmasked phone numbers** (visible on trip/dispatch screens) versus masked ones (visible in chat screens) — the RBAC system to scope this exists, but which roles get which visibility wasn't directly confirmed.
11. **Final wording for subscription pricing** (removing "fixed price per student," REBAT-104) is still pending a decision from Samah, and the phrase is still live in the current design as of this writing.
12. **Is English in the first release at all?** The Figma design carries a full English/LTR track, but the student user-story doc marks this explicitly unconfirmed (ST-26).
13. **Is live trip sharing with family/trusted contacts in the first release?** Distinct from the SOS/trusted-contacts safety mechanism — this is about passive, ongoing location sharing during a normal trip, not an emergency. Explicitly unconfirmed per the student doc (ST-12); "no decision recorded."
14. **What is the cancellation and refund policy, and does a cancelled trip return to the student's trip balance?** Explicitly unconfirmed per the student doc (ST-10, ST-14) — a real gap given subscriptions are prepaid for a trip count.
15. **Is there a re-apply flow for a driver whose application was rejected?** The pending-review screen's copy implies one ("update your details and re-apply"), but the driver doc found no dedicated screen for it — today a rejected applicant can only contact support (§2.1).
