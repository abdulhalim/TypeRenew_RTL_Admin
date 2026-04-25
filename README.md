# TypeRenew RTL - راست‌چین کردن پنل مدیریت TypeRenew

افزودن پشتیبانی کامل راست‌چین (RTL) به پنل مدیریت TypeRenew به همراه **انعطاف کامل در انتخاب فونت فارسی**.

## ✨ قابلیت‌ها

- ✅ راست‌چین کردن کامل سایدبار و تمام المان‌های پنل مدیریت
- ✅ پشتیبانی از اعداد فارسی با استفاده از `font-feature-settings`
- ✅ فونت پیش‌فرض وزیرمتن (امکان تغییر به هر فونت دلخواه)
- ✅ سازگاری کامل با تم TypeRenew
- ✅ تغییر فقط **یک خط** در یک فایل + **اختیاری** اضافه کردن فونت
- ✅ بدون نیاز به تغییر فایل‌های اصلی CSS پوسته

## 🧩 ساختار فایل‌ها (حداقل حالت)

```
/your-website/admin/
├── css/
│   └── rtl.css          (فایل اصلی راست‌چین - اجباری)
```

> **توجه**: فایل `fonts.css` **اختیاری** است. اگر فایل جداگانه‌ای برای فونت تعریف نکنید، سیستم از فونت پیش‌فرض مرورگر (Tahoma, Segoe UI) استفاده می‌کند.

---

## 🖋️ مدیریت فونت فارسی (سه روش مختلف)

### روش اول: استفاده از فونت وزیرمتن (محلی - پیشنهادی)

این روش سریع‌ترین و پایدارترین روش است.

#### مرحله 1: دانلود فایل‌های فونت

