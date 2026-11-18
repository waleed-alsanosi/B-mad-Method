# PRD Quality Review — YYO — منصة مكتب يحي ياسين عبيسي للخدمات العامة (revision 2)

## Overall verdict
Revision 2 is decisive and unusually concrete at the micro level: the three lifecycle tables (§6), the notification matrix (FR-26), the payments/invoicing rules (FR-16–FR-19) and the explicit Non-Goals (§4) give UX design a solid spine. What is at risk sits one level up. The PRD never confronts the macro choices Yahya must make before signing (simplified vs integrated store, a month-or-less initial delivery vs a 49-FR, three-surface platform, Hull as the front door vs a catalog storefront). The lifecycle also breaks its own headline rule «لا حالة انتظار في المنصة بلا مهلة وتذكير ومخرج» in several states, including a 7-vs-14-day contradiction. Fix those before UX starts and the PRD is fit to drive the pre-signature design.

## Decision-readiness — adequate
Micro-decisions are stated as decisions, not "considerations": deposit 0–100% in 10% steps (FR-12), one final payment only (FR-17, glossary), manager's decision final with a Ministry of Commerce link (FR-39), per-staff calendars (FR-20). The 18 post-review decisions in `decisions-round-1.md` are almost all carried in faithfully, and §10.1 asks real questions rather than rhetorical ones.

The gap is the decisions that matter most to the stated reader, Yahya, "لمراجعة النطاق قبل عرض التصميم عليه" (§0). The meeting notes record that Yahya is weighing «متجر إلكتروني مبسّط» against «متكامل», and that Waleed's agreed next step was «نطاق عمل لكل خيار (مبسّط ومتكامل)». The RFP asks for «التنفيذ الأولي خلال شهر أو أقل». The PRD delivers one undifferentiated scope (website, web store, native iOS/Android app, dashboard, ZATCA e-invoicing, multi-item quotes, per-staff scheduling, post/delivery logistics) with no phasing, no cut line and no statement of what was given up. The commercial model gets the same treatment. The RFP specifies performance-based revenue share («لا دفع مستحق دون وجود عميل قام بشراء منتج أو خدمة»), while the PRD assumes a Dreamy subscription in one inline tag on FR-30 and does not list it among the questions for Yahya. There are no `[NOTE FOR PM]` callouts anywhere, so neither tension is marked.

### Findings
- **[high]** No scope options or phasing for a pre-signature review (§0, §5, whole of §7) — Yahya's own framing (simplified vs integrated) and the RFP's «شهر أو أقل» initial delivery are absent. §5 lists every surface and capability as v1 with no MVP line, so the design shown before signing will imply the full 49-FR scope. *Fix:* Add a short "خيارات النطاق" section: a simplified cut (for example web store + dashboard, instant services + quote acceptance + Mada, no native app, no delivery logistics) vs the integrated cut, each mapped to FR IDs, with what each gives up. Tag the FR list with phase.
- **[medium]** Business-model conflict missing from the questions for Yahya (FR-30, §10.1, §10.2) — the RFP's revenue-share model (collection into the office's account, partner deductions, a qualifying-sales report) conflicts with the assumed subscription. It changes FR-30 and possibly payment settlement, yet §10.1 has no question on it. *Fix:* Add it as §10.1 Q12 and as a `[NOTE FOR PM]` at FR-30. State which FRs change under revenue share (a qualifying-sales report after refunds, partner deduction export).

## Substance over theater — strong
Personas are three one-line job statements (§3.1) that each drive a part of the product; there is no persona theater. The Vision (§2) is specific to this office (1,987,336 SAR latent vs 15,580 SAR deposited, manual follow-up as the bottleneck) and could not be swapped into another PRD. NFRs are mostly bounded (99.5% monthly, daily backup, WCAG 2.1 AA, <3s on 4G, NCA ECC). The notification matrix is real working content, not furniture.

### Findings
- **[low]** Performance bound covers store pages only (§8 «صفحات المتجر تُحمَّل في أقل من 3 ثوانٍ») — no bound for the dashboard, payment return or file upload/download, which are the heavy paths. *Fix:* Add bounds for the dashboard list views and upload throughput, or state explicitly that none are required.

