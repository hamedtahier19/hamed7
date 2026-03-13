فكرة التطبيق (Vision)

تطبيق حضور وغياب خاص بالمعلم فقط
يساعد الدكتور على:

تسجيل الحضور والغياب

متابعة تحسّن الطالب

حساب نسب الحضور تلقائياً

تصدير التقارير (PDF / Excel)

رؤية إحصائيات واضحة وسريعة

التطبيق لا يُستخدم من الطالب ❌
فقط واجهة معلم ذكية وبسيطة ✅

---

## تلخيص المتطلبات وتحويلها إلى خطة تنفيذ (Flutter)

### 1) ملخص المتطلبات (Requirements Summary)

#### الهدف

تطبيق لإدارة **الحضور والغياب** خاص بالمعلم فقط (Teacher Only)، يسهّل تسجيل الحالات، يعرض إحصائيات وتنبيهات، ويصدر تقارير PDF/Excel.

#### المستخدمون والصلاحيات

- المعلم فقط هو المستخدم الأساسي.
- التطبيق لا يُستخدم من الطالب.
- تسجيل دخول للمعلم.

#### الوظائف الأساسية (MVP)

- تسجيل حالة الطالب لكل محاضرة: حاضر / غائب / متأخر.
- حفظ سريع (بنقرة واحدة) وتغيير الحالة بسهولة.
- حساب نسب الحضور تلقائياً.
- Dashboard نظرة عامة + تنبيهات للطلاب المهددين.
- ملف طالب: بيانات + نسبة حضور + عدد الغيابات + رسم يوضح التحسن + تنبيه تجاوز الحد.
- Reports: تصدير PDF / Excel.
- Analytics: رسوم/إحصائيات مع فلترة حسب مادة/شعبة/فترة.

#### UI/UX

- Minimal & Academic.
- ألوان هادئة (أزرق – أخضر – رمادي).
- Cards + Charts بسيطة.

---

### 2) خطة التنفيذ (Execution Plan)

#### مبدأ التنفيذ

العمل يكون مباشرة: نبني مشروع Flutter ثم ننفذ البيانات والشاشات بالتدرّج (MVP أولاً) ثم التحسينات.

#### المرحلة (0): بدء المشروع (Bootstrap)

- إنشاء مشروع Flutter جديد.
- ضبط Theme (ألوان/خطوط) من البداية.
- تجهيز ملاحة واضحة (Bottom Navigation) للشاشات الأساسية.

#### المرحلة (1): البيانات (Data Model) + التخزين (Storage)

##### الكيانات الأساسية

- Teacher: id, name, universityName, email
- Subject: id, name
- Section: id, subjectId, name
- Student: id (الرقم الجامعي), fullName, sectionId
- LectureSession: id, subjectId, sectionId, dateTime
- AttendanceRecord: id, sessionId, studentId, status(P/A/L), note(اختياري)

##### عمليات البيانات المطلوبة

- CRUD للمواد/الشعب/الطلاب.
- إنشاء Session لكل محاضرة.
- حفظ AttendanceRecord لكل طالب داخل session.

##### الحسابات (Metrics)

- نسبة الحضور = (الحضور + التأخر * معامل) / إجمالي المحاضرات.
- At Risk حسب حد/نسبة الحرمان في الإعدادات.

#### المرحلة (2): تنفيذ الشاشات بالترتيب (Screens Order)

1) Splash
2) Login (Teacher Only)
3) Dashboard
4) Subjects Screen -> داخلها Sections
5) Attendance Screen (تسجيل يومي مع P/A/L)
6) Student Profile
7) Analytics
8) Reports & Export
9) Settings

#### المرحلة (3): التقارير (PDF / Excel)

##### محتوى التقرير

- Header: الجامعة + اسم المعلم + المادة/الشعبة + الفترة.
- جدول: التاريخ + اسم الطالب + الحالة.
- ملخص: إجمالي المحاضرات + نسب الحضور + عدد الغيابات.

##### نطاقات التقرير

- مادة كاملة.
- شعبة محددة.
- طالب واحد.

---

### 3) خطة البدء مباشرة (Start Now Checklist)

