# تطبيق الخربقة لأندرويد (APK)

التطبيق يعرض اللعبة (`app/src/main/assets/index.html`) بملء الشاشة داخل WebView، مع زر الرجوع، وبقاء الشاشة مضاءة، وحفظ الاسم والسجل.

## قبل البناء: إعدادات اللعب عبر الإنترنت
افتح `app/src/main/assets/index.html` وضع إعدادات مشروعك في `FIREBASE_CONFIG` (الخطوات في `firebase-setup-ar.md`).
داخل التطبيق يعمل الموقع من العنوان `https://appassets.androidplatform.net`. إن رفضت Firebase الدخول المجهول، أضف هذا النطاق في
Authentication ← Settings ← Authorized domains.

## الطريقة 1: بناء الـAPK على GitHub (بلا تثبيت أي برنامج)
1. أنشئ حساباً مجانياً على github.com ثم مستودعاً جديداً (New repository) واجعله Private إن شئت.
2. ارفع كل محتويات هذا المجلد إلى المستودع (Add file ← Upload files).
   إن لم يُرفع المجلد المخفي `.github`: اختر Add file ← Create new file، واكتب الاسم `.github/workflows/build-apk.yml`، والصق فيه محتوى الملف `build-apk.yml` الموجود في جذر المشروع.
3. افتح تبويب **Actions** ← **Build APK** ← **Run workflow** (يعمل أيضاً تلقائياً عند الرفع). ينتهي البناء خلال 3 إلى 6 دقائق.
4. افتح التشغيل المكتمل ونزّل الملف **kharbga-apk** من قسم Artifacts، ثم فك الضغط لتحصل على `app-debug.apk`.
5. انقل الملف إلى هاتفك وافتحه. اسمح بـ«التثبيت من مصادر غير معروفة» إن طلب الهاتف ذلك.

## الطريقة 2: Android Studio
افتح المجلد في Android Studio ← انتظر مزامنة Gradle ← Build ← Build APK(s). الملف في `app/build/outputs/apk/debug/`.

## ملاحظات
- الـAPK موقَّع بمفتاح تجريبي (debug)، وهو مناسب للتثبيت المباشر. للنشر على Google Play تحتاج حزمة AAB موقَّعة بمفتاحك الخاص.
- الخطوط تُحمَّل من Google Fonts، فبدون إنترنت تظهر خطوط النظام. اللعب ضد الحاسوب يعمل دون اتصال.
- لتحديث اللعبة لاحقاً: استبدل `app/src/main/assets/index.html` (احتفظ بسطر `window.__back` في آخره وتعديل `wv` في كود ملء الشاشة) وأعد البناء. ارفع `versionCode` في `app/build.gradle` عند كل إصدار.
- اسم الحزمة: `com.kharbga.game`.

## النشر على Google Play
راجع `play-store/PLAY-CHECKLIST-ar.md`. الناتج المطلوب هو ملف **AAB** (يُبنى في GitHub Actions بعد إضافة أسرار التوقيع)، ومستوى `targetSdk` الحالي 36.