## Strategic coherence — adequate
There is a clear thesis: quotes die from manual follow-up, so every waiting state gets a timeout, a reminder and an exit (§2). SM-1 (quotes accepted and paid ÷ sent) validates it directly, and SM-C1 is a real counter-metric. That is better than most.

Three things weaken the arc. First, the source says the 1.98M SAR came from «عروض لم تُنفّذ لعدم تجاوب أقل من 10 عملاء». The latent value sits in a handful of large B2B deals, which automated reminders may or may not convert. The PRD drops that qualifier, and nothing addresses those existing open quotes. Second, the office profile states Hull is «نقطة البداية لكل عميل … العميل لا يشتري خدمة منفصلة بل حلًا متكاملًا». The PRD makes Hull one product among a browsable catalog (FR-7, FR-14) and opens its first journey with a catalog purchase (UJ-1). That is an unacknowledged departure from the owner's product thesis, and it decides the store's information architecture, which is exactly what UX designs next. Third, §10.2 says «لا أهداف رقمية بعد» even though the PRD itself cites a baseline.

### Findings
- **[high]** Hull-first vs catalog-first not decided (§2, §3.2 UJ-1/UJ-2, FR-7, FR-14) — the owner's profile positions Hull as every customer's entry point. The PRD's storefront is catalog-led, with Hull as a peer product. This decides the home screen, navigation and primary call to action of the design Yahya will see. *Fix:* State the choice as a decision with its trade-off, or make it §10.1 Q12/13 with a `[NOTE FOR PM]`. If catalog-first stays, say why (instant services in the RFP catalog) and what Hull's placement is.
- **[medium]** Thesis evidence overstated and existing pipeline ignored (§2) — «طلبات كامنة بنحو 1.98 مليون ريال» omits «أقل من 10 عملاء». There is no FR or Non-Goal for loading the office's existing open quotes or clients onto the platform, which is the most direct test of the thesis. *Fix:* Restore the qualifier. Add an FR-38-style "import existing quote" path for the manager, or list it explicitly as a Non-Goal.
- **[medium]** Success Metrics have no targets or windows despite a baseline (§9, §10.2 «لا أهداف رقمية بعد») — the cited numbers imply a current quote-to-cash conversion below 1%. SM-2 (monthly revenue) is activity without a baseline, and SM-4 has no FR trace. *Fix:* Give SM-1 a baseline, a target and a window (for example quotes sent in a 30-day cohort), set SM-2 against the 15,580 SAR deposits, and link SM-4 to FR-1/FR-2/FR-9. Add a counter-metric for reminder fatigue (unsubscribes or complaints per reminder), since the thesis is reminder-driven.

## Done-ness clarity — adequate
The lifecycle tables and the FRs with «نتائج قابلة للاختبار» (FR-1–FR-4, FR-12, FR-13, FR-16, FR-18, FR-19, FR-20) are testable as written, and many shorter FRs carry their rules inline (FR-27, FR-29, FR-41, FR-42). But the lifecycle, the part story creation will lean on hardest, contradicts itself and violates its own rule in specific places. Several FRs also leave the "done" condition to the reader.

### Findings
- **[high]** Lifecycle states without an exit or with contradictory timeouts (§6.1, §6.2, §6.3) — this violates the PRD's own rule «لكل حالة انتظار مهلة وتذكير ومخرج (FR-33)»:
  - §6.1 «بانتظار معلومة منك»: the timeout column says «بعد 7 أيام معلّق», but the transitions say «14 يومًا دون رد ← معلّق للمتابعة اليدوية». «معلّق» has no row, no timeout and no exit, and it is not in the glossary.
  - «بانتظار اعتماد المدير» (§6.2 «قيد الدراسة») is referenced but has no row and no timeout.
  - §6.1 «بانتظار اعتماد المسودة» has reminders but no exit if the customer never responds.
  - §6.2 «المعاينة جاهزة» «14 يومًا ← متابعة المدير» and §6.3 unbooked session «بعد 14 يومًا متابعة الموظف» end in manual follow-up with no terminal outcome.
  - §6.2 «قيد الدراسة» and «بانتظار البدء» give «يوما عمل» with no stated consequence; §6.1 says «ثم تنبيه للمدير».

  *Fix:* Resolve 7 vs 14 days and add a «معلّق» row with its exits (resume / manager cancel with refund). Add a row for «بانتظار اعتماد المدير». Give each remaining state an explicit consequence. Where manual follow-up is the intended terminal outcome, state it as a deliberate exception to the rule.
