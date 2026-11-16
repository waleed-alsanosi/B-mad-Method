---
name: "تَوزيع (Tawzee)"
description: "هوية بصرية لمنصة توزيعات الجملة — دافئة بما يكفي لمناسبة، موثوقة بما يكفي لعملية شراء بالجملة بآلاف الريالات."
status: draft
updated: 2026-11-16
sources:
  - _bmad-output/planning-artifacts/prds/prd-tawzee-2026-11-16/prd.md
colors:
  brand-primary: '#B0561F'
  brand-primary-dark: '#8A4217'
  brand-primary-tint: '#F1DCC9'
  brand-secondary: '#1F4B4A'
  brand-secondary-tint: '#D9E6E5'
  occasion-gold: '#D4A13D'
  surface-base: '#FBF7F1'
  surface-raised: '#FFFFFF'
  surface-admin: '#F4F6F6'
  border-subtle: '#E7DFD3'
  border-admin: '#DCE2E1'
  text-primary: '#241C14'
  text-secondary: '#6B5F50'
  text-inverse: '#FFFFFF'
  success: '#256B46'
  warning: '#C77C11'
  danger: '#B3342A'
  info: '#2C6E8E'
typography:
  display:
    fontFamily: "Tajawal, system-ui, sans-serif"
    fontWeight: 800
  heading:
    fontFamily: "Tajawal, system-ui, sans-serif"
    fontWeight: 700
  body:
    fontFamily: "Tajawal, system-ui, sans-serif"
    fontWeight: 400
  body-emphasis:
    fontFamily: "Tajawal, system-ui, sans-serif"
    fontWeight: 600
  numeric:
    fontFamily: "Tajawal, system-ui, sans-serif"
    fontWeight: 500
    note: "أرقام جدولية (tabular figures) لمحاذاة الأسعار والكميات في الجداول"
  caption:
    fontFamily: "Tajawal, system-ui, sans-serif"
    fontWeight: 400
    fontSize: "0.8125rem"
rounded:
  sm: '6px'
  md: '10px'
  lg: '16px'
  xl: '24px'
  full: '9999px'
  DEFAULT: '10px'
spacing:
  '1': '4px'
  '2': '8px'
  '3': '12px'
  '4': '16px'
  '5': '20px'
  '6': '24px'
  '8': '32px'
  '10': '40px'
  '12': '48px'
  gutter-mobile: '16px'
  gutter-web: '24px'
  section-gap: '32px'
components:
  button-primary:
    background: '{colors.brand-primary}'
    text: '{colors.text-inverse}'
    radius: '{rounded.md}'
    padding: '{spacing.3} {spacing.6}'
    hover: '{colors.brand-primary-dark}'
  button-secondary:
    background: 'transparent'
    border: '1px solid {colors.brand-secondary}'
    text: '{colors.brand-secondary}'
    radius: '{rounded.md}'
  card-product:
    background: '{colors.surface-raised}'
    radius: '{rounded.lg}'
    border: '1px solid {colors.border-subtle}'
    padding: '{spacing.4}'
  badge-occasion:
    background: '{colors.occasion-gold}'
    text: '{colors.text-primary}'
    radius: '{rounded.full}'
    padding: '{spacing.1} {spacing.3}'
  status-pill:
    radius: '{rounded.full}'
    padding: '{spacing.1} {spacing.3}'
    variants:
      pending: { background: '{colors.brand-primary-tint}', text: '{colors.brand-primary-dark}' }
      success: { background: '#DCEFE2', text: '{colors.success}' }
      danger: { background: '#F6DEDB', text: '{colors.danger}' }
  chat-bubble:
    radius: '{rounded.lg}'
    sent: { background: '{colors.brand-secondary}', text: '{colors.text-inverse}' }
    received: { background: '{colors.surface-raised}', text: '{colors.text-primary}', border: '1px solid {colors.border-subtle}' }
  admin-table-row:
    background: '{colors.surface-raised}'
    border-bottom: '1px solid {colors.border-admin}'
    hover: '{colors.surface-admin}'
---

## الهوية والطابع (Brand & Style)

**تَوزيع** يقف في منتصف المسافة بين تجربتين متناقضتين: تطبيق هدايا احتفالي (ألوان دافئة، مناسبات، فرح) ومنصة مشتريات بالجملة جادة (مبالغ كبيرة، قرارات مؤسسية، عقود). الهوية البصرية تحل هذا التوتر بفصل واضح: **سطح العميل** (موبايل وويب) دافئ واحتفالي بقدر مدروس — يُذكّر بأن كل طلب هو مناسبة حقيقية (يوم وطني، عيد، تخرج) — بينما **سطح الأدمن** يستخدم نفس اللغة البصرية لكن بكثافة أعلى وحياد أكبر، لأن مهمته مراقبة ونزاعات لا احتفال.

