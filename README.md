
# راهنمای استفاده از LatestReleaseMirror

در صورت عدم دسترسی به ساب‌دامین `release-assets.githubusercontent.com` برای دریافت فایل از بخش ریلیز‌های هر مخزن گیت‌هاب، [**این پروژه**](https://github.com/Ehs6n/LatestReleaseMirror) آخرین نسخه منتشر شده (latest release) مخازن مختلف مدنظر کاربر را بر اساس فیلتر تعریف شده از گیت‌هاب آن مخازن دریافت کرده و در یک ساختار پوشه‌ای مرتب در ریپوی کاربر ذخیره می‌کند. به این ترتیب امکان دسترسی به آن‌ها از طریق ساب‌دامین `raw.githubusercontent.com` فراهم می‌شود. این روش تا زمان در دسترس بودن این ساب‌دامین، قابل استفاده خواهد بود. البته محدودیت‌هایی در استفاده وجود دارد که در ادامه توضیح داده خواهد شد.


- [شروع سریع](#-%D8%B4%D8%B1%D9%88%D8%B9-%D8%B3%D8%B1%DB%8C%D8%B9)
* ۰. [پیش‌نیاز](#%DB%B0-%D9%BE%DB%8C%D8%B4%E2%80%8C%D9%86%DB%8C%D8%A7%D8%B2)
* ۱. [فورک (Fork) کردن مخزن](#%DB%B1-%D9%81%D9%88%D8%B1%DA%A9-fork-%DA%A9%D8%B1%D8%AF%D9%86-%D9%85%D8%AE%D8%B2%D9%86)
* ۲. [ویرایش فایل `repos.txt`](#%DB%B2-%D9%88%DB%8C%D8%B1%D8%A7%DB%8C%D8%B4-%D9%81%D8%A7%DB%8C%D9%84-repostxt)
* ۳. [اجرای workflow](#%DB%B3-%D8%A7%D8%AC%D8%B1%D8%A7%DB%8C-workflow)
* ۴. [نحوه‌ی مشاهده و دانلود فایل‌ها](#%DB%B4-%D9%86%D8%AD%D9%88%D9%87%E2%80%8C%DB%8C-%D9%85%D8%B4%D8%A7%D9%87%D8%AF%D9%87-%D9%88-%D8%AF%D8%A7%D9%86%D9%84%D9%88%D8%AF-%D9%81%D8%A7%DB%8C%D9%84%E2%80%8C%D9%87%D8%A7)
* ۵. [حذف یک مخزن یا تغییر فیلترها](#%DB%B5-%D8%AD%D8%B0%D9%81-%DB%8C%DA%A9-%D9%85%D8%AE%D8%B2%D9%86-%DB%8C%D8%A7-%D8%AA%D8%BA%DB%8C%DB%8C%D8%B1-%D9%81%DB%8C%D9%84%D8%AA%D8%B1%D9%87%D8%A7)
* ۶. [نکات مهم و محدودیت‌ها](#%DB%B6-%D9%86%DA%A9%D8%A7%D8%AA-%D9%85%D9%87%D9%85-%D9%88-%D9%85%D8%AD%D8%AF%D9%88%D8%AF%DB%8C%D8%AA%E2%80%8C%D9%87%D8%A7)
- [بررسی صحت فایل‌ها (SHA256)](#-%D8%A8%D8%B1%D8%B1%D8%B3%DB%8C-%D8%B5%D8%AD%D8%AA-%D9%81%D8%A7%DB%8C%D9%84%E2%80%8C%D9%87%D8%A7-sha256)
- [رفع مسئولیت (Disclaimer)](#%EF%B8%8F-%D8%B1%D9%81%D8%B9-%D9%85%D8%B3%D8%A6%D9%88%D9%84%DB%8C%D8%AA-disclaimer)
- [مشاهده و دانلود آخرین ریلیز‌ها](#-%D9%85%D8%B4%D8%A7%D9%87%D8%AF%D9%87-%D9%88-%D8%AF%D8%A7%D9%86%D9%84%D9%88%D8%AF-%D8%A2%D8%AE%D8%B1%DB%8C%D9%86-%D8%B1%DB%8C%D9%84%DB%8C%D8%B2%E2%80%8C%D9%87%D8%A7)



## 🚀 شروع سریع

### ۰. پیش‌نیاز
- دسترسی به گیت‌هاب
- داشتن حساب کاربری در گیت‌هاب و لاگین کردن به آن

### ۱. فورک (Fork) کردن مخزن

- روی دکمه‌ی **Fork** در بالای **[این صفحه](https://github.com/Ehs6n/LatestReleaseMirror)** کلیک کنید. (یا مستقیما می‌توانید روی [این لینک](https://github.com/Ehs6n/LatestReleaseMirror/fork) کلیک کنید)
- در صفحه بعد روی گزینه **Create Fork** کلیک کنید.
- مخزن فورک شده در اکانت گیت‌هاب شما با موفقیت ساخته می‌شود.

### ۲. ویرایش فایل `repos.txt`

در مخزن فورک شده در حساب کاربری خودتان، فایل `repos.txt` را باز کنید و ریپو‌های مدنظر خود را مطابق فایل نمونه (`repos.txt.example‍‍`) که در زیر توضیح داده شده است، ویرایش و ذخیره کنید:

```text
# repos.txt.example – copy to repos.txt and edit

# Format: owner/repo|filter1|filter2|...
# Filters are case‑insensitive regular expressions (grep -E).

# 1. No filter – keep all assets from the release
therealaleph/MasterHttpRelayVPN-RUST

# 2. Match keywords (e.g., linux-amd64, darwin-amd64)
NullLatency/FlowDriver|linux-amd64|darwin-amd64

# 3. Mix of keywords and file extensions (note escaping of dots)
SagerNet/sing-box|windows-amd64|darwin-amd64.tar.gz|darwin-arm64|arm64-v8a.apk

# 4. Only specific file extensions (use .dmg and .exe – backslashes for literal dot)
KaringX/karing|\.dmg|\.exe

# 5. Disable a line by commenting it with #
# masterking32/MasterDnsVPN|Client_MacOS_AMD64.zip|Client_Windows_AMD64.zip
```

#### توضیح خطوط
- هر خط به صورت `...|فیلتر 2|فیلتر 1|owner/repo` نوشته می‌شود.
- فیلترها حساس به حروف بزرگ و کوچک نیستند (case‑insensitive).
- اگر فیلتری ننویسید (فقط `owner/repo`) همهٔ فایل‌های آن ریلیز دانلود می‌شوند.
- فیلتر‌ها را می‌توانید اضافه، ویرایش یا حذف کنید.
- در صورتی که بخواهید یک ریپو را از لیست حذف کنید می‌توانید خط مربوط به آن را حذف کرده و یا با قرار دادن کاراکتر `#` در ابتدای خط، آن را کامنت کنید.

### ۳. اجرای workflow
پس از تکمیل فایل repos.txt و ذخیره کردن و commit کردن آن، می‌توانید workflow را اجرا نمایید.


** جهت اجرا بصورت دستی:

- به برگه (تب) Actions در مخزن فورک شده در پروفایل خودتان بروید.
- در سمت چپ، روی Sync latest releases & update README کلیک کنید.
- دکمه‌ی Run workflow (سمت راست) را بزنید، سپس Run workflow را تأیید کنید.
- پس از تکمیل فرآیند و موفق بودن آن، لینک‌های دانلود در README قابل مشاهده است.

** اجرا بصورت خودکار بر اساس زمان‌بندی تعریف‌شده توسط کاربر:

- در صورتی که می‌خواهید فرآیند بررسی ریپو‌های ذخیره شده در فایل repos.txt بر اساس یک برنامه‌ی زمانی بصورت خودکار و متناوب انجام شود، می‌توانید خطوط ۴و۵ فایل `.github/workflows/sync-multiple-repos.yml` را از حالت کامنت خارج کنید و مطابق زمان‌بندی مدنظر خود ویرایش کنید.
- پیشنهاد می‌شود فاصله‌ی زمانی بین بررسی‌ها خیلی کوتاه نباشد. روزی یک یا دو بار اجرا بصورت خودکار (برای مثال هر ۱۲ یا ۱۸ یا ۲۴ ساعت یک‌بار) مناسب است و تعداد اجرای خودکار بیشتر از آن توصیه نمی‌شود.
- برای تغییر زمان‌بندی، خط `cron` را ویرایش کنید و در صورتی که پس از فعالسازی اجرای خودکار بخواهید آن را لغو کنید، می‌توانید این دو خط را مجددا کامنت کرده و یا از فایل حذف کنید.

```
  schedule:
    - cron: '0 */12 * * *'
```

### ۴. نحوه‌ی مشاهده و دانلود فایل‌ها
پس از اتمام workflow، فایل‌های دانلود شده در پوشه‌ی `releases/owner/repo/` در ریپو خودتان ذخیره می‌شوند.
همچنین می‌توانید لینک‌های دانلود را از طریق جدول ایجاد شده در انتهای فایل README.md نیز مشاهده کنید و با کلیک روی ⬇️ Download آن‌ها را دانلود کنید.


### ۵. حذف یک مخزن یا تغییر فیلترها

اگر یک خط را از repos.txt حذف یا کامنت (#) کنید، در اجرای بعدی workflow، کل پوشه‌ی آن مخزن از releases/ حذف می‌شود و فایل README.md نیز بصورت خودکار اصلاح می‌شود.

اگر فیلترها را تغییر دهید (مثلاً فیلتر جدید اضافه یا فیلتر‌های قدیمی را حذف کنید)، فایل‌هایی که دیگر با فیلتر جدید همخوانی ندارند نیز حذف خواهند شد و در ریلیز بعدی، فقط فایل‌های جدید منطبق با فیلتر اعمال شده دانلود می‌شوند.

### ۶. نکات مهم و محدودیت‌ها
- به علت محدودیت‌های گیت‌هاب در آپلود فایل با سایز بزرگتر از ۱۰۰ مگابایت، این فایل‌ها به پارت‌های کوچکتر (مانند `file.001`،`file.002`، …) تقسیم شده‌اند. پس از دانلود همه‌ی پارت‌ها، می‌توانید با استفاده از ابزار HTML موجود در `docs/merger.html` یا دستور `cat` در ترمینال، فایل اصلی را بازسازی کنید.
- تمام لینک‌های دانلود به صورت خودکار به مخزن فورک شده شما اشاره می‌کنند (نیازی به ویرایش دستی نیست).
- استفاده از GitHub Actions محدودیت‌هایی در تعداد ریکوئست، مدت زمان اجرا دارد که می‌توانید آن‌ها را از طریق **[مستندات گیت‌هاب](https://docs.github.com/en/actions/reference/limits)** بررسی فرمایید. همچنین محدودیت‌هایی در دانلود و آپلود و پهنای باند مورد استفاده از طریق گیتهاب وجود دارد که بهتر است قبل از استفاده، آن‌ها را بررسی نمایید.
- برای روبرو نشدن با محدودیت‌ها بهتر است تعداد ریپو‌های کمی را در فایل repos.txt قرار دهید و با قرار دادن فیلتر مناسب، فقط فایل‌های مد نظر خود را با استفاده از این روش دریافت نمایید.
- پس از چند بار اجرای workflow و دانلود و آپلود نسخه‌های مختلف ریلیز‌ها، حجم ریپوی شما ممکن است تا چند گیگ نیز افزایش یابد و clone کردن آن سخت باشد یا محدودیت‌هایی از سمت گیت‌هاب اعمال شود. از طریق اجرای Clear releases history (در تب اکشن) می‌توانید تاریخچه commit‌های پوشه releases خود را حذف نمایید تا حجم ریپوی شما بصورت چشم‌گیری کاهش یابد. اجرای این action تاریخچه گیت را برای پوشه releases بازنویسی می‌کند و در مخازن عمومی که دیگران فورک کرده‌اند ممکن است باعث ایجاد مشکل شود. فقط زمانی از آن استفاده کنید که به تنهایی روی مخزن کار می‌کنید.
- برای جلوگیری از مشکلات و رفع محدودیت‌ها هر نفر می‌تواند برای استفاده‌ی شخصی خود پروژه را فورک کرده و بر حسب نیاز خود فایل repos.txt را با تعداد کمی از ریپو‌های مدنظرش تکمیل کرده و استفاده کند. مسئولیت استفاده بر عهده کاربران است.



## 🔒 بررسی صحت فایل‌ها (SHA256)


⚠️ پیش از اجرا یا نصب فایل‌های دانلود شده از این ریپو (و بصورت کلی هر جایی به جز منبع اصلی)، یک‌بار Checksum فایل دانلود شده را با مقدار اصلی (که در صفحه Release هر پروژه در بخش Assets و در کنار هر فایل برای تمام ورژن‌ها بصورت `sha256:abcdef01234567890ab...` قابل مشاهده‌است) مقایسه کنید. برای حاصل شدن اطمینان از اینکه فایل‌ها دستکاری نشده‌اند و دقیقا همان نسخه منتشر شده در سورس اصلی می‌باشند، باید مقدار هش‌ sha256 یک نسخه از یک فایل خاص با مقدار هشی که برای همان نسخه و فایل در سورس اصلی قابل مشاهده‌است، کاملا یکسان باشد. در صورت مغایرت، از نصب آن خود‌داری کنید.

در اینجا یک راهنمای کوتاه برای بررسی فایل‌های دانلود شده از منبعی به جز سورس اصلی، با استفاده از SHA256 در سیستم‌عامل‌های مختلف آورده شده است.



### 🍎 macOS / 🐧 Linux (ترمینال)
```bash
sha256sum FILE_NAME
```
(در macOS قدیمی‌تر ممکن است به جای آن از shasum -a 256 FILE_NAME استفاده کنید)


### 🪟 Windows (PowerShell)


```powershell
Get-FileHash -Algorithm SHA256 FILE_NAME
```

### 📱 Android (با ترمینال یا Termux)
```bash
sha256sum FILE_NAME
```
(اگر دستور در دسترس نبود، ابتدا pkg install coreutils را در Termux اجرا کنید)


## ⚠️ رفع مسئولیت (Disclaimer)
استفاده از این ابزار و سرویس‌های گیت‌هاب (GitHub Actions، GitHub API، فضای ذخیره‌سازی مخزن، پهنای باند و …) تحت مسئولیت کامل کاربر نهایی است.
کاربر موظف است هنگام استفاده از این ریپوزیتوری، همه‌ی **[محدودیت‌های اعلام شده توسط گیت‌هاب](https://docs.github.com/en/actions/reference/limits)** از جمله محدودیت نرخ درخواست API، حداکثر حجم فایل در هر commit (۱۰۰ مگابایت)، مدت زمان اجرای workflow، تعداد دفعات اجرا، حجم مخزن و پهنای باند را رعایت کند.
تخلف از محدودیت‌های گیت‌هاب ممکن است منجر به مسدود شدن حساب کاربری یا مسدود شدن مخزن شما شود. بنابراین توصیه می‌شود:
- تعداد مخازن تحت نظر را محدود نگه دارید.
- فاصله زمانی اجرای خودکار workflow را خیلی کوتاه انتخاب نکنید (مثلاً کمتر از هر ۱۲ ساعت نباشد).
- از فیلترهای مناسب برای کاهش تعداد فایل‌های دانلودی استفاده کنید.
- در صورت افزایش حجم فایل‌ها و تاریخچه‌ی گیت، از قابلیت Clear releases history با آگاهی از عواقب آن (بازنویسی تاریخچه گیت) استفاده کنید.
  
ایجاد این ریپوزیتوری هیچ تعهدی مبنی بر در دسترس بودن مستمر سرویس‌های گیت‌هاب یا صحت عملکرد آن‌ها ایجاد نمی‌کند. هرگونه مشکل احتمالی ناشی از تغییر قوانین یا محدودیت‌های گیت‌هاب بر عهده کاربر خواهد بود.

این ابزار برای دانلود فایل‌های غیرقانونی، دارای مالکیت معنوی یا مغایر با قوانین گیت‌هاب طراحی نشده است. مسئولیت محتوای دانلود شده و انطباق آن با قوانین محلی بر عهده کاربر است.



## 📦 مشاهده و دانلود آخرین ریلیز‌ها

پس از اجرای موفق workflow، جداول مربوط به ریپو‌های درخواستی کاربر در این بخش قابل مشاهده است:


<!-- RELEASES_START -->
<div id="2dust--v2rayn"></div>

### 2dust--v2rayN

🔗 [source](https://github.com/2dust/v2rayN) – [<code><small>7.21.3</small></code>](https://github.com/2dust/v2rayN/releases/tag/7.21.3)

| File | Size | Download |
|------|------|----------|
| `v2rayN-windows-64-desktop.zip (part 1 of 2)` | 90.0 MB | [⬇️ Download (Part 1)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayN/v2rayN-windows-64-desktop.zip.001) |
| `v2rayN-windows-64-desktop.zip (part 2 of 2)` | 28.1 MB | [⬇️ Download (Part 2)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayN/v2rayN-windows-64-desktop.zip.002) |

---

<div id="2dust--v2rayng"></div>

### 2dust--v2rayNG

🔗 [source](https://github.com/2dust/v2rayNG) – [<code><small>2.1.7</small></code>](https://github.com/2dust/v2rayNG/releases/tag/2.1.7)

| File | Size | Download |
|------|------|----------|
| `v2rayNG_2.1.7-fdroid_arm64-v8a.apk` | 26.8 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7-fdroid_arm64-v8a.apk) |
| `v2rayNG_2.1.7-fdroid_armeabi-v7a.apk` | 27.1 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7-fdroid_armeabi-v7a.apk) |
| `v2rayNG_2.1.7-fdroid_universal.apk` | 61.8 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7-fdroid_universal.apk) |
| `v2rayNG_2.1.7-fdroid_x86.apk` | 28.0 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7-fdroid_x86.apk) |
| `v2rayNG_2.1.7-fdroid_x86_64.apk` | 27.6 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7-fdroid_x86_64.apk) |
| `v2rayNG_2.1.7_arm64-v8a.apk` | 26.8 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7_arm64-v8a.apk) |
| `v2rayNG_2.1.7_armeabi-v7a.apk` | 27.1 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7_armeabi-v7a.apk) |
| `v2rayNG_2.1.7_universal.apk` | 61.8 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7_universal.apk) |
| `v2rayNG_2.1.7_x86.apk` | 28.0 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7_x86.apk) |
| `v2rayNG_2.1.7_x86_64.apk` | 27.6 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/2dust/v2rayNG/v2rayNG_2.1.7_x86_64.apk) |

---

<div id="dignezzz--v2raytun"></div>

### DigneZzZ--v2raytun

🔗 [source](https://github.com/DigneZzZ/v2raytun) – [<code><small>5.23.73</small></code>](https://github.com/DigneZzZ/v2raytun/releases/tag/5.23.73)

| File | Size | Download |
|------|------|----------|
| `v2RayTun_universal.apk` | 94.7 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/DigneZzZ/v2raytun/v2RayTun_universal.apk) |

---

<div id="gfw-knocker--mahsang"></div>

### GFW-knocker--MahsaNG

🔗 [source](https://github.com/GFW-knocker/MahsaNG) – [<code><small>v16-(1405-2-25)</small></code>](https://github.com/GFW-knocker/MahsaNG/releases/tag/v16-(1405-2-25))

| File | Size | Download |
|------|------|----------|
| `MahsaNG_16_arm64-v8a.apk` | 59.2 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/GFW-knocker/MahsaNG/MahsaNG_16_arm64-v8a.apk) |
| `MahsaNG_16_armeabi-v7a.apk` | 60.3 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/GFW-knocker/MahsaNG/MahsaNG_16_armeabi-v7a.apk) |
| `MahsaNG_16_universal.apk (part 1 of 2)` | 90.0 MB | [⬇️ Download (Part 1)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/GFW-knocker/MahsaNG/MahsaNG_16_universal.apk.001) |
| `MahsaNG_16_universal.apk (part 2 of 2)` | 82.3 MB | [⬇️ Download (Part 2)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/GFW-knocker/MahsaNG/MahsaNG_16_universal.apk.002) |
| `MahsaNG_16_x86.apk` | 63.7 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/GFW-knocker/MahsaNG/MahsaNG_16_x86.apk) |
| `MahsaNG_16_x86_64.apk` | 62.3 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/GFW-knocker/MahsaNG/MahsaNG_16_x86_64.apk) |

---

<div id="happ-proxy--happ-android"></div>

### Happ-proxy--happ-android

🔗 [source](https://github.com/Happ-proxy/happ-android) – [<code><small>3.21.1</small></code>](https://github.com/Happ-proxy/happ-android/releases/tag/3.21.1)

| File | Size | Download |
|------|------|----------|
| `Happ.apk` | 56.2 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/Happ-proxy/happ-android/Happ.apk) |
| `Happ_beta.apk` | 56.2 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/Happ-proxy/happ-android/Happ_beta.apk) |

---

<div id="happ-proxy--happ-desktop"></div>

### Happ-proxy--happ-desktop

🔗 [source](https://github.com/Happ-proxy/happ-desktop) – [<code><small>2.14.0</small></code>](https://github.com/Happ-proxy/happ-desktop/releases/tag/2.14.0)

| File | Size | Download |
|------|------|----------|
| `setup-Happ.x64.exe (part 1 of 2)` | 90.0 MB | [⬇️ Download (Part 1)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/Happ-proxy/happ-desktop/setup-Happ.x64.exe.001) |
| `setup-Happ.x64.exe (part 2 of 2)` | 21.7 MB | [⬇️ Download (Part 2)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/Happ-proxy/happ-desktop/setup-Happ.x64.exe.002) |

---

<div id="thisisdara--mhr-cfw-go"></div>

### ThisIsDara--mhr-cfw-go

🔗 [source](https://github.com/ThisIsDara/mhr-cfw-go) – [<code><small>v1.4.0</small></code>](https://github.com/ThisIsDara/mhr-cfw-go/releases/tag/v1.4.0)

| File | Size | Download |
|------|------|----------|
| `mhr-cfw-go-windows-amd64.exe` | 6.6 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/ThisIsDara/mhr-cfw-go/mhr-cfw-go-windows-amd64.exe) |

---

<div id="anonvector--slipnet"></div>

### anonvector--SlipNet

🔗 [source](https://github.com/anonvector/SlipNet) – [<code><small>v2.5.3</small></code>](https://github.com/anonvector/SlipNet/releases/tag/v2.5.3)

| File | Size | Download |
|------|------|----------|
| `SlipNet-v2.5.3-lite-release-universal.apk` | 22.5 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/anonvector/SlipNet/SlipNet-v2.5.3-lite-release-universal.apk) |
| `slipnet-windows-amd64.exe` | 11.1 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/anonvector/SlipNet/slipnet-windows-amd64.exe) |

---

<div id="davudsedft--purvpn"></div>

### davudsedft--purvpn

🔗 [source](https://github.com/davudsedft/purvpn) – [<code><small>11.9</small></code>](https://github.com/davudsedft/purvpn/releases/tag/11.9)

| File | Size | Download |
|------|------|----------|
| `purvpn-11.9-release.apk` | 80.3 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/davudsedft/purvpn/purvpn-11.9-release.apk) |

---

<div id="hiddify--hiddify-app"></div>

### hiddify--hiddify-app

🔗 [source](https://github.com/hiddify/hiddify-app) – [<code><small>v4.1.1</small></code>](https://github.com/hiddify/hiddify-app/releases/tag/v4.1.1)

| File | Size | Download |
|------|------|----------|
| `Hiddify-Android-arm64.apk (part 1 of 2)` | 90.0 MB | [⬇️ Download (Part 1)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/hiddify/hiddify-app/Hiddify-Android-arm64.apk.001) |
| `Hiddify-Android-arm64.apk (part 2 of 2)` | 23.5 MB | [⬇️ Download (Part 2)](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/hiddify/hiddify-app/Hiddify-Android-arm64.apk.002) |
| `Hiddify-Windows-Setup-x64.exe` | 34.7 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/hiddify/hiddify-app/Hiddify-Windows-Setup-x64.exe) |

---

<div id="iampedii--whitedns"></div>

### iampedii--WhiteDNS

🔗 [source](https://github.com/iampedii/WhiteDNS) – [<code><small>1.5.1</small></code>](https://github.com/iampedii/WhiteDNS/releases/tag/1.5.1)

| File | Size | Download |
|------|------|----------|
| `WhiteDNS-1.5.1-arm64-v8a.apk` | 5.6 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-arm64-v8a.apk) |
| `WhiteDNS-1.5.1-arm64-v8a.apk.idsig` | 54 KB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-arm64-v8a.apk.idsig) |
| `WhiteDNS-1.5.1-armeabi-v7a.apk` | 5.5 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-armeabi-v7a.apk) |
| `WhiteDNS-1.5.1-armeabi-v7a.apk.idsig` | 54 KB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-armeabi-v7a.apk.idsig) |
| `WhiteDNS-1.5.1-universal.apk` | 16.9 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-universal.apk) |
| `WhiteDNS-1.5.1-universal.apk.idsig` | 142 KB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-universal.apk.idsig) |
| `WhiteDNS-1.5.1-x86.apk` | 6.1 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-x86.apk) |
| `WhiteDNS-1.5.1-x86.apk.idsig` | 58 KB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-x86.apk.idsig) |
| `WhiteDNS-1.5.1-x86_64.apk` | 5.9 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-x86_64.apk) |
| `WhiteDNS-1.5.1-x86_64.apk.idsig` | 54 KB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/iampedii/WhiteDNS/WhiteDNS-1.5.1-x86_64.apk.idsig) |