- **[medium]** Foreigner path contradicts the account rules (§4, FR-38, FR-2, FR-26) — FR-38 serves «الأجانب بلا نفاذ» by creating an account «برقمه وبريده». FR-2 restricts phone accounts to «للأرقام السعودية فقط», and SMS is used only for OTP. So it is undefined how such a customer logs in, accepts a quote (FR-13 records «هوية القابل») or pays. The profile names foreign nationals as a strategic segment. *Fix:* Specify the on-behalf account: an email-OTP login, or manager-mediated acceptance and payment by link, with what identity is recorded on acceptance.
- **[medium]** Pending payment after 30 minutes is ambiguous (FR-16 vs §6 general rule) — a pending result is «تُعامل كفاشلة» after 30 minutes, which unblocks a second payment. A late success is refunded only «إن أُلغي الطلب». The case of a late success after the customer has already paid again is not covered, and it is a double-charge path. *Fix:* Add the outcome: the duplicate is auto-refunded and the order is not double-advanced. Name who is notified.
- **[medium]** FR-30 report not specified (FR-30) — «تقرير الإيرادات والضريبة لفترة، ويصدّره» gives no columns, export format, period granularity, or treatment of deposits vs revenue in the tax view. UJ-4 ends on this report. *Fix:* List the fields (invoice no., date, buyer, net, VAT, credit notes, refunds), the format (CSV/XLSX), and how a «دفعة مستلمة» appears in the VAT figures.
- **[medium]** Hull offer approval drifted from the accepted decision (FR-15, §6.3 vs `decisions-round-1.md` §4) — the decision says «يسعّرها الموظف ويعتمدها المدير قبل الإرسال» for every Hull offer. The PRD routes it «وفق FR-12», which requires approval only above the threshold. *Fix:* Restore mandatory manager approval for Hull offers, or record that the decision was reversed.
- **[low]** Revision-round count conflicts (FR-22 vs FR-28) — FR-22 fixes «جولتان للخدمة الفورية», while FR-28 makes «جولات التعديل» a per-service catalog field. *Fix:* State that the catalog value governs, with a default of 2.
- **[low]** Hull fee deduction edge cases (FR-15) — the PRD does not say what happens when the deposit is 0% or smaller than the Hull fee, or how the deduction appears on the deposit invoice (FR-18). *Fix:* Say whether the deduction carries to the final payment, and that it shows as an invoice line.
- **[low]** Nafath-required services have no catalog flag (FR-2, FR-28, FR-49) — «الخدمات الحكومية وتسجيل العلامة التجارية تتطلب حسابًا موثّقًا بالنفاذ», but FR-28's catalog fields include only the power-of-attorney input. *Fix:* Add a "requires Nafath" attribute to FR-28.
- **[low]** Unaccepted items after a partial acceptance (FR-12, FR-35, UJ-2) — «بعد القبول لا تُرسل نسخ». UJ-2 accepts one of two items, and the PRD does not say whether the second item can be accepted later or needs a new quote request. *Fix:* State it in one line.
- **[low]** Vague outcome words — FR-1 «برسالة واضحة» and FR-42 «بملاحظة آمنة» (encrypted? viewable once? hidden from staff after delivery?). *Fix:* Define «ملاحظة آمنة». The message copy can be left to UX.

## Scope honesty — adequate
§4 Non-Goals does real work: it names travel tickets, international post, multi-account organisations, foreigners' self-signup and the other phases. Inline `[ASSUMPTION]` tags are indexed in §10.2. The open-items density (11 questions plus about 14 assumption groups) is acceptable when UX design is the next step, though Q2 (Hull tiers) and Q3 (instant prices) affect the core screens.

The weakness is the tagging convention. §0 says «ما لم يؤكده يحيى مُعلَّم [ASSUMPTION]», but most of §6–§7 comes from Waleed's 18 decisions and was never confirmed by Yahya: the 18+ age, per-staff calendars, two delivery attempts, 12-month output retention, and so on. A reader following §0 will take untagged content as agreed with the client.

