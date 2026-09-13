<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.4

Version 1.1.4 delivers lightning-fast **sub-50ms Advanced Search** across indexed mailboxes, an upgrade to **Microsoft.Data.Sqlite 10.0.12** and native **SQLite 3.53.4**, full **High-DPI & multi-monitor responsive layout** across Advanced Search and Task Tracker, rock-solid **Outlook startup resiliency** eliminating splash screen freezes, and **graceful legacy archive rule cleanup**.

### Highlights (Ordered by Priority)

1. **Sub-50ms Advanced Search & MAPI Crawl Elimination:**
   - **Eliminated 10–15s Search Delay:** Fixed a critical issue where searching by field (e.g. `From:`, `Subject:`, `To:`) erroneously aborted the instant SQLite metadata query and fell back to recursive live MAPI folder crawling (`StartPreparedTimerScan`). Field searches across all mailboxes now execute directly against SQLite `mail_meta` in under 50ms.
   - **Proactive Index Priming:** Automatically initializes and opens the SQLite index (`OpenForSearch()`) the moment the Advanced Search window appears, guaranteeing instant results on the first keystroke with zero warmup latency.

2. **SQLite Database Engine Upgrade (`Microsoft.Data.Sqlite.Core 10.0.12`):**
   - **Modern Data Provider:** Upgraded from `Microsoft.Data.Sqlite.Core 10.0.11` to `10.0.12` alongside `SQLitePCLRaw 3.0.5` bundles.
   - **Latest Native C Engine:** Integrated `SourceGear.sqlite3 3.53.4` for both 32-bit (`x86`) and 64-bit (`x64`) architectures.
   - **High-Concurrency WAL & Timeout Resilience:** Hardened Write-Ahead Logging (WAL) concurrency and multi-threaded read/write balancing between background body indexing and user searches, with an increased 30-second query timeout floor to eliminate busy locks under heavy I/O.

3. **High-DPI & Multi-Monitor Responsive UI Layout:**
   - **Advanced Search Panel (`MailSearchPanel`):** Implemented a responsive 60/40 splitter allocation with DPI-scaled minimum pane boundaries (`380px` / `250px`). Set the `Subject` column to automatic `Fill` (`minWidth = 160px`) and dynamically scaled all column widths with `D(...)`.
   - **Compacted Action Toolbar:** Streamlined second-row controls (Save, Delete, Export, Reset, Saved dropdown) from ~637px down to ~417px (saving >220px), ensuring the "Export" button is never clipped or pushed off-screen on 1080p laptops running at 125% or 150% display scaling.
   - **Task Tracker Form (`TaskTrackerForm`):** Added comprehensive DPI scaling (`DeviceDpi / 96f`) across toolbar height (`38px`), action buttons, search field (`240px`), and grid columns with minimum widths and `Fill` subject column.
   - **Themed Dialogs (`ThemedDialog`):** Corrected title bar docking and z-order (`closeBtn.BringToFront()`) so header title hosts never obscure or capture clicks on the Close button. Enabled `StringTrimming.EllipsisCharacter` to prevent clipped title text on non-standard DPI scales.

4. **Outlook Startup & Splash Screen Resiliency (Zero Freezes on "Loading Profile..."):**
   - **Splash Screen Window Detection:** Added Win32 `IsWindowVisible` verification in `DeferredInit`. If the main Outlook Explorer window is not yet visible, initialization gracefully defers by 1,000ms, preventing hangs while the splash screen is displayed.
   - **Decoupled Exchange Account Discovery:** Separated registry resiliency (<1ms pure registry check with zero MAPI calls) from Exchange account auto-discovery (`EnsureAutoDiscoverResiliency()`), moving account inspection to a 12-second delayed background coordinator timer after Outlook has fully launched.
   - **Safe Archive Mount Delay:** Increased early seasonal archive mount timer from 100ms to 4,000ms with active window visibility guards to prevent COM contention during profile loading.

