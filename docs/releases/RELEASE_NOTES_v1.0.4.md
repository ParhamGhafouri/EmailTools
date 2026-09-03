<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.4

This release hardens Smart Archive, Emergency Archive, GAL rule repair, protected mail handling, and large-mailbox search.

### Highlights

- Smart Archive now follows the configured mailbox target, increases pressure through 30/20/10/8/6/4/2/1-day passes, and protects the newest 24 hours.
- Emergency Archive and Vacation Mode use verified destinations and stop at their intended target instead of over-draining the mailbox.
- Legacy PST migration uses exact destination checks and exact-zero source verification; protected mail is queued for the signed closed-Outlook worker.
- GAL rule repair changes only the cached display label, saves in place, and fails closed if identity or destination checks do not match.
- Conversation History repair is bounded, while Advanced Search uses cached sender data, local time, and a virtual grid for large result sets.
- Verified updates are staged in the background and handed to the signed runner after Outlook exits.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights.

**Release assets:** **EmailTools_Setup.rar** is the recommended manual package; **EmailTools_Setup.exe** is also used by the in-app updater; **version.json** is the updater manifest and does not need to be downloaded manually.

**Requirements:** Windows 10 or Windows 11 - Microsoft Outlook 2016, 2019, 2021, or Microsoft 365 desktop - .NET Framework 4.8.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه Smart Archive، Emergency Archive، اصلاح Ruleهای GAL، مدیریت پیام‌های محافظت‌شده و جست‌وجو در صندوق‌های بزرگ را پایدارتر می‌کند.</p>

  <h3>ویژگی‌های اصلی</h3>
  <ul>
    <li>Smart Archive از هدف تنظیم‌شده صندوق پیروی می‌کند، فشار را در بازه‌های 30/20/10/8/6/4/2/1 روز افزایش می‌دهد و ایمیل‌های 24 ساعت اخیر را حفظ می‌کند.</li>
    <li>Emergency Archive و Vacation Mode مقصد را تأیید می‌کنند و در هدف موردنظر متوقف می‌شوند تا صندوق بیش از حد تخلیه نشود.</li>
    <li>انتقال PST قدیمی مقصد دقیق و صفرشدن منبع را بررسی می‌کند؛ پیام‌های محافظت‌شده برای Worker امضاشده بعد از بسته‌شدن Outlook صف می‌شوند.</li>
    <li>اصلاح Ruleهای GAL فقط برچسب نمایشی ذخیره‌شده را تغییر می‌دهد و اگر هویت یا مقصد منطبق نباشد، بدون ذخیره متوقف می‌شود.</li>
    <li>Conversation History محدود و قابل پایان است؛ Advanced Search نیز برای نتیجه‌های بزرگ از داده Sender ذخیره‌شده، زمان محلی و Grid مجازی استفاده می‌کند.</li>
    <li>به‌روزرسانی تأییدشده در پس‌زمینه آماده و پس از خروج Outlook به Runner امضاشده تحویل می‌شود.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب فقط برای حساب Windows شما انجام می‌شود و به دسترسی Administrator نیاز ندارد.</p>

  <p><strong>فایل‌های انتشار:</strong> <strong>EmailTools_Setup.rar</strong> بسته پیشنهادی نصب دستی است؛ <strong>EmailTools_Setup.exe</strong> توسط به‌روزرسان داخلی نیز استفاده می‌شود؛ <strong>version.json</strong> اطلاعات به‌روزرسان است و نیازی به دانلود دستی ندارد.</p>

  <p><strong>پیش‌نیازها:</strong> Windows 10 یا Windows 11 - نسخه دسکتاپ Microsoft Outlook 2016، 2019، 2021 یا Microsoft 365 - ‎.NET Framework 4.8.</p>
</div>
