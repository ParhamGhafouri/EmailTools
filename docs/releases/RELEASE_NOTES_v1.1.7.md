<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.7

Version 1.1.7 focuses on **accurate body-search highlighting and match navigation**, **multi-word and Persian/Arabic body search**, **multi-monitor and high-DPI layout reliability for the message-list search bar**, **real-time live email indexing and Task Tracker monitoring**, and **updated SQLite runtime performance**.

> This is an older release. Install the [latest version](https://github.com/ParhamGhafouri/EmailTools/releases/latest) for current fixes and safety improvements.

### Highlights (Ordered by Priority)

1. **Advanced Search Body Highlighting, Match Navigation & Persian/Arabic Search:**
   - Fixed body-search highlighting in Conversation History and RTL/inline-styled HTML messages where matched text could become invisible against the highlight background.
   - Fixed the body match counter (`1/1`) and highlight refresh when editing the **Body** search filter while the same message remains selected in the preview pane.
   - Added multi-word token matching and automatic Persian/Arabic character normalization (`ی`/`ي`, `ک`/`ك`) across both indexed body searches and preview match highlighting.
   - Added **F3** (Next match) and **Shift+F3** (Previous match) keyboard shortcuts to step through highlighted body matches directly from Advanced Search, and removed unwanted focus-cue borders around the inline `<` / `>` match navigation and clear/exclude (`×` / `−`) field buttons.
   - Restored custom start/end times (`HH:mm`) when loading saved searches in a single pass, enforced inline negated terms (`-term` / `NOT term`) across indexed **From**, **To**, and **Cc** searches, and synchronized message flag changes directly with the local index so the **Flagged** filter reflects updates immediately.
   - Prevented duplicate style injection in messages containing nested HTML fragments, flattened deeply nested HTML wrapper chains (`<div>`/`<span>`/`<blockquote>`) to prevent `MSHTML.dll` stack overflows (`0xc00000fd`), eliminated script-engine initialization in the preview pane to prevent `jscript9.dll` fail-fast exceptions (`0xc0000602`) on hardened Windows 11 24H2 systems, and expanded the preview cache with most-recently-used retention and preserved header/attachment state.

2. **Message-List Search Bar, Multi-Monitor & High-DPI Reliability:**
   - Improved per-monitor DPI scaling and cross-monitor transitions for the integrated **Advanced Search (`Ctrl+F3`)** message-list bar and high-DPI vector icons across Advanced Search and Task Tracker.
   - Fixed multi-window Explorer switching so the previous Outlook window's message-list position is cleanly restored when moving between multiple open Outlook windows.
   - Hardened folder and view transitions so switching to non-mail views, mailbox root/home pages, or **Deleted Items** hides the search bar cleanly without layout gaps or flicker.
   - Scoped `Ctrl+F3` and `Ctrl+F4` shortcut handling strictly to the Outlook UI thread so global desktop typing is never affected.
   - Ensured **Reply with Attachment(s)** and **Forward without Attachment(s)** bring the newly opened compose window directly to the foreground.

3. **Live Email Arrival, Index Reconciliation & Task Tracker Monitoring:**
   - Recorded accurate modification timestamps during live email indexing (`NewMailEx`, `ItemAdd`, `ItemChange`), preserved seamless Exchange short-term to long-term EntryID reconciliation without duplicate rows, and matched both binary `PR_ENTRYID` and Outlook `EntryID` formats during folder deletion reconciliation.
   - Activated deferred background folder hooks for **Sent Items** and **Deleted Items** shortly after Outlook startup settles, ensuring sent-reply task completion and deleted-email cleanup work in real time even before the Task Tracker window is opened.
   - Added a direct **Run rules** action alongside **Preview matches** in the Task Tracker rule scan dialog while preserving the selected scope and day window, fixed single-click column sorting in the Task Tracker grid, and sanitized Task Tracker Excel (`.xls`) exports against XML control characters and formula prefixes.
   - Added automatic SQLite query-planner optimization (`PRAGMA optimize`) during idle index checkpoints and upgraded the embedded SQLite engine to **3.54.0** (`Microsoft.Data.Sqlite 10.0.13`).

4. **Installer & Runtime Verification:**
   - Strengthened Setup verification to validate installed runtime files and VSTO trust registration before reporting installation completion, and refined offline PST profile cleanup detection so background Windows `SearchIndexer` and Microsoft `Teams` processes do not falsely report Outlook as open.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.1.7 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۱.۷ بر <strong>اصلاح هایلایت و پیمایش نتایج جست‌وجوی متن پیام</strong>، <strong>پشتیبانی از جست‌وجوی چندکلمه‌ای و یکسان‌سازی حروف فارسی و عربی</strong>، <strong>پایداری نوار جست‌وجوی بالای فهرست ایمیل‌ها در چند مانیتور و DPIهای مختلف</strong>، <strong>ایندکس آنی ایمیل‌های جدید و ردیابی خودکار در Task Tracker</strong> و <strong>ارتقای موتور پایگاه‌داده SQLite</strong> تمرکز دارد.</p>

  <blockquote>این نسخه قدیمی است. برای دریافت اصلاحات و بهبودهای ایمنی فعلی، <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest">جدیدترین نسخه</a> را نصب کنید.</blockquote>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>اصلاح هایلایت متن، پیمایش نتایج و جست‌وجوی فارسی/عربی در Advanced Search:</strong>
      <ul>
        <li>رفع مشکل ناپدید شدن متن‌های هایلایت‌شده در پیام‌های Conversation History و ایمیل‌های راست‌به‌چپ (RTL).</li>
        <li>اصلاح شمارندهٔ نتایج داخل متن (مانند <code>1/1</code>) و به‌روزرسانی خودکار هایلایت‌ها هنگام تغییر عبارت بخش <strong>Body</strong> روی پیام انتخاب‌شده.</li>
        <li>پشتیبانی از جست‌وجو و هایلایت چندکلمه‌ای و یکسان‌سازی خودکار حروف فارسی و عربی (<code>ی</code>/<code>ي</code> و <code>ک</code>/<code>ك</code>) در جست‌وجوی ایندکس و پیش‌نمایش پیام.</li>
        <li>افزودن کلیدهای میانبر <strong>F3</strong> (مورد بعدی) و <strong>Shift+F3</strong> (مورد قبلی) برای جابه‌جایی سریع بین عبارت‌های هایلایت‌شده در متن ایمیل و حذف کادر مربعی ناخواسته دور دکمه‌های <code>&lt;</code> / <code>&gt;</code> و دکمه‌های پاک‌سازی/استثنا (<code>×</code> / <code>−</code>).</li>
        <li>بازیابی کامل ساعت شروع و پایان (<code>HH:mm</code>) هنگام بارگذاری جست‌وجوهای ذخیره‌شده، اعمال دقیق عبارت‌های منفی (<code>-term</code> / <code>NOT term</code>) در فیلدهای ایندکس‌شدهٔ <strong>From</strong>، <strong>To</strong> و <strong>Cc</strong>، و همگام‌سازی فوری وضعیت پرچم (Flag) پیام‌ها با ایندکس محلی.</li>
        <li>جلوگیری از تزریق تکراری استایل در ایمیل‌های دارای ساختار HTML تودرتو، ساده‌سازی زنجیره‌های تودرتوی بیش‌ازحد تگ‌های HTML (<code>&lt;div&gt;</code>/<code>&lt;span&gt;</code>/<code>&lt;blockquote&gt;</code>) برای جلوگیری از سرریز پشته در <code>MSHTML.dll</code> (<code>0xc00000fd</code>)، حذف فراخوانی موتور اسکریپت در پنل پیش‌نمایش برای جلوگیری از خطای <code>jscript9.dll</code> (<code>0xc0000602</code>) در ویندوز ۱۱ نسخهٔ 24H2، و افزایش ظرفیت کش پیش‌نمایش با حفظ کامل اطلاعات سربرگ و پیوست‌ها.</li>
      </ul>
    </li>
    <li><strong>پایداری نوار جست‌وجوی بالای ایمیل‌ها در چند مانیتور و تغییر پوشه‌ها:</strong>
      <ul>
        <li>بهبود مقیاس‌بندی DPI در مانیتورهای مختلف و بازطراحی خودکار نوار <strong>Advanced Search (<code>Ctrl+F3</code>)</strong> و آیکون‌های برداری هنگام جابه‌جایی پنجرهٔ اوت‌لوک بین نمایشگرها.</li>
        <li>اصلاح جابه‌جایی بین چند پنجرهٔ باز اوت‌لوک (Multi-Explorer) به‌گونه‌ای که موقعیت فهرست پیام‌ها در پنجرهٔ قبلی بدون ایجاد فاصلهٔ خالی به حالت استاندارد بازگردد.</li>
        <li>عملکرد دقیق‌تر هنگام تغییر پوشه و نما (از جمله صفحات اصلی صندوق، نماهای غیرایمیل و پوشهٔ <strong>Deleted Items</strong>) بدون پرش تصویر یا به‌هم‌ریختگی چیدمان.</li>
        <li>محدودسازی کلیدهای میانبر <code>Ctrl+F3</code> و <code>Ctrl+F4</code> به رشتهٔ رابط کاربری اوت‌لوک تا تایپ در سایر برنامه‌های ویندوز هیچ‌گاه تحت تأثیر قرار نگیرد.</li>
        <li>نمایش مستقیم پنجرهٔ ارسال پیام در پیش‌زمینه هنگام استفاده از قابلیت‌های <strong>Reply with Attachment(s)</strong> و <strong>Forward without Attachment(s)</strong>.</li>
      </ul>
    </li>
    <li><strong>ایندکس آنی ایمیل‌های جدید و پایش خودکار در Task Tracker:</strong>
      <ul>
        <li>ثبت دقیق زمان آخرین ویرایش پیام‌ها در ایندکس لحظه‌ای (<code>NewMailEx</code>، <code>ItemAdd</code> و <code>ItemChange</code>) و تطبیق کامل شناسه‌های <code>PR_ENTRYID</code> و <code>EntryID</code> هنگام همگام‌سازی پیام‌های حذف‌شده.</li>
        <li>فعال‌سازی خودکار پایش پوشه‌های <strong>Sent Items</strong> و <strong>Deleted Items</strong> در پس‌زمینه پس از راه‌اندازی اوت‌لوک، به‌طوری که تکمیل خودکار وظایف با ارسال پاسخ و پاک‌سازی ایمیل‌های حذف‌شده حتی پیش از باز کردن پنجرهٔ Task Tracker انجام شود.</li>
        <li>افزودن دکمهٔ اجرای مستقیم قوانین (<strong>Run rules</strong>) در کنار پیش‌نمایش نتایج در پنجرهٔ اسکن قوانین Task Tracker با حفظ محدوده و بازهٔ زمانی انتخاب‌شده، اصلاح مرتب‌سازی ستون‌ها با یک کلیک، و پاک‌سازی کاراکترهای کنترلی غیرمجاز هنگام خروجی گرفتن فایل اکسل (<code>.xls</code>).</li>
        <li>اجرای خودکار بهینه‌سازی پایگاه‌داده (<code>PRAGMA optimize</code>) در زمان بیکاری سیستم و ارتقای موتور داخلی SQLite به نسخهٔ <strong>3.54.0</strong> (<code>Microsoft.Data.Sqlite 10.0.13</code>).</li>
      </ul>
    </li>
    <li><strong>تأیید یکپارچگی نصب و فایل‌های اجرایی:</strong>
      <ul>
        <li>ارتقای بررسی‌های صحت فایل‌های نصب‌شده و گواهی اعتماد VSTO پیش از اعلام پایان نصب، و اصلاح تشخیص بسته بودن اوت‌لوک هنگام پاک‌سازی پروفایل‌های PST بدون تأثیرپذیری از سرویس‌های پس‌زمینهٔ ویندوز (<code>SearchIndexer</code> و <code>Teams</code>).</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.7 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>
