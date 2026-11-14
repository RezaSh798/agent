---
name: gitlab-report
description: Generate structured, human-readable GitLab progress and spend reports detailing problems solved, technical fixes, development iterations, and time tracking.
---

# GitLab Report Skill (`/gitlab-report`)

Generate professional, engineering-grade work reports for GitLab merge requests, issues, or standup updates. The report balances clarity and conciseness with technical depth, making it effortless for humans to review while transparently documenting the full effort and complexity (including debugging iterations) to justify the logged `/spend` time.

## Arguments & Input
- **Input:** Context from the current conversation, modified git files, git log/diff, test results, or explicit user guidelines.
- If invoked without specific parameters, analyze the recent conversation history, git diff, and completed tasks to generate the report.

## Tone & Style
- **Language:** Semi-formal, technical Persian (فارسی روان و مهندسی).
- **Concise & Direct:** Avoid unnecessary flattery, corporate fluff, or repetitive phrases.
- **Human-Readable:** Use clean markdown lists, bold keywords, and well-organized sections so a tech lead or manager can scan it in under 60 seconds.

## Standard Report Template

Each report must follow this exact section structure:

```markdown
## 🎯 خلاصه دستاوردها
<یک تا دو جمله کوتاه و شفاف درباره هدف اصلی و نتیجه نهایی تسک>

---

## 🔍 شرح چالش‌ها و راهکارهای فنی (به تفکیک بخش‌ها)
### ۱. <نام بخش / سناریو>
- **چالش / ریسک:** <مشکل دقیق فنی، ریس‌کاندیشن، قطعی، یا ناسازگاری داده>
- **راهکار اعمال‌شده:** <تغییرات مهندسی در لایه کدهای پروژه، ریپازیتوری یا الگوریتم>

### ۲. ...

---

## 🔄 چالش‌های مسیر توسعه و بازنگری‌ها (Debugging & Iterations)
> بیان مواردی که در حین پیاده‌سازی یا تست کشف شدند، رویکردهایی که بازنگری شدند یا خطاهایی که شناسایی و عیب‌یابی شدند:
- **<مورد اول>:** <رویکرد اولیه -> چالش/باگ پنهانی که نمایان شد -> نحوه اصلاح نهایی>
- **<مورد دوم>:...**

---

## 🧪 نتایج اعتبارسنجی و تست‌ها
- **تست‌های واحد و همزمانی:** <تعداد کل تست‌ها و پوشش سناریوها>
- **تست در محیط زنده (Live Store Probe):** <بررسی مستقیم روی سرویس‌های ردیس/دیتابیس بدون ماک>

---

/spend <مدت زمان واقع‌بینانه مانند 2d یا 16h یا 4h>
```

## Guidelines for Content Quality
1. **Highlight Real Iterations:** Do not pretend everything was a straight path. Documenting that an edge case or environment constraint was hit and overcome shows real engineering diligence and justifies time tracking.
2. **Action-Oriented Explanations:** Focus on *why* a decision was made (e.g., CAS atomic check vs double refresh, post-save cleanup vs race conditions).
3. **Accurate Spend Suggestion:** Propose a realistic `/spend` duration matching the actual scope and effort.
