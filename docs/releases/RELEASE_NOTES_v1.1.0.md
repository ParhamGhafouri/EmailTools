<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.1.0

This release introduces high-speed attachment name and extension search, instant search loading across all mailboxes, permanent add-in resiliency protection against Outlook startup disabling, and clean enterprise code signing with zero antivirus false positives.

### Highlights

- **Instant Search Loading:** Opening Advanced Search (`Ctrl+F3`) now renders all 12,500+ messages across all mailboxes and archive PST stores instantaneously in under 10 milliseconds.
- **Attachment Name & Extension Search:** Added a dedicated search box in the Advanced Search UI to quickly filter emails by attachment filename (e.g. `test`, `invoice`, `report`) or wildcard extension (e.g. `*.pdf`, `*.xlsx`, `*.docx`, `*.zip`).
- **Interactive Search UI Controls:** The attachment search box includes a quick-clear button (`✕`), an informative hover tooltip, and refined text padding to ensure smooth typing.
- **Permanent Add-in Resiliency:** Enforced `DoNotDisableAddinList` and `LoadBehavior = 3` policies in the registry, permanently preventing Microsoft Outlook from ever automatically disabling the add-in on startup.
- **Antivirus & GPO Deployment Compatibility:** Updated code obfuscation and packaging to be fully compliant with Windows Defender and enterprise EDR heuristics, eliminating false-positive threat detections (such as `Trojan:Win32/Cloxer`) and ensuring smooth, unblocked silent deployments via GPO.
- **Setup & Process Management:** Setup now automatically handles background Outlook instances to avoid locked file errors (`e_sqlite3.dll`) during updates.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users should install v1.1.0 over the current version without uninstalling first.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه قابلیت جستجوی سریع بر اساس نام و پسوند فایل‌های پیوست، بارگذاری آنی نتایج جستجو در تمام صندوق‌های پستی، پایداری دائمی افزونه در برابر غیرفعال‌سازی توسط اوت‌لوک و سازگاری کامل با آنتی‌ویروس‌ها و استقرار سازمانی را معرفی می‌کند.</p>

  <h3>ویژگی‌های کلیدی</h3>
  <ul>
    <li><strong>بارگذاری آنی نتایج جستجو:</strong> باز شدن پنل جستجوی پیشرفته (<code>Ctrl+F3</code>) اکنون تمامی ایمیل‌ها را در تمام صندوق‌های پستی و فایل‌های آرشیو PST بدون هیچ معطلی و در کمتر از ۱۰ میلی‌ثانیه نمایش می‌دهد.</li>
    <li><strong>جستجوی نام و پسوند فایل‌های پیوست:</strong> اضافه شدن باکس اختصاصی برای جستجوی دقیق ایمیل‌ها بر اساس نام فایل پیوست (مانند <code>test</code>، <code>invoice</code>، <code>report</code>) یا پسوند فایل‌ها با ساختار ستاره (مانند <code>*.pdf</code>، <code>*.xlsx</code>، <code>*.docx</code>، <code>*.zip</code>).</li>
    <li><strong>بهبود رابط کاربری جستجو:</strong> باکس جستجوی پیوست مجهز به دکمه پاک‌سازی سریع (<code>✕</code>)، راهنمای شناور (Tooltip) و فاصله استاندارد متن از لبه‌ها برای تجربه کاربری بهتر شده است.</li>
    <li><strong>پایداری دائمی افزونه (عدم غیرفعال‌سازی):</strong> اعمال تنظیمات پایداری اوت‌لوک (<code>DoNotDisableAddinList</code> و <code>LoadBehavior = 3</code>) جهت جلوگیری قطعی از غیرفعال شدن خودکار افزونه توسط اوت‌لوک هنگام شروع به کار سیستم.</li>
    <li><strong>سازگاری کامل با آنتی‌ویروس و استقرار از طریق GPO:</strong> بازطراحی ساختار محافظت از کدها منطبق با استانداردهای Windows Defender و سیستم‌های امنیتی، رفع هشدارهای نادرست آنتی‌ویروس (مانند خطای False Positive با عنوان <code>Trojan:Win32/Cloxer</code>) و تضمین نصب خودکار و بدون مسدودی از طریق GPO در شبکه.</li>
    <li><strong>مدیریت فرآیند نصب و ارتقا:</strong> نصاب برنامه اکنون پردازه‌های باز اوت‌لوک در پس‌زمینه را مدیریت کرده تا از خطاهای قفل بودن فایل‌ها در حین نصب یا به‌روزرسانی جلوگیری شود.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و اکسترکت کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا نمایید. نصب برای کاربر فعلی انجام می‌شود و نیازی به دسترسی Administrator ندارد. کاربران فعلی می‌توانند نسخه 1.1.0 را مستقیماً روی نسخه قبلی نصب کنند.</p>
</div>
