<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.9

This release introduces dynamic working hours filtering natively integrated with your Outlook Calendar settings, along with critical fixes for search preview stability and UI layouts.

### Highlights

- **Working Hours Filter:** Replaced the manual time spinners with a new smart drop-down filter for "Working Hours" and "Outside Working Hours" in the Advanced Search UI.
- **Native Outlook Integration:** The working hours filter now dynamically reads your actual working days and start/end times directly from your Outlook Calendar settings (File > Options > Calendar). It correctly accounts for weekends and customized schedules.
- **RTL Calendar Auto-Correction:** Added an intelligent auto-correction layer for Iranian timezones that automatically bypasses a known Microsoft Outlook bug where Right-To-Left (RTL) calendar UI selections (like Sat-Wed) are incorrectly saved in the registry. 
- **Search Preview Fix:** Fixed a critical issue where the text-highlighting engine (TreeWalker) would occasionally crash the reading pane. The rendering engine now strictly forces modern IE11 Edge emulation.
- **UI Layout Fixes:** Fixed a layout glitch in the Advanced Search panel where the body-match navigation capsule (e.g. < 1/2 >) would push the search text box completely out of view when the Exclude field was also visible. The fields now resize gracefully with guaranteed minimum widths.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users should install v1.0.9 over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه فیلتر هوشمند ساعات کاری را با یکپارچگی کامل با تقویم Outlook معرفی می‌کند. همچنین مشکلات مربوط به پایداری پیش‌نمایش جستجو و ظاهر برنامه برطرف شده است.</p>

  <h3>ویژگی‌های کلیدی</h3>
  <ul>
    <li><strong>فیلتر ساعات کاری:</strong> انتخابگرهای دستی زمان حذف شده و با یک منوی کشویی هوشمند برای فیلتر کردن «ساعات کاری» (Working Hours) و «خارج از ساعات کاری» (Outside Working Hours) در جستجوی پیشرفته جایگزین شده است.</li>
    <li><strong>یکپارچگی با تقویم Outlook:</strong> فیلتر ساعات کاری اکنون روزهای کاری و ساعات شروع/پایان را مستقیماً از تنظیمات تقویم Outlook شما (File > Options > Calendar) می‌خواند. این فیلتر به درستی روزهای تعطیل و برنامه‌های شخصی‌سازی شده را در نظر می‌گیرد.</li>
    <li><strong>اصلاح خودکار تقویم راست‌چین (RTL):</strong> یک لایه اصلاح هوشمند برای منطقه زمانی ایران اضافه شده است که به طور خودکار باگ شناخته شده Outlook را (که در آن انتخاب روزهای کاری شنبه تا چهارشنبه در رابط کاربری، به اشتباه در رجیستری ذخیره می‌شود) دور می‌زند.</li>
    <li><strong>رفع خطای پیش‌نمایش جستجو:</strong> مشکل مهمی که در آن موتور هایلایت متن (TreeWalker) گاهی باعث کرش کردن پنل خواندن می‌شد، برطرف گردید. موتور رندر اکنون به طور اجباری از حالت مدرن IE11 Edge استفاده می‌کند.</li>
    <li><strong>اصلاح چیدمان رابط کاربری:</strong> مشکل ظاهری در پنل جستجوی پیشرفته که در آن کپسول پیمایش نتایج (مانند < 1/2 >) باعث ناپدید شدن تکست‌باکس جستجو در زمان فعال بودن فیلتر Exclude می‌شد، برطرف گردید. فیلدها اکنون با حفظ حداقل عرض ممکن، به درستی تغییر اندازه می‌دهند.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و اکسترکت کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.0.9 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>