1) إنشاء مشروع Flutter جديد.
2) إعداد Theme + الملاحة الأساسية.
3) تنفيذ Data Model + Storage محلي.
4) تنفيذ الشاشات: Splash -> Login -> Dashboard -> Subjects/Sections -> Attendance -> Student Profile -> Reports.
5) بعد اكتمال الـ MVP: Analytics ثم تحسينات وإعدادات متقدمة.

---

### 4) رفع المشروع وبناء APK (حسب الموجود في الملف)

بعد الانتهاء:

1) ترفعه على GitHub
2) تعيد بناء APK
3) تثبّت الإصدار الجديد

#### كيف تربط GitHub مع Flutter (من الصفر)

##### الخطوة 1: إنشاء Repository

GitHub → New Repository
الاسم: attendance_app
Public أو Private

##### الخطوة 2: ربط المشروع المحلي

داخل مشروع Flutter:

git init
git add .
git commit -m "Initial Flutter project"
git branch -M main
git remote add origin https://github.com/USERNAME/attendance_app.git
git push -u origin main

##### الخطوة 3: بعد كل تعديل

git add .
git commit -m "Update attendance UI"
git push

##### بنية .gitignore (مهم)

Flutter ينشئه تلقائيًا ✔️
لا ترفع:

build/
.android/
.ios/

##### نصيحة احترافية جدًا

لا ترفع APK داخل الكود
ارفعه فقط داخل GitHub Releases ✅

---

### 5) مراجعة نهائية (Final Verification)

- كل الشاشات الأساسية موجودة: Login / Dashboard / Subjects / Attendance / Student Profile / Reports / Settings.
- At Risk + نسب الحضور تعمل وفق إعدادات الحرمان.
- التصدير يعمل: PDF + Excel وبالنطاقات الثلاثة.
- البيانات محفوظة بدون فقد.
- لا توجد أي واجهة للطالب.
- المشروع مرفوع على GitHub وملف APK مرفوع داخل Releases فقط.

🧠 تقسيم التطبيق (App Architecture)
1️⃣ الواجهة الرئيسية (Dashboard)

قلب التطبيق – أول ما يفتحه الدكتور

🔹 تعرض:

عدد الطلاب الكلي

نسبة الحضور اليوم

نسبة الغياب

أكثر الطلاب انتظامًا

تنبيه عن طلاب مهددين بالحرمان

📊 عناصر UI:

Cards

Progress Rings

Charts بسيطة

ألوان هادئة (أزرق – أخضر – رمادي)

2️⃣ قسم الشعب / المواد

📚

قائمة المواد التي يدرسها المعلم

داخل كل مادة:

الشعب

عدد الطلاب

نسبة الحضور العامة

3️⃣ قسم تسجيل الحضور

📝

قائمة الطلاب

أزرار:

حاضر ✅

غائب ❌

متأخر ⏱️

تسجيل سريع (Swipe أو Tap)

💡 UX:

تسجيل بنقرة واحدة

تغيير الحالة بسهولة

حفظ تلقائي

4️⃣ ملف الطالب (Student Profile)

👤
لكل طالب صفحة خاصة تشمل:

الاسم + الرقم الجامعي

نسبة الحضور

عدد الغيابات

رسم بياني يوضح التحسن أو التراجع

تنبيه في حال تجاوز حد الغياب

5️⃣ الإحصائيات والتحليلات

📈

رسوم بيانية:

الحضور الشهري

مقارنة بين الطلاب

تحسّن الطالب عبر الزمن

فلترة:

حسب مادة

حسب شعبة

حسب فترة زمنية

6️⃣ التقارير والتصدير

📤

تصدير:

PDF رسمي

Excel

تقارير:

طالب واحد

شعبة كاملة

مادة كاملة

7️⃣ الإعدادات

⚙️

اسم المعلم

اسم الجامعة

نسبة الحرمان

لغة التطبيق

الوضع الليلي 🌙

🎨 أسلوب UI / UX المقترح

Minimal & Academic

خطوط:

Cairo / Poppins

ألوان:

Primary: Dark Blue

Secondary: Green

Background: Light Grey

أيقونات: Material Icons