المرجعية البصرية مستقاة من أنماط سوق إلكتروني ناضج — فلاتر علوية واضحة بصيغة Chips (كـZalando)، بطاقات منتج كبيرة بصورة مهيمنة (كـAmazon وWolt)، ولوحة أدمن جدولية كثيفة (كـShopify Orders وEventbrite) — لا ابتكار بصري لأجل الابتكار، بل أنماط مثبَتة في منصات حقيقية مأخوذة عبر Mobbin.

`[ASSUMPTION: هوية بصرية كاملة من تأليف دريمي — لا يوجد شعار أو هوية سابقة لعائشة. راجعها معها قبل أي استثمار في تصميم الشعار الفعلي]`

## الألوان (Colors)

- **{colors.brand-primary}** (تراكوتا دافئ) — لون العلامة الأساسي. يُستخدم في أزرار الفعل الأساسية (تأكيد الطلب، الدفع)، وفي عناصر التمييز القليلة. ليس لون خلفية كبيرة — يظهر كلمسة، لا كغمر كامل للشاشة.
- **{colors.brand-secondary}** (أخضر-كحلي عميق/تيل) — لون الثقة. يُستخدم في روابط، في سطح الأدمن كلون تمييز أساسي بدل التراكوتا (الأدمن يحتاج هدوءًا لا احتفالًا)، وفي فقاعات الشات المُرسَلة.
- **{colors.occasion-gold}** — يُستخدم حصرًا لشارات المناسبات الموسمية (اليوم الوطني، الأعياد، رمضان) — لون نادر الظهور يُبقي إحساس "المناسبة" حيًا بدون ما يتحول لزخرفة دائمة.
- **{colors.surface-base}** (كريمي دافئ، ليس أبيض ناصع) — خلفية سطح العميل. يمنح دفئًا بصريًا يناسب منتج هدايا.
- **{colors.surface-admin}** — خلفية سطح الأدمن، أبرد وأكثر حيادًا من surface-base عمدًا — يفصل بصريًا بين "تجربة الاحتفال" و"تجربة العمل".
- **{colors.danger}** — للنزاعات والرفض ومهلة انتهاء الصلاحية فقط. لا يُستخدم كلون تزييني أبدًا.

## الخطوط (Typography)

- **{typography.display}** (Tajawal، وزن 800) — العناوين الكبيرة فقط (شاشة البداية، اسم المناسبة، عنوان المنتج الرئيسي). الأثر الاحتفالي يتركّز هنا.
- **{typography.heading}** (Tajawal، وزن 700) — عناوين الأقسام والبطاقات.
- **{typography.body}** / **{typography.body-emphasis}** (Tajawal، وزن 400 و500–700) — كل نص تشغيلي: أوصاف المنتجات، رسائل الشات، نصوص الأدمن. الخط موحّد مع العناوين لأن IBM Plex Sans Arabic غير متاح في ملف فيغما؛ اعتُمد Tajawal لعائلة واحدة عبر كل الأسطح.
- **{typography.numeric}** — أرقام الأسعار والكميات تستخدم أرقامًا جدولية (tabular) لمحاذاة الأعمدة في جداول الأدمن وملخصات السلة.
- كلا الخطين يدعمان العربية كلغة أساسية؛ أي نص إنجليزي (أسماء العلامات التجارية، SKU) يُعرض بنفس العائلة إن توفرت، أو بخط نظام افتراضي محايد.

## التخطيط والتباعد (Layout & Spacing)

مقياس تباعد بخطوة 4px ({spacing.1} إلى {spacing.12}) يغطي كل شيء من تباعد الأيقونات الداخلي إلى الفراغ بين الأقسام ({spacing.section-gap}). الهامش الجانبي الافتراضي {spacing.gutter-mobile} على الموبايل و{spacing.gutter-web} على الويب — أوسع على الويب لأن شاشات جهة الطلب والأدمن تُستخدم غالبًا على كمبيوتر مكتبي بعرض أكبر.

شبكة بطاقات المنتج: عمودان على الموبايل، 3-4 أعمدة على الويب حسب العرض. جداول الأدمن (الطلبات، الموردين) صف واحد لكل سجل، بدون تكسير الصف على الشاشات الضيقة — الأدمن يُستخدم من جهاز بعرض كافٍ دائمًا (لوحة أدمن ويب فقط، لا نسخة موبايل مطلوبة في v1).

