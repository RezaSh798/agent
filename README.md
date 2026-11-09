# Agent Skills Suite

مجموعه مهارت‌های استاندارد و پیشرفته برای هوش مصنوعی کدنویسی و ایجنت‌های توسعه نرم‌افزار، مبتنی بر قرارداد رسمی **Agent Skills Specification** (کاملاً سازگار با **Google Antigravity**, **Kilo Code**, **Claude Code**, **Cursor** و سایر ابزارهای مدرن).

---

## 🏛️ ساختار معماری (Skills Architecture)

در این مخزن، تمامی قابلیت‌ها بر پایه استاندارد یکپارچه **Agent Skills** ساختاربندی شده‌اند. طبق این قرارداد استاندارد:
1. هر قابلیت به عنوان یک پوشه مجزا درون `skills/` به همراه سند دستورالعمل `SKILL.md` تعریف می‌شود.
2. هر مهارت به صورت دوگانه قابل استفاده است:
   - **فراخوانی صریح (Slash Commands):** از طریق تایپ اسلش‌کامند در محیط چت (مانند `/code-review` یا `/spec-runner`).
   - **فعال‌سازی هوشمند زمینه‌ای (Semantic Activation):** ایجنت در مواجهه با تسک‌های مرتبط به صورت خودکار دانش رویه‌ای مهارت مربوطه را لود و به کار می‌گیرد.
3. فایل‌های کمکی، قالب‌ها یا تعاریف ایجنت‌ها به صورت ایزوله در پوشه‌های `references/` یا `scripts/` همان مهارت نگهداری می‌شوند.

```text
skills/
├── code-review/
│   └── SKILL.md
├── gitlab-issue/
│   └── SKILL.md
├── prompt-architect/
│   └── SKILL.md
├── refactor-module/
│   └── SKILL.md
├── spec-kit/
│   └── SKILL.md
└── spec-runner/
    ├── SKILL.md
    └── references/
        └── task-runner.md
```

---

## ⚡ فهرست مهارت‌ها (Skills Catalog)

### 🔍 [`code-review`](./skills/code-review/SKILL.md)
بررسی خودکار، دقیق و موضعی کدهای شاخه جاری در مقایسه با شاخه مرجع (`develop` یا `master`) بر اساس سه اصل اساسی:
1. **صحت عملکردی و باگ‌ها (Functionality & Correctness)**
2. **معماری تمیز و حفظ مرزبندی لایه‌ها (Clean Architecture)**
3. **کد تمیز و نگه‌داری‌پذیری (Clean Code & Readability)**

- **اسلش‌کامند:** `/code-review`
- **ورودی‌ها:** نام شاخه مبنا (اختیاری) و/یا آدرس Merge Request گیت‌لب.
- **ویژگی‌ها:**
  - **تردهای بحث خطی و موضعی (Inline Discussion Threads):** تفکیک دقیق هر ایراد بر روی خط و فایل تغییریافته.
  - **حالت دوگانه اجرا (Dual Modes):**
    - *ثبت خودکار در گیت‌لب:* در صورت دسترسی به توکن (`GITLAB_TOKEN`) یا `glab` CLI، تردها مستقیم در MR گیت‌لب ثبت می‌شوند.
    - *کارت‌های آماده کپی:* در صورت نبود توکن یا دسترسی آفلاین، هر ایراد در قالب کارت‌های تفکیک‌شده مارک‌داون جهت کپی و پیست سریع در تب Changes گیت‌لب نمایش داده می‌شود.
  - **تمرکز انحصاری بر تغییرات MR (Diff-Only Review):** پرهیز کامل از ایرادگیری به کدهای قدیمی دست‌نخورده پروژه.

---

### 🦊 [`gitlab-issue`](./skills/gitlab-issue/SKILL.md)
تبدیل یادداشت‌های خام، گزارش‌های باگ یا ایده‌های فیچر به ایشوهای استاندارد و حرفه‌ای گیت‌لب در نقش Technical PM / Issue Writer (بدون ارائه مستقیم کد).