### Findings
- **[medium]** Tagging convention overstates what Yahya confirmed (§0, §10.2) — untagged rules are Dreamy/Waleed proposals, not Yahya's. *Fix:* Reword §0 along these lines: "everything not marked (الكراسة) is a Dreamy proposal; `[ASSUMPTION]` marks values we are least sure of". Alternatively, add a "مصدر القرار" note per section.
- **[medium]** «هللة» mislabelled as a later phase (§4) — the profile lists «هللة» in «المرحلة الأولى» alongside «كاتبة» and YYO Technic. Excluding it may be right, but calling it «وحدات المراحل اللاحقة» is inaccurate, and Yahya will notice. *Fix:* List it as its own Non-Goal for this platform, with the reason.
- **[low]** RFP pre-launch item dropped silently (§8 «ما قبل الإطلاق») — the RFP's pre-launch list includes «حملة تسويقية»; §8 omits it without comment. §4 does exclude marketing as a product feature. *Fix:* Note that the campaign is a pre-launch Dreamy service condition outside the product.

## Downstream usability — adequate
The glossary (§1) is strong and mostly honoured. IDs are unique and FR-1–FR-49 are contiguous. UJs have named protagonists, and SMs cite FRs. The lifecycle tables extract cleanly for UX and architecture.

### Findings
- **[medium]** «مراجعة» names two different things (FR-13 «طلب مراجعة» on an offer vs the state «قيد المراجعة» for disputes and cancellations in §6, FR-24, FR-39) — the UX copy and the state model will collide: a customer who "requested a review" of an offer is not «قيد المراجعة». *Fix:* Rename one, for example «طلب تعديل العرض» for the offer or «قيد قرار المدير» for the dispute state, and add both to §1.
- **[low]** Terms used but not in the glossary — «معلّق», «الحد» (approval threshold), «فترة الدعم» (appears only inside the «عرض السعر» entry), and the spelling drift «حل المخصص» (§6.2 heading) vs «حل مخصص» (§1, FR-14). *Fix:* Add the terms to §1 and normalise the spelling.

## Shape fit — strong
This is a multi-stakeholder consumer + B2B product with an office back-office and meaningful UX, so UJs with named protagonists are load-bearing, and they are present. Lifecycle tables suit a state-heavy service business, and the shape matches the product. This is a chain-top PRD (feeds UX next), and traceability is good.

### Findings
- **[low]** Office-side UJs are thin (§3.2 UJ-3, UJ-4) — they are arrow chains with no context or failure paths, and no UJ covers the on-behalf (FR-38) or bank-transfer (FR-37) flows, which are distinct dashboard screens. *Fix:* Add one line of context and 2–3 failure paths each (for example the customer never uploads the missing file, or the manager rejects an over-threshold offer). Consider a short UJ for the on-behalf order.

## Mechanical notes
- **Cross-refs:** the §0 sources `research/meeting-yahya-obaisi-2026-11-09.md` and `research/yyo-documents-extract.md` do not resolve relative to the PRD folder; the files live at `_bmad-output/planning-artifacts/research/`. Use `../../research/…`.
- **ID ordering:** FR-33–FR-49 are interleaved out of numeric order (for example FR-43 under §7.1, FR-33 at the end of §7.9). This is acceptable because §0 says «أرقام المتطلبات ثابتة»; no gaps or duplicates.
- **Assumptions Index roundtrip:** §10.2 indexes items with no inline tag: «القسم 6: كل المهل», «FR-39: 14 يومًا», «§9: لا أهداف رقمية». The inline FR-42 tag sits on the first bullet only, while the index also covers «مدة إتاحة المخرجات». Add inline tags at §6, FR-39 and the FR-42 retention bullet.
- **Lifecycle consistency:** §6.1 «قيد التنفيذ» lacks the «طلب إلغاء ← قيد المراجعة» transition that FR-24 and §6.2 have, although §6.1 «قيد المراجعة» lists «طلب إلغاء» as a trigger. The «مغلق» button reads «اطلب عرضًا جديدًا» (§6.2) where `decisions-round-1.md` §1 says «اطلب خدمة أخرى»; this is probably intentional, so confirm.
- **Required sections:** all present for a commercial-launch, UX-next PRD.
