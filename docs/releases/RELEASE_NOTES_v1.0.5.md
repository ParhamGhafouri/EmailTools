<p align="center">
  <a href="#english"><strong>English</strong></a>
  <span> | </span>
  <a href="#farsi"><strong>فارسی</strong></a>
</p>

<a id="english"></a>
## English

# Email Tools v1.0.5

This release fixes the complete legacy-PST migration lifecycle, startup maintenance stalls, search-index readiness reporting, and update/worker coordination found after v1.0.4.

### Highlights

- Legacy PSTs now remain mounted and visible while they are processed one at a time in chronological order. Their full folder hierarchy is reproduced in the exact managed account and seasonal destination.
- Copy verification is occurrence-aware, so duplicate message identities cannot collapse into one destination proof. Only exact proven source identities are hard-deleted through the PST provider; migrated mail never passes through Outlook's Deleted Items.
- A legacy source is detached only after recursive exact-zero verification. After Outlook exits, the signed worker removes and verifies the exact Outlook profile service, search, navigation, cache, and orphaned provider references without launching or remounting Outlook, then invokes the signed cleanup runner.
- Outlook may compact an empty PST after detachment. v1.0.5 accepts that final header flush only when the creation identity is unchanged and the proof-origin Outlook session has exited. The delete proof is retained until the path remains physically absent across repeated checks; a lock, reappearance, malformed record, or identity mismatch cannot be reported as cleanup success.
- Smart Archive and maintenance-only legacy migration use the same guarded legacy move, destination-proof, detach, and shutdown-cleanup chain. Emergency Archive keeps live-mailbox priority first; normal startup maintenance resumes any legacy sources afterward.
- Startup mailbox-metric readiness is bounded, so unavailable or slow quota data can no longer block legacy maintenance, GAL synchronization, or body indexing indefinitely.
- Search indexing now advances after maintenance and reports the real persisted count instead of remaining at a misleading `ready (0 indexed)` state. Priority pauses name the task they are waiting for and resume immediately when that pass finishes.
- Completed archive scans no longer repeat in a zero-progress loop, and deferred legacy work no longer causes the mailbox to be drained again.
- A staged verified update has priority over shutdown maintenance. The signed updater waits for the worker lane, validates SHA-256 and the pinned publisher, and retains a bounded recovery retry if installer handoff fails.
- The close-time maintenance worker no longer mistakes an invisible Outlook object for the user reopening Outlook. It keeps ownership until the exact hidden Outlook process has exited, so a leftover background Outlook process cannot block the updater or the next visible launch.
- The signed v1.0.5 candidate completed an installed end-to-end test with three mounted legacy PSTs: 2025-Season4, 2026-Season1, and 2026-Season2 were processed in order; destinations matched the original PST allocations; sources reached recursive exact zero and detached; all three exact orphaned profile registrations were retired and all three physical sources were deleted after shutdown; and the local index was ready with 10,549 searchable messages.

**Install:** Download **EmailTools_Setup.rar**, extract it, then run **EmailTools_Setup.exe**. Setup is per-user and needs no administrator rights. Existing users should install v1.0.5 over the current version without uninstalling first.

**Release assets:** **EmailTools_Setup.rar** is the recommended manual package; **EmailTools_Setup.exe** is also used by the in-app updater; **version.json** is the updater manifest and does not need to be downloaded manually.

**Requirements:** Windows 10 or Windows 11 - Microsoft Outlook 2016, 2019, 2021, or Microsoft 365 desktop - .NET Framework 4.8.

---

<a id="farsi"></a>
<h2 dir="rtl" align="right">فارسی</h2>

