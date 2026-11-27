<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.2.3

Version 1.2.3 is a flagship **Microsoft Fluent 2 UI modernization, 1-click `Forward as Attachment` workflow, large-mailbox (`200k–500k` items) scaling, UI responsiveness, and Advanced Search results-table upgrade**. It delivers a cohesive Windows 11 / Fluent 2 visual refresh across **Advanced Search**, **Task Tracker**, **Rule Scan**, and context menus, adds 1-click **Forward as Attachment (`Ctrl+Shift+F`)** across the Ribbon and reading panes, eliminates progressive indexing slowdowns, Windows Search `Event ID 29` PST store-reset I/O storms, `Outlook (Not Responding)` UI stalls, Windows 11 ghost taskbar previews, and background busy-cursor (`IDC_APPSTARTING`) flicker—while introducing **Archive + Folder origin display**, a **`Size` column**, **per-column Excel-style header filters**, and an expanded **`Filter / Arrange by / Sort`** menu, all with **zero index rebuilds (`SCHEMA_VERSION = 1`)** and the `45 GB` seasonal PST rollover policy preserved.

### Highlights (Ordered by Priority)

1. **1-Click `Forward as Attachment` (`Ctrl+Shift+F`) & Microsoft Fluent 2 UI / Iconography Modernization:**
   - **1-Click `Forward as Attachment` Everywhere:** Select one or multiple messages on the Outlook Home Ribbon, Read-Message Inspector Ribbon, **Advanced Search**, **Task Tracker**, or **Rule Scan** (via the **`Fwd as Att`** reading-pane button, right-click menu, or **`Ctrl+Shift+F`**) to attach full `.msg` email items directly onto a single new compose draft with smart `FW:` subject handling and IRM protection awareness.
   - **Windows 11 / WinUI 3 Context Menus & Grounded Vector Iconography:** Upgraded all right-click menus (`Advanced Search`, `Task Tracker`, `Rule Scan`, `Task Rules`, and attachment menus) into unified single-list WinUI 3 `MenuFlyout` surfaces (`#FCFCFD` Light / `#2C2C2F` Dark, `8px` DWM rounded corners with anti-aliased contours, `4px` inset hover pills, flush right-aligned shortcut hints across both main menus and submenus, anti-aliased chevrons, and zero redundant section spacers) paired with `4x`-supersampled pure-vector icons (`Forward as Attachment`, `Reply +Att`, `Reply All +Att`, `Forward −Att` slashed-clip, `Save Attachments…`, `Track as Task`, `Export to CSV`, and full Task Tracker action icons) grounded on a strict optical baseline.
   - **Holistic A-to-Z WinUI 3 Surface Layering, Custom Scrollbars & Zero-Flash Chrome:** Unified every window, dialog, warning, and prompt (`Advanced Search`, `Task Tracker`, `Rule Scan`, `Task Rules`, `Rule Editor`, `Settings` with WinUI 3 `InfoBar` severity badges, `Vacation Mode`, `Status`, `Smart Archive`, `Save Search`, `Move to Folder`, `About`, and `ThemedMessage` semantic alert badges) with compact `34px` Windows 11 captions + crisp `1px` full-bleed structural separators, crisp rounded Attachment filter input framing without border clipping, Classic Outlook / Windows 11 custom scrollbars (capsule track, rounded triangle arrows, wheel hook, and `AttachWebBrowser` reading-pane scrollbars using `0xc0000602`-safe `IHTMLElement2` DOM scrolling), `DWMWA_CLOAK` zero-white-flash / zero-ghost window presentation, unified `80%` retention/threshold caps (`20%–80%` Archive Settings, `1%–80%` Vacation Mode) with inline warnings, and zero-`RecreateHandle()` unowned taskbar lifecycle (`WS_EX_APPWINDOW` + `ITaskbarList`).

