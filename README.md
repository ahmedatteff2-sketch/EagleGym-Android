# Eagle Gym - Android App

تطبيق Eagle Gym لنظام Android — Capacitor wrapper لتطبيق Eagle Gym الويب،
بيحمّل الواجهة من السيرفر مباشرة بدون أي إعداد إضافي.

> هذا الريبو متزامن مع مشروع Capacitor الموجود داخل
> [`Eagles-Backend/client/android`](https://github.com/ahmedatteff2-sketch/Eagles-Backend/tree/main/client/android)
> ومتسبَّتلَه `@capacitor/android` كـ Gradle module محلي عشان يبني standalone من غير Node/npm.

## 📋 المتطلبات

- **Android Studio** (Koala أو أحدث)
- **Android SDK** (يتم تحميله تلقائياً مع Android Studio)
- **Java JDK 21** (يأتي مع Android Studio Koala+)

## 🚀 طريقة التثبيت والبناء

### الطريقة الأسرع (من غير PC) — تحميل APK جاهز من GitHub Actions

كل ما تـ push كود على branch `master` (أو تفتح PR) GitHub Actions هيبني الـ APK تلقائياً.

1. افتح تبويب **Actions** في الريبو على GitHub.
2. اختار آخر run ناجح من workflow **Build APK**.
3. انزل تحت لقسم **Artifacts** وحمّل:
   - `EagleGym-release-apk` (موصى به)
   - `EagleGym-debug-apk` (للتجربة)
4. فك ضغط الزيب اللي اتحمل، وثبّت ملف الـ APK على موبايلك (تحتاج تفعّل "السماح بالتثبيت من مصادر مجهولة").

> لو عايز توقّع الـ release APK بـ keystore ثابت بدل الـ ad-hoc keystore اللي الـ workflow بينشئه كل مرة،
> ضيف الـ secrets دي في **Settings → Secrets and variables → Actions** على الريبو:
> - `KEYSTORE_BASE64` — محتوى الـ `.jks` بصيغة base64 (`base64 -w0 keystore.jks`)
> - `KEYSTORE_PASSWORD`
> - `KEY_ALIAS`
> - `KEY_PASSWORD`

لو دفعت tag بصيغة `v*` (مثل `v1.0.0`) الـ workflow هيعمل **GitHub Release** ويرفع الـ APKs فيها مباشرة.

### الطريقة المحلية (لو عندك PC)

#### 1. استنساخ المشروع

```bash
git clone https://github.com/ahmedatteff2-sketch/EagleGym-Android.git
cd EagleGym-Android
```

### 2. فتح المشروع في Android Studio

1. افتح **Android Studio**
2. اختر **Open**
3. انتقل إلى مجلد المشروع
4. انتظر **Gradle Sync** حتى يكتمل (أول مرة سيحمل Gradle 8.14.3 + AndroidX dependencies)

### 3. بناء الـ APK

#### للتجربة (Debug APK):
- **Build → Build Bundle(s) / APK(s) → Build APK(s)**
- الـ APK سيكون في: `app/build/outputs/apk/debug/app-debug.apk`

#### للنشر (Release APK):
- **Build → Generate Signed Bundle / APK**
- اختر **APK**
- أنشئ **Key Store** جديد (أول مرة فقط):
  - File: `keystore.jks`
  - Password: اختر كلمة مرور قوية
  - Key alias: `eagle-gym`
  - Key password: اختر كلمة مرور
- اختر **release** واضغط **Finish**
- الـ APK سيكون في: `app/build/outputs/apk/release/app-release.apk`

## 📱 معلومات التطبيق

| الخصيصة | القيمة |
|---|---|
| **اسم التطبيق** | Eagle Gym |
| **Package Name** | com.eaglegym.app |
| **Minimum SDK** | Android 5.0 (API 21) |
| **Target SDK** | Android 14 (API 34) |
| **Server URL** | https://eagles-backend-fu2p.onrender.com |

## ⚙️ الإعدادات

### تغيير Server URL

لو عايز تغير السيرفر:

1. افتح `app/src/main/assets/capacitor.config.json`
2. عدّل قيمة `server.url`

```json
{
  "server": {
    "url": "https://your-server.com"
  }
}
```

### تغيير اسم التطبيق

1. افتح `app/src/main/res/values/strings.xml`
2. عدّل `app_name`

## 🔧 حل المشاكل

### Gradle sync فشل

```bash
# حذف cache وإعادة المحاولة
./gradlew clean
```

### خطأ "SDK location not found"

في Android Studio:
1. **File → Settings → Languages & Frameworks → Android SDK**
2. في **SDK Location** اختر مسار الـ SDK
3. أو أنشئ مجلد `C:\gradle-home` وضبط `GRADLE_USER_HOME` environment variable إليه

### خطأ "relative path" في Gradle

أضف environment variable:
- Name: `GRADLE_USER_HOME`
- Value: `C:\gradle-home`

## 📦 الخواص المتوفرة

- 🌙 Dark/Light mode toggle
- 🔔 تنبيهات صوتية للتايمر
- 📈 الأرقام الشخصية + حاسبة 1RM
- 🏅 الإنجازات والشارات
- 💬 ملاحظات المدرب
- 📷 مقارنة صور التقدم
- 📅 تقويم التمارين
- 📱 Push Notifications
- 📊 تقرير شهري
- 🏷️ فئات الأعضاء (VIP/عادي/تجريبي)

## 📄 الترخيص

© 2024 Eagle Gym