<div dir="rtl" align="right">
  <p>این نسخه چرخهٔ کامل انتقال PSTهای قدیمی، توقف‌های نگهداری هنگام شروع Outlook، نمایش وضعیت Search Index و هماهنگی Update با Worker را که پس از نسخهٔ 1.0.4 دیده شده بود اصلاح می‌کند.</p>

  <h3>ویژگی‌های اصلی</h3>
  <ul>
    <li>PSTهای قدیمی هنگام پردازش داخل Outlook متصل و قابل مشاهده می‌مانند، به‌ترتیب زمانی و یکی‌یکی انجام می‌شوند و ساختار کامل پوشه‌ها در Account و آرشیو فصلی دقیق حفظ می‌شود.</li>
    <li>تأیید Copy تعداد تکرارها را نیز در نظر می‌گیرد تا هویت‌های تکراری در یک Proof ادغام نشوند. فقط هویت دقیقاً تأییدشدهٔ منبع با Hard Delete خود PST حذف می‌شود و ایمیل منتقل‌شده هرگز وارد Deleted Items نمی‌شود.</li>
    <li>منبع قدیمی فقط بعد از تأیید بازگشتی و دقیق صفر بودن از Outlook جدا می‌شود. پس از خروج Outlook، Worker امضاشده بدون اجرای مجدد یا Mount کردن Outlook، سرویس Profile، Search، Navigation، Cache و Provider باقی‌ماندهٔ دقیق همان مسیر را حذف و نبودشان را تأیید می‌کند و سپس حذف فیزیکی را به Cleanup Runner امضاشده می‌سپارد.</li>
    <li>Outlook ممکن است PST خالی را پس از جداسازی Compact کند. نسخهٔ 1.0.5 این Final Header Flush را فقط با Creation Identity یکسان و Session خارج‌شده می‌پذیرد. Proof تا وقتی نبود فیزیکی فایل در چند بررسی پایدار نماند حفظ می‌شود و Lock، بازگشت فایل، Record خراب یا Identity نامنطبق هرگز به‌عنوان موفقیت گزارش نمی‌شود.</li>
    <li>Smart Archive و انتقال نگهداری‌محور PST قدیمی از همان زنجیرهٔ محافظت‌شدهٔ انتقال، تأیید مقصد، جداسازی و پاک‌سازی پس از خروج استفاده می‌کنند. Emergency Archive ابتدا با اولویت روی صندوق زنده کار می‌کند و سپس نگهداری عادی هنگام شروع Outlook ادامهٔ PSTهای قدیمی را انجام می‌دهد.</li>
    <li>انتظار برای اطلاعات حجم و Quota هنگام شروع Outlook محدود شده است؛ کندی یا در دسترس نبودن این اطلاعات دیگر نمی‌تواند انتقال PST، همگام‌سازی GAL یا ایندکس متن ایمیل‌ها را برای همیشه متوقف کند.</li>
    <li>Search Index پس از پایان نگهداری واقعاً ادامه پیدا می‌کند و به‌جای وضعیت گمراه‌کنندهٔ <code>ready (0 indexed)</code> تعداد ذخیره‌شدهٔ واقعی را نشان می‌دهد. Pauseهای اولویت‌دار نام کار واقعی را نمایش می‌دهند و بلافاصله پس از پایان آن ادامه پیدا می‌کنند.</li>
    <li>اسکن کامل‌شدهٔ آرشیو دیگر وارد حلقهٔ بدون پیشرفت نمی‌شود و کار Deferred مربوط به PST قدیمی نیز باعث تخلیهٔ دوبارهٔ صندوق نمی‌شود.</li>
    <li>Update تأییدشدهٔ آماده‌شده در زمان خروج اولویت دارد. Updater امضاشده منتظر آزادشدن مسیر Worker می‌ماند، SHA-256 و Publisher سنجاق‌شده را بررسی می‌کند و در صورت شکست تحویل Installer یک Retry محدود و پایدار نگه می‌دارد.</li>
    <li>Worker زمان خروج دیگر یک شیء نامرئی Outlook را با بازگشت کاربر اشتباه نمی‌گیرد. مالکیت Worker تا خروج کامل همان Process مخفی Outlook حفظ می‌شود تا Process باقی‌مانده نتواند Update یا اجرای قابل‌مشاهدهٔ بعدی Outlook را متوقف کند.</li>
    <li>نسخهٔ امضاشدهٔ 1.0.5 یک آزمایش کامل نصب‌شده با سه PST قدیمی را با موفقیت گذراند: 2025-Season4، 2026-Season1 و 2026-Season2 به‌ترتیب پردازش شدند، اندازهٔ Allocation مقصدها با PSTهای اصلی برابر بود، منابع دقیقاً صفر و جدا شدند، سه ثبت orphan دقیق در Profile پاک شد، هر سه فایل فیزیکی پس از خروج حذف شدند و Index محلی با 10,549 پیام قابل جست‌وجو آماده بود.</li>
  </ul>

  <p><strong>نصب:</strong> فایل <strong>EmailTools_Setup.rar</strong> را دانلود و استخراج کنید، سپس <strong>EmailTools_Setup.exe</strong> را اجرا کنید. نصب فقط برای حساب Windows شما انجام می‌شود و به دسترسی Administrator نیاز ندارد. کاربران نسخهٔ قبلی باید 1.0.5 را بدون Uninstall روی نسخهٔ فعلی نصب کنند.</p>

  <p><strong>فایل‌های انتشار:</strong> <strong>EmailTools_Setup.rar</strong> بستهٔ پیشنهادی نصب دستی است؛ <strong>EmailTools_Setup.exe</strong> توسط به‌روزرسان داخلی نیز استفاده می‌شود؛ <strong>version.json</strong> اطلاعات به‌روزرسان است و نیازی به دانلود دستی ندارد.</p>

  <p><strong>پیش‌نیازها:</strong> Windows 10 یا Windows 11 - نسخهٔ دسکتاپ Microsoft Outlook 2016، 2019، 2021 یا Microsoft 365 - ‎.NET Framework 4.8.</p>
</div>
