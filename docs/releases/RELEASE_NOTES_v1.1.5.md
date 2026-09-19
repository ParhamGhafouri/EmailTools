<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.5

Version 1.1.5 delivers **seamless Deleted Items native Recovery banner compatibility**, a revamped **Fluent 2 Status & Indexing Dashboard** with live items counts, active folder progress, and queue metrics, an **ultra-fast 1-column Reconcile engine** eliminating post-indexing write storms and I/O bloat, and **multi-conditional search acceleration** with zero hiccups or query drops.

### Highlights (Ordered by Priority)

1. **Deleted Items & Native Exchange Recovery Banner Protection:**
   - **Native Recovery Infobar Restored:** Fixed an issue where the embedded message list search band physically overlapped and obscured Outlook's native recovery notification bar (*"Recover items recently removed from this folder"*).
   - **Multi-Language Awareness:** Added comprehensive detection for Deleted Items across 10+ languages (English, Persian, German, French, Spanish, Italian, Dutch, Polish, Russian, Arabic) via folder path, MAPI `CompareEntryIDs`, parent hierarchy, and native window text scanning.
   - **Automatic Band Suppression & Grid Realignment:** The embedded search band automatically hides when navigating to Deleted Items or when native recovery banners are detected, restoring the message list grid flush against the folder header so deleted items can be restored without obstruction.

2. **Revamped Windows 11 Fluent 2 Visual Status Dashboard:**
   - **Two-Tier Real-Time Metrics:** Upgraded the Search Index & Engine card in the Status window (`ThemedStatusForm`) to display live two-tier metrics instead of generic status text:
     - **Primary Metric:** Shows exact progress (`12,450 of 15,200 indexed (82%)` or `15,200 indexed • Up to date`).
     - **Live Sub-Details:** Displays the active folder being scanned (`Folder: Inbox (120 of 300)`), writer queue depth (`Queue: 140`), and precise pause reasons (`Paused: Outlook is in use (resumes in 2.5s)`).
   - **Fluent Colored Badge Pills:** Real-time visual status pills with theme-adaptive styling: Green (`Ready`), Orange (`Indexing`), Blue (`Paused`), and Gray (`Unavailable`).

3. **High-Speed 1-Column Reconcile Engine (Zero Write Storms):**
   - **Optimized Reconcile Pass:** In `BodyIndexBuilder.StepReconcile`, once store metadata is already prepared, the background pass opens the MAPI table requesting only **1 column** (`PR_ENTRYID`) instead of querying all 13 metadata properties.
   - **Eliminated Write Storms & High Disk I/O:** Compares entry IDs directly against SQLite `mail_meta` without allocating tens of thousands of duplicate metadata objects. Missing and purged items are removed directly via indexed lookups, completely skipping expensive full FTS scans.
   - **Non-Blocking Checkpoints:** Replaced runtime `wal_checkpoint(TRUNCATE)` calls with non-blocking `PASSIVE` checkpoints, preventing database lockouts and disk spikes while indexing completes.

4. **Multi-Conditional Search Acceleration & Hiccup Elimination:**
   - **Fixed 100,000 Cap Escalation Bug:** Resolved an issue where combining header filters (`From:`, `Subject:`, `To:`, exclusions) escalated the internal query limit to 100,000 rows, causing SQLite to omit its `ORDER BY` clause and overloading memory with unsorted records. Queries now execute with strict bounding to `planCap` directly inside SQLite in under 50ms.
   - **Fixed Attachment-Only & Time-Only Queries:** Resolved a condition where searches specifying only attachment names or specific hour ranges were mistakenly dismissed as empty forms.
   - **Eliminated Search Interruption Loops:** `RefreshBodySearchAfterIndexCommit` no longer restarts or aborts in-flight searches when background indexing commits new revisions, and never interrupts the user while inspecting the results grid or reading pane.
   - **Universal Inactivity Watchdog:** Extended the 30-second watchdog timer to cover all search criteria (not just body text), guaranteeing the search UI never gets indefinitely stuck on *"Searching..."*.
   - **Smooth UI Interaction:** Debounced grid row selection (`CellClick`) to eliminate synchronous COM reading pane stutter, and added Enter key handling to Exclude text boxes for immediate execution.
   - **Database Index Optimization:** Added composite SQLite indexes on `(storekey, folderid, received_ticks)`, unread status, attachments, and flagged items, while setting `wal_autocheckpoint=1000` to prevent WAL file bloat.