تصميم Cards واضح ومريح للعين

📱 تصور بصري للتطبيق (UI Inspiration)

هذه الصور للتغذية البصرية فقط
نفس الفكرة لكن يتم تنفيذها بـ Flutter

🧩 هيكل الشاشات (Flutter Screens)
- Splash Screen
- Login (Teacher Only)
- Dashboard
- Subjects Screen
- Attendance Screen
- Student Profile
- Analytics
- Reports
- Settings
الواجهة الرئيسية (Dashboard) ⭐⭐⭐

أهم شاشة في التطبيق

🎯 ماذا يرى المعلم؟

📊 نسبة الحضور العامة

❌ نسبة الغياب

👥 عدد الطلاب

📅 عدد المحاضرات

⚠️ تنبيه طلاب منخفضي الحضور

🧱 مكونات الواجهة:

AppBar بسيط

اسم المادة

أيقونة الإعدادات

Cards إحصائية

Attendance %

Absence %

Chart

تحسّن / تراجع الحضور

زر سريع

➕ تسجيل حضور محاضرة جديدة




🧠 Architecture العامة للتطبيق

أنت عندك 3 طبقات رئيسية:

Frontend (Web + Flutter)
        ↓
Backend (API)
        ↓
Database (PostgreSQL)

1️⃣ Backend + Database
🐘 PostgreSQL (اختيار ممتاز 👏)
لماذا PostgreSQL؟

قوي جدًا للمشاريع الجامعية والاحترافية

يدعم العلاقات (Relations) بشكل ممتاز

آمن

سريع

مناسب للتحليلات والإحصائيات

يعمل بشكل ممتاز مع Flutter و React

✔️ اختيارك صحيح 100%

2️⃣ Frontend (Web)

أنت اخترت:

HTML

CSS

JavaScript

Bootstrap

React.js

لماذا هذا الاختيار جيد؟

React ممتاز لـ Dashboard المعلم

Bootstrap يسرّع التصميم

JS للتحكم والمنطق

يمكن استخدامه كـ:

لوحة تحكم Web

أو نسخة Web للتطبيق

3️⃣ Flutter (Mobile App)

Flutter (Dart) سيكون:

تطبيق الجوال

يستهلك نفس الـ API

لا يتصل مباشرة بقاعدة البيانات ❌

يتصل بالـ Backend فقط ✅

🗄️ تصميم قاعدة البيانات (Database Design)
🎯 الهدف

تسجيل حضور

تتبع طالب

حساب نسب

تقارير

إحصائيات

📦 الجداول الأساسية (Core Tables)
1️⃣ teachers
id (PK)
full_name
email
password_hash
university_name
created_at

2️⃣ subjects
id (PK)
teacher_id (FK)
subject_name
semester

3️⃣ classes (الشُعب)
id (PK)
subject_id (FK)
class_name

4️⃣ students
id (PK)
full_name
student_number

5️⃣ enrollments (ربط الطالب بالشعبة)
id (PK)
student_id (FK)
class_id (FK)

6️⃣ attendance
id (PK)
student_id (FK)
class_id (FK)
date
status (present / absent / late)

7️⃣ attendance_summary (اختياري – للأداء)
student_id
class_id
attendance_percentage
absent_count

🔗 العلاقات (Relations)

Teacher ⟶ Subjects (1:N)

Subject ⟶ Classes (1:N)

Class ⟶ Students (N:N)

Student ⟶ Attendance (1:N)

📊 حساب نسبة الحضور (Logic)
نسبة الحضور =
(عدد أيام الحضور ÷ مجموع الحصص) × 100


💡 الأفضل:

الحساب يتم في Backend

Flutter و React فقط تعرض النتيجة

⚙️ Backend Technology (مهم جدًا)
أفضل الخيارات مع PostgreSQL:
✅ Node.js + Express

سهل

شائع

يعمل ممتاز مع React و Flutter

أو:
✅ NestJS (احترافي أكثر)

منظم

مناسب لمشاريع جامعية كبيرة

🔌 API Structure (مثال)
POST   /login
GET    /dashboard
GET    /subjects
GET    /classes/:id/students
POST   /attendance
GET    /students/:id/report
GET    /export/pdf

