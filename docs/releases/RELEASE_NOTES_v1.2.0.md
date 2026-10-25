<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.2.0

Version 1.2.0 introduces **Smart Archive Operating Modes (`Auto Archive` / `Manual Only` / `Disabled`)** with full policy control and transition confirmation, **Outlook-style Reply/Forward status banners with one-click `"Find related messages"`** in the message preview pane, **forced Left-to-Right (LTR) attachment chip rendering** for RTL emails, **multi-token and initial-based person/alias filtering** across Advanced Search and Task Tracker, **complete email indexing without duplicate rows after flag changes**, and **more reliable header verification and improved indexing efficiency**.

### Highlights (Ordered by Priority)

1. **Smart Archive Operating Mode (`Auto Archive` / `Manual Only` / `Disabled`):**
   - **Three-Tier Operating Mode Selector:** Added an **ARCHIVE OPERATING MODE** card to **Smart Archive → Settings** (`ArchiveSettingsForm`) allowing users to switch between:
     - **Auto Archive (Default):** Full automatic background protection—monitors mailbox quota, runs scheduled and **Emergency Archive** passes, auto-mounts seasonal PSTs, and performs **Flag Recovery**.
     - **Manual Only:** Disables all automatic background archiving and **automatic Emergency Archive** (even above 90% quota), while keeping manual **Archive Now**, **Vacation Mode**, and automatic seasonal PST mounting available. Automatic Flag Recovery resumes in **Auto Archive** mode.
     - **Disabled (Search & Tasks Only):** Completely deactivates all archiving and archive-maintenance features—including automatic archiving, **Emergency Archive**, manual **Archive Now**, **Vacation Mode**, automatic PST mounting/creation, and **Flag Recovery**—so the add-in operates strictly as **Advanced Search (`Ctrl+F3`)** and **Task Tracker (`Ctrl+F4`)**.
   - **Dynamic Policy & Warning Banners:** Selecting a mode in Settings immediately displays a color-coded policy banner (Blue for `Auto Archive`, Amber warning for `Manual Only`, Red alert for `Disabled`) detailing exactly which background services remain active or are turned off.
   - **Validated Mode Transitions & Single-Step Confirmation:** Every mode change is validated with a single DPI-aware confirmation dialog before taking effect:
     - Switching from **Manual Only** or **Disabled** to **Auto Archive** restarts the automatic maintenance workflow without restarting Outlook, including quota checks, archive preparation, scheduled archiving and Flag Recovery.
     - Switching to **Manual Only** stops automatic background scheduling and halts any active background archive task.
     - Switching to **Disabled** confirms deactivation and immediately halts any active or queued archive, vacation, or maintenance tasks.
   - **Restored Flag Recovery:** Auto Archive checks managed archive PSTs and returns eligible follow-up flagged messages to the Inbox. Recovery is recorded as complete only after the destination and retained flag are verified.

2. **Interactive Reply / Forward InfoBar with `"Find related messages"` in Preview:**
   - **Native MAPI Last-Verb Tracking:** Reads `PR_LAST_VERB_EXECUTED` (`0x10810003`: `102` = Reply to Sender, `103` = Reply to All, `104` = Forward, `108` = Reply to Forward) and `PR_LAST_VERB_EXECUTION_TIME` (`0x10820040`) directly from the message item.
   - **Outlook-Style Header InfoBar:** Displays a compact, text-fitted banner (`ⓘ You replied to this message on M/d/yyyy h:mm tt.` or `ⓘ You forwarded this message on M/d/yyyy h:mm tt.`) directly below the `To`/`Cc` header lines in both **Advanced Search** and **Task Tracker** preview panes.
   - **Clickable `"Find related messages"` Menu & Dash-Subject Support:** Clicking the InfoBar opens the minimal **`Find related messages`** menu right at the cursor position to filter the grid to the complete conversation thread, including subjects containing dash-prefixed tokens (such as `-Spare` or `-Mordad`).
   - **Live Cache Refresh on Reply/Forward:** Replying or forwarding from Advanced Search or Task Tracker automatically invalidates the cached preview for that message so the new Reply/Forward timestamp appears immediately.

