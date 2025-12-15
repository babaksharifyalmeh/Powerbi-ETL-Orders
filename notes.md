# Project Notes – Power BI ETL Orders

## Overview

این فایل به‌عنوان **دفترچه یادداشت اجرایی پروژه** استفاده می‌شود و ثبت‌کننده‌ی تصمیمات، اقدامات انجام‌شده، و نکات مهم در حین اجرای تسک‌هاست. هدف از این فایل، مستندسازی سریع و غیررسمی اتفاقات پروژه است (در مقابل `project-report.md` که گزارش رسمی و نهایی‌تر خواهد بود).

---

## Task 1 – Environment Setup & Core ETL (Completed)

**Status:** ✅ Completed

### 1. Environment Setup

* آخرین نسخه **Power BI Desktop** از وب‌سایت رسمی Microsoft نصب شد.
* پروژه به‌صورت **Power BI Project (.pbip)** ایجاد شد تا سازگاری بهتری با Git داشته باشد.
* ساختار پوشه‌ها مطابق با تمپلیت اولیه پروژه ایجاد و تأیید شد.

**Notes:**

* استفاده از PBIP باعث می‌شود تغییرات مدل، کوئری‌ها و ریپورت قابل ردیابی در Git باشند.
* در حال حاضر فایل `requirements.txt` خالی است (نیازی به Python یا ابزار جانبی وجود نداشت).

---

### 2. Data Ingestion (Excel Sources)

* داده‌ها از مسیر زیر واکشی شدند:

  `Data/Raw Data/`

* منابع داده:

  * **List of Order**
  * **OrderBreakdown**

* هر دو منبع از طریق مسیر **Get Data → Excel** وارد Power Query Editor شدند.

**Notes:**

* در این مرحله هیچ فیلتری روی داده خام اعمال نشد.
* بررسی کیفیت داده‌ها قبلاً به‌صورت Exploratory در commit جداگانه مستند شده است.

---

### 3. Data Transformation – Business Logic

#### 3.1 Profit Categorization

* یک **Conditional Column** با نام `Profit Category` ایجاد شد:

  * Profit < 0  → `Negative profit`
  * Profit = 0  → `Break-even`
  * Profit > 0  → `Positive profit`

**Purpose:**

* ساده‌سازی تحلیل سودآوری و شناسایی سفارش‌های زیان‌ده در گزارش‌ها.

---

#### 3.2 Country Standardization

* در ستون `Country` مقدار **United Kingdom** به **UK** تغییر داده شد.

**Reason:**

* جلوگیری از چندگانگی نام کشورها در ویژوال‌ها و KPIها.

---

#### 3.3 Product Name Normalization

* ستون `Product Name` که شامل نام محصول + ویژگی بود Split شد.
* نام ستون ویژگی به `Product Name2` تغییر داده شد.

**Outcome:**

* امکان تحلیل جداگانه بر اساس نام محصول و ویژگی آن فراهم شد.

---

### 4. Merge vs Append (Learning-Oriented Step)

* دو کوئری `List of Order` و `OrderBreakdown`:

  * با استفاده از **Merge Queries (Join)** ترکیب شدند.
  * خروجی در کوئری جدیدی با نام `Total` ذخیره شد.

* به‌صورت آموزشی، یک **Append Queries** نیز انجام شد تا تفاوت Merge و Append در عمل بررسی شود.

**Key Takeaway:**

* Merge → ترکیب افقی بر اساس کلید مشترک
* Append → ترکیب عمودی ردیف‌ها

---

### 5. Persian Calendar Integration

* به دلیل نیاز کاربر نهایی به تاریخ شمسی:

  * یک فایل Excel حاوی **تاریخ میلادی، تاریخ شمسی و ماه شمسی** ایجاد شد.
  * این فایل از طریق Get Data وارد Power BI شد.

* پس از `Close & Apply`، در **Model View**:

  * بین `Order Date` و ستون تاریخ میلادی در جدول تقویم شمسی Relationship ایجاد شد.

**Result:**

* امکان استفاده از تاریخ شمسی در Slicerها و ویژوال‌ها فراهم شد.

---

### 6. Data Type & Formatting

* در Power Query Editor:

  * تمام ستون‌ها Select شدند.
  * گزینه **Detect Data Type** اعمال شد.

* ستون‌های مالی:

  * `Sale`
  * `Profit`

  به نوع **Fixed Decimal Number** تغییر داده شدند.

**Reason:**

* جلوگیری از خطاهای محاسباتی و نمایش استاندارد مقادیر مالی.

---

## General Notes

* در این تسک اسکرین‌شاتی در پوشه `Outputs/` ذخیره نشده است.
* برای تسک‌های بعدی، ثبت اسکرین‌شات از مراحل کلیدی الزامی خواهد بود.
* این تسک پایه‌ی تمام مراحل بعدی (مدل‌سازی، DAX، داشبوردسازی) محسوب می‌شود.

---

## Git Status

* این مرحله آماده‌ی Commit است.
* Commit پیشنهادی:

```bash
 git add docs/notes.md
 git commit -m "docs: add execution notes for Task 1 (core ETL steps)"
```

---

*Last updated: Dec 2025*