---

<div id="maattyi--masterhttprelayvpngui"></div>

### maattyi--MasterHttpRelayVpnGUI

🔗 [source](https://github.com/maattyi/MasterHttpRelayVpnGUI) – [<code><small>tag2</small></code>](https://github.com/maattyi/MasterHttpRelayVpnGUI/releases/tag/tag2)

| File | Size | Download |
|------|------|----------|
| `MasterRelayVPN-v1.1.0.zip` | 75.6 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/maattyi/MasterHttpRelayVpnGUI/MasterRelayVPN-v1.1.0.zip) |

---

<div id="masterking32--masterdnsvpn"></div>

### masterking32--MasterDnsVPN

🔗 [source](https://github.com/masterking32/MasterDnsVPN) – [<code><small>v2026.05.10.180256-27c7e11</small></code>](https://github.com/masterking32/MasterDnsVPN/releases/tag/v2026.05.10.180256-27c7e11)

| File | Size | Download |
|------|------|----------|
| `MasterDnsVPN_Client_Windows_AMD64.zip` | 4.0 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/masterking32/MasterDnsVPN/MasterDnsVPN_Client_Windows_AMD64.zip) |

---

<div id="telegramdesktop--tdesktop"></div>

### telegramdesktop--tdesktop

🔗 [source](https://github.com/telegramdesktop/tdesktop) – [<code><small>v6.8.2</small></code>](https://github.com/telegramdesktop/tdesktop/releases/tag/v6.8.2)

| File | Size | Download |
|------|------|----------|
| `tsetup-x64.6.8.2.exe` | 49.2 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/telegramdesktop/tdesktop/tsetup-x64.6.8.2.exe) |

---

<div id="therealaleph--masterhttprelayvpn-rust"></div>

### therealaleph--MasterHttpRelayVPN-RUST

🔗 [source](https://github.com/therealaleph/MasterHttpRelayVPN-RUST) – [<code><small>v1.9.31</small></code>](https://github.com/therealaleph/MasterHttpRelayVPN-RUST/releases/tag/v1.9.31)

| File | Size | Download |
|------|------|----------|
| `mhrv-rs-android-arm64-v8a-v1.9.31.apk` | 18.6 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/therealaleph/MasterHttpRelayVPN-RUST/mhrv-rs-android-arm64-v8a-v1.9.31.apk) |
| `mhrv-rs-android-universal-v1.9.31.apk` | 41.4 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/therealaleph/MasterHttpRelayVPN-RUST/mhrv-rs-android-universal-v1.9.31.apk) |
| `mhrv-rs-windows-amd64.zip` | 7.5 MB | [⬇️ Download](https://raw.githubusercontent.com/amindeist/LatestReleaseMirror/main/releases/therealaleph/MasterHttpRelayVPN-RUST/mhrv-rs-windows-amd64.zip) |
<!-- RELEASES_END -->