3. **Fixed Right-Aligned Attachment Chips on RTL (Persian / Arabic) Emails:**
   - Enforced explicit Left-to-Right layout isolation (`dir='ltr'` and `direction:ltr!important;text-align:left!important;unicode-bidi:embed;`) on the preview attachment container (`BuildAttachmentBar`, `BuildEmbeddedAttachmentBar`), individual attachment chips (`AttachmentChip`, `EmbeddedAttachmentChip`), meeting info bars, and `#emailtools-preview-css` (`div[etns='1'],div[etns='1'] *`).
   - Prevents emails authored with `<body dir="rtl">` or global `div { direction: rtl; }` styles from pushing attachment chips to the right side of the preview pane or reversing file sizes (`"80.4 KB"` into `"KB 80.4"`).

4. **Multi-Token, Initial & Alias Person Filtering (Advanced Search & Task Tracker):**
   - **Multi-Word & Initial Matching:** Fixed multi-token person queries (such as `mehdi q`, `mehdi o`, `mostafa s`, `mostafa m`, `mehdi m`, `mostafa mofa`) across `ConversationPersonResolver`, `MailSearchEngine`, `BodyIndex`, `TaskRuleEvaluator`, and `TaskTrackerForm`. Multi-word queries now require every token to match as a word/segment prefix on the same person identity, preventing single-letter surname initials from matching unrelated mid-word letters or domains.
   - **Bidirectional Alias & Display-Name Directory:** Links Exchange display names (e.g., `Parham Ghafouri [ Vista Service ]`), SMTP email addresses (`parham.g@iranvs.ir`), and username/local-part aliases (`parham.g`) across **From**, **To**, **Cc**, and **Exclude** filters in both Advanced Search and Task Tracker.
   - **Domain-Qualified Address Matching:** Queries such as `iam@mtn` no longer expand to an unrelated address such as `iam@iranvs.ir` just because both share the same local name or display label.
   - **Isolated Per-Search Criteria Expansion:** Clones `MailSearchCriteria` per search execution so removing or modifying a person filter never retains expanded alias terms from an earlier query.

5. **Eliminated Duplicate Results After Flagging or Clearing Flags:**
   - Resolved the identity mismatch between Outlook's 24-byte short-term table EntryID (`EF000000...` with Exchange X500 `sender_email`) and the 70-byte long-term EntryID (`00000000...` with SMTP `sender_email`) delivered by `Items.ItemChange` when flagging, unflagging, or marking an email read/unread.
   - `BodyIndex.UpsertLiveSync` updates the existing canonical row in place and cleans up any lingering duplicate row, complemented by a one-time startup migration (`search_index_repair_v120`).

6. **Missing Emails, Watermark Completeness & Fast Header Verification:**
   - Fixed `BodyIndexBuilder.StepBuild` so per-store watermarks only skip a folder when the item's `EntryID` is confirmed present in `_curStoreIndexedIds`, ensuring previously unindexed older emails and imported PST items are always indexed.
   - Preserved verified long headers across periodic reconciliation so recipient names near the end of long **To/Cc** lists remain searchable.
   - Added lightweight header-only verification, including support for meeting messages, delivery reports and other Outlook item types, without rereading message bodies or attachments.
   - Failed header reads now preserve previously indexed text and remain eligible for retry; they can no longer erase search fields or falsely mark them complete. Confirmed absent properties are handled separately from read failures.
   - Existing verification records from the affected version receive a one-time background recheck. **Message headers awaiting verification** may appear during this pass; **Ready** returns once verification and the remaining index work complete.
   - Removed repeated full-table scans from upgrade cleanup and reduced redundant database writes and folder lookups during indexing.
   - Header-search completeness now follows the fields and location being searched, rather than inheriting warnings from unrelated long recipient lists.

7. **Upgraded Embedded SQLite Engine to 3.54.1 (2026-10-16 Release):**
   - Updated the bundled `x86` and `x64` native SQLite engines (`e_sqlite3.dll`) to **SQLite 3.54.1** (released October 16, 2026), resolving the 32-bit heap-buffer overflow fixed in 3.54.1 along with 3.54.0 query planner improvements, faster `UNION ... LIMIT 1` execution, and Windows Slim Reader/Writer Lock (`SRWL`) mutexes for lower concurrency overhead across WAL readers and background index writers.