2. **Advanced Search Results Table Upgrade — Archive Origin, `Size` Column, Per-Column Filters & Classic `Arrange by / Sort` Menu:**
   - **Unified Archive + Folder Location Display:** Results from `.pst` archives now display their exact archive origin directly inside the `Folder` column (`2026-Season2 \ Inbox`, `2025-Season4 \ Sent Items`) with full file-path hover tooltips, while primary live mailbox messages stay clean (`Inbox`).
   - **Message `Size` Column, Zero-Rebuild Backfill & Smart Viewport Fit:** Added a right-aligned **`Size` column** (`B`, `KB`, `MB`) backed by non-destructive `mail_meta.msg_size` migration and automatic read-only `Folder.GetTable` backfill during reconciliation (zero `MailItem` opens, zero PST dirtying, zero index rebuilds). Columns auto-fit cleanly to the pane on open (no horizontal scrollbar initially) and seamlessly unlock horizontal scrolling if widened manually.
   - **Per-Column Header Filter Popups:** Clicking the hover filter button (or right-clicking any column header) opens a Fluent rounded filter popup with contextual sort shortcuts, text narrowing, logical multi-select buckets—including **Live Mailbox / Archive** and **Folder** checklists on `Folder`, size tiers on `Size`, and chronological buckets on `Date`—plus automatic scroll-to-top on sort/arrange and one-click `Clear` / `Clear All` / `Reset Widths`.
   - **Clean `Search in` vs `Filter` Architecture:** Unified **`Search in`** strictly around storage locations (`All Mailboxes`, `Current Mailbox`, **`Archived Mail`**, `Current Folder`, `Current Folder & Subfolders`, mounted Season PSTs, and `Favorites`, grouped cleanly under scope headers) and dedicated **`Filter`** strictly to message attributes (`All Mail`, `Unread Mail`, `Flagged Mail`, `High Importance`, `Has Attachments`, `Meetings`), plus **`Arrange by`** (`Date`, `Size`, `From`, `To`, `Subject`, `Folder`, `Attachments`, `Flag Status`, `Importance`) and dynamic **`Sort`** (`Newest / Oldest`, `Largest / Smallest`, `A / Z on Top`)—with WinUI 3 `3px` vertical Accent selection indicator pills and automatic backward-compatible saved-search migration.
   - **Engine-Accurate `Preview Eligible...` Simulation:** Upgraded Archive Settings' dry-run preview to simulate the exact Smart Archive threshold gate (reporting `0` eligible when mailbox usage is below your configured trigger or when mode is `Disabled`), `30 → 1 day` pressure-ladder escalation, message-size target stop, 24-hour safety floor, protected folders, and follow-up flag protection.

3. **Strictly Read-Only Extended MAPI Indexing & Stage 2 Attachment Streaming (`RawMapiIndexReader`) — Zero PST Dirty-Writes (`Event ID 29`):**
   - Opens messages and attachments directly via `IMAPIFolder::OpenEntry` and `IMessage::OpenAttach` with strictly read-only flags (`ulFlags = 0` — never `MAPI_MODIFY` or `SaveChanges`), frees `SRowSet` buffers cleanly via `FreeProws`, streams `PR_BODY_W` / `PR_HTML` (capped at `512 KB`) / `PR_RTF_COMPRESSED` / `PR_BODY_A` and `PR_ATTACH_DATA_BIN` (`64 KB` chunks with user-input yield), verifies strict `PT_UNICODE` / `MAPI_E_NOT_FOUND` header integrity, skips `MSGSTATUS_HEADERONLY` stubs safely, and preserves IRM (`MailProtection`) and OOM fallbacks.

4. **Sustained High-Speed `200k–500k` Mailbox SQLite & FTS5 Scaling Engine (`BodyIndex` & `BodyIndexBuilder`):**
   - Fixed cold-build bulk SQLite/FTS5 activation (`256 MB` x64 writer cache, `128 MB` WAL auto-checkpoint, `automerge = 8` / `crisismerge = 32` even when opened early before `Start()`) and automatic post-build snapshot refresh so unattended cold builds reliably persist `initial_build_complete = 1`, restore steady-state tuning, and fold the bulk-build WAL via passive checkpoint; suppressed mid-build `ReconcileBodyMetadataParitySync()` full-table `NOT IN` writer locks and contentless FTS5 `DELETE` tombstones; restored `1,000–2,000`-doc bulk flushes after the first `2,000` fast-visibility rows; replaced `500k`-row `body_fts` string scans with compact `8-byte` `HashSet<long>` covering-index joins (~95% less RAM); added composite `ix_mail_meta_storeid_entryid` attachment-search index and SQL-bounded Top-N metadata snapshot queries; enabled instant interrupted-build resume; rewrote `OR` repair queries into `NOT EXISTS` probes; batched verified empty-body updates; and ensured graceful WAL `TRUNCATE` drain on normal close.

