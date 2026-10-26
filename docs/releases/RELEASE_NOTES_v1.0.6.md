<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.6

This release completes the legacy-PST recovery and shutdown-cleanup work introduced in v1.0.5, improves reliability on older and multi-account Outlook profiles, and fixes a rare stale-result case in Advanced Search.

> This is an older release. Install the [latest version](https://github.com/ParhamGhafouri/EmailTools/releases/latest) for current fixes and safety improvements.

### Highlights (Ordered by Priority)

1. Legacy PST files located directly under the configured archive root are now discovered and processed one at a time. Managed seasonal destinations and PST files already owned by the verified cleanup queue remain protected from accidental remounting or migration.
2. Recovery is handled per PST instead of as one all-or-nothing batch. An empty, verified source can continue to detach and deletion while another PST is still draining, temporarily unreadable, locked, or waiting for re-verification.
3. Multi-account Outlook profiles can resolve a legacy PST's owning mailbox from Outlook account and message evidence instead of relying only on the containing folder name or a `.account` marker. The addon does not silently choose a random or default account when the evidence is ambiguous.
4. Exact-zero verification preserves the existing guarded state transitions while avoiding redundant empty-folder and zero-row work. This prevents long pauses and repeated `source rows hard-deleted 0/0` or Smart Archive restart loops on already-empty PST files.
5. Close-time cleanup now processes every verified PST record independently. One unresolved file cannot prevent other eligible files from being deleted, and valid records are retried while Outlook remains closed.
6. Stale, changed, or incomplete cleanup records no longer remain permanently trapped outside Outlook. Records that cannot safely use their previous proof are returned to the re-verification path instead of being reported as successful or ignored forever.
7. Outlook profile cleanup now supports older and alternate PST registrations, including Unicode and ANSI PST paths, EntryID-embedded paths, message-service and provider references, orphaned profile sections, and the global AutoArchive path properties `001f0324`, `001e0324`, `001f032c`, and `001e032c`. Only references that match the exact retiring PST path are removed.
8. Read-only legacy PST files are normalized before deletion, while managed archive destinations, mismatched file identities, surviving Outlook references, and reopened Outlook sessions continue to fail closed.
9. Advanced Search now removes a successfully cleared item immediately from the **Flagged Mail** result set. A delayed Exchange/MAPI property refresh can no longer restore the stale red flag in the cached row; the last result and multi-selection cases are also handled correctly.
10. GAL synchronization, body indexing, Smart Archive movement, staged-update verification, and the signed shutdown workers remain isolated in their existing coordinated work lanes.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users should install v1.0.6 over the current version without uninstalling first.

**Release assets:** **EmailTools_Setup.rar** is the recommended manual package; 
**EmailTools_Setup.exe** is also used by the in-app updater; 
**version.json** is the updater manifest and does not need to be downloaded manually.

**Requirements:** Windows 10 or Windows 11 - Microsoft Outlook 2016, 2019, 2021, or Microsoft 365 desktop - .NET Framework 4.8.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه کار بازیابی و پاک‌سازی PSTهای قدیمی پس از خروج Outlook را که در نسخهٔ 1.0.5 آغاز شده بود کامل می‌کند، پایداری را در Profileهای قدیمی و چندحسابی Outlook افزایش می‌دهد و یک حالت نادر باقی‌ماندن نتیجهٔ قدیمی در Advanced Search را اصلاح می‌کند.</p>

  <blockquote>این نسخه قدیمی است. برای دریافت اصلاحات و بهبودهای ایمنی فعلی، <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest">جدیدترین نسخه</a> را نصب کنید.</blockquote>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li>PSTهای قدیمی که مستقیماً داخل مسیر اصلی آرشیو تنظیم‌شده قرار دارند اکنون یکی‌یکی شناسایی و پردازش می‌شوند. مقصدهای فصلی مدیریت‌شده و PSTهایی که قبلاً در صف پاک‌سازی تأییدشده قرار گرفته‌اند از Mount یا انتقال اشتباه محافظت می‌شوند.</li>
    <li>بازیابی برای هر PST به‌صورت مستقل انجام می‌شود و دیگر یک Batch سراسری همه‌چیز را متوقف نمی‌کند. یک منبع خالی و تأییدشده می‌تواند به جداسازی و حذف ادامه دهد، حتی اگر PST دیگری هنوز در حال تخلیه، موقتاً غیرقابل‌خواندن، قفل‌شده یا منتظر Re-verification باشد.</li>
    <li>در Profileهای دارای چند حساب، مالک PST قدیمی می‌تواند با استفاده از اطلاعات واقعی Account و پیام‌های Outlook تشخیص داده شود و وابستگی فقط به نام پوشه یا فایل <code>.account</code> نیست. اگر شواهد مبهم باشد، افزونه هیچ Account پیش‌فرض یا تصادفی را انتخاب نمی‌کند.</li>
    <li>تأیید صفر دقیق، همان انتقال‌های حالت محافظت‌شدهٔ قبلی را حفظ می‌کند اما کار تکراری روی پوشه‌های خالی و Rowهای صفر را انجام نمی‌دهد. در نتیجه توقف طولانی، وضعیت تکراری <code>source rows hard-deleted 0/0</code> و حلقهٔ شروع مجدد Smart Archive برای PST خالی برطرف می‌شود.</li>
    <li>پاک‌سازی زمان خروج همهٔ Recordهای PST تأییدشده را مستقل از یکدیگر پردازش می‌کند. یک فایل حل‌نشده دیگر مانع حذف فایل‌های آمادهٔ دیگر نمی‌شود و Recordهای معتبر تا زمانی که Outlook بسته است دوباره تلاش می‌شوند.</li>
    <li>Recordهای قدیمی، تغییرکرده یا ناقص دیگر برای همیشه بیرون Outlook گیر نمی‌کنند. اگر Proof قبلی دیگر با ایمنی قابل استفاده نباشد، همان PST به مسیر Re-verification برگردانده می‌شود و به‌اشتباه موفق یا نادیده گرفته نمی‌شود.</li>
    <li>پاک‌سازی Profile در Outlook اکنون ثبت‌های قدیمی و متفاوت PST را نیز پشتیبانی می‌کند؛ از جمله مسیرهای Unicode و ANSI، مسیرهای داخل EntryID، Service و Provider، Sectionهای orphan و Propertyهای سراسری AutoArchive با نام‌های <code>001f0324</code>، <code>001e0324</code>، <code>001f032c</code> و <code>001e032c</code>. فقط Referenceهایی حذف می‌شوند که دقیقاً با مسیر PST در حال حذف مطابقت دارند.</li>
    <li>ویژگی Read-only فایل PST قدیمی قبل از حذف اصلاح می‌شود، اما مقصدهای آرشیو مدیریت‌شده، Identity نامنطبق، Reference باقی‌مانده در Outlook و بازشدن دوبارهٔ Outlook همچنان به‌صورت Fail-closed مانع حذف ناامن می‌شوند.</li>
    <li>در Advanced Search، پس از موفقیت دستور Clear Flag، پیام بلافاصله از نتیجه‌های <strong>Flagged Mail</strong> حذف می‌شود. تأخیر Exchange/MAPI در به‌روزرسانی Property دیگر نمی‌تواند پرچم قرمز قدیمی را در Row ذخیره‌شده بازگرداند و حالت آخرین نتیجه و انتخاب چندتایی نیز درست مدیریت می‌شود.</li>
    <li>همگام‌سازی GAL، ایندکس متن، انتقال Smart Archive، تأیید Update آماده‌شده و Workerهای امضاشدهٔ زمان خروج در همان مسیرهای هماهنگ و جدا از یکدیگر باقی مانده‌اند.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب فقط برای حساب Windows شما انجام می‌شود و به دسترسی Administrator نیاز ندارد. کاربران نسخه‌های قبلی باید 1.0.6 را بدون Uninstall روی نسخهٔ فعلی نصب کنند.</p>

  <p><strong>فایل‌های انتشار:</strong> 
<strong>EmailTools_Setup.rar</strong> بستهٔ پیشنهادی نصب دستی است؛ 
<strong>EmailTools_Setup.exe</strong> توسط به‌روزرسان داخلی نیز استفاده می‌شود؛ 
<strong>version.json</strong> اطلاعات به‌روزرسان است و نیازی به دانلود دستی ندارد.</p>

  <p><strong>پیش‌نیازها:</strong> Windows 10 یا Windows 11 - نسخهٔ دسکتاپ Microsoft Outlook 2016، 2019، 2021 یا Microsoft 365 - ‎.NET Framework 4.8.</p>
</div>
