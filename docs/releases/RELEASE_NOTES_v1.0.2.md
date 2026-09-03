<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.2

This release strengthens archive maintenance, legacy PST migration, index coordination, and installation checks.

> This is an older release. Install the [latest version](https://github.com/ParhamGhafouri/EmailTools/releases/latest) for current fixes and safety improvements.

### Highlights

- Uses verified mailbox metrics for Emergency Archive and runs maintenance tasks through one coordinated lane.
- Drains legacy PST files to the correct managed archive and removes a source only after exact-zero verification.
- Repairs seasonal archive placement and reports the real maintenance stage in Status.
- Prevents indexing, GAL maintenance, and archive work from restarting or blocking one another.
- Tightens dependency, package, signature, repair, and downgrade validation.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights.

**Release assets:** **EmailTools_Setup.rar** is the recommended manual package; **EmailTools_Setup.exe** is also used by the in-app updater; **version.json** is the updater manifest and does not need to be downloaded manually.

**Requirements:** Windows 10 or Windows 11 - Microsoft Outlook 2016, 2019, 2021, or Microsoft 365 desktop - .NET Framework 4.8.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه نگهداری آرشیو، انتقال PSTهای قدیمی، هماهنگی ایندکس و بررسی‌های نصب را پایدارتر می‌کند.</p>

  <blockquote>این نسخه قدیمی است. برای دریافت اصلاحات و بهبودهای ایمنی فعلی، <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest">جدیدترین نسخه</a> را نصب کنید.</blockquote>

  <h3>ویژگی‌های اصلی</h3>
  <ul>
    <li>برای Emergency Archive از اندازه تأییدشده صندوق استفاده می‌کند و کارهای نگهداری را در یک مسیر هماهنگ اجرا می‌کند.</li>
    <li>PSTهای قدیمی را به آرشیو مدیریت‌شده درست منتقل می‌کند و منبع را فقط پس از تأیید صفر دقیق حذف می‌کند.</li>
    <li>محل پیام‌ها در آرشیوهای فصلی را اصلاح می‌کند و مرحله واقعی نگهداری را در Status نشان می‌دهد.</li>
    <li>از شروع دوباره یا مسدودکردن یکدیگر توسط Indexing، GAL و Archive جلوگیری می‌کند.</li>
    <li>بررسی وابستگی‌ها، بسته، امضا، Repair و Downgrade را سخت‌گیرانه‌تر می‌کند.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب فقط برای حساب Windows شما انجام می‌شود و به دسترسی Administrator نیاز ندارد.</p>

  <p><strong>فایل‌های انتشار:</strong> <strong>EmailTools_Setup.rar</strong> بسته پیشنهادی نصب دستی است؛ <strong>EmailTools_Setup.exe</strong> توسط به‌روزرسان داخلی نیز استفاده می‌شود؛ <strong>version.json</strong> اطلاعات به‌روزرسان است و نیازی به دانلود دستی ندارد.</p>

  <p><strong>پیش‌نیازها:</strong> Windows 10 یا Windows 11 - نسخه دسکتاپ Microsoft Outlook 2016، 2019، 2021 یا Microsoft 365 - ‎.NET Framework 4.8.</p>
</div>
