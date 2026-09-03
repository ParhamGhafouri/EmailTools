<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.7

This release resolves the post-exit legacy PST offline deletion lifecycle, fixes zero-length MAPI counted store-list parsing in global Outlook profile sections, enhances Persian/regional calendar date handling across search and archive pipelines, and delivers overall improvements to the search and indexing engine.

### Highlights

- **Persian & Regional Calendar Date Formatting Fixes:** Enforced invariant culture formatting (`CultureInfo.InvariantCulture`) across all date operations, custom search date range boundaries, registry state tracking (`LastRunDate`), and preview timestamps. This prevents date parsing errors, query mismatches, and state corruption on systems configured with Persian (Solar Hijri / Shamsi) or other regional calendar locales.
- **Search & Body Indexing Engine Enhancements:** Improved search responsiveness and reliability across large mailboxes and multi-year archives. Custom date range filtering, sender/recipient resolution, attachment filters, real-time indexing status reporting, and CSV result exports now operate with consistent accuracy and robust background watchdog handling.
- **Reliable Offline Process-Exit Detection & PST Deletion:** Fixed a critical issue where the signed post-exit background cleaner (`EmailTools.NameRepairWorker.exe` / `EmailTools.UpdateRunner.exe`) could evaluate `process.StartTime` on an exited Outlook process handle before checking `process.HasExited`, resulting in `InvalidOperationException` or a false "still running" indication. The cleaner now immediately verifies `HasExited` and handles process lifecycle transitions cleanly, ensuring drained legacy PST files are settled and physically deleted from disk upon Outlook closure without deferral loops.
- **Global Profile Cache Store-List Parsing:** Updated `TryReadCountedStoreListLayout` in `EmailTools.PstProfileAdmin.cs` to correctly support valid zero-length entries (`rawLength == 0` with contiguous offset markers) within Outlook's global profile cache (`1102022a`). Drained legacy PST references are cleanly filtered while preserving all unrelated store descriptors byte-for-byte.
- **Complete Offline Profile Reference Settlement:** Before physical `.pst` deletion, the signed background worker retires and verifies the absence of exact MAPI message services, provider sections, search catalog entries, navigation pane XML storeblocks, and counted profile caches. This completely prevents Outlook missing-data-file prompts on subsequent launches.
- **Guard Rails & Invariant Protection:** All contract tests, invariant AST checks, Authenticode signatures, and strict SHA-256 staging checks passed cleanly across the entire multi-process architecture.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users should install v1.0.7 over the current version without uninstalling first.

**Release assets:** **EmailTools_Setup.rar** is the recommended manual package; **EmailTools_Setup.exe** is also used by the in-app updater; **version.json** is the updater manifest and does not need to be downloaded manually.

