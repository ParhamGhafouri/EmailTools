<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.8

Version 1.1.8 focuses on **reliable attachment detection across Outlook, Advanced Search and Task Tracker**, **accurate combined search criteria and exclusions**, **consistent Reset and saved-search behavior**, and **responsive large result lists**.

> This is an older release. Install the [latest version](https://github.com/ParhamGhafouri/EmailTools/releases/latest) for current fixes and safety improvements.

### Highlights (Ordered by Priority)

1. **Attachment Detection & Reply/Forward Actions:**
   - Fixed visible image attachments such as `Signature (2).png`, `logo.png` and `image001.png` incorrectly being treated as inline signature images, leaving attachment actions disabled.
   - Removed filename and zero-size assumptions from the shared classifier. Outlook can report zero attachment size even when the file contains valid data; hidden metadata and actual references from the message body now determine inline handling.
   - Fixed images being hidden merely because their filename, CID or content-location appeared in prose, a download link or an unrelated remote image. The fallback now checks rendered image/CSS/VML references and complete resource identities.
   - Applied the correction to the Outlook mailbox and message ribbon, Advanced Search previews and Task Tracker previews. Real file attachments remain available while hidden and body-referenced inline images stay excluded from attachment-copy actions.

2. **Advanced Search Criteria, Exclusions, Reset & Saved Searches:**
   - Includes fixes for combining multiple search fields, refreshing results when a condition is removed, and ensuring the latest criteria win when edits occur during an in-flight search or Task Tracker reload.
   - Fixed Persian/Arabic body exclusions that could behave differently after the last positive body condition was removed. Positive terms, inline `NOT` / minus exclusions and exclusion boxes now share handling of common Kaf/Yeh spelling styles (`ک`/`ك`, `ی`/`ي`), including mixed styles, without rebuilding the existing index. Preview highlighting uses the same spelling variants.
   - Reset restores the opening **All Mail** view, default dropdowns, cleared include/exclude fields, empty selection and empty preview. Advanced Search and Task Tracker no longer focus their search text fields automatically on opening.
   - Fixed saved-search handling so custom dates and times, working-hours filters, attachment names and Unicode text survive saving and loading, while cancelling Save or Delete leaves saved entries unchanged.

3. **Large Result Lists & Responsiveness:**
   - Fixed an accessibility inspection path that materialized every result row and cell despite virtual mode, causing excessive memory use and blocking Outlook on large result sets.
   - Accessibility enumeration now follows the visible viewport while retaining the complete result set, normal scrolling, headers, focused-cell access and hit testing. The shared correction also covers Task Tracker grids.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe** after closing Outlook. Setup is per-user and needs no administrator rights. Existing users can install v1.1.8 directly over the current version without uninstalling first or deleting the local search index.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>نسخه ۱.۱.۸ بر <strong>تشخیص دقیق پیوست‌ها در اوت‌لوک، جست‌وجوی پیشرفته و Task Tracker</strong>، <strong>اعمال صحیح شرط‌های ترکیبی و عبارت‌های مستثنا</strong>، <strong>عملکرد یکسان بازنشانی و جست‌وجوهای ذخیره‌شده</strong>، <strong>پاسخ‌گویی فهرست‌های بزرگ نتایج</strong> تمرکز دارد.</p>

  <blockquote>این نسخه قدیمی است. برای دریافت اصلاحات و بهبودهای ایمنی فعلی، <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest">جدیدترین نسخه</a> را نصب کنید.</blockquote>

  <h3>ویژگی‌ها و تغییرات کلیدی (به ترتیب اولویت و اهمیت)</h3>
  <ul>
    <li><strong>تشخیص پیوست‌ها و دکمه‌های پاسخ و فوروارد:</strong>
      <ul>
        <li>رفع مشکل تشخیص اشتباه تصاویر پیوست‌شده مانند <code>Signature (2).png</code>، <code>logo.png</code> و <code>image001.png</code> به‌عنوان تصویر امضای درون متن که باعث غیرفعال شدن دکمه‌های پیوست می‌شد.</li>
        <li>حذف تصمیم‌گیری صرفاً بر اساس نام فایل یا اندازه صفر گزارش‌شده توسط Outlook؛ اندازه صفر به‌تنهایی نشانه نبود فایل نیست و اطلاعات مخفی بودن و ارجاع تصویر از متن پیام برای تشخیص تصویر درون متن بررسی می‌شوند.</li>
        <li>رفع تشخیص اشتباه تصاویر به دلیل ذکر نام فایل، شناسه CID یا مسیر آن در متن عادی، لینک دانلود یا تصویر اینترنتی نامرتبط؛ تشخیص اکنون بر اساس ارجاع واقعی تصویر در HTML، CSS و VML و تطبیق کامل شناسه منبع انجام می‌شود.</li>
        <li>اعمال اصلاح مشترک در نوار ابزار صندوق پستی و پنجره پیام، پیش‌نمایش Advanced Search و پیش‌نمایش Task Tracker، با حفظ جداسازی تصاویر مخفی و تصاویر ارجاع‌شده در متن از پیوست‌های واقعی.</li>
      </ul>
    </li>
    <li><strong>شرط‌های جست‌وجو، عبارت‌های مستثنا، بازنشانی و جست‌وجوهای ذخیره‌شده:</strong>
      <ul>
        <li>اعمال اصلاحات ترکیب چند فیلد جست‌وجو، تازه‌سازی نتایج پس از حذف شرط و نمایش نتیجه مطابق آخرین تغییرات حتی هنگام اجرای جست‌وجو یا بارگذاری مجدد وظایف.</li>
        <li>رفع ناهماهنگی عبارت‌های مستثنای فارسی و عربی پس از حذف آخرین شرط مثبت بخش Body؛ عبارت‌های مثبت، عبارت‌های منفی <code>NOT</code> / <code>-term</code> و فیلدهای استثنا اکنون از منطق مشترک حروف <code>ک</code>/<code>ك</code> و <code>ی</code>/<code>ي</code>، از جمله حالت‌های ترکیبی رایج، استفاده می‌کنند و نیازی به ساخت مجدد ایندکس ندارند. هایلایت پیش‌نمایش نیز از همین شکل‌های حروف استفاده می‌کند.</li>
        <li>بازگشت Reset به نمای اولیه <strong>All Mail</strong>، مقادیر پیش‌فرض فیلترها، پاک شدن فیلدهای مثبت و منفی و خالی شدن انتخاب و پیش‌نمایش. هنگام باز شدن Advanced Search و Task Tracker، نشانگر تایپ به‌صورت خودکار وارد فیلد جست‌وجو نمی‌شود.</li>
        <li>اصلاح نگهداری تاریخ و ساعت سفارشی، ساعات کاری، نام پیوست و متن یونیکد هنگام ذخیره و بارگذاری جست‌وجو؛ لغو ذخیره یا حذف، جست‌وجوهای ذخیره‌شده را تغییر نمی‌دهد.</li>
      </ul>
    </li>
    <li><strong>فهرست‌های بزرگ نتایج و پاسخ‌گویی رابط کاربری:</strong>
      <ul>
        <li>رفع مسیری در بررسی دسترس‌پذیری که برخلاف حالت مجازی، برای همه ردیف‌ها و سلول‌ها شیء ایجاد می‌کرد و موجب مصرف زیاد حافظه و توقف پاسخ‌گویی Outlook می‌شد.</li>
        <li>محدود شدن پیمایش دسترس‌پذیری به ردیف‌های قابل مشاهده، با حفظ تمام نتایج، پیمایش عادی، سربرگ‌ها، دسترسی به سلول فعال و تشخیص محل سلول‌ها؛ این اصلاح مشترک در فهرست‌های Task Tracker نیز اعمال می‌شود.</li>
      </ul>
    </li>
</ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس پس از بستن Outlook، فایل <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.8 را مستقیماً روی نسخه قبلی نصب کنند؛ حذف برنامه یا ایندکس محلی جست‌وجو لازم نیست.</p>
</div>