## الظل والعمق (Elevation & Depth)

ظل خفيف جدًا وناعم على البطاقات العائمة (بطاقة المنتج، نافذة الدردشة) للإيحاء بإمكانية اللمس دون ثقل بصري. سطح الأدمن يستخدم حدودًا خطية (`{colors.border-admin}`) بدل الظلال في الجداول — تمييز متعمد: الظل للمحتوى الاحتفالي القابل للمس، الخط للبيانات الكثيفة القابلة للمسح السريع.

## الأشكال (Shapes)

انحناء متوسط إلى كبير ({rounded.md} إلى {rounded.lg}) على البطاقات والأزرار — ودود بما يكفي لمنتج هدايا، دون الانزلاق لطابع لعبي بالكامل (لا {rounded.full} إلا على الشارات وحالات الحبوب/Pills مثل status-pill وbadge-occasion). عناصر الأدمن (الجداول، الحقول) تستخدم {rounded.sm} فقط — زوايا أقرب للمستقيم تعكس طابعًا تشغيليًا جادًا.

## المكونات (Components)

- **button-primary** — تراكوتا، نص أبيض، زوايا متوسطة. الفعل الوحيد الحاسم في كل شاشة (تأكيد، دفع، إرسال). لا يتكرر أكثر من زر أساسي واحد ظاهر بالشاشة الواحدة.
- **button-secondary** — إطار فقط بلون الثقة (teal)، بلا خلفية — للأفعال الثانوية (إلغاء، رجوع، تعديل).
- **card-product** — الوحدة الأساسية لتصفح الكتالوج (FR-1، FR-2): صورة مهيمنة، اسم، سعر بحسب الشريحة، شارة مناسبة اختيارية.
- **badge-occasion** — شارة ذهبية صغيرة فوق بطاقة المنتج عند ارتباطه بمناسبة (اليوم الوطني، عيد...).
- **status-pill** — حالة الطلب (بانتظار الموافقة / مقبول / مرفوض) بثلاثة تلوينات دلالية (pending/success/danger) — تُستخدم في كل من تطبيق العميل والمورد ولوحة الأدمن بنفس المنطق.
- **chat-bubble** — فقاعة مرسلة بلون الثقة، مستلمة بخلفية بيضاء وحدّ خفيف — يعكس أن الشات (FR-7) مساحة محايدة وآمنة، لا مساحة بيع.
- **admin-table-row** — صف جدول كثيف بحد سفلي خفيف، بلا ظل، مع تمييز عند المرور (hover) بلون surface-admin.

## نظام التصميم في فيغما

الملف: https://www.figma.com/design/xo8TVFRlfd4MimTajXSgCn

- **المتغيرات (78):** مجموعة `Primitives` (25 لونًا أوليًا مخفيًا)، `Color` (33 لونًا دلاليًا يشير كلٌّ منها إلى لون أولي)، `Spacing` (13)، `Radius` (7). أسماء المتغيرات الدلالية تطابق رموز هذه الوثيقة مع بادئة `color/` وتجميع بالشرطة المائلة (مثل `color/brand/primary`).
- **أنماط النصوص (14)** وأنماط الظل (2): `shadow/card` و`shadow/overlay`.
- **المكوّنات (33) والأيقونات (33)** في صفحة «المكوّنات»، وكل تعبئاتها وحدودها ومسافاتها وزواياها مربوطة بالمتغيرات.

## ما يجب وما لا يجب (Do's and Don'ts)

- ✅ استخدم {colors.brand-primary} فقط للفعل الأساسي الواحد في الشاشة — أبدًا كخلفية كاملة.
- ✅ استخدم {colors.occasion-gold} بشكل نادر ومتعمد (شارة واحدة أو بانر موسمي) — ليس كلون متكرر.
- ✅ حافظ على الفصل البصري بين سطح العميل (دافئ) وسطح الأدمن (محايد وكثيف) حتى مع تقاسم نفس نظام الألوان.
- ❌ لا تستخدم {colors.danger} أو {colors.warning} لأي غرض تزييني أو لجذب الانتباه خارج سياق خطأ/نزاع/مهلة فعلية.
- ❌ لا تستخدم زوايا {rounded.full} في عناصر الأدمن الجدولية — الطابع التشغيلي يتطلب زوايا مستقيمة الأثر.
- ❌ لا تُكرر شارة المناسبة الذهبية على كل بطاقة بلا استثناء — تفقد قيمتها الدلالية عند التكرار المفرط.
