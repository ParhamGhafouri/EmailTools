<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.9

Version 1.1.9 focuses on **search results staying in sync with the selected conditions**, **complete matching across mailbox and archive scopes**, and **consistent attachment detection and filename searches**.

> This is an older release. Install the [latest version](https://github.com/ParhamGhafouri/EmailTools/releases/latest) for current fixes and safety improvements.

### Highlights (Ordered by Priority)

1. **Advanced Search & Task Tracker Filter Refresh:**
   - Prevented an older search from replacing results after its conditions have changed.
   - Added automatic recovery when a filter change is missed, so changing or removing conditions no longer depends on closing and reopening the window.
   - Advanced Search now shows **Searching...** when the criteria change instead of continuing to present the previous result count as current. A stalled request receives one automatic retry.
   - Applied filter-state verification to Task Tracker, including search text, exclusions, status, category and priority.
   - Fixed live refresh losing an index change that arrived during search completion. Recipient-only changes now refresh the displayed rows too.
   - Prevented a dropped search-completion callback from leaving live indexing paused, and stopped automatic refreshes from repeatedly pausing indexing on its own changes.
   - Kept bounded indexing and folder-event discovery running while either results window is open. Outlook moves and deletions now queue reconciliation of the affected folder.
   - Subscribed newly created folders to live updates without requiring an Outlook restart.
   - Invalidated the affected preview when Outlook edits a message, so cached headers, body and attachment chips refresh with the results.
   - Corrected Task Tracker deletion handling when Outlook changes a message identifier on its way to Deleted Items, while preserving task notes during ordinary moves.
   - Fixed Task Tracker keeping the old folder after a move. Moved messages, including messages moved into an archive, now stay linked to their task and notes. A copied message no longer takes over the original message's task.
   - Corrected live event handling to avoid prematurely releasing message objects still used by Outlook or another subscriber.

2. **Search Matching & Archive Scope Accuracy:**
   - Repaired truncated message headers from Outlook table reads, restoring matches near the end of long **To/Cc** recipient lists. Full header reads run in small background batches without rereading message bodies.
   - Aligned database filtering and final result checks for sender names, punctuation, Unicode case matching, and common Persian/Arabic letter variants.
   - Applied all remaining conditions before limiting body-search results, preventing qualifying messages from being dropped from combined searches.
   - Included the subfolder path in search-cache identity and corrected matching at subfolder boundaries.
   - Prevented a saved search for an unavailable archive or folder from silently switching to a different saved location.

3. **Attachment Filters & Filename Searches:**
   - Unified indexing with the attachment detection used by mailbox actions and message previews. Genuine files named `image001.png`, `Signature.png`, or similar are retained; rendered inline images remain excluded.
   - Distinguished a message known to contain only inline images from one whose attachment information has not yet been read. Failed reads remain eligible for retry.
   - Corrected legacy attachment-cache entries without rebuilding stored message bodies, and completed attachment repair in small background batches instead of processing only one page per maintenance cycle.
   - Marked attachment-filter results as partial while required attachment information is still being indexed.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.1.9 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۱.۹ بر <strong>هماهنگ ماندن نتایج با شرط‌های انتخاب‌شده</strong>، <strong>دقت جست‌وجو در صندوق‌های پستی و آرشیوها</strong> و <strong>یکسان‌سازی تشخیص پیوست و جست‌وجوی نام فایل‌ها</strong> تمرکز دارد.</p>

  <blockquote>این نسخه قدیمی است. برای دریافت اصلاحات و بهبودهای ایمنی فعلی، <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest">جدیدترین نسخه</a> را نصب کنید.</blockquote>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>به‌روزرسانی فیلترها در Advanced Search و Task Tracker:</strong>
      <ul>
        <li>جلوگیری از جایگزین شدن نتایج توسط جست‌وجوی قدیمی پس از تغییر شرط‌ها.</li>
        <li>بازیابی خودکار تغییر فیلترهایی که اعلان آن‌ها از دست رفته است؛ تغییر یا حذف شرط‌ها دیگر به بستن و باز کردن دوباره پنجره وابسته نیست.</li>
        <li>نمایش <strong>Searching...</strong> پس از تغییر شرط‌ها، به‌جای نمایش شمارنده قبلی به‌عنوان نتیجه فعلی، و یک تلاش مجدد خودکار برای درخواست متوقف‌شده.</li>
        <li>بررسی وضعیت واقعی فیلترهای Task Tracker شامل متن جست‌وجو، استثناها، وضعیت، دسته‌بندی و اولویت.</li>
        <li>رفع از دست رفتن تغییر ایندکس هنگام تکمیل جست‌وجو و به‌روزرسانی ردیف‌ها حتی زمانی که فقط گیرندگان پیام تغییر کرده‌اند.</li>
        <li>جلوگیری از متوقف ماندن ایندکس آنی پس از از دست رفتن پاسخ جست‌وجو و جلوگیری از توقف‌های مکرر ایندکس بر اثر به‌روزرسانی خودکار نتایج.</li>
        <li>ادامه ایندکس در دسته‌های محدود و ثبت رویدادهای پوشه هنگام باز بودن پنجره نتایج؛ جابه‌جایی و حذف پیام در اوت‌لوک اکنون بررسی پوشه مربوطه را در صف قرار می‌دهد.</li>
        <li>ثبت رویدادهای پوشه‌های تازه‌ساخته‌شده برای به‌روزرسانی آنی، بدون نیاز به راه‌اندازی مجدد اوت‌لوک.</li>
        <li>بی‌اعتبار کردن پیش‌نمایش همان پیام پس از ویرایش در اوت‌لوک، برای به‌روزرسانی سربرگ، متن و نمایش پیوست‌ها همراه با نتایج.</li>
        <li>اصلاح حذف وظیفه در Task Tracker زمانی که شناسه پیام در انتقال به Deleted Items تغییر می‌کند، همراه با حفظ یادداشت‌های وظیفه در جابه‌جایی عادی پیام.</li>
        <li>رفع باقی ماندن پوشه قبلی در Task Tracker پس از جابه‌جایی پیام. پیام‌های جابه‌جاشده، از جمله پیام‌های منتقل‌شده به بایگانی، اکنون به وظیفه و یادداشت‌های خود متصل می‌مانند و کپی یک پیام دیگر وظیفه پیام اصلی را تصاحب نمی‌کند.</li>
        <li>اصلاح مدیریت رویدادهای آنی برای جلوگیری از آزادسازی زودهنگام شیء پیامی که اوت‌لوک یا دریافت‌کننده دیگری هنوز از آن استفاده می‌کند.</li>
      </ul>
    </li>
    <li><strong>دقت تطبیق نتایج و محدوده آرشیو:</strong>
      <ul>
        <li>ترمیم سربرگ‌های کوتاه‌شده در خواندن جدولی اوت‌لوک و بازیابی نتایج مربوط به نام‌های انتهای فهرست‌های طولانی <strong>To/Cc</strong>؛ خواندن کامل سربرگ‌ها در دسته‌های کوچک پس‌زمینه و بدون خواندن دوباره متن پیام انجام می‌شود.</li>
        <li>هماهنگ‌سازی فیلتر پایگاه‌داده و بررسی نهایی نتایج برای نام فرستنده، علائم نگارشی، حروف بزرگ و کوچک یونیکد و شکل‌های رایج حروف فارسی و عربی.</li>
        <li>اعمال همه شرط‌های باقی‌مانده پیش از محدود کردن تعداد نتایج جست‌وجوی متن پیام، برای جلوگیری از حذف پیام‌های منطبق در جست‌وجوهای ترکیبی.</li>
        <li>در نظر گرفتن مسیر زیرپوشه در کش جست‌وجو و اصلاح تطبیق مرز زیرپوشه‌ها.</li>
        <li>جلوگیری از تغییر پنهانی محدوده جست‌وجوی ذخیره‌شده به آرشیو یا پوشه‌ای دیگر، زمانی که محل اصلی در دسترس نیست.</li>
      </ul>
    </li>
    <li><strong>فیلتر پیوست و جست‌وجوی نام فایل:</strong>
      <ul>
        <li>یکسان‌سازی تشخیص پیوست در ایندکس، عملیات صندوق پستی و پیش‌نمایش پیام. فایل‌های واقعی با نام‌هایی مانند <code>image001.png</code> و <code>Signature.png</code> حفظ می‌شوند و تصاویر نمایش‌داده‌شده در متن همچنان کنار گذاشته می‌شوند.</li>
        <li>تفکیک پیام دارای تصاویر درون‌متنی از پیامی که اطلاعات پیوست آن هنوز خوانده نشده است؛ خواندن‌های ناموفق برای تلاش مجدد باقی می‌مانند.</li>
        <li>اصلاح کش قدیمی پیوست‌ها بدون بازسازی متن پیام‌ها و تکمیل ترمیم اطلاعات پیوست در دسته‌های کوچک پس‌زمینه، به‌جای پردازش فقط یک صفحه در هر چرخه نگهداری.</li>
        <li>نمایش وضعیت ناقص بودن نتایج فیلتر پیوست تا زمان تکمیل اطلاعات موردنیاز در ایندکس.</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب برای کاربر فعلی انجام می‌شود و به دسترسی مدیر نیاز ندارد. کاربران فعلی می‌توانند نسخه ۱.۱.۹ را مستقیماً روی نسخه موجود نصب کنند و نیازی به حذف نسخه قبلی نیست.</p>
</div>