8. **Preview Menus & Window Layout:**
   - Matched the attachment and **Find related messages** popup styles, including full-width hover highlights and separators without the unused right-side gap.
   - Corrected the Status window header layout so the title leaves room for the close button at different display scales.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.2.0 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۲.۰ شامل <strong>سه حالت کاری جدید برای بایگانی هوشمند (<code>Auto Archive</code> / <code>Manual Only</code> / <code>Disabled</code>) همراه با راهنمای رنگی سیاست‌ها و تأییدیه تغییر وضعیت</strong>، <strong>نوار وضعیت پاسخ و فوروارد (Reply/Forward InfoBar) در پیش‌نمایش پیام با قابلیت کلیک و اجرای <code>Find related messages</code></strong>، <strong>اصلاح کامل چیدمان چپ‌به‌راست (LTR) فایل‌های پیوست در ایمیل‌های فارسی و راست‌به‌چپ</strong>، <strong>جست‌وجوی دقیق چندبخشی و حرف اول نام خانوادگی در Advanced Search و Task Tracker</strong>، <strong>رفع ردیف‌های تکراری پس از تغییر پرچم (Flag)</strong> و <strong>افزایش دقت بررسی سربرگ‌ها و بهبود کارایی ایندکس</strong> است.</p>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>سه حالت کاری بایگانی هوشمند در تنظیمات (<code>Auto Archive</code> / <code>Manual Only</code> / <code>Disabled</code>):</strong>
      <ul>
        <li><strong>انتخابگر حالت عملکرد بایگانی (Archive Operating Mode):</strong> افزودن بخش جدیدی در پنجره تنظیمات بایگانی هوشمند (<code>Smart Archive → Settings</code>) با سه حالت مجزا:
          <ul>
            <li><strong>حالت خودکار (Auto Archive - پیش‌فرض):</strong> فعال بودن کامل پایش خودکار حجم صندوق، اجرای بایگانی زمان‌بندی‌شده و اضطراری (<strong>Emergency Archive</strong>)، اتصال خودکار فایل‌های PST فصلی، تعمیر <strong>Conversation History</strong> و بازیابی ایمیل‌های پرچم‌دار (<strong>Flag Recovery</strong>).</li>
            <li><strong>حالت فقط دستی (Manual Only):</strong> غیرفعال شدن تمامی بایگانی‌های خودکار پس‌زمینه و همچنین <strong>غیرفعال شدن بایگانی اضطراری خودکار (حتی بالای ۹۰٪ ظرفیت صندوق)</strong>؛ در این حالت عملیات بایگانی تنها با کلیک دستی کاربر روی <strong>Archive Now</strong> یا <strong>Vacation Mode</strong> اجرا می‌شود، و اتصال خودکار PSTهای فصلی در دسترس است. بازیابی خودکار پیام‌های پرچم‌دار با بازگشت به حالت <strong>Auto Archive</strong> از سر گرفته می‌شود.</li>
            <li><strong>حالت غیرفعال کامل (Disabled - Search &amp; Tasks Only):</strong> غیرفعال‌سازی کامل تمامی قابلیت‌های بایگانی و نگهداری مرتبط با آن — شامل بایگانی خودکار، <strong>Emergency Archive</strong>، اجرای دستی <strong>Archive Now</strong>، <strong>Vacation Mode</strong>، ساخت یا اتصال خودکار فایل‌های PST، تعمیر <strong>Conversation History</strong> و <strong>Flag Recovery</strong> — به طوری که افزونه صرفاً برای <strong>جست‌وجوی پیشرفته (<code>Ctrl+F3</code>)</strong> و <strong>ردیاب وظایف (<code>Ctrl+F4</code>)</strong> کار می‌کند.</li>
          </ul>
        </li>
        <li><strong>بنرهای راهنما و هشدار رنگی پویا:</strong> با انتخاب هر حالت در تنظیمات، کادر راهنمای رنگی (آبی برای خودکار، کهربایی هشدار برای دستی، و قرمز برای غیرفعال) بلافاصله جزئیات دقیق سرویس‌های فعال و غیرفعال را نمایش می‌دهد.</li>
        <li><strong>اعتبارسنجی، تأییدیه و اجرای فوری در هر مرحله:</strong> هرگونه تغییر حالت هنگام ذخیره تنظیمات با پیام تأییدیه شفاف همراه است؛ بازگشت از حالت دستی یا غیرفعال به حالت خودکار، بررسی ظرفیت، آماده‌سازی آرشیو، بایگانی زمان‌بندی‌شده و بازیابی پیام‌های پرچم‌دار را بدون راه‌اندازی مجدد اوت‌لوک از سر می‌گیرد؛ تغییر به حالت دستی امکان اجرای فوری یک نوبت بایگانی دستی را فراهم می‌کند، و تغییر به حالت غیرفعال تمامی عملیات بایگانی یا تعمیر در حال اجرا را متوقف می‌سازد.</li>
        <li><strong>بازیابی واقعی پیام‌های پرچم‌دار:</strong> در حالت خودکار، پیام‌های واجد شرایط از PSTهای آرشیو مدیریت‌شده به Inbox برگردانده می‌شوند. تکمیل بازیابی تنها پس از تأیید مقصد و حفظ پرچم ثبت می‌شود.</li>
      </ul>
    </li>
    <li><strong>نوار اطلاع‌رسانی پاسخ و فوروارد (Reply/Forward InfoBar) همراه با قابلیت کلیک و یافتن پیام‌های مرتبط:</strong>
      <ul>
        <li><strong>خواندن مستقیم وضعیت پاسخ و فوروارد از MAPI:</strong> خواندن ویژگی‌های <code>PR_LAST_VERB_EXECUTED</code> و <code>PR_LAST_VERB_EXECUTION_TIME</code> برای تشخیص دقیق آخرین عملیات پاسخ (Reply / Reply All) یا هدایت (Forward) روی پیام.</li>
        <li><strong>نمایش نوار وضعیت به سبک اوت‌لوک در پیش‌نمایش:</strong> نمایش نوار باریک <code>ⓘ You replied to this message on ...</code> یا <code>ⓘ You forwarded this message on ...</code> در زیر ردیف‌های <code>To</code> و <code>Cc</code> در پیش‌نمایش <strong>Advanced Search</strong> و <strong>Task Tracker</strong>.</li>
        <li><strong>منوی قابل کلیک <code>Find related messages</code>:</strong> با قرار گرفتن نشانگر ماوس روی این نوار، کل نوار برجسته شده و با کلیک روی هر نقطه از آن، منوی <strong><code>Find related messages</code></strong> باز می‌شود که با یک کلیک تمام پیام‌های مرتبط در همان زنجیره مکاتبه را فیلتر و نمایش می‌دهد.</li>
      </ul>
    </li>
    <li><strong>اصلاح نمایش فایل‌های پیوست در سمت چپ برای ایمیل‌های راست‌به‌چپ (فارسی/عربی):</strong>
      <ul>
        <li>اعمال ایزولاسیون صریح چپ‌به‌راست (<code>dir='ltr'</code> و <code>direction:ltr!important;text-align:left!important;unicode-bidi:embed;</code>) روی نوار پیوست‌ها و تک‌تک کارت‌های فایل پیوست در پیش‌نمایش.</li>
        <li>جلوگیری از منتقل شدن کارت‌های پیوست به سمت راست صفحه یا برعکس شدن نمایش حجم فایل (مانند تبدیل <code>80.4 KB</code> به <code>KB 80.4</code>) در ایمیل‌های دارای <code>dir="rtl"</code>.</li>
      </ul>
    </li>
    <li><strong>جست‌وجو و فیلتر دقیق چندکلمه‌ای، حرف اول نام خانوادگی و نام کاربری در Advanced Search و Task Tracker:</strong>
      <ul>
        <li>اصلاح کامل جست‌وجوهای چندبخشی و دارای حرف اول نام خانوادگی (مانند <code>mehdi q</code>، <code>mehdi o</code>، <code>mostafa s</code>، <code>mostafa m</code> و <code>mostafa mofa</code>) در تمام بخش‌های جست‌وجوی پیشرفته و ردیاب وظایف، به گونه‌ای که تمام بخش‌های عبارت باید به صورت پیشوند کلمه/بخش در همان شخص صدق کنند.</li>
        <li>اصلاح جست‌وجوی آدرس دارای دامنه؛ برای نمونه، عبارت <code>iam@mtn</code> دیگر صرفاً به دلیل نام کاربری یا نام نمایشی مشترک، آدرس نامرتبط <code>iam@iranvs.ir</code> را شامل نمی‌شود.</li>
        <li>ساخت فهرست دوطرفه محلی برای تطبیق خودکار نام نمایشی اکسچنج، آدرس ایمیل کامل و نام کاربری در فیلدهای <strong>From</strong>، <strong>To</strong>، <strong>Cc</strong> و <strong>Exclude</strong>.</li>
      </ul>
    </li>
    <li><strong>رفع نتایج تکراری پس از افزودن یا پاک کردن پرچم (Flag):</strong>
      <ul>
        <li>رفع ناهماهنگی میان شناسه کوتاه جدولی اوت‌لوک (<code>EF000000...</code>) و شناسه بلند پیام (<code>00000000...</code>) در <code>UpsertLiveSync</code> و اجرای خودکار تعمیر اولیه پایگاه‌داده (<code>search_index_repair_v120</code>) برای پاک‌سازی ردیف‌های تکراری قبلی.</li>
      </ul>
    </li>
    <li><strong>رفع جا افتادن ایمیل‌های قدیمی و بهبود سرعت بررسی سربرگ‌ها در صندوق‌های بزرگ:</strong>
      <ul>
        <li>اصلاح بررسی نشانگر زمانی (Watermark) در <code>StepBuild</code> برای اطمینان از ایندکس شدن کامل پیام‌های قدیمی و آرشیوهای واردشده، و حفظ سربرگ‌های کامل تأییدشده در بررسی‌های دوره‌ای برای حفظ قابلیت جست‌وجوی گیرندگان انتهای فهرست‌های بلند <strong>To/Cc</strong>.</li>
        <li>بررسی سبک سربرگ‌ها بدون خواندن مجدد متن و پیوست‌ها، همراه با پشتیبانی از پیام‌های جلسه، گزارش‌های تحویل و سایر انواع پیام اوت‌لوک.</li>
        <li>حفظ متن ایندکس‌شده قبلی هنگام خطای خواندن سربرگ و تلاش مجدد؛ خطا دیگر باعث پاک شدن فیلدهای جست‌وجو یا تأیید نادرست تکمیل بررسی نمی‌شود. نبود واقعی یک ویژگی از خطای خواندن آن تفکیک شده است.</li>
        <li>بررسی مجدد یک‌باره سوابق تأیید نسخه آسیب‌دیده در پس‌زمینه؛ در این مدت ممکن است پیام <code>Message headers awaiting verification</code> نمایش داده شود. پس از پایان بررسی و سایر کارهای ایندکس، وضعیت به <strong>Ready</strong> برمی‌گردد.</li>
        <li>حذف اسکن‌های تکراری کل جدول هنگام ارتقا و کاهش نوشتن‌های اضافی پایگاه‌داده و خواندن‌های تکراری اطلاعات پوشه هنگام ایندکس.</li>
        <li>محاسبه کامل بودن نتایج بر اساس فیلدها و محل جست‌وجوی انتخاب‌شده، بدون انتقال هشدار فهرست گیرندگان نامرتبط به سایر جست‌وجوها.</li>
      </ul>
    </li>
    <li><strong>ارتقای موتور پایگاه‌داده داخلی SQLite به نسخه 3.54.1 (انتشار ۱۶ اکتبر ۲۰۲۶):</strong>
      <ul>
        <li>به‌روزرسانی موتور بومی <code>e_sqlite3.dll</code> (در هر دو معماری ۳۲ بیتی و ۶۴ بیتی) به نسخه <strong>SQLite 3.54.1</strong> جهت رفع آسیب‌پذیری سرریز بافر در نسخه‌های ۳۲ بیتی، بهره‌مندی از بهینه‌سازی‌های برنامه‌ریز پرس‌وجو (Query Planner) و استفاده از قفل‌های سریع‌تر ویندوز (Slim Reader/Writer Locks - SRWL) برای کاهش تأخیر هم‌زمانی میان خواننده‌های جست‌وجو و نویسنده پس‌زمینه.</li>
      </ul>
    </li>
    <li><strong>یکسان‌سازی منوهای پیش‌نمایش و اصلاح چیدمان پنجره:</strong>
      <ul>
        <li>یکسان‌سازی ظاهر منوی پیوست و <code>Find related messages</code>، با برجسته‌سازی تمام عرض ردیف و حذف فاصله اضافی سمت راست.</li>
        <li>اصلاح سربرگ پنجره Status برای حفظ فضای دکمه بستن در مقیاس‌های مختلف نمایشگر.</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب برای کاربر فعلی انجام می‌شود و به دسترسی مدیر نیاز ندارد. کاربران فعلی می‌توانند نسخه ۱.۲.۰ را مستقیماً روی نسخه موجود نصب کنند و نیازی به حذف نسخه قبلی نیست.</p>
</div>
