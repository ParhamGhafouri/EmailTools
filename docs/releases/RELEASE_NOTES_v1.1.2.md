<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.2

This major update brings comprehensive stability, search accuracy, and performance optimizations across the entire Email Tools suite—delivering unified attachment search, eliminating indexing bottlenecks, resolving endless archiving loops, and hardening COM memory management and legacy storage cleanup.

### Highlights (Ordered by Priority)

1. **Attachment Search & Database Join Unification:** Resolved a critical discrepancy where historical attachment entries were keyed by MAPI StoreID rather than the store path. Search queries now join transparently across both identifiers, accompanied by an automatic startup self-healing database migration that normalizes and deduplicates all existing attachment records.
2. **Folder-Level Attachment Filtering:** Fixed MAPI fallback search so that filtering by attachment filename (e.g., `*.pdf`, `invoice`, `*.xlsx`) is fully enforced even when searching within the "Current Folder" scope.
3. **Smart Archive Ladder Acceleration & Oldest-First Prioritization:** Resolved an issue where mailboxes with large volumes of newer mail caused Smart Archive to repeatedly scan without finding eligible items. The engine now dynamically measures the oldest observed mail age (`_oldestObservedMailboxAgeDays`) to skip empty date brackets, sorts MAPI folder tables oldest-first under emergency pressure, and enforces a 2-hour safety floor cooldown.
4. **High-Speed Batched Attachment Indexing:** Completely redesigned attachment indexing from slow single-item commits to high-throughput batch operations (`UpsertAttachmentsBatch`) and a 50-item backfill buffer (`StepAttachmentBackfill`). Attachment indexing for large mailboxes (40k+ emails) now finishes in minutes rather than hours.
5. **Outlook UI Responsiveness & Anti-Stutter Balancing:** Relaxed background indexing worker timers from 5ms/10ms to balanced 35ms/45ms/60ms intervals and deferred the warm maintenance timer to 5 minutes, completely freeing the Outlook UI message loop and eliminating typing lag.
6. **Guaranteed Legacy PST Deletion via Reboot Delay Fallback:** Upgraded `EmailTools.UpdateRunner.exe` with `MoveFileEx` (`MOVEFILE_DELAY_UNTIL_REBOOT`). If open file handles from Outlook or external search services prevent immediate physical deletion of a drained legacy PST, the system automatically registers the file for guaranteed kernel-level deletion upon the next system restart.
7. **COM RCW Hygiene in Reminder Dismisser:** Wrapped calendar reminder items and associated appointment COM wrappers in explicit `try/finally` blocks with `Marshal.ReleaseComObject`, preventing lingering calendar locks in long-running Outlook sessions.
8. **Inline Signature Image Filtering:** Filtered out inline images (`image001.png`, etc.) during attachment extraction, preventing email signature logos from bloating the attachment search index.
9. **Culture-Invariant Date Parsing:** Enhanced search criteria deserialization with `CultureInfo.InvariantCulture`, preventing parsing errors on Windows systems configured with non-Gregorian (e.g. Solar Hijri) calendars.
10. **Authenticode Code Signing & Defender Clean:** Signed with the official developer certificate (`42536C317058B3308A75D89E19F849B0B08BD39A`) and verified 100% clean in Windows Defender.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.1.2 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این به‌روزرسانی جامع شامل ارتقای اساسی در دقت جستجو، رفع گلوگاه‌های عملکردی، پایداری آرشیو خودکار و مدیریت بهینه حافظه در سراسر افزونه ابزارهای ایمیل است.</p>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>دقت ۱۰۰٪ در جستجوی فایل‌های پیوست و یکپارچه‌سازی پایگاه‌داده:</strong> رفع قطعی عدم تطابق کلید ذخیره‌سازی در جدول پیوست‌ها و پیاده‌سازی مایگریشن خودکار خودترمیمی (Self-Healing) در ابتدای اجرای افزونه جهت اصلاح و یکپارچه‌سازی تمامی سوابق پیوست‌های قبلی و حذف رکوردهای تکراری.</li>
    <li><strong>اعمال فیلتر نام فایل پیوست در جستجوی پوشه جاری:</strong> رفع نقص موجود در اسکن پوشه‌ای MAPI به‌گونه‌ای که فیلتر نام یا پسوند فایل پیوست (مانند <code>*.pdf</code> یا <code>*.xlsx</code>) حتی در حالت جستجو در «پوشه جاری» (Current Folder) نیز با دقت اعمال می‌شود.</li>
    <li><strong>شتاب‌بخشی هوشمند به چرخه آرشیو و اولویت‌بندی از قدیمی‌ترین ایمیل:</strong> رفع مشکل جستجوی مکرر و بی‌نتیجه در صندوق‌های دارای ایمیل‌های جدید از طریق پایش پویای سن قدیمی‌ترین ایمیل (<code>_oldestObservedMailboxAgeDays</code>)، جهش هوشمند از بازه‌های زمانی خالی، مرتب‌سازی جداول پوشه‌ها از قدیمی‌ترین تاریخ (Oldest-First) و فعال‌سازی وقفه ایمن ۲ ساعته جهت جلوگیری از درگیری مداوم پردازنده.</li>
    <li><strong>نمایه‌سازی دسته‌ای و فوق‌سریع فایل‌های پیوست:</strong> بازنویسی کامل ایندکس فایل‌های پیوست به تراکنش‌های دسته‌ای (<code>UpsertAttachmentsBatch</code>) همراه با پایپ‌لاین پشتیبان ۵۰تایی (<code>StepAttachmentBackfill</code>) که زمان ایندکس پیوست‌ها در صندوق‌های بزرگ (بیش از ۴۰ هزار ایمیل) را از چندین ساعت به چند دقیقه کاهش داده است.</li>
    <li><strong>حذف کامل لگ و روانی ۱۰۰٪ رابط کاربری اوت‌لوک:</strong> تنظیم و متعادل‌سازی تایمرهای پس‌زمینه ایندکس روی فواصل ۳۵/۴۵/۶۰ میلی‌ثانیه و ارتقای تایمر بررسی دوره‌ای به ۵ دقیقه، که از قفل شدن نخ رابط کاربری (UI Thread) اوت‌لوک و کندی تایپ یا اسکرول کاملاً جلوگیری می‌کند.</li>
    <li><strong>تضمین حذف فیزیکی PSTهای قدیمی تخلیه‌شده:</strong> ارتقای دستیار خروج <code>EmailTools.UpdateRunner.exe</code> به قابلیت <code>MoveFileEx</code> با پرچم تأخیر تا ری‌استارت ویندوز (<code>MOVEFILE_DELAY_UNTIL_REBOOT</code>). در صورت وجود هندل‌های باز مانع حذف، فایل به صورت قطعی در راه‌اندازی بعدی سیستم در سطح کرنل ویندوز پاک خواهد شد.</li>
    <li><strong>مدیریت بهینه اشیای COM در دستیار یادآورها (Reminders):</strong> آزادسازی قطعی اشیای COM رویدادها و قرارهای تقویم با استفاده از <code>Marshal.ReleaseComObject</code> در بلوک‌های <code>finally</code> جهت جلوگیری از انباشت اشیای باز در حافظه در نشست‌های طولانی‌مدت اوت‌لوک.</li>
    <li><strong>فیلتر خودکار تصاویر امضای ایمیل:</strong> جلوگیری از ثبت تصاویر درون‌متنی امضاها (مانند <code>image001.png</code>) در جدول فایل‌های پیوست، جهت کاهش حجم دیتابیس و جلوگیری از نتایج نامربوط.</li>
    <li><strong>سازگاری با تقویم‌های محلی و سیستم‌های فارسی:</strong> تجزیه مقاوم تاریخ‌ها با استفاده از <code>CultureInfo.InvariantCulture</code> جهت جلوگیری از بروز خطای بازخوانی بازه‌های زمانی در سیستم‌هایی که تقویم پیش‌فرض ویندوز روی هجری شمسی تنظیم شده است.</li>
    <li><strong>امضای دیجیتال رسمی و سازگاری کامل با آنتی‌ویروس:</strong> دارای امضای رسمی Authenticode با شناسه گواهی معتبر <code>42536C317058B3308A75D89E19F849B0B08BD39A</code> و بررسی کاملاً پاک و بدون خطا در Windows Defender.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و اکسترکت کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.2 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>