📱 أفضل قاعدة بيانات لـ Flutter؟

⚠️ Flutter لا يستخدم PostgreSQL مباشرة

الخيارات الصحيحة:
✅ PostgreSQL عبر API (أفضل حل)

Backend هو الوسيط

أمان عالي

أداء ممتاز

❌ لا أنصح:

SQLite فقط (محدود)

Firebase (غير مناسب للتحليلات المعقدة)

✔️ الحل المثالي:
Flutter
   ↓ HTTP
Backend (Node/Nest)
   ↓ SQL
PostgreSQL

🧩 Flutter Packages مفيدة
http
provider / bloc
charts_flutter
pdf
intl

🚀 الخطوة الجاية؟

أقدر:
1️⃣ أصمم لك ER Diagram
2️⃣ أكتب لك SQL كامل
3️⃣ أجهّز Backend API
4️⃣ أبدأ معك Flutter Screens + Logic
5️⃣ أكتب لك Documentation جامعية

📌 قلّي: نبدأ بأي نقطة؟




أنت تريد موقع يعمل على الهاتف كأنه تطبيق 📱
وتقدر:

تحمّله على جهازك

ترفعه على GitHub

تعدّل عليه في أي وقت


يعمل على الهاتف
✅ يُثبَّت مثل تطبيق (أيقونة على الشاشة)
✅ يعمل بدون إنترنت (جزئياً)
✅ ترفعه على GitHub
✅ تعدّل عليه بسهولة
✅ لا تحتاج Play Store


رفع المشروع على GitHub
1️⃣ إنشاء Repository جديد

افتح GitHub

New Repository

اسم المشروع

2️⃣ رفع المشروع
git init
git add .
git commit -m "Initial attendance app"
git branch -M main
git remote add origin https://github.com/USERNAME/attendance-app.git
git push -u origin main

🌍 الخطوة 5: نشر الموقع (GitHub Pages)
npm install gh-pages --save-dev


في package.json:

"homepage": "https://USERNAME.github.io/attendance-app",
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}


ثم:

npm run deploy


🎉 الموقع أصبح أونلاين + قابل للتثبيت

✏️ التعديل على الموقع لاحقاً
git add .
git commit -m "Update UI"
git push
npm run deploy


ماذا يعمل GitHub بالضبط؟

✔️ يحفظ كود Flutter
✔️ يسمح لك بالتعديل
✔️ يسمح لك بالرجوع لإصدارات قديمة
✔️ يسهل تسليم المشروع للجامعة

📱 كيف يعمل التطبيق فعليًا إذًا؟
الطريق الصحيح:
GitHub (كود فقط)
     ↓
Flutter SDK (يبني التطبيق)
     ↓
APK / AAB
     ↓
تثبيت على الهاتف

🛠️ الخطوات الصحيحة لتشغيل التطبيق
1️⃣ ترفع الكود على GitHub
git push

2️⃣ تبني التطبيق محليًا
flutter build apk

3️⃣ تثبيت التطبيق على الهاتف

تنسخ ملف APK

تثبّته يدويًا

🚀 لو غيرت الكود؟

تعدّل الكود

ترفعه على GitHub

تعيد بناء APK

تثبّت الإصدار الجديد



كيف تربط GitHub مع Flutter (من الصفر)
🔹 الخطوة 1: إنشاء Repository

GitHub → New Repository

الاسم: attendance_app

Public أو Private

🔹 الخطوة 2: ربط المشروع المحلي

داخل مشروع Flutter:

git init
git add .
git commit -m "Initial Flutter project"
git branch -M main
git remote add origin https://github.com/USERNAME/attendance_app.git
git push -u origin main

🔹 الخطوة 3: بعد كل تعديل
git add .
git commit -m "Update attendance UI"
git push

🔹 بنية .gitignore (مهم)

Flutter ينشئه تلقائيًا ✔️
لا ترفع:

build/
.android/
.ios/

🔥 نصيحة احترافية جدًا

لا ترفع APK داخل الكود
ارفعه فقط داخل GitHub Releases ✅


وفي النهاية اريد {flutter build app}
