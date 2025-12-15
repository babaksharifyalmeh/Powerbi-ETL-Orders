# Troubleshooting – Power BI ETL Orders

این فایل برای **ثبت مشکلات واقعی پروژه، علت‌ها و راه‌حل‌ها** ایجاد شده است. هدف این داک:

* مستندسازی تجربه عملی
* جلوگیری از تکرار خطاها
* افزایش ارزش پروژه برای ارائه حرفه‌ای (GitHub / منتور / مصاحبه)

---

## Issue 1: Incorrect Data Types After Import

**Status:** Resolved

### Problem

پس از ایمپورت فایل‌های Excel، برخی ستون‌ها (Sales، Profit، Date) با نوع داده نادرست شناسایی شدند (Text به‌جای Number/Date).

### Root Cause

Power BI هنگام Load اولیه، به دلیل ناسازگاری داده‌ها یا وجود مقادیر خاص، نوع داده را اشتباه تشخیص داده بود.

### Solution

* انتخاب تمام ستون‌ها در Power Query Editor

* استفاده از مسیر:

  `Transform → Detect Data Type`

* سپس تغییر دستی ستون‌های `Sales` و `Profit` به **Fixed Decimal Number**

### Prevention

* همیشه قبل از Close & Apply، نوع داده‌ها بررسی و تثبیت شوند.

---

## Issue 2: Duplicate Rows After Merge

**Status:** Resolved

### Problem

پس از Merge کردن جداول `List of Order` و `OrderBreakdown`، برخی سفارش‌ها چند بار تکرار شدند.

### Root Cause

Join Key به‌درستی انتخاب نشده بود و رابطه One-to-Many رعایت نشده بود.

### Solution

* بازبینی ستون کلید مشترک (Order ID)
* استفاده از **Merge Queries as New**
* اطمینان از نوع Join صحیح (Left Outer Join)

### Prevention

* قبل از Merge، یکتایی کلیدها بررسی شود.

---

## Issue 3: Country Name Inconsistency

**Status:** Resolved

### Problem

کشور United Kingdom با دو نام متفاوت (UK و United Kingdom) در ویژوال‌ها نمایش داده می‌شد.

### Root Cause

عدم استانداردسازی نام کشورها در داده خام.

### Solution

* استفاده از Replace Values در ستون `Country`
* تغییر `United Kingdom` به `UK`

### Prevention

* اجرای مرحله Data Standardization در ابتدای ETL.

---

## Issue 4: Product Name and Attributes Mixed

**Status:** Resolved

### Problem

ستون Product Name شامل نام محصول و ویژگی آن به‌صورت ترکیبی بود.

### Root Cause

ساختار داده خام به‌صورت Unnormalized.

### Solution

* استفاده از **Split Column** در Power Query
* ایجاد ستون مجزا برای ویژگی محصول (`Product Name2`)

### Prevention

* نرمال‌سازی داده‌ها قبل از مدل‌سازی.

---

## Issue 5: Unable to Use Persian Dates in Visuals

**Status:** Resolved

### Problem

امکان استفاده از تاریخ شمسی در Slicerها و نمودارها وجود نداشت.

### Root Cause

Power BI به‌صورت پیش‌فرض فقط از تاریخ میلادی پشتیبانی می‌کند.

### Solution

* ایجاد فایل Excel تقویم شمسی (Gregorian ↔ Shamsi)
* ایمپورت فایل تقویم به Power BI
* ایجاد Relationship بین `Order Date` و تاریخ میلادی تقویم

### Prevention

* همیشه یک Date Table مستقل برای تحلیل زمانی ایجاد شود.

---

## Issue 6: Ambiguous Relationships in Model View

**Status:** Resolved

### Problem

پس از افزودن جدول تقویم، هشدار Ambiguous Relationship نمایش داده شد.

### Root Cause

وجود بیش از یک مسیر ارتباطی بین جداول.

### Solution

* غیرفعال‌سازی روابط غیرضروری
* تنظیم Cross Filter Direction به Single

### Prevention

* طراحی مدل داده قبل از ساخت Relationship‌ها.

---

## Issue 7: Large File Size & Git Conflicts

**Status:** Mitigated

### Problem

فایل‌های Power BI حجیم بوده و برای Git مناسب نیستند.

### Root Cause

استفاده از فرمت سنتی `.pbix` و فایل‌های کش محلی.

### Solution

* استفاده از **Power BI Project (.pbip)**
* به‌روزرسانی `.gitignore` برای فایل‌های محیطی و کش

### Prevention

* استفاده از PBIP در پروژه‌های Version-controlled.

---

## General Notes

* این فایل به‌صورت تدریجی و با پیشرفت پروژه تکمیل خواهد شد.
* هر Issue جدید باید بلافاصله ثبت شود.

---

## Git Commit

```bash
git add docs/troubleshooting.md
git commit -m "docs: add troubleshooting log for core ETL phase"
```

---

*Last updated: Dec 2025*