فایل‌های وزیرمتن را از [GitHub - rastikerdar/vazirmatn](https://github.com/rastikerdar/vazirmatn/releases/latest) دانلود کنید. فقط این دو فایل `.woff2` را بردارید:

- `Vazirmatn-Regular.woff2`
- `Vazirmatn-Bold.woff2`

#### مرحله 2: آپلود فایل‌های فونت در مسیر مشخص

فایل‌های دانلود شده را در مسیر زیر روی هاست خود آپلود کنید:

```
/your-website/admin/fonts/
├── Vazirmatn-Regular.woff2
└── Vazirmatn-Bold.woff2
```

> **نکته مهم**: پوشه `fonts` باید در کنار پوشه `css` قرار گیرد. یعنی:
> - فایل‌های CSS در `/admin/css/`
> - فایل‌های فونت در `/admin/fonts/`

#### مرحله 3: ایجاد فایل fonts.css در مسیر `/admin/css/`:

```css
/* =============================================
   فونت وزیرمتن - نسخه محلی (Local)
   ============================================= */

@font-face {
    font-family: 'Vazirmatn';
    src: url('../fonts/Vazirmatn-Regular.woff2') format('woff2');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
}

@font-face {
    font-family: 'Vazirmatn';
    src: url('../fonts/Vazirmatn-Bold.woff2') format('woff2');
    font-weight: 700;
    font-style: normal;
    font-display: swap;
}

body,
body.tr-admin {
    font-family: 'Vazirmatn', system-ui, 'Segoe UI', Tahoma, sans-serif !important;
    font-feature-settings: "ss01" !important;
    font-variant-numeric: persian !important;
}
```

#### مرحله 4: اضافه کردن هر دو فایل CSS به `header.php`:

```php
<link rel="stylesheet" href=".../css/rtl.css">
<link rel="stylesheet" href=".../css/fonts.css">
```

---

### روش دوم: استفاده از CDN وزیرمتن (سریع برای نصب اولیه)

اگر نمی‌خواهید فایل‌های فونت را روی هاست خود آپلود کنید، از CDN استفاده کنید.

**بدون نیاز به دانلود و آپلود فایل** - فقط فایل `fonts-cdn.css` را بسازید:

```css
/* =============================================
   فونت وزیرمتن - نسخه CDN (ریموت)
   منبع: cdn.fontcdn.ir
   ============================================= */

@font-face {
    font-family: 'Vazirmatn';
    src: url('https://cdn.fontcdn.ir/Fonts/Vazirmatn/Vazirmatn-Regular.woff2') format('woff2');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
}

@font-face {
    font-family: 'Vazirmatn';
    src: url('https://cdn.fontcdn.ir/Fonts/Vazirmatn/Vazirmatn-Bold.woff2') format('woff2');
    font-weight: 700;
    font-style: normal;
    font-display: swap;
}

body,
body.tr-admin {
    font-family: 'Vazirmatn', system-ui, 'Segoe UI', Tahoma, sans-serif !important;
    font-feature-settings: "ss01" !important;
    font-variant-numeric: persian !important;
}
```

---

### روش سوم: استفاده از فونت دلخواه شما (مثل ایران‌سنس، ایران‌نستعلیق، وغیره)

اگر می‌خواهید از فونت دیگری غیر از وزیرمتن استفاده کنید:

#### مرحله 1: فایل فونت خود را در مسیر `/admin/fonts/` آپلود کنید

```
/your-website/admin/fonts/
├── MyFont-Regular.woff2
└── MyFont-Bold.woff2
```

> **نکته**: فرمت‌های بهینه: `woff2` > `woff` > `ttf`

#### مرحله 2: فایل `fonts-custom.css` را با محتوای زیر بسازید:

```css
/* =============================================
   فونت دلخواه شما - جایگزین کنید
   ============================================= */

@font-face {
    font-family: 'MyCustomFont';
    src: url('../fonts/MyFont-Regular.woff2') format('woff2');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
}

@font-face {
    font-family: 'MyCustomFont';
    src: url('../fonts/MyFont-Bold.woff2') format('woff2');
    font-weight: 700;
    font-style: normal;
    font-display: swap;
}

body,
body.tr-admin {
    font-family: 'MyCustomFont', 'Vazirmatn', Tahoma, sans-serif !important;
    font-feature-settings: "ss01" !important;
    font-variant-numeric: persian !important;
}
```

#### مرحله 3: نام فونت خود را در فایل `fonts-custom.css` مقداردهی کنید

تمام تنظیمات در همین فایل انجام می‌شود و نیازی به تغییر `rtl.css` نیست.

---

## ⚖️ مقایسه: فونت محلی (Local) در مقابل ریموت (CDN)

| ویژگی | محلی (Local) | ریموت (CDN) |
|--------|--------------|-------------|
| **سرعت بارگذاری اول** | 🐢 کندتر (بستگی به هاست شما دارد) | 🚀 سریع (سرورهای بهینه) |
| **پایداری** | 🟢 بالا (وابسته به هاست خودتان) | 🟡 متوسط (وابسته به CDN شخص ثالث) |
| **آفلاین بودن** | ✅ کار می‌کند | ❌ قطعی اینترنت = بدون فونت |
| **سازگاری با قوانین GDPR/حریم خصوصی** | ✅ عالی (درخواست خارجی ندارد) | 🟡 متوسط (درخواست به دامنه دیگر) |
| **امنیت** | 🟢 کنترل کامل روی فایل | 🟡 ریسک جایگزینی فایل توسط CDN |
| **زمان تنظیم** | نیاز به دانلود + آپلود (~5 دقیقه) | فوری (فقط کپی لینک) |
| **فشرده‌سازی** | توسط شما (می‌توانید بهینه کنید) | خودکار توسط CDN |
| **کش شدن در مرورگر** | بستگی به هدرهای هاست دارد | معمولاً عالی |
| **محدودیت پهنای باند هاست** | مصرف می‌کند | مصرف نمی‌کند |

### توصیه نهایی:

- **برای سایت‌های عمومی و پربازدید** → استفاده از **CDN** (سرعت بالاتر، فشار کمتر روی هاست)
- **برای اینترانت، لوکال هاست یا سایت‌های حساس امنیتی** → **محلی** (بدون وابستگی خارجی)
- **برای توسعه و تست** → هر دو روش خوب است، CDN سریع‌تر برای راه‌اندازی اولیه

---

## 🚀 نصب و فعال‌سازی (حداقل حالت - فقط RTL بدون فونت خاص)

### مرحله 1: کپی فایل `rtl.css`

فایل `rtl.css` را در مسیر `/admin/css/rtl.css` قرار دهید.

### مرحله 2: ویرایش فایل `header.php`

فایل `/admin/header.php` را باز کنید و خطوط مربوط به CSS را پیدا کنید (حدود خط 30):

```php
$header .= '<link rel="stylesheet" href="' . $options->adminStaticUrl('css', 'normalize.css', true) . '">
<link rel="stylesheet" href="' . $options->adminStaticUrl('css', 'grid.css', true) . '">
<link rel="stylesheet" href="' . $options->adminStaticUrl('css', 'style.css', true) . '">
<link rel="stylesheet" href="' . $options->adminStaticUrl('css', 'renew-ui.css', true) . '">';
```

**فقط همین یک خط را به انتها اضافه کنید:**

```php
$header .= '<link rel="stylesheet" href="' . $options->adminStaticUrl('css', 'rtl.css', true) . '">';
```

### مرحله 3 (اختیاری): اضافه کردن فونت دلخواه

اگر می‌خواهید فونت خاصی اعمال شود، خط دوم نیز اضافه کنید:

```php
$header .= '<link rel="stylesheet" href="' . $options->adminStaticUrl('css', 'rtl.css', true) . '">
<link rel="stylesheet" href="' . $options->adminStaticUrl('css', 'fonts.css', true) . '">';
```

### مرحله 4: پاک کردن کش مرورگر

- **Windows/Linux**: `Ctrl + Shift + R`
- **Mac**: `Cmd + Shift + R`

---

## ❌ حذف و غیرفعال‌سازی

برای برگشت به حالت عادی (LTR بدون فونت خاص):

- خط اضافه شده مربوط به `rtl.css` را از `header.php` حذف کنید
- (اختیاری) خط `fonts.css` را نیز حذف کنید

---

## 📄 لایسنس

- این پروژه: **MIT**
- فونت وزیرمتن: **SIL Open Font License (OFL)**

---

## 🙏 تشکر

از تمام کسانی که این پروژه را آزمایش کردند، بازخورد دادند و به بهبود آن کمک کردند، سپاسگزارم.

تشکر ویژه از:
- تیم **TypeRenew** برای ساخت یک پنل مدیریت عالی
- **rastikerdar** برای فونت زیبای وزیرمتن
- همه کاربرانی که این پروژه را نصب و استفاده کردند

---

**مخزن پروژه در گیت‌هاب:**  
[https://github.com/abdulhalim/TypeRenew_RTL_Admin](https://github.com/abdulhalim/TypeRenew_RTL_Admin)
