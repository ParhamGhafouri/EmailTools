<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.8

This release introduces powerful new exclusion filters, significant improvements to full-text body search accuracy, UI polishing, and under-the-hood engine upgrades for better performance.

### Highlights

- **Exclude Filters:** Advanced Search now fully supports excluding specific words or phrases. You can use the newly added dedicated exclusion textboxes in the UI to precisely filter out unwanted results across the From, To, Subject, and Body fields.
- **Body Search Improvements:** The live full-text indexing engine has been upgraded to properly process complex exclusions, drastically improving the precision of body text searches.
- **UI & Layout Fixes:** 
  - **Responsive Grid:** The "Subject" column in the search results now automatically stretches to fill empty space when the window is maximized.
  - **Modernized Preview:** The empty reading pane has been redesigned with a crisp SVG envelope matching Outlook's native design, with improved vertical spacing.
  - **Alignment:** The "Saved Searches" dropdown label was realigned to perfectly match the padding of the other search fields.
- **Engine & Performance Upgrades:** Upgraded the native database engine to SQLite v3.53.4, bringing the latest FTS5 query planner optimizations. The ADO.NET provider (`Microsoft.Data.Sqlite.Core`) was also upgraded to v10.0.11, significantly reducing background memory allocations when loading thousands of results.
- **False Positives in Attachment Search:** Removed the experimental "Attachment Contains" (filename wildcard) search filter, as relying purely on Exchange DASL queries for filename matching caused severe false positives. You can still accurately filter by the *presence* of attachments (Yes/No/Any).
- **SmartScreen / Windows Defender:** Added missing Authenticode code-signing to the core `EmailTools.dll` assembly during the build pipeline, preventing sporadic SmartScreen warnings when the installer extracts the payload.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users should install v1.0.8 over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه شامل قابلیت جدید فیلترهای استثنا (Exclude)، بهبود چشمگیر دقت جستجو در متن ایمیل‌ها، اصلاحات ظاهری و ارتقای اساسی موتور دیتابیس می‌باشد.</p>

  <h3>ویژگی‌های برجسته</h3>
  <ul>
    <li><strong>فیلترهای استثنا (Exclude):</strong> جستجوی پیشرفته اکنون به طور کامل از حذف کلمات یا عبارات خاص پشتیبانی می‌کند. می‌توانید از فیلدهای اختصاصی Exclude در رابط کاربری استفاده کنید تا نتایج نامطلوب از فیلدهای گیرنده، فرستنده، موضوع و متن ایمیل با دقت بالا فیلتر شوند.</li>
    <li><strong>بهبود جستجوی متن ایمیل (Body Search):</strong> موتور جستجوی متن‌کامل (FTS) ارتقا یافته است تا کلمات استثنا را به درستی پردازش کند که دقت جستجو در محتوای ایمیل‌ها را به شدت افزایش می‌دهد.</li>
    <li><strong>اصلاحات رابط کاربری و چیدمان:</strong> 
      <ul>
        <li><strong>گرید ریسپانسیو:</strong> ستون «موضوع» (Subject) در لیست نتایج اکنون به صورت خودکار تغییر اندازه می‌دهد تا در صورت تمام‌صفحه کردن پنجره، فضای خالی را پر کند.</li>
        <li><strong>مدرن‌سازی پنل پیش‌نمایش:</strong> ظاهر صفحه خالی در پنل پیش‌نمایش کاملاً بازطراحی شده و اکنون از یک آیکون SVG پاکت‌نامه کاملاً هماهنگ با ظاهر مدرن Outlook استفاده می‌کند.</li>
        <li><strong>ترازبندی:</strong> لیبل مربوط به جستجوهای ذخیره‌شده (Saved Searches) برای هماهنگی بیشتر با سایر فیلدها تراز شد.</li>
      </ul>
    </li>
    <li><strong>به‌روزرسانی موتور دیتابیس و عملکرد بهتر:</strong> موتور دیتابیس داخلی به SQLite نسخه 3.53.4 ارتقا یافت که باعث بهینه‌سازی کوئری‌های FTS5 می‌شود. همچنین درایور <code>Microsoft.Data.Sqlite.Core</code> به نسخه 10.0.11 ارتقا یافت که مصرف حافظه در هنگام بارگذاری هزاران نتیجه را به شدت کاهش می‌دهد.</li>
    <li><strong>رفع خطاهای جستجوی فایل‌های پیوست:</strong> فیلتر آزمایشی جستجو بر اساس بخشی از «نام فایل پیوست» (Attachment Contains) به دلیل ایجاد خطاهای False Positive فراوان حذف شد. جستجو بر اساس <em>وجود یا عدم وجود</em> فایل پیوست همچنان با دقت بالا در دسترس است.</li>
    <li><strong>رفع خطای SmartScreen / Windows Defender:</strong> فایل اصلی <code>EmailTools.dll</code> اکنون در طول فرآیند بیلد به صورت دیجیتال (Authenticode) ساین می‌شود که از نمایش هشدارهای امنیتی نادرستِ SmartScreen جلوگیری می‌کند.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و اکسترکت کرده، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب برنامه مختص کاربر فعلی ویندوز است و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.0.8 را مستقیماً روی نسخه قبلی نصب کنند و نیازی به پاک کردن نسخه پیشین نیست.</p>
</div>