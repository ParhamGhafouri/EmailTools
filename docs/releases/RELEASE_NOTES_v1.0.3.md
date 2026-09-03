<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.3

This release introduces Smart Archive for automatic PST quota management, improves Vacation Mode, and hardens background worker coordination.

### Highlights

- Smart Archive automatically creates and manages quarterly PST archives based on mailbox pressure and size limits.
- Vacation Mode moves recent email to the current quarterly archive before extended absences.
- Background worker handles offline registry updates and profile maintenance safely after Outlook exits.
- Enhanced search indexing reliability and responsive UI during background indexing passes.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights.

**Release assets:** **EmailTools_Setup.rar** is the recommended manual package; **EmailTools_Setup.exe** is also used by the in-app updater; **version.json** is the updater manifest and does not need to be downloaded manually.

**Requirements:** Windows 10 or Windows 11 - Microsoft Outlook 2016, 2019, 2021, or Microsoft 365 desktop - .NET Framework 4.8.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه بر سرعت Advanced Search، دقت پیش‌نمایش و مدیریت ایمن‌تر آرشیوها و پیام‌های محافظت‌شده تمرکز دارد.</p>

  <blockquote>این نسخه قدیمی است. برای دریافت اصلاحات و بهبودهای ایمنی فعلی، <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest">جدیدترین نسخه</a> را نصب کنید.</blockquote>

  <h3>ویژگی‌های اصلی</h3>
  <ul>
    <li>تغییر فیلترها و نمایش مجموعه‌های بزرگ نتیجه در Advanced Search را سریع‌تر می‌کند.</li>
    <li>جابجایی بین تطابق‌های Body، زمان محلی، نام پوشه خواناتر و پیش‌نمایش دقیق‌تر HTML را اضافه می‌کند.</li>
    <li>محتوای PST قدیمی را به آرشیو صندوق درست می‌فرستد و پاک‌سازی صفر دقیق را بهبود می‌دهد.</li>
    <li>پیام‌های Rights-managed را بدون بازکردن محتوای محافظت‌شده در زمان اسکن تشخیص می‌دهد.</li>
    <li>نگهداری GAL، شروع و خروج Outlook و مدیریت Resiliency در Installer را پایدارتر می‌کند.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب فقط برای حساب Windows شما انجام می‌شود و به دسترسی Administrator نیاز ندارد.</p>

  <p><strong>فایل‌های انتشار:</strong> <strong>EmailTools_Setup.rar</strong> بسته پیشنهادی نصب دستی است؛ <strong>EmailTools_Setup.exe</strong> توسط به‌روزرسان داخلی نیز استفاده می‌شود؛ <strong>version.json</strong> اطلاعات به‌روزرسان است و نیازی به دانلود دستی ندارد.</p>

  <p><strong>پیش‌نیازها:</strong> Windows 10 یا Windows 11 - نسخه دسکتاپ Microsoft Outlook 2016، 2019، 2021 یا Microsoft 365 - ‎.NET Framework 4.8.</p>
</div>