**Requirements:** Windows 10 or Windows 11 - Microsoft Outlook 2016, 2019, 2021, or Microsoft 365 desktop - .NET Framework 4.8.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه چرخهٔ حذف فیزیکی PSTهای قدیمی پس از خروج از Outlook را اصلاح می‌کند، خواندن و فیلتر آرایه‌های MAPI با ورودی‌های خالی در Profile سراسری Outlook را بهبود می‌بخشد، خطاهای مرتبط با تقویم فارسی (شمسی) و تاریخ‌های محلی را در جست‌وجو و آرشیو برطرف می‌سازد و پایداری و کارایی موتور جست‌وجو و ایندکس را ارتقا می‌دهد.</p>

  <h3>ویژگی‌های اصلی</h3>
  <ul>
    <li><strong>اصلاح خطاهای تاریخ فارسی و تقویم‌های محلی:</strong> تمامی عملیات مربوط به تاریخ، فیلترهای بازهٔ زمانی دلخواه (Custom Date)، ذخیره و بازیابی وضعیت در رجیستری (مانند <code>LastRunDate</code>) و برچسب‌های پیش‌نمایش، به فرمت استاندارد و مستقل از Culture (با <code>CultureInfo.InvariantCulture</code>) تغییر یافتند تا در سیستم‌هایی با تقویم فارسی (خورشیدی/شمسی) یا تنظیمات منطقه‌ای مختلف، هیچ‌گونه خطا در فیلتر، جست‌وجو یا پردازش تاریخ رخ ندهد.</li>
    <li><strong>بهبود موتور جست‌وجو و ایندکس متن ایمیل‌ها:</strong> پایداری و سرعت جست‌وجو در صندوق‌های بزرگ و آرشیوهای چندساله ارتقا یافت. فیلترهای بازهٔ تاریخی، نام فرستنده/گیرنده، وضعیت پیوست‌ها، نمایش وضعیت لحظه‌ای ایندکس و خروجی CSV با دقت بالا و مدیریت امن در پس‌زمینه انجام می‌شوند.</li>
    <li><strong>تشخیص دقیق خروج Outlook و حذف فیزیکی PSTها:</strong> مشکلی که در آن Worker امضاشدهٔ پس از خروج (<code>EmailTools.NameRepairWorker.exe</code> و <code>EmailTools.UpdateRunner.exe</code>) هنگام بررسی پروسهٔ در حال خروج Outlook با خطای <code>InvalidOperationException</code> مواجه می‌شد یا خروج پروسه را تشخیص نمی‌داد برطرف شد. اکنون خروج پروسه فوراً با <code>HasExited</code> و مدیریت استثناهای پروسه بررسی می‌شود و تمام PSTهای تخلیه‌شده و جداشده، پس از بستن Outlook بدون ورود به حلقهٔ تأخیر، از دیسک حذف می‌شوند.</li>
    <li><strong>پشتیبانی از ورودی‌های خالی در کش Profile سراسری:</strong> متد <code>TryReadCountedStoreListLayout</code> برای پشتیبانی از ساختارهای معتبر با طول صفر (Empty Slots) در شناسهٔ <code>1102022a</code> پروفایل Outlook به‌روزرسانی شد. ارجاعات PSTهای قدیمی به‌طور تمیز حذف می‌شوند و داده‌های سایر فایل‌ها بدون تغییر بایت‌به‌بایت حفظ می‌گردد.</li>
    <li><strong>پاک‌سازی کامل و آفلاین رجیستری و پروفایل:</strong> پیش از حذف فیزیکی فایل‌های <code>.pst</code>، تمام سرویس‌های MAPI، بخش‌های Provider، ثبت‌های جست‌وجو (Search Catalog)، بلوک‌های Navigation XML و کش‌های پروفایل حذف و نبودِ آن‌ها تأیید می‌شود تا Outlook در اجرای بعدی هرگز پیام خطای گم‌شدن فایل داده (Data File Missing) نمایش ندهد.</li>
    <li><strong>تست‌ها و امضای امنیتی:</strong> تمامی آزمون‌های یکپارچگی (Contract Tests)، بررسی‌های ساختاری کد (Invariants) و امضاهای دیجیتال Authenticode با موفقیت انجام و تأیید شدند.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب فقط برای حساب Windows شما انجام می‌شود و به دسترسی Administrator نیاز ندارد. کاربران نسخهٔ قبلی می‌توانند نسخهٔ 1.0.7 را بدون Uninstall روی نسخهٔ فعلی نصب کنند.</p>

  <p><strong>فایل‌های انتشار:</strong> <strong>EmailTools_Setup.rar</strong> بستهٔ پیشنهادی نصب دستی است؛ <strong>EmailTools_Setup.exe</strong> توسط به‌روزرسان داخلی نیز استفاده می‌شود؛ <strong>version.json</strong> اطلاعات به‌روزرسان است و نیازی به دانلود دستی ندارد.</p>

  <p><strong>پیش‌نیازها:</strong> Windows 10 یا Windows 11 - نسخهٔ دسکتاپ Microsoft Outlook 2016، 2019، 2021 یا Microsoft 365 - ‎.NET Framework 4.8.</p>
</div>
