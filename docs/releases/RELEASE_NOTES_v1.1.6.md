<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.6

Version 1.1.6 focuses on **lower background CPU usage**, **faster first searches in Advanced Search**, **more faithful email previews**, **reliable attachment actions**, and **a more responsive Task Tracker** for large mailboxes.

> This is an older release. Install the [latest version](https://github.com/ParhamGhafouri/EmailTools/releases/latest) for current fixes and safety improvements.

### Highlights (Ordered by Priority)

1. **Advanced Search First-Search Responsiveness:**
   - Fixed the lengthy pause when the first filtered search replaced a large initial result list, including after closing and reopening Advanced Search.
   - Improved result-list updates when narrowing a search from tens of thousands of messages to a small set of matches.
   - Moved search filtering and sorting off the interface thread, with cancellation and protection against outdated results replacing a newer search.
   - Preserved large initial result lists while improving responsiveness when users enter or change search criteria.

2. **Reduced Background CPU Usage & Unnecessary Work:**
   - Prevented repeated background scan requests when the index is already complete and no new work is required.
   - Reduced repeated status calculations and duplicate search processing.
   - Added bounded search-result caching to reuse recent results while limiting memory consumption.

3. **Corrected Email Preview Layout & Fonts:**
   - Removed preview formatting that stretched tables, signatures, and images across the available width.
   - Preserved message-defined dimensions and font choices, with suitable fallbacks when a requested font is unavailable.
   - Restored horizontal and vertical scrolling for wide tables and long messages.
   - Improved preview caching so cached messages retain their header and attachment information.

4. **Attachment Copy & Save Reliability:**
   - Corrected attachment recognition so genuine files remain available even when they contain a content ID, while inline signature images stay excluded from normal attachment actions.
   - Fixed attachment save-dialog ownership and the Save As / Save All Attachments workflows.
   - Improved file-copy clipboard handling for pasting attachments into a new Outlook message. Paste into the message body to insert the copied file.
   - Ensured attachment actions use the message currently displayed in the preview, with visible errors when an operation cannot complete.

5. **Task Tracker Responsiveness & Safer Preview Handling:**
   - Moved rule scans, task-list filtering, and sorting to background work, with cancellation and protection against outdated scan results.
   - Improved large task-list updates and rule-save completion handling.
   - Corrected dispatch of background notifications to the interface thread.
   - Added ordered background task saves with recovery of pending changes, and moved live task processing and manual tracking database work off the interface thread.
   - Reduced repeated body-rule queries and preserved user notes during reply-driven status updates.
   - Prevented temporary message-preview failures from removing indexed messages or tracked tasks.
   - Corrected linked-task cleanup before Task Tracker is opened and across archive mailboxes; pending task recovery now respects confirmed email deletions.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users can install v1.1.6 directly over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۱.۶ بر <strong>کاهش مصرف پردازنده در پس‌زمینه</strong>، <strong>بهبود سرعت اولین جست‌وجو در Advanced Search</strong>، <strong>اصلاح نمایش ایمیل‌ها</strong>، <strong>رفع مشکلات عملیات پیوست‌ها</strong> و <strong>روان‌تر شدن Task Tracker</strong> در صندوق‌های پستی بزرگ تمرکز دارد.</p>

  <blockquote>این نسخه قدیمی است. برای دریافت اصلاحات و بهبودهای ایمنی فعلی، <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest">جدیدترین نسخه</a> را نصب کنید.</blockquote>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>رفع مکث اولین جست‌وجو در Advanced Search:</strong>
      <ul>
        <li>رفع مکث طولانی هنگام جایگزینی فهرست اولیه بزرگ با نتایج اولین جست‌وجوی فیلترشده، از جمله پس از بستن و باز کردن مجدد پنجره جست‌وجو.</li>
        <li>بهبود به‌روزرسانی جدول هنگام محدود کردن ده‌ها هزار پیام به تعداد کمی نتیجه.</li>
        <li>انتقال فیلتر و مرتب‌سازی جست‌وجو به پس‌زمینه، همراه با امکان لغو و جلوگیری از جایگزینی نتایج جدید با نتایج قدیمی.</li>
        <li>حفظ فهرست اولیه بزرگ و بهبود پاسخ‌گویی هنگام وارد کردن یا تغییر شرایط جست‌وجو.</li>
      </ul>
    </li>
    <li><strong>کاهش مصرف پردازنده و پردازش‌های غیرضروری:</strong>
      <ul>
        <li>جلوگیری از درخواست‌های تکراری اسکن در پس‌زمینه پس از تکمیل ایندکس، زمانی که کار جدیدی وجود ندارد.</li>
        <li>کاهش محاسبات تکراری وضعیت و پردازش‌های اضافی جست‌وجو.</li>
        <li>استفاده مجدد از نتایج اخیر با کش محدود برای کنترل مصرف حافظه.</li>
      </ul>
    </li>
    <li><strong>اصلاح چیدمان و فونت پیش‌نمایش ایمیل:</strong>
      <ul>
        <li>حذف قالب‌بندی‌هایی که جدول‌ها، امضاها و تصاویر را در عرض پنجره کشیده می‌کردند.</li>
        <li>حفظ ابعاد و فونت‌های تعریف‌شده در پیام و استفاده از فونت جایگزین مناسب در صورت نبود فونت اصلی.</li>
        <li>اصلاح اسکرول افقی و عمودی برای جدول‌های عریض و پیام‌های طولانی.</li>
        <li>بهبود کش پیش‌نمایش برای حفظ اطلاعات سربرگ و پیوست‌های پیام.</li>
      </ul>
    </li>
    <li><strong>رفع مشکلات کپی و ذخیره پیوست‌ها:</strong>
      <ul>
        <li>اصلاح تشخیص پیوست‌های واقعی، حتی در صورت داشتن Content ID، و جدا نگه داشتن تصاویر درون‌متنی امضا از عملیات معمول پیوست‌ها.</li>
        <li>اصلاح ارتباط پنجره‌های ذخیره با پنجره اصلی و عملکرد گزینه‌های Save As و Save All Attachments.</li>
        <li>بهبود کپی فایل در کلیپ‌بورد برای درج پیوست در ایمیل جدید اوت‌لوک؛ برای درج فایل کپی‌شده، عملیات Paste را داخل بدنه پیام انجام دهید.</li>
        <li>اجرای عملیات پیوست روی پیام نمایش‌داده‌شده در پیش‌نمایش و نمایش خطا در صورت ناموفق بودن عملیات.</li>
      </ul>
    </li>
    <li><strong>بهبود پاسخ‌گویی Task Tracker و ایمنی پیش‌نمایش:</strong>
      <ul>
        <li>انتقال اسکن قوانین، فیلتر و مرتب‌سازی فهرست وظایف به پس‌زمینه، همراه با لغو و جلوگیری از نمایش نتایج اسکن قدیمی.</li>
        <li>بهبود به‌روزرسانی فهرست‌های بزرگ و تکمیل عملیات ذخیره قوانین.</li>
        <li>اصلاح ارسال اعلان‌های پس‌زمینه به رشته رابط کاربری.</li>
        <li>ذخیره ترتیبی وظایف در پس‌زمینه همراه با بازیابی تغییرات معلق و انتقال عملیات پایگاه‌داده مربوط به پیام‌های جدید و ثبت دستی وظایف از رشته رابط کاربری.</li>
        <li>کاهش پرس‌وجوهای تکراری قوانین متن پیام و حفظ یادداشت‌های کاربر هنگام تغییر وضعیت بر اساس پاسخ دریافتی.</li>
        <li>جلوگیری از حذف پیام‌های ایندکس‌شده یا وظایف ثبت‌شده بر اثر خطاهای موقت در باز کردن پیش‌نمایش پیام.</li>
        <li>اصلاح پاک‌سازی وظیفه مرتبط با ایمیل حتی پیش از باز شدن Task Tracker و در صندوق‌های آرشیو؛ بازیابی وظایف معلق اکنون حذف تأییدشده ایمیل را رعایت می‌کند.</li>
      </ul>
    </li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.6 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>