5. **Legacy PST Drain & Outlook Rules Resiliency:**
   - **Zero-Item PST Rule Verification Fix:** Resolved an infinite 15-minute retry loop that could occur during Smart Archive legacy PST drain when encountering broken, deleted, or orphaned Outlook rule target folders.
   - **Safe COM Exception Handling:** Wrapped rule target folder resolution in defensive exception guards, recognizing inaccessible folders as non-matching targets and allowing drained PSTs to safely close and retire without halting archiving.

6. **Authenticode Code Signing & Production Verification:**
   - Binaries, obfuscated DLLs, and helper scripts are signed with the official Authenticode certificate (`42536C317058B3308A75D89E19F849B0B08BD39A`).
   - Verified 100% clean in Windows Defender and passes all 7 automated contract test suites.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.1.4 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۱.۴ شامل ارتقای چشمگیر سرعت <strong>جست‌وجوی پیشرفته به کمتر از ۵۰ میلی‌ثانیه</strong>، به‌روزرسانی پایگاه‌داده به <strong>Microsoft.Data.Sqlite 10.0.12</strong> و موتور بومی <strong>SQLite 3.53.4</strong>، سازگاری کامل رابط کاربری با <strong>نمایشگرهای High-DPI و بزرگ‌نمایی چندگانه</strong> در جست‌وجو و ردیاب وظایف، <strong>رفع کامل توقف و فریز در صفحه لودینگ اوت‌لوک</strong>، و <strong>پایداری کامل فرآیند تخلیه آرشیوهای فصلی قدیمی</strong> است.</p>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>جست‌وجوی پیشرفته زیر ۵۰ میلی‌ثانیه و حذف اسکن زنده MAPI:</strong>
      <ul>
        <li><strong>حذف تأخیر ۱۰ تا ۱۵ ثانیه‌ای:</strong> رفع خطایی که در آن جست‌وجو بر اساس فیلدهای خاص (مانند فرستنده، موضوع یا گیرنده) به اشتباه کوئری مستقیم SQLite را لغو کرده و به اسکن بازگشتی و سنگین پوشه‌های اوت‌لوک (MAPI) برمی‌گشت. اکنون جست‌وجو در تمام صندوق‌ها مستقیماً در دیتابیس لوکال و در کسری از ثانیه اجرا می‌شود.</li>
        <li><strong>آماده‌سازی پیش‌دستانه ایندکس (Warmup):</strong> بازگشایی و آماده‌سازی خودکار ایندکس دیتابیس (<code>OpenForSearch</code>) هم‌زمان با باز شدن پنجره جست‌وجو، جهت ارائه نتایج فوری با فشردن نخستین کلید بدون کوچک‌ترین مکث.</li>
      </ul>
    </li>
    <li><strong>به‌روزرسانی موتور پایگاه‌داده (Microsoft.Data.Sqlite.Core 10.0.12):</strong>
      <ul>
        <li><strong>کتابخانه ارتباطی مدرن:</strong> ارتقا به نسخه <code>Microsoft.Data.Sqlite.Core 10.0.12</code> (از نسخه 10.0.11) همراه با بسته‌های <code>SQLitePCLRaw 3.0.5</code>.</li>
        <li><strong>موتور بومی جدید SQLite:</strong> ادغام آخرین نگارش موتور C به نسخه <code>SourceGear.sqlite3 3.53.4</code> برای هر دو معماری ۳۲ بیتی (x86) و ۶۴ بیتی (x64).</li>
        <li><strong>همزمانی بالا در حالت WAL و تاب‌آوری کوئری‌ها:</strong> تقویت پایداری خواندن و نوشتن همزمان میان ایندکس‌گذاری پس‌زمینه و جست‌وجوی کاربر، همراه با ارتقای تایم‌اوت به ۳۰ ثانیه جهت جلوگیری از قفل‌های موقت در فشارهای سنگین دیسک.</li>
      </ul>
    </li>
    <li><strong>طراحی واکنش‌گرا و سازگاری کامل با نمایشگرهای High-DPI و لپ‌تاپ‌ها:</strong>
      <ul>
        <li><strong>پنل جست‌وجوی پیشرفته (MailSearchPanel):</strong> بازطراحی تقسیم‌بندی به نسبت منعطف ۶۰ به ۴۰ با حداقل ابعاد متناسب با بزرگ‌نمایی DPI، پر شدن خودکار فضای خالی توسط ستون موضوع (<code>Fill</code>) و مقیاس‌بندی دقیق تمام ستون‌ها.</li>
        <li><strong>فشرده‌سازی نوار ابزار عملیات:</strong> کاهش عرض دکمه‌های ردیف دوم (ذخیره، حذف، خروجی اکسل، بازنشانی و جست‌وجوهای ذخیره‌شده) از ۶۳۷ به ۴۱۷ پیکسل (بیش از ۲۲۰ پیکسل صرفه‌جویی)، که از بیرون افتادن دکمه خروجی (Export) در لپ‌تاپ‌های دارای مقیاس ۱۲۵٪ و ۱۵۰٪ کاملاً جلوگیری می‌کند.</li>
        <li><strong>فرم ردیاب وظایف (TaskTrackerForm):</strong> اعمال مقیاس‌بندی کامل DPI برای نوار ابزار بالا، دکمه‌های عملیاتی، کادر جست‌وجو و ستون‌های جدول همراه با نسبت ۶۰/۴۰ واکنش‌گرا.</li>
        <li><strong>پنجره‌های اعلان و پیام‌ها (ThemedDialog):</strong> اصلاح ترتیب لایه‌ها و داکینگ هدر تا پنل عنوان مانع کلیک روی دکمه بستن (Close) نشود، همراه با فعال‌سازی سه‌نقطه در انتهای متن‌های طولانی عنوان.</li>
      </ul>
    </li>
    <li><strong>پایداری اجرای اوت‌لوک و رفع هنگ در صفحه اسپلش ("Loading Profile..."):</strong>
      <ul>
        <li><strong>تشخیص پنجره فعال اوت‌لوک:</strong> اعتبارسنجی نمایش قطعی پنجره اکسپلورر با توابع Win32 پیش از راه‌اندازی افزونه؛ در صورت فعال بودن صفحه Splash، اجرای اولیه ۱۰۰۰ میلی‌ثانیه به تعویق می‌افتد تا اوت‌لوک کاملاً بالا بیاید.</li>
        <li><strong>تفکیک فرآیند بررسی حساب‌های کاربری:</strong> جداسازی کدهای رجیستری (زیر ۱ میلی‌ثانیه و بدون فراخوانی MAPI) از بررسی حساب‌های کاربری Exchange، و انتقال آن به تایمر پس‌زمینه ۱۲ ثانیه پس از لود کامل اوت‌لوک.</li>
        <li><strong>تأخیر ایمن در اتصال آرشیوها:</strong> افزایش تایمر اتصال زودهنگام فایل‌های آرشیو به ۴ ثانیه جهت جلوگیری از تداخل پردازش‌های اولیه.</li>
      </ul>
    </li>
    <li><strong>پایداری فرآیند تخلیه PSTهای قدیمی و بررسی قوانین (Rules):</strong>
      <ul>
        <li><strong>رفع حلقه تکرار ۱۵ دقیقه‌ای:</strong> حل مشکل توقف آرشیو خودکار در صورت وجود قوانین قدیمی اوت‌لوک با پوشه‌های مقصد حذف‌شده یا نامعتبر.</li>
        <li><strong>مدیریت خطاهای COM:</strong> هدایت امن استثناهای ناشی از دسترسی به پوشه‌های نامعتبر، تشخیص عدم وابستگی آن‌ها به فایل PST، و امکان بستن و بایگانی امن فایل‌های خالی‌شده بدون توقف فرآیند آرشیو.</li>
      </ul>
    </li>
    <li><strong>امضای دیجیتال رسمی Authenticode و تأییدیه امنیتی:</strong>
      <ul>
        <li>امضای معتبر کلیه باینری‌ها، ماژول‌ها و نصاب با گواهی رسمی توسعه‌دهنده (شناسه <code>42536C317058B3308A75D89E19F849B0B08BD39A</code>) و قبولی ۱۰۰٪ در آزمون‌های ویندوز دیفندر و تست‌های اعتبارسنجی.</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و اکسترکت کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.4 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>