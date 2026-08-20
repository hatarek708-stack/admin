# ⚠️ حل المشكلة نهائياً — اتبع هذه الخطوات

## المشكلة
لا يمكنك إضافة/تعديل/حذف الباقات والمتاجر لأن:
1. حسابك غير مُسجّل في `admin_users`
2. سياسات RLS تمنع العمليات
3. `auto_setup_first_admin` RPC غير موجود

## الحل (3 خطوات بسيطة)

### الخطوة 1: افتح Supabase SQL Editor

🔗 اضغط هنا: https://supabase.com/dashboard/project/tgqkathfzrnkiyxwzkbc/sql/new

### الخطوة 2: انسخ والصق هذا SQL

انسخ كل المحتوى من هذا الرابط:
```
https://raw.githubusercontent.com/hatarek708-stack/shopevelo/main/supabase/migration_auto_setup_admin.sql
```

أو انسخه مباشرة من الصندوق أدناه:

```sql
-- انسخ من: migration_auto_setup_admin.sql
```

### الخطوة 3: اضغط Run

ستظهر رسالة "Success. No rows returned." — هذا طبيعي.

## بعد التطبيق

1. افتح admin-local: https://hatarek708-stack.github.io/admin/
2. اعمل Hard Refresh: `Ctrl + Shift + R`
3. سجّل دخول ببريدك وكلمة مرورك
4. ستظهر رسالة: "✅ تم تعيينك كأدمن أول تلقائيًا"
5. جرب إضافة/تعديل/حذف الباقات — ستعمل!

## ماذا يفعل هذا الـ migration؟

1. **ينشئ RPC `auto_setup_first_admin`**:
   - أول مستخدم يسجل دخول يصبح `super_admin` تلقائياً
   - لو يوجد super_admin، يتحقق من صلاحيات المستخدم الحالي

2. **يُعيد تطبيق كل سياسات RLS** لتستخدم `is_admin_or_staff()`

3. **يُصلح triggers** (`protect_store_owner`, `protect_profile_sensitive`)

4. **يضبط `profiles.role = 'admin'`** لكل أدمن نشط

## للتشخيص

لو استمرت المشاكل، افتح صفحة التشخيص:
```
https://hatarek708-stack.github.io/admin/diag-full.html
```
سجّل دخول وسترى تقريراً مفصلاً عن صلاحياتك.
