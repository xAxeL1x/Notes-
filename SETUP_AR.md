# إعداد Firebase المجاني وبناء الـAPK

## أولًا: سيرفر Firebase (مجاني، خطة Spark، من غير كارت)
1. افتحي console.firebase.google.com بحساب Google، واضغطي Add project. اكتبي أي اسم، وقفلي Google Analytics، واضغطي Create.
2. من القائمة: Build ثم Authentication، اضغطي Get started، واختاري Email/Password وفعّليه واضغطي Save.
3. من Build ثم Firestore Database، اضغطي Create database، واختاري أي منطقة، وابدئي بوضع Production واضغطي Enable.
4. افتحي تبويب Rules، وامسحي اللي مكتوب والصقي ده، واضغطي Publish:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```
5. من أيقونة الترس ثم Project settings، في تبويب General هتلاقي Project ID. وفي نفس الصفحة Web API Key. لو ما ظهرش، اضغطي Add app واختاري Web، وهتلاقي apiKey وprojectId.

## ثانيًا: بناء الـAPK على GitHub
1. اعملي مستودع جديد (Public أو Private) وارفعي كل الملفات اللي في الـzip، بما فيها مجلدي .github وassets (الأيقونة وشاشة البداية بتتولّد منهم تلقائي).
2. افتحي تبويب Actions، واختاري Build APK، واضغطي Run workflow.
3. بعد 5 إلى 10 دقايق نزّلي notes-apk من قسم Artifacts. فكّي الـzip وثبّتي app-debug.apk.

## ثالثًا: ربط التطبيق
افتحي التطبيق، وروحي الإعدادات، واكتبي Project ID وAPI key والإيميل وكلمة السر، واضغطي «حساب جديد» (أول مرة)، أو «دخول» (على باقي الأجهزة). نفس الحساب على كل أجهزتك.

## الأيقونة والشاشة الافتتاحية
مجلد assets فيه الأيقونة (icon-only وicon-foreground وicon-background) وشاشة البداية (splash). الـworkflow بيولّد منها كل مقاسات أندرويد تلقائيًا. لو عايزة تغيّري الأيقونة، استبدلي الصور دي بنفس الأسماء والمقاس (1024×1024 للأيقونة، و2732×2732 للـsplash).
