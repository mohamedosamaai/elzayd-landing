# elzayd.com — صفحة هبوط لبيع النطاق

صفحة هبوط احترافية (ملف `index.html` واحد مستقل بالكامل — بدون أي build) لعرض نطاق **elzayd.com** للبيع، ثنائية اللغة (عربي RTL افتراضياً + زر تبديل للإنجليزية).

## المحتوى

- Hero باسم النطاق + زر **اشترِ الآن** يوجّه إلى صفحة النطاق على Dan.com
- زر **قدّم عرض سعر** (نفس صفحة Dan) + زر تواصل مباشر عبر البريد
- أقسام: لماذا النطاق؟ / حالات الاستخدام / خطوات الشراء الآمن / أسئلة شائعة
- SEO كامل: meta + Open Graph + Schema.org (Product/Offer) + canonical

## تعديل رابط الشراء

الرابط المستخدم حالياً هو الصيغة القياسية لصفحة Dan.com:

```
https://dan.com/buy-domain/elzayd.com
```

لو عندك رابط "Buy Now" مخصص من لوحة تحكم Dan، ابحث في `index.html` عن الرابط أعلاه واستبدله (موجود في 3 مواضع + الـ JSON-LD).

## النشر وربط الدومين (Cloudflare)

الصفحة static بالكامل، فأي استضافة تنفع. الأسهل مع إعدادك الحالي:

### الخيار الأول: Cloudflare Pages (موصى به — نفس حساب الـ DNS)

1. من لوحة Cloudflare → **Workers & Pages → Create → Pages**، واربط هذا الريبو (`elzayd-landing`) مباشرة — بدون build command، والـ output directory هو الجذر `/`.
2. بعد النشر → **Custom domains → Add** واكتب `elzayd.com` — سيضيف Cloudflare سجل الـ CNAME تلقائياً.
3. أضف `www` كـ custom domain أيضاً أو أنشئ Redirect Rule من `www` إلى الجذر.

### الخيار الثاني: GitHub Pages

1. من إعدادات هذا الريبو → **Pages**، فعّل Pages من فرع `main` والجذر `/`.
2. في إعدادات Pages ضع Custom domain = `elzayd.com`.
3. في Cloudflare DNS أضف:
   - `A` records للجذر `@` → عناوين GitHub Pages (`185.199.108.153` وأخواتها)
   - `CNAME` لـ `www` → `<username>.github.io`
   - اترك سجل الـ TXT الحالي (`_gh-...`) كما هو — خاص بتوثيق الدومين.
4. اجعل الـ Proxy status **DNS only** حتى يُصدر GitHub شهادة SSL، ثم فعّل البروكسي لاحقاً إن أردت.