- **اسلش‌کامند:** `/gitlab-issue`
- **ورودی‌ها:** یادداشت یا شرح اولیه باگ/فیچر.
- **ویژگی‌ها:**
  - عنوان انگلیسی استاندارد با افعال قراردادی (`Fix...`, `Add...`, `Improve...`).
  - بدنه ساختاریافته به فارسی نیمه‌رسمی (شامل بخش‌های: خلاصه، وضعیت فعلی، انتظار ما، پیشنهاد مسیرهای بررسی، و نکات).
  - دستورات سریع گیت‌لب (GitLab Quick Actions) شامل مایلستون، اساین و برچسب‌های تفکیک‌شده در یک کدبلاک منسجم و آماده کپی.

---

### 🎯 [`prompt-architect`](./skills/prompt-architect/SKILL.md)
تبدیل ایده‌ها و درخواست‌های اولیه توسعه‌دهنده به پرامپت‌های مهندسی‌شده، دقیق و استاندارد برای ایجنت‌های کدنویسی هوش مصنوعی.

- **اسلش‌کامند:** `/prompt-architect`
- **ورودی‌ها:** ایده یا شرح اولیه تسک به فارسی یا انگلیسی.
- **ویژگی‌ها:**
  - تعامل و گفت‌وگو به زبان فارسی جهت شفاف‌سازی و ارائه پیشنهادهای بهبود.
  - اعمال اصول ضدتوهم (Anti-hallucination Guardrails).
  - تولید پرامپت نهایی به زبان انگلیسی در یک کدبلاک مستقل شامل بخش‌های استاندارد: Role، Objective، Context، Technical Environment (پیش‌فرض Node.js)، Constraints، Evaluation Criteria، و Output Format.

---

### 🛠️ [`refactor-module`](./skills/refactor-module/SKILL.md)
مهارت ریفکتورینگ عمل‌گرایانه، امن و نگه‌داری‌پذیر ماژول‌های جاوااسکریپت و تایپ‌اسکریپت در محیط Node.js بدون ایجاد تغییرات مخرب (Zero Breaking Changes) یا پیچیدگی کاذب.

- **اسلش‌کامند:** `/refactor-module`
- **ورودی‌ها:** مسیر ماژول هدف (`.js`, `.ts`, `.mjs`, `.cjs`).
- **ویژگی‌ها:**
  - مستندسازی کامل متدها، پارامترها و خروجی‌ها با JSDoc.
  - پیاده‌سازی اصول SOLID (شکستن توابع بلند بر اساس SRP، جدول استراتژی برای OCP، اینترفیس‌های کوچک، تزریق وابستگی).
  - استفاده از Guard Clauses و Early Returns برای کاهش تو رفتگی کدهای شرطی.
  - استخراج مقادیر جادویی (Magic Values) به ثابت‌های فریز شده ماژول.
  - ارتقای کدهای پرامیس به `async/await` و بهینه‌سازی پرتاب خطاها.

---

### 📋 [`spec-kit`](./skills/spec-kit/SKILL.md)
توسعه مبتنی بر مشخصات (Spec-Driven Development) با استفاده مستقیم از ابزار رسمی **GitHub Spec Kit (`specify` CLI)** جهت تبدیل ایده‌ها به اسناد استاندارد مشخصات، پلن‌های معماری و تسک‌های اجرایی اتمیک.

- **اسلش‌کامند:** `/spec-kit`
- **ورودی‌ها:** عنوان یا شرح خلاصه فیچر جدید.
- **ویژگی‌ها:**
  - شفاف‌سازی تعاملی سناریوهای کاربری، اولویت‌ها (P1, P2)، مرزهای سیستم و استک فنی پیش از ایجاد فایل‌ها.
  - گیت تأیید صریح کاربر (Approval Gate).
  - سازگاری کامل با **Google Antigravity** (`--ai agy`)، **Kilo Code** (`--integration kilocode`)، و سایر ایجنت‌ها.
  - اجرای خودکار اسکریپت‌های رسمی Spec Kit (`create-new-feature.sh`، `setup-plan.sh`، `setup-tasks.sh`) و ایجاد فایل‌های `spec.md`، `plan.md` و `tasks.md`.

