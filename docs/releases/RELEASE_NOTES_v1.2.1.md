<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.2.1

Version 1.2.1 delivers critical stability, layout synchronization, search precision, and attachment classification fixes. It resolves **frozen or half-height WebBrowser preview rendering** between Task Tracker and Advanced Search, **Outlook COM/MAPI error `0x80004005` and persistent "Verification pending" stalls** during seasonal archive preparation, **zero-result sender searches on bracketed corporate names**, **spurious `.emz` / `.wmz` attachments generated during Reply with Attachment(s)**, **hashtag distribution group and single-symbol `#` search inaccuracies**, and **comprehensive query parser edge cases identified during local database auditing**.

### Highlights (Ordered by Priority)

1. **Task Tracker & Mail Search — Fixed Preview Pane Rendering "In Half" & Frozen Right Canvas:**
   - **Nested Win32 ActiveX HWND Synchronization:** The WinForms WebBrowser control hosts three nested Win32 ActiveX child windows (`Shell Embedding` → `Shell DocObject View` → `Internet Explorer_Server`). When both `TaskTrackerForm` and `MailSearchPanel` hosted ActiveX WebBrowser instances on the same Outlook UI thread or when splitter/header layout changes occurred while navigating via `DocumentText`, the inner ActiveX child HWNDs desynchronized from the outer control's `ClientSize`, leaving the right half unpainted with stale pixels.
   - **Recursive HWND Resizing & Redraw:** Implemented `WindowPositionHelper.SyncWebBrowserBounds`, which aligns outer WebBrowser bounds with its host panel and header, enumerates all descendant Win32 HWNDs (`EnumChildWindows` + `SetWindowPos`) to enforce 100% client width and height, and invalidates/erases the complete HWND hierarchy (`RedrawWindow`).
   - **Lifecycle Event Integration:** Wired bounds synchronization across `MailSearchPanel` and `TaskTrackerForm` in `NavigatePreview`, `DocumentCompleted`, `SizeChanged`, `VisibleChanged`, and host panel resize events.

2. **Archive Mounting & Index Readiness — Fixed Error `0x80004005` & Indefinite "Verification Pending":**
   - **Resilient Archive Preparation (Error 0x80004005):** Removed redundant synchronous pre-mounting from `SmartArchive.BeginArchivePreparation`. When an archive PST has a locked or corrupted header returning `0x80004005` (*The Outlook data file (.pst) failed to load for this session*), `SmartArchive` now tracks unloadable paths per session (`_unmountableSeasonPstPaths`), skips 0-byte or corrupted files during auto-mount, and automatically rolls over to `<Season>-2.pst` in `ResolveSeasonPstWithRoom` and `MoveOneAtIndex`.
   - **Persistent "Verification Pending" Loop Resolution:**
     - In `BodyIndex.MarkHeaderCandidateVerifiedSync`, fixed a bug where `headers_full:<rid>` was set in metadata without deleting the corresponding row from `header_repair_pending`, which left `EXISTS(SELECT 1 FROM header_repair_pending)` permanently true.
     - In `BodyIndexBuilder.StepHeaderRepair`, cleared unopenable or deleted items when `GetItemFromID` fails so missing items no longer block verification completion.
     - In `StepSetup` and `StepReconcile`, added logic to skip inaccessible non-default stores without indexed rows, and added `ReconcileBodyMetadataParitySync` to restore exact row parity between `body_fts` and `mail_meta`.

3. **Smart Reply with Attachment(s) — Elimination of Spurious `.emz` / `.wmz` Metafiles:**
   - **Gateway Stripped Content-ID Fallback:** When security gateways or message hygiene scanners prepend inspection notices (e.g. `[WARNING: ATTACHMENT UNSCANNED]`) and strip `PR_ATTACH_CONTENT_ID` (`0x3712001F`) from the attachment table, the content ID was left empty. Updated `ReplyWithAttachments.ImageResourceMatches` and `MailSearchEngine` so `cid:<filename>@<content-id>` references in HTML fallback to matching `<filename>`.
   - **Office Metafile Classification:** Added `.emz`, `.wmz`, `.emf`, and `.wmf` to `InlineImageExtensions` and expanded safety rules to ensure compressed Office vector drawings, equations, and shape graphics are strictly classified as inline body resources and never copied as user attachments.
   - **Preserved VML Conditional Comments:** Updated HTML preprocessing in `ReplyWithAttachments.cs` to preserve downlevel-hidden conditional comment blocks (`<!--(?!\[if\b)[\s\S]*?-->`) so `<v:imagedata>` and `<v:fill>` tags and their namespace attributes (such as `o:href`) remain visible for inline inspection.

