<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.1

This maintenance release includes comprehensive add-in resiliency and anti-deactivation hardening across all Microsoft Outlook versions, automated cleanup of stale disabled registry items, and package dependency verification.

### Highlights

- **Comprehensive Add-in Resiliency & Anti-Deactivation:** Setup now automatically purges all historical `DisabledItems`, `CrashingAddinList`, and `NotificationReminderAddinData` records across Outlook 2013, 2016, 2019, 2021, and Office 365, instantly resolving issues where Outlook kept the add-in unchecked in the COM Add-ins list.
- **Runtime Self-Healing:** The add-in automatically verifies and restores its `DoNotDisableAddinList = 1` and `LoadBehavior = 3` registry policies during startup to ensure it stays permanently active.
- **Enhanced VSTO Trust Registration:** Expanded the VSTO Inclusion List registration with multi-variant URI normalization, guaranteeing seamless trust validation across various Windows locales and drive casing formats.
- **Instant Search & Attachment Search:** Includes all high-speed indexed search features from v1.1.0 (sub-10ms query times and dedicated attachment filename / wildcard extension search).
- **Verified Clean Code Protection:** Fully compliant with Microsoft Defender and enterprise EDR heuristics with zero false-positive alerts and seamless silent GPO deployment support.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users should install v1.1.1 over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه شامل بهبودهای جامع پایداری افزونه، رفع قطعی مشکل غیرفعال شدن خودکار توسط اوت‌لوک، پاک‌سازی کامل سوابق غیرفعال‌سازی در رجیستری و به‌روزرسانی وابستگی‌های برنامه است.</p>

  <h3>ویژگی‌های کلیدی</h3>
  <ul>
    <li><strong>پایداری کامل و جلوگیری از غیرفعال‌سازی افزونه:</strong> نصاب برنامه اکنون تمامی سوابق قدیمی موجود در <code>DisabledItems</code>، <code>CrashingAddinList</code> و هشدارهای تأخیری را در تمام نسخه‌های اوت‌لوک (۲۰۱۳، ۲۰۱۶، ۲۰۱۹، ۲۰۲۱ و آفیس ۳۶۵) پاک‌سازی کرده و مشکل تیک نخوردن افزونه در بخش COM Add-ins را به طور خودکار و قطعی برطرف می‌کند.</li>
    <li><strong>بازیابی و تثبیت خودکار در حین اجرا (Self-Healing):</strong> افزونه هنگام اجرا وضعیت کلیدهای رجیستری <code>DoNotDisableAddinList = 1</code> و <code>LoadBehavior = 3</code> را به طور خودکار بررسی و تثبیت می‌کند تا از هرگونه غیرفعال شدن احتمالی در آینده جلوگیری شود.</li>
    <li><strong>بهبود ساختار ثبت اعتماد VSTO:</strong> رجیستری فهرست شمول VSTO با الگوهای چندگانه آدرس فایل ارتقا یافته تا اعتبارسنجی گواهی در تمامی زبان‌ها و سیستم‌های ویندوز بدون نمایش هیچ‌گونه اخطاری انجام شود.</li>
    <li><strong>جستجوی آنی و فایل‌های پیوست:</strong> بهره‌مندی از تمام امکانات پیشرفته نسخه ۱.۱.۰ شامل باز شدن آنی پنل جستجو (زیر ۱۰ میلی‌ثانیه) و جستجوی پیشرفته بر اساس نام و پسوند فایل‌های پیوست (مانند <code>test</code>، <code>*.pdf</code>، <code>*.xlsx</code>).</li>
    <li><strong>سازگاری کامل با آنتی‌ویروس و نصب سازمانی:</strong> بسته‌بندی امن و عاری از هرگونه هشدار False Positive در Windows Defender با پشتیبانی کامل از استقرار خودکار تحت شبکه (GPO).</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و اکسترکت کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.1 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>