5. **Security, Installer Lifecycle, Full-Speed Idle Pacing & `Status` Dialog Polish:**
   - **Hardened Preview Sanitizer & Packaging Verification:** Hardened `SanitizePreviewHtml` with multi-pass tag-reassembly XSS normalization, NUL-byte stripping, entity-decoded URI scheme blocking, `<svg>`/`xlink:href`/`srcset` beacon blocking, and `/\\` UNC SMB NTLM leak neutralization; aligned `EmailTools.dll.config` NuGet assembly binding redirects (`Unsafe 6.0.3.0`, `Buffers 4.0.5.0`); and added explicit detached helper worker termination in Setup/Uninstall to prevent installer file-lock races.
   - **Zero Idle Slowdown + Stall-Only Backoff:** Preserves full `5 ms` deep-idle indexing cadence and full `35 / 125 / 275 ms` multi-item `Phase.Legacy` PST drain throughput within budget (`+60 ms` grace), scaling intervals only when a PST call genuinely stalls and yielding immediately on foreground user input.
   - **Eliminated Background Busy-Cursor (`Pointer + Blinking Circle`) Flicker:** Launches background helper `.exe`s via `CreateProcessW` with `STARTF_FORCEOFFFEEDBACK` + immediate `PeekMessage` initialization, deduplicates `EmailToolsStatus` updates (removing invalid `Explorer.StatusBar` IDispatch calls), and guards background timer slices against `mso.dll` `IDC_APPSTARTING` cursor flips.
   - **Accurate, Non-Activating `Status` Dialog:** Shows `"Paused — Waiting for Smart Archive"` while `MaintenanceLane` is busy, resizes live via `SetWindowPos(..., SWP_NOMOVE | SWP_NOZORDER | SWP_NOACTIVATE)` so it never steals focus, and caches `Legacy cleanup` / PST store scans for `30s`.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.2.3 directly over v1.2.2 without uninstalling first, and existing search indexes are preserved without rebuilding.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="justify">
  <p>نسخه ۱.۲.۳ یک به‌روزرسانی پرچم‌دار شامل <strong>مدرن‌سازی کامل رابط کاربری بر اساس استاندارد Microsoft Fluent 2 / Windows 11، قابلیت ارسال ایمیل به‌عنوان فایل پیوست (<code>Forward as Attachment</code>)، سرعت پایدار نمایه‌سازی برای صندوق‌های بسیار بزرگ (۲۰۰ تا ۵۰۰ هزار ایمیل)، حذف هنگ‌های لحظه‌ای و چشمک زدن نشانگر ماوس، و ارتقای کامل جدول نتایج جست‌وجو</strong> است — با حفظ ۱۰۰٪ حداکثر سرعت در زمان بیکاری سیستم، حفظ پایگاه‌داده جست‌وجوی فعلی کاربران بدون نیاز به ساخت مجدد (<code>SCHEMA_VERSION = 1</code>) و حفظ سقف استاندارد ۴۵ گیگابایتی آرشیوهای فصلی.</p>

  <h3 align="right">ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>قابلیت یک‌کلیکی <code>Forward as Attachment</code> (<code>Ctrl+Shift+F</code>) و بازطراحی مدرن رابط کاربری Fluent 2:</strong>
      <ul>
        <li><strong>ارسال ایمیل به‌عنوان پیوست (<code>.msg</code>) در تمامی بخش‌ها:</strong> امکان انتخاب یک یا چند ایمیل در ریبون اصلی اوت‌لوک، پنجره مطالعه ایمیل، <strong>Advanced Search</strong>، <strong>Task Tracker</strong> و <strong>Rule Scan</strong> (از طریق دکمه <code dir="ltr">Fwd as Att</code>، منوی کلیک راست یا کلید میانبر <code dir="ltr">Ctrl+Shift+F</code>) و پیوست خودکار آن‌ها روی یک ایمیل جدید.</li>
        <li><strong>بازطراحی حرفه‌ای منوهای کلیک راست و آیکون‌های برداری Fluent 2:</strong> گوشه‌های گرد ویندوز ۱۱ (<code dir="ltr">DWMWCP_ROUNDSMALL</code>)، انتخاب کپسولی مدرن، چیدمان راست‌چین دقیق کلیدهای میانبر در منوی اصلی و زیرمنوها، فلش‌های زیرمنوی شفاف و آیکون‌های برداری اختصاصی با هاله شفاف (<code dir="ltr">SourceCopy</code>) برای تمامی گزینه‌ها از جمله <code dir="ltr">Save Attachments…</code>، <code dir="ltr">Track as Task</code>، <code dir="ltr">Forward without Attachment(s)</code> و تمامی منوهای Task Tracker.</li>
        <li><strong>نوسازی کامل پنجره‌های جست‌وجو و مدیریت وظایف، اسکرول‌بار سفارشی و باز شدن بدون پرش سفید:</strong> اسکرول‌بارهای هماهنگ با اوت‌لوک کلاسیک/ویندوز ۱۱ در جداول و پنل پیش‌نمایش پیام، حذف کامل پرش سفید هنگام باز شدن پنجره‌ها با <code dir="ltr">DWMWA_CLOAK</code>، پرش خودکار به ابتدای جدول پس از مرتب‌سازی، سقف یکپارچه ۸۰٪ برای تنظیمات بایگانی (<code dir="ltr">20%–80%</code>) و حالت مرخصی (<code dir="ltr">1%–80%</code>) همراه با هشدار خطی، نوار ابزار آیکون‌دار پنل پیش‌نمایش و حذف کامل پیش‌نمایش روح (Ghost Thumbnail) در تسک‌بار ویندوز ۱۱.</li>
      </ul>
    </li>
    <li><strong>ارتقای کامل جدول نتایج جست‌وجوی پیشرفته — نمایش فایل آرشیو، ستون حجم (<code>Size</code>)، فیلتر ستونی و منوی <code>Arrange by / Sort</code>:</strong>
      <ul>
        <li><strong>نمایش یکپارچه نام آرشیو و پوشه در ستون <code>Folder</code>:</strong> ایمیل‌های موجود در فایل‌های آرشیو <code>.pst</code> اکنون نام دقیق آرشیو و پوشه خود را به‌صورت شفاف نمایش می‌دهند (مانند <code dir="ltr">2026-Season2 \ Inbox</code> به‌همراه نمایش مسیر کامل فایل در Tooltip)، درحالی‌که ایمیل‌های صندوق زنده بدون شلوغی اضافی (<code dir="ltr">Inbox</code>) نمایش داده می‌شوند.</li>
        <li><strong>ستون جدید حجم ایمیل (<code>Size</code>) و چیدمان هوشمند ستون‌ها:</strong> افزودن ستون <code>Size</code> (نمایش حجم به بایت، کیلوبایت و مگابایت) با ارتقای غیرمخرب جدول <code>mail_meta</code> و تکمیل خودکار حجم ایمیل‌های قبلی در پس‌زمینه؛ عرض ستون‌ها در بدو باز شدن دقیقاً منطبق بر کادر تنظیم می‌شود (بدون اسکرول افقی اولیه) و در صورت بزرگ‌تر کردن دستی ستون‌ها، اسکرول افقی به‌طور خودکار فعال می‌گردد.</li>
        <li><strong>فیلتر مجزا روی تک‌تک سرستون‌ها:</strong> با کلیک روی دکمه فیلتر سرستون (یا کلیک راست روی هر سرستون)، پنجره فیلتر اختصاصی با دکمه‌های مرتب‌سازی متناسب، جست‌وجوی متنی، دسته‌بندی منطقی مقادیر (از جمله تفکیک <strong>صندوق زنده / آرشیوها</strong> و <strong>پوشه</strong> در ستون <code>Folder</code>، رده‌های حجمی در ستون <code>Size</code> و بازه‌های زمانی در ستون <code>Date</code>) و دکمه‌های <code dir="ltr">Clear</code> / <code dir="ltr">Clear All</code> باز می‌شود.</li>
        <li><strong>تفکیک شفاف <code>Search in</code> و <code>Filter</code> به‌همراه نشانگر انتخاب WinUI 3:</strong> اختصاص منوی <code dir="ltr">Search in</code> صرفاً به محل ذخیره‌سازی (<code dir="ltr">All Mailboxes</code>، <code dir="ltr">Current Mailbox</code>، <strong><code dir="ltr">Archived Mail</code></strong>، پوشه جاری، زیرپوشه‌ها، آرشیوهای فصلی PST و پوشه‌های منتخب با گروه‌بندی واضح) و اختصاص منوی <code dir="ltr">Filter</code> به ویژگی‌های پیام (<code dir="ltr">Unread Mail</code>، <code dir="ltr">Flagged Mail</code>، <code dir="ltr">High Importance</code>، <code dir="ltr">Has Attachments</code>، <code dir="ltr">Meetings</code>) به‌همراه بخش‌های یکپارچه <strong><code dir="ltr">Arrange by</code></strong> و <strong><code dir="ltr">Sort</code></strong>.</li>
        <li><strong>شبیه‌سازی دقیق پیش‌نمایش آزمایشی <code>Preview Eligible...</code>:</strong> همگام‌سازی ۱۰۰٪ پیش‌نمایش تنظیمات آرشیو با منطق واقعی موتور بایگانی هوشمند (رعایت حالت انتخابی بایگانی، نمایش صادقانهٔ عدد <code dir="ltr">0</code> هنگام پایین بودن مصرف از درصد تنظیمی، پلکان ۳۰ تا ۱ روزه، توقف در حجم هدف و حفاظت از ایمیل‌های پرچم‌دار).</li>
      </ul>
    </li>
    <li><strong>موتور نمایه‌سازی و استخراج پیوست کاملاً فقط‌خواندنی Extended MAPI (<code>RawMapiIndexReader</code>) و حذف کامل <code>Event ID 29</code>:</strong>
      <ul>
        <li>خواندن متن ایمیل‌ها و جریان فایل‌های پیوست مستقیماً با پرچم کاملاً فقط‌خواندنی (<code dir="ltr">ulFlags = 0</code>) بدون تغییر صفحات فایل‌های PST روی دیسک، بررسی دقیق سربرگ‌ها، تشخیص آیتم‌های <code dir="ltr">MSGSTATUS_HEADERONLY</code> و رعایت کامل ایمیل‌های محافظت‌شده (IRM).</li>
      </ul>
    </li>
    <li><strong>معماری مقیاس‌پذیر SQLite و FTS5 و مقاوم‌سازی امنیتی برای صندوق‌های ۲۰۰ تا ۵۰۰ هزار ایمیلی:</strong>
      <ul>
        <li>فعال‌سازی قطعی حالت Bulk (<code dir="ltr">256 MB</code> کش، <code dir="ltr">128 MB</code> WAL و <code dir="ltr">automerge=8</code>) از ابتدای ساخت اولیه و به‌روزرسانی خودکار شمارنده‌ها برای ثبت قطعی <code dir="ltr">initial_build_complete</code> و جمع‌کردن WAL پس از اتمام، ایندکس مرکب جست‌وجوی پیوست‌ها (<code dir="ltr">ix_mail_meta_storeid_entryid</code>)، حذف قفل‌های میانی جدول، کاهش ۹۵ درصدی مصرف رم در تطبیق مخازن (<code dir="ltr">HashSet&lt;long&gt;</code>)، مقاوم‌سازی کامل <code dir="ltr">SanitizePreviewHtml</code> در برابر XSS و نشت شبکه UNC/NTLM و خاتمه تمیز ابزارهای کمکی در نصب‌کننده.</li>
      </ul>
    </li>
    <li><strong>حفظ حداکثر سرعت در زمان بیکاری، حذف چشمک زدن نشانگر ماوس (<code>IDC_APPSTARTING</code>) و اصلاح پنجره <code>Status</code>:</strong>
      <ul>
        <li><strong>رفع کامل حالت مشغول ماوس (نشانگر + دایره چشمک‌زن) در پس‌زمینه:</strong> اجرای ابزارهای کمکی پس‌زمینه با پرچم ویندوزی <code dir="ltr">STARTF_FORCEOFFFEEDBACK</code> و مقداردهی اولیه <code dir="ltr">PeekMessage</code>، حذف فراخوانی‌های تکراری <code>EmailToolsStatus</code> و محافظت از نشانگر ماوس در تیک‌های پس‌زمینه اوت‌لوک.</li>
        <li><strong>سرعت ۱۰۰٪ در حالت بیکاری و پنجره وضعیت دقیق و بدون پرش فوکوس:</strong> حفظ سرعت کامل ایندکسینگ و ادغام آرشیوهای قدیمی هنگام بیکاری سیستم با توقف فوری هنگام فعالیت کاربر، نمایش پیام دقیق <code dir="ltr">Paused — Waiting for Smart Archive</code>، تغییر ارتفاع بدون سرقت فوکوس (<code dir="ltr">SWP_NOACTIVATE</code>) و کش ۳۰ ثانیه‌ای وضعیت PST.</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب برای کاربر فعلی انجام می‌شود و به دسترسی مدیر نیاز ندارد. کاربران فعلی می‌توانند نسخه ۱.۲.۳ را مستقیماً روی نسخه موجود نصب کنند و ایندکس قبلی آن‌ها بدون نیاز به ساخت مجدد حفظ می‌شود.</p>
</div>