4. **Advanced Search & Find Related — Corporate Bracketed Names & Directory Aliases:**
   - **Bracket & Delimiter Token Sanitization:** When a corporate sender name (e.g. `Name [ Company - Dept ]`) was placed in search fields, space tokenization previously split brackets into standalone `[` and `]` tokens, failing `ConversationPersonResolver.PersonTargetMatchesToken` when an email only stored the bare human name or SMTP address. Added `CleanPersonQueryToken` to strip standalone bracket and punctuation tokens across `ConversationPersonResolver`, `MailSearchEngine`, `BodyIndex`, and `TaskRuleEvaluator`.
   - **Multi-Word Sender Alternative Matching:** Updated `MailSearchEngine.PersonFieldMatchesInclude` so `FromAlternatives` are evaluated whenever `neg.Count == 0`, eliminating an issue where alternatives were previously checked only when positive tokens were `pos.Count <= 1`.
   - **Suffix Stripping & Two-Way Resolution:** Added `StripBracketSuffix(name)` to `ResolveQueryPersonAlternatives` and `ResolveSenderSearchTerms` so bracketed display names, bare names, SMTP addresses, and Exchange X500 directory aliases (`/O=ORGANIZATION/...`) cross-match seamlessly across all search scopes.

5. **Hashtag Groups, Single Symbol `#` Matching & Angle-Bracket Contact Syntax:**
   - **Single-Symbol `#` Query Preservation:** Previously, entering `#` in the `To` or `From` field stripped the symbol during alphanumeric cleanup, producing an empty token list that bypassed SQL filters and returned all mailbox emails. `CleanPersonQueryToken` now retains `#`, and `BodyIndex.AppendPersonFilterSql` applies fallback literal matching (`instr(lower(primaryCol), lower($raw)) > 0`) so single-symbol and hashtag searches return only messages containing the symbol.
   - **Semicolon-Separated Multi-Recipient Splitting:** Single-token queries (`pos.Count > 0`) in `MailSearchEngine.PersonFieldMatchesInclude` now evaluate each semicolon-separated recipient capsule individually instead of treating the entire recipient list as a single bracketed person name and truncating after the first tag.
   - **Hashtag Distribution Group & Email Resolution:** Removed the `LIMIT 3000` cap on directory loading and eliminated the restrictive domain-omission check in `ResolveRecipientAlternatives`. Hashtag email addresses (e.g. `#group@domain.com` or `#group@domain`) and their display names (e.g. `#Group Name`) are registered in `_hashGroupDirectory` and `_emailToDisplayName`, allowing searches by email address or display name to match all group messages interchangeably.
   - **Composite Contact Query Decomposition (`DisplayName <email@domain>`):** Pasting contacts directly from Outlook in composite format previously required both the display name words and the angle-bracketed email address to appear literally in the same text field. `ConversationPersonResolver`, `BodyIndex`, and `MailSearchEngine` now decompose composite queries into display name tokens and email address alternatives, matching either one positively.

6. **Search Query Parser — Subjects Containing English "not" or Starting with "NOT ":**
   - **Uppercase-Only Boolean NOT:** Updated `QueryParser.Parse` so only uppercase `"NOT "` acts as the boolean negation operator, while lowercase `"not "` and titlecase `"Not "` (e.g. *"Issue is not resolved"*, *"Not assigned"*) are parsed as ordinary search words.
   - **Literal Subject Prefix Protection:** Added `TreatSubjectNegationAsLiteral` and `BaseSubjectForNegationCheck` across `MailSearchEngine`, `BodyIndex`, and `TaskRuleEvaluator` so subjects beginning with `"NOT "` (even after `Re:` / `Fw:`) are treated as positive search terms, preventing messages from mistakenly excluding themselves when searching by subject or using **Find Related → Messages in Conversation**.