5. **Production Build & Authenticode Verification:**
   - Binaries and installer packages are fully obfuscated (`ConfuserEx strong` preset) and Authenticode signed with developer certificate (`42536C317058B3308A75D89E19F849B0B08BD39A`).
   - Verified 100% clean in Windows Defender and passes all production contract test suites.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.1.5 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۱.۵ شامل <strong>سازگاری کامل با بنر بازیابی آیتم‌های حذف‌شده (Recover Items) در اوت‌لوک</strong>، ارتقای چشمگیر <strong>داشبورد وضعیت و نمایش زنده جزئیات ایندکس‌گذاری</strong>، موتور بهینه‌سازی‌شده <strong>همگام‌سازی تک‌ستونه (Reconcile) جهت حذف فشار دیسک و پردازش‌های سنگین پس از ایندکس</strong>، و <strong>شتاب‌بخشی به جست‌وجوهای چندشرطی و رفع هرگونه مکث یا توقف</strong> است.</p>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>پوشش و سازگاری کامل با بخش پیام‌های حذف‌شده (Deleted Items) و لینک بازیابی:</strong>
      <ul>
        <li><strong>نمایش کامل بنر بومی بازیابی:</strong> رفع مشکلی که در آن نوار جست‌وجوی تعبیه‌شده در بالای لیست پیام‌ها، روی بنر رسمی اوت‌لوک (<em>"Recover items recently removed from this folder"</em> یا <em>"بازیابی موارد اخیراً حذف شده از این پوشه"</em>) قرار می‌گرفت و مانع از دیده شدن یا کلیک روی آن می‌شد.</li>
        <li><strong>پشتیبانی از بیش از ۱۰ زبان مختلف:</strong> تشخیص دقیق پوشه Deleted Items و معادل‌های آن در زبان‌های مختلف (انگلیسی، فارسی، آلمانی، فرانسوی، اسپانیایی، ایتالیایی، هلندی، لهستانی، روسی و عربی) از طریق مسیر پوشه، توابع MAPI و بررسی متن پنجره‌های سیستمی.</li>
        <li><strong>تنظیم خودکار موقعیت جدول:</strong> نوار جست‌وجو در این پوشه به‌صورت خودکار مخفی شده و بالای جدول پیام‌ها دقیقاً زیر نوار ابزار اصلی قرار می‌گیرد تا بنر بازیابی بدون کوچک‌ترین تداخل در دسترس باشد.</li>
      </ul>
    </li>
    <li><strong>داشبورد نوین وضعیت و ایندکس‌گذاری (Windows 11 Fluent 2):</strong>
      <ul>
        <li><strong>نمایش دوسطحی و زنده وضعیت:</strong> کارت ایندکس و موتور جست‌وجو در پنجره وضعیت افزونه (ThemedStatusForm) ارتقا یافته و اکنون آمار دقیق را در دو سطح ارائه می‌دهد:
          <ul>
            <li><strong>آمار اصلی:</strong> نمایش دقیق تعداد ایمیل‌های ایندکس‌شده نسبت به کل صندوق (مانند <code>12,450 of 15,200 indexed</code> همراه با درصد پیشرفت یا <code>All stores synchronized • Up to date</code>).</li>
            <li><strong>جزئیات زنده و پویا:</strong> نمایش نام پوشه در حال پردازش (مانند <code>Folder: Inbox (120 of 300)</code>)، حجم صف نویسنده (<code>Queue: 140</code>) و علت دقیق مکث ایندکس (مانند <code>Paused: Outlook is in use (resumes in 2.5s)</code>).</li>
          </ul>
        </li>
        <li><strong>نشان‌های رنگی هوشمند (Badge Pills):</strong> نمایش وضعیت ایندکس با کپسول‌های رنگی استاندارد فلوئنت شامل سبز (<code>Ready</code>)، نارنجی (<code>Indexing</code>)، آبی (<code>Paused</code>) و خاکستری (<code>Unavailable</code>).</li>
      </ul>
    </li>
    <li><strong>موتور همگام‌سازی تک‌ستونه فوق‌سریع (حذف فشار دیسک و هارد پس از اتمام ایندکس):</strong>
      <ul>
        <li><strong>بهینه‌سازی فاز Reconcile:</strong> در مرحله بررسی و پاک‌سازی نهایی (StepReconcile)، در صورتی که متادیتای صندوق قبلاً آماده شده باشد، جدول پیام‌ها تنها با <strong>یک ستون (PR_ENTRYID)</strong> باز می‌شود و از بارگذاری غیرضروری ۱۳ ستون سنگین متادیتا جلوگیری می‌گردد.</li>
        <li><strong>حذف تخصیص‌های سنگین حافظه و نوشتن روی دیسک:</strong> مقایسه شناسه‌ها مستقیماً در حافظه با دیتابیس لوکال انجام شده و آیتم‌های حذف‌شده به‌صورت مستقیم از ایندکس پاک می‌شوند؛ بدون نیاز به اسکن مجدد کل دیتابیس FTS.</li>
        <li><strong>چک‌پوینت‌های غیرمسدودکننده:</strong> جایگزینی دستورات سنگین Truncate با چک‌پوینت‌های غیرمسدودکننده Passive در SQLite جهت پیشگیری از هرگونه قفل پایگاه‌داده یا درگیری دیسک.</li>
      </ul>
    </li>
    <li><strong>شتاب‌بخشی به جست‌وجوهای چندشرطی و رفع مکث‌های تصادفی:</strong>
      <ul>
        <li><strong>رفع باگ افزایش سقف جست‌وجو به ۱۰۰ هزار آیتم:</strong> رفع مشکلی که در آن ترکیب چند شرط (مانند فرستنده، موضوع و کلمات مستثنی‌شده) باعث افزایش سقف داخلی جست‌وجو به ۱۰۰،۰۰۰ و حذف مرتب‌سازی بر اساس تاریخ در دیتابیس می‌شد. اکنون نتایج مستقیماً در دیتابیس SQLite با سرعت زیر ۵۰ میلی‌ثانیه فیلتر و مرتب می‌شوند.</li>
        <li><strong>اصلاح جست‌وجوی تک‌فیلدی پیوست‌ها و ساعات خاص:</strong> رفع نقصی که جست‌وجو بر اساس نام پیوست یا بازه ساعتی را به اشتباه فرم خالی تشخیص می‌داد.</li>
        <li><strong>حذف حلقه‌های لغو جست‌وجو:</strong> فرآیند به‌روزرسانی نتایج پس از ایندکس دیگر جست‌وجوهای فعال در حال اجرا را لغو نمی‌کند و با فوکوس کاربر روی جدول نتایج تداخلی ایجاد نمی‌نماید.</li>
        <li><strong>واچ‌داگ سراسری عدم پاسخ‌دهی:</strong> تایمر محافظ ۳۰ ثانیه‌ای برای کلیه حالت‌های جست‌وجو فعال شد تا پنل جست‌وجو هیچ‌گاه در حالت Searching باقی نماند.</li>
        <li><strong>روان‌سازی کلیک و پیش‌نمایش ایمیل‌ها:</strong> ایجاد تأخیر کنترل‌شده (Debounce) در رویداد کلیک ماوس روی جدول جهت حذف فریز لحظه‌ای رابط کاربری هنگام خواندن پیش‌نمایش، و اتصال کلید اینتر به کادرهای کلمات مستثنی‌شده (Exclude).</li>
        <li><strong>ایندکس‌های ترکیبی دیتابیس:</strong> ایجاد ایندکس‌های تخصصی در SQLite برای وضعیت پرچم‌دار (Flagged)، خوانده‌نشده (Unread) و پیوست‌ها، همراه با تنظیم نقطه بازرسی لاگ WAL روی ۱۰۰۰ صفحه جهت جلوگیری از افزایش حجم فایل.</li>
      </ul>
    </li>
    <li><strong>بسته‌بندی رسمی، امضای دیجیتال Authenticode و اعتبارسنجی تولید:</strong>
      <ul>
        <li>کلیه فایل‌های اجرایی و افزونه با استفاده از ConfuserEx (پریست استاندارد strong) مبهم‌سازی شده و با گواهی رسمی توسعه‌دهنده (<code>42536C317058B3308A75D89E19F849B0B08BD39A</code>) امضا گردیده‌اند و دارای تأییدیه ۱۰۰٪ از ویندوز دیفندر می‌باشند.</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و اکسترکت کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.5 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>