---

### ⚙️ [`spec-runner`](./skills/spec-runner/SKILL.md)
اجرای ترتیبی و گام‌به‌گام تسک‌های مشخص‌شده در اسناد Spec یا آرگومان‌های ورودی با استفاده از ساب‌ایجنت‌های ایزوله (`task-runner`).

- **اسلش‌کامند:** `/spec-runner`
- **ورودی‌ها:** مسیر فایل تسک‌های مشخصات (`tasks.md`) یا لیست تسک‌ها.
- **ویژگی‌ها:**
  - اجرای اتمیک و مستقل هر تسک با کانتکست تازه از طریق ساب‌ایجنت ایزوله بر اساس دستورالعمل استاندارد [task-runner.md](./skills/spec-runner/references/task-runner.md).
  - پشتیبانی از فراخوانی ساب‌ایجنت در **Antigravity** (با `define_subagent` / `invoke_subagent`) و **Kilo** (با ابزار `task`).
  - اعتبارسنجی مرحله‌ای هر تسک با اجرای تست‌ها و لینت در ترمینال پیش از رفتن به تسک بعدی.
  - ارائه گزارش نهایی و خلاصه‌ای ساختاریافته از تغییرات اعمال‌شده.

---

## 📥 راهنمای نصب و راه‌اندازی (Installation Guide)

### ۱. نصب در Google Antigravity

#### الف) نصب سراسری برای تمامی پروژه‌ها (Global):
برای اینکه تمام اسکیل‌ها در کلیه پروژه‌های بازشده در Antigravity در دسترس باشند:

```bash
# ایجاد دایرکتوری اسکیل‌های گلوبال Antigravity
mkdir -p ~/.gemini/config/skills

# ایجاد سیم‌لینک برای همگام‌سازی خودکار با پول کردن ریپو
ln -sfn /path/to/agent/skills/* ~/.gemini/config/skills/

# یا کپی مستقیم:
# cp -r /path/to/agent/skills/* ~/.gemini/config/skills/
```

#### ب) نصب محلی فقط در یک پروژه مشخص (Workspace-Level):
```bash
# در ریشه پروژه مقصد
mkdir -p .agents/skills
ln -sfn /path/to/agent/skills/* .agents/skills/
```

---

### ۲. نصب در Kilo Code

#### الف) نصب سراسری (Global):
```bash
mkdir -p ~/.agents/skills
ln -sfn /path/to/agent/skills/* ~/.agents/skills/
```

#### ب) نصب از طریق ابزار استاندارد Skills CLI:
```bash
npx skills add RezaSh798/agent@refactor-module -g
npx skills add RezaSh798/agent@code-review -g
npx skills add RezaSh798/agent@gitlab-issue -g
npx skills add RezaSh798/agent@prompt-architect -g
npx skills add RezaSh798/agent@spec-kit -g
npx skills add RezaSh798/agent@spec-runner -g
```

---

## 🤝 توسعه و مشارکت

تمامی اسکیل‌ها تحت استاندارد باز Agent Skills توسعه می‌یابند. در صورتی که مایل به افزودن مهارت جدید هستید:
1. پوشه‌ای هم‌نام با مهارت در مسیر `skills/<skill-name>/` ایجاد کنید.
2. فایل `SKILL.md` را با فرانت‌متر `name` و `description` آغاز کنید.
3. در صورت نیاز به اسکریپت یا تعاریف ایجنت، آن‌ها را در پوشه‌های `scripts/` یا `references/` داخل همان مهارت قرار دهید.
