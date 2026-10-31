# سوق القامشلي — تطبيق Android

تطبيق سوق إلكتروني محلي لبيع وشراء الموبايلات والأجهزة الإلكترونية في مدينة القامشلي.

## المزايا المتوفرة (MVP)
- تسجيل دخول / إنشاء حساب (Email + Password عبر Firebase Auth)
- نشر إعلان: صور (حتى 6) + سعر + وصف + فئة + حالة (جديد/مستعمل)
- تصفح الإعلانات + بحث نصي + فلترة حسب الفئة ونطاق السعر
- صفحة تفاصيل الإعلان
- تواصل مباشر: زر اتصال هاتفي + شات داخل التطبيق بين البائع والمشتري
- الملف الشخصي: بيانات المستخدم + قائمة إعلاناته

## التقنيات
- Kotlin + Jetpack Compose + Material 3
- Firebase: Authentication, Firestore, Storage
- Coil لتحميل الصور

## خطوات التشغيل

### 1) تثبيت Android Studio
نزّل Android Studio (أحدث إصدار) وافتح هذا المجلد (`SouqQamishli`) كمشروع موجود (Open an existing project).

### 2) ربط المشروع بـ Firebase (ضروري جداً)
التطبيق يحتاج قاعدة بيانات حقيقية، فلازم تربطه بمشروع Firebase خاص فيك:

1. روح إلى https://console.firebase.google.com وأنشئ مشروع جديد.
2. أضف تطبيق Android جديد داخل المشروع، وحط Package name بالضبط:
   `com.souq.qamishli`
3. نزّل ملف `google-services.json` اللي بيعطيك ياه Firebase، وحطه داخل مجلد:
   `app/google-services.json`
   (هذا الملف غير موجود حالياً بالمشروع لأنه خاص فيك ومربوط بمفاتيحك).
4. من قائمة Firebase اليسرى فعّل:
   - **Authentication** → Sign-in method → فعّل **Email/Password**
   - **Firestore Database** → أنشئ قاعدة بيانات (Production mode)
   - **Storage** → فعّله لتخزين صور الإعلانات
5. انسخ محتوى ملف `firestore.rules` من هذا المشروع إلى Firestore Rules بالكونسول، ومحتوى `storage.rules` إلى Storage Rules، وانشرهم (Publish).

### 3) تشغيل التطبيق
بعد ما تحط `google-services.json`، اعمل Sync للمشروع بـ Android Studio (File → Sync Project with Gradle Files)، وبعدين شغّل التطبيق على موبايل حقيقي أو محاكي (Run ▶).

## بنية المشروع
```
app/src/main/java/com/souq/qamishli/
├── MainActivity.kt
├── SouqApp.kt
├── model/Models.kt          # User, Listing, ChatThread, ChatMessage
├── data/                    # Firebase repositories
│   ├── AuthRepository.kt
│   ├── ListingRepository.kt
│   └── ChatRepository.kt
├── ui/
│   ├── SouqNavGraph.kt       # التنقل بين الشاشات
│   ├── theme/                 # ألوان التطبيق
│   ├── components/            # ListingCard
│   └── screens/                # كل الشاشات
```

## اللوغو وهوية التطبيق
الأيقونة الحالية placeholder بسيطة (حقيبة تسوق). لما يصير عندك لوغو نهائي للتطبيق:
- استبدل `app/src/main/res/drawable/ic_launcher_foreground.xml`
- أو أرسل لي صورة اللوغو وبجهزلك الأيقونة بكل الأحجام المطلوبة.

## أفكار للتوسعة لاحقاً
- تسجيل دخول برقم الهاتف (OTP) بدل البريد فقط
- إشعارات push عند وصول رسالة جديدة
- تقييم البائعين
- لوحة تحكم لحذف الإعلانات المخالفة