7. **Hyphenated Subjects — Space-Dash Disambiguation in Multi-Word Titles:**
   - **Title Substring & Hyphen Context Preservation:** In multi-word subjects containing a space before a dash (e.g. `Project-ABC -Subgroup`), the dash-prefixed token was previously parsed as a negation filter (`-Subgroup` = exclude). Updated `TreatSubjectNegationAsLiteral` and `HasSubject` so that when a query matches the subject substring or when preceding tokens contain hyphens, the dash-prefixed token is matched positively while preserving short explicit exclusions (e.g., `audit -draft`).

8. **Task Tracker Multi-Recipient List Isolation:**
   - **Address Entry Token Scoping:** Updated `TaskRuleEvaluator.AddressEntryMatchesTargets` to split semicolon-separated recipient strings into individual recipient entities before evaluating token rules, preventing tokens from one recipient from interfering with word matching for other recipients on the same email.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.2.1 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۲.۱ شامل مجموعه‌ای از بهبودهای اساسی پایداری، رفع ایرادات چیدمان پیش‌نمایش، ارتقای دقت موتور جست‌وجو و اصلاح هوشمند پیوست‌ها است. این نسخه به طور ویژه مشکلات <strong>نمایش نصفه و فریز شدن پنل پیش‌نمایش در جابه‌جایی میان Task Tracker و Advanced Search</strong>، <strong>خطای <code>0x80004005</code> در اتصال فایل‌های PST و توقف طولانی وضعیت اعتبارسنجی سربرگ‌ها</strong>، <strong>عدم نمایش نتایج جست‌وجو برای نام‌های سازمانی دارای براکت</strong>، <strong>پیوست شدن ناخواسته فایل‌های گرافیکی آفیس (<code>.emz</code> و <code>.wmz</code>) در عملیات Reply with Attachment</strong>، <strong>خطاهای جست‌وجوی گروه‌های هشتگ‌دار و نویسه تنها (<code>#</code>)</strong> و <strong>موارد ظریف تحلیلگر پرس‌وجو در ممیزی پایگاه‌داده</strong> را برطرف می‌کند.</p>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>ردیاب وظایف و جست‌وجوی ایمیل — رفع مشکل نمایش نصفه پیش‌نمایش و فریز شدن کادر سمت راست:</strong>
      <ul>
        <li><strong>همگام‌سازی سلسله‌مراتب پنجره‌های بومی اکتیوایکس:</strong> کنترل WebBrowser در WinForms شامل سه لایه پنجره فرزند بومی ویندوز (<code>Shell Embedding</code> ← <code>Shell DocObject View</code> ← <code>Internet Explorer_Server</code>) است. در مواردی که هر دو پنجره <code>TaskTrackerForm</code> و <code>MailSearchPanel</code> از کنترل‌های وب روی یک نخ رابط کاربری استفاده می‌کردند یا تغییرات تقسیم‌کننده در هنگام ناوبری با <code>DocumentText</code> رخ می‌داد، هندل‌های داخلی با اندازه کنترل اصلی ناهماهنگ شده و سمت راست پنل با پیکسل‌های قبلی بدون رندر باقی می‌ماند.</li>
        <li><strong>محاسبه مجدد و رسم دوباره تمام هندل‌ها (HWND Tree):</strong> پیاده‌سازی متد <code>WindowPositionHelper.SyncWebBrowserBounds</code> که ابعاد مرورگر را با پنل والد و هدر همگام کرده، تمام پنجره‌های فرزند را با <code>EnumChildWindows</code> و <code>SetWindowPos</code> به عرض و ارتفاع ۱۰۰٪ مقید می‌کند و کل درخت پنجره‌ها را با <code>RedrawWindow</code> بازسازی می‌نماید.</li>
        <li><strong>اتصال به رویدادهای چرخه حیات:</strong> اتصال این همگام‌سازی در <code>MailSearchPanel</code> و <code>TaskTrackerForm</code> به رویدادهای <code>NavigatePreview</code>، <code>DocumentCompleted</code>، <code>SizeChanged</code>، <code>VisibleChanged</code> و تغییر اندازه پنل‌ها.</li>
      </ul>
    </li>
    <li><strong>اتصال آرشیو و نگهداری ایندکس — رفع خطای <code>0x80004005</code> و توقف وضعیت اعتبارسنجی (Verification Pending):</strong>
      <ul>
        <li><strong>اتصال پایدار آرشیو و مدیریت خطای 0x80004005:</strong> حذف اتصال همزمان اضافه در <code>SmartArchive.BeginArchivePreparation</code>. در مواردی که یک فایل PST فصلی دارای قفل موقت یا سربرگ آسیب‌دیده با خطای <code>0x80004005</code> (عدم امکان بارگذاری فایل دیتا) بود، افزونه اکنون این مسیرها را در طول نشست ثبت کرده (<code>_unmountableSeasonPstPaths</code>)، فایل‌های صفر بایتی یا غیرقابل بارگذاری را در آماده‌سازی رد می‌کند و در <code>ResolveSeasonPstWithRoom</code> و <code>MoveOneAtIndex</code> به طور خودکار به جلد بعدی (مانند <code>&lt;Season&gt;-2.pst</code>) منتقل می‌شود.</li>
        <li><strong>رفع توقف دائمی وضعیت بررسی سربرگ‌ها:</strong>
          <ul>
            <li>در متد <code>BodyIndex.MarkHeaderCandidateVerifiedSync</code>، پرچم <code>headers_full:&lt;rid&gt;</code> در متادیتا ثبت می‌شد اما ردیف متناظر از <code>header_repair_pending</code> حذف نمی‌شد که باعث می‌شد شرط وجود کاندیدا همواره برقرار بماند؛ این نقص برطرف شد.</li>
            <li>در <code>BodyIndexBuilder.StepHeaderRepair</code>، خطای <code>GetItemFromID</code> روی پیام‌های حذف‌شده یا غیرقابل دسترس شناسایی شده و وضعیت معلق آنها پاک می‌شود تا مانع از تکمیل اعتبارسنجی نشوند.</li>
            <li>در <code>StepSetup</code> و <code>StepReconcile</code>، ذخیره‌سازهای غیرپیش‌فرض و غیرقابل دسترس که فاقد ردیف ایندکس هستند نادیده گرفته می‌شوند، و متد <code>ReconcileBodyMetadataParitySync</code> همخوانی دقیق ردیف‌های <code>body_fts</code> و <code>mail_meta</code> را برقرار می‌سازد.</li>
          </ul>
        </li>
      </ul>
    </li>
    <li><strong>پاسخ همراه با پیوست‌ها (Reply with Attachment) — حذف قطعی فایل‌های گرافیکی ناخواسته آفیس (<code>.emz</code> و <code>.wmz</code>):</strong>
      <ul>
        <li><strong>تطبیق شناسه محتوا پس از حذف توسط گیت‌وی‌های ایمیل:</strong> در ایمیل‌هایی که سامانه‌های بازرسی امنیتی (مانند هشدارهای اسکن) ویژگی <code>PR_ATTACH_CONTENT_ID</code> (کد <code>0x3712001F</code>) را از جدول پیوست‌ها حذف می‌کنند، متدهای <code>ReplyWithAttachments.ImageResourceMatches</code> و <code>MailSearchEngine</code> ارتقا یافتند تا ارجاعات <code>cid:&lt;filename&gt;@&lt;content-id&gt;</code> در متن HTML با نام فایل متناظر تطبیق داده شوند.</li>
        <li><strong>گسترش طبقه‌بندی متاتگ‌های آفیس:</strong> افزودن پسوندهای <code>.emz</code>، <code>.wmz</code>، <code>.emf</code> و <code>.wmf</code> به <code>InlineImageExtensions</code> و اعمال قانون ایمنی قطعی جهت تلقی این فایل‌ها به عنوان منابع گرافیکی درون‌متنی و جلوگیری از کپی آنها به عنوان فایل پیوست.</li>
        <li><strong>حفظ کامنت‌های شرطی حاوی VML:</strong> اصلاح پیش‌پردازش متن HTML در <code>ReplyWithAttachments.cs</code> جهت حفظ بلوک‌های شرطی <code>&lt;!--[if gte vml 1]&gt;...&lt;![endif]--&gt;</code> تا تگ‌های <code>&lt;v:imagedata&gt;</code> و <code>&lt;v:fill&gt;</code> و ویژگی‌های با پیشوند اختصاصی (مانند <code>o:href</code>) برای شناسایی پیوست‌های درون‌متنی در دسترس بمانند.</li>
      </ul>
    </li>
    <li><strong>جست‌وجوی پیشرفته و پیام‌های مرتبط — پشتیبانی از نام‌های سازمانی دارای براکت و آدرس‌های دایرکتوری:</strong>
      <ul>
        <li><strong>پالایش توکن‌های براکت و علائم نگارشی:</strong> هنگام قرار گرفتن نام سازمانی (مانند <code>Name [ Company - Dept ]</code>) در فیلد فرستنده، تفکیک با فاصله براکت‌ها را به توکن‌های جداگانه <code>[</code> و <code>]</code> تبدیل می‌کرد که باعث شکست تطبیق با نام‌های ساده یا آدرس SMTP می‌شد. متد <code>CleanPersonQueryToken</code> اضافه شد تا علائم نگارشی و براکت‌های تنها در تمام بخش‌های تطبیق حذف شوند.</li>
        <li><strong>تطبیق گزینه‌های فرستنده در نام‌های چندکلمه‌ای:</strong> متد <code>MailSearchEngine.PersonFieldMatchesInclude</code> اصلاح شد تا ارزیابی <code>FromAlternatives</code> در تمام موارد بدون شرط نفی (<code>neg.Count == 0</code>) انجام پذیرد، نه صرفاً در مواردی که تعداد توکن‌های مثبت ۱ یا کمتر بود.</li>
        <li><strong>حذف هوشمند پسوند و تطبیق دوجانبه:</strong> استفاده از <code>StripBracketSuffix</code> در <code>ResolveQueryPersonAlternatives</code> و <code>ResolveSenderSearchTerms</code> جهت تطبیق یکپارچه میان نام کامل سازمانی، نام ساده، آدرس SMTP و آدرس‌های دایرکتوری Exchange X500 در تمامی محدوده‌های جست‌وجو.</li>
      </ul>
    </li>
    <li><strong>پشتیبانی از گروه‌های هشتگ‌دار، نویسه تنها (<code>#</code>) و ترکیب نام و آدرس (<code>Name &lt;email&gt;</code>):</strong>
      <ul>
        <li><strong>حفظ نویسه <code>#</code> در جست‌وجو:</strong> قبلاً وارد کردن علامت <code>#</code> در فیلدهای گیرنده به دلیل فیلترسازی الفبایی-عددی حذف شده و تمام ایمیل‌های صندوق بدون شرط بازگردانده می‌شدند. اکنون متد <code>CleanPersonQueryToken</code> نویسه <code>#</code> را حفظ کرده و با پشتیبانی مستقیم در لایه پایگاه‌داده (<code>instr</code>) صرفاً ایمیل‌های دارای این علامت بازیابی می‌شوند.</li>
        <li><strong>تفکیک فهرست گیرندگان دارای سمی‌کالن در جست‌وجوهای تک‌توکنی:</strong> متد <code>PersonFieldMatchesInclude</code> اکنون در پرس‌وجوهای تک‌توکنی (<code>pos.Count &gt; 0</code>) کپسول‌های گیرندگان را به تفکیک سمی‌کالن ارزیابی می‌کند تا فهرست‌های چندگیرنده‌ای به اشتباه به عنوان یک شخص واحد و بریده‌شده تلقی نگردند.</li>
        <li><strong>ارتباط دوسویه نام نمایشی و آدرس ایمیل گروه‌های هشتگ‌دار:</strong> با حذف محدودیت ۳۰۰۰ ردیفی و اصلاح شرط بررسی دامنه در <code>ResolveRecipientAlternatives</code>، آدرس‌های ایمیل گروه‌ها (مانند <code>#group@domain.com</code>) و نام نمایشی آنها (مانند <code>#Group Name</code>) به طور خودکار به یکدیگر نگاشت شده و جست‌وجوی هر یک، تمامی ایمیل‌های مرتبط را بازمی‌گرداند.</li>
        <li><strong>تجزیه هوشمند ترکیب مخاطب (<code>DisplayName &lt;email&gt;</code>):</strong> هنگام قرار دادن مخاطبان با ساختار براکت شکسته از اوت‌لوک، سیستم به طور خودکار نام نمایشی و آدرس ایمیل را تفکیک کرده و تطبیق مثبت هر یک را به عنوان نتیجه معتبر می‌پذیرد.</li>
      </ul>
    </li>
    <li><strong>تحلیلگر پرس‌وجو — اصلاح جست‌وجوی عناوینی که شامل "not" انگلیسی هستند یا با "NOT " شروع می‌شوند:</strong>
      <ul>
        <li><strong>عملگر نفی صرفاً با حروف بزرگ:</strong> اصلاح <code>QueryParser.Parse</code> به گونه‌ای که تنها کلمه <code>"NOT "</code> با حروف بزرگ به عنوان عملگر نفی منطقی شناخته شود و عبارات <code>"not "</code> یا <code>"Not "</code> (مانند عناوین حاوی "is not working" یا "Not assigned") به عنوان کلمات متنی عادی جست‌وجو شوند.</li>
        <li><strong>حفاظت از عناوینی که با "NOT " شروع می‌شوند:</strong> متدهای <code>TreatSubjectNegationAsLiteral</code> و <code>BaseSubjectForNegationCheck</code> در موتور جست‌وجو، ایندکس و ارزیابی قوانین وظایف به گونه‌ای به‌روزرسانی شدند که عناوینی که با عبارت "NOT " آغاز می‌شوند (حتی پس از Re: یا Fw:) به عنوان کلمات مثبت جست‌وجو شوند تا ایمیل‌ها در جست‌وجوی موضوعی یا اجرای «پیام‌های مرتبط در مکالمه» خودشان را نفی نکنند.</li>
      </ul>
    </li>
    <li><strong>عناوین خط‌تیره‌دار — تفکیک خط‌تیره در موضوعات چندکلمه‌ای:</strong>
      <ul>
        <li><strong>حفظ مفهوم خط‌تیره در متن عنوان:</strong> در موضوعاتی که پیش از خط‌تیره فاصله وجود دارد (مانند ترکیب کد پروژه و زیرگروه)، توکن خط‌تیره‌دار قبلاً به اشتباه به عنوان فیلتر استثنا (Exclude) تفسیر می‌شد. با اصلاح <code>TreatSubjectNegationAsLiteral</code> و <code>HasSubject</code>، این موارد به عنوان تطبیق مثبت عنوان تحلیل می‌شوند و تنها عبارات استثنای واقعی تفکیک می‌گردند.</li>
      </ul>
    </li>
    <li><strong>تفکیک فهرست‌های چندگیرنده‌ای در قوانین خودکار ردیاب وظایف (Task Tracker):</strong>
      <ul>
        <li>متد <code>TaskRuleEvaluator.AddressEntryMatchesTargets</code> اصلاح شد تا فهرست‌های گیرندگان دارای سمی‌کالن ابتدا به تک‌تک اشخاص تفکیک شده و سپس شرایط هر شخص به طور مستقل ارزیابی شود تا توکن‌های افراد مختلف در یک ایمیل با یکدیگر تداخل پیدا نکنند.</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب برای کاربر فعلی انجام می‌شود و به دسترسی مدیر نیاز ندارد. کاربران فعلی می‌توانند نسخه ۱.۲.۱ را مستقیماً روی نسخه موجود نصب کنند و نیازی به حذف نسخه قبلی نیست.</p>
</div>
