# Administrator Quick Reference Guide
# Sotuvchi Arizalarini Boshqarish Bo'yicha Qo'llanma

## 📋 Tizimga Kirish

1. Admin hisobingiz bilan tizimga kiring
2. Chap tarafdagi menyudan **"Sotuvchi arizalari"** bo'limini tanlang
3. Yoki to'g'ridan-to'g'ri `/admin/seller-applications` sahifasiga o'ting

---

## 👥 Arizalarni Ko'rish

### Filtrlar

Arizalarni holati bo'yicha filtrlash:
- **Barchasi** - Barcha arizalar
- **Kutilmoqda** - Ko'rib chiqilishi kerak bo'lgan arizalar
- **Tasdiqlangan** - Tasdiqlangan arizalar
- **Rad etilgan** - Rad etilgan arizalar

### Ariza Ma'lumotlari

Har bir arizada quyidagi ma'lumotlar ko'rsatiladi:
- Foydalanuvchi ismi
- Telefon raqami
- Korxona nomi
- Ariza topshirilgan sana
- Holati (Kutilmoqda/Tasdiqlangan/Rad etilgan)

---

## ✅ Arizani Tasdiqlash

### Qadamlar:

1. **Arizani tanlang**
   - Kutilayotgan arizalar ro'yxatidan kerakli arizani toping
   - "Tasdiqlash" tugmasini bosing

2. **Ma'lumotlarni tekshiring**
   - Foydalanuvchi ismi va familiyasi
   - Telefon raqami
   - Korxona nomi
   - Manzil
   - Foydalanuvchi ID

3. **Izoh qo'shing (ixtiyoriy)**
   - Kerak bo'lsa, administrator izohi qo'shing
   - Masalan: "Barcha hujjatlar to'g'ri"

4. **Tasdiqlang**
   - "Tasdiqlash" tugmasini bosing
   - Tizim avtomatik ravishda:
     - Foydalanuvchi rolini "sotuvchi"ga o'zgartiradi
     - Ariza holatini "tasdiqlangan"ga o'zgartiradi
     - Rol o'zgarishini tarixga yozadi
     - Foydalanuvchiga xabar yuboradi

### Natija:

✅ Foydalanuvchi endi sotuvchi hisoblanadi va quyidagi imkoniyatlarga ega bo'ladi:
- Mahsulot qo'shish
- Buyurtmalarni ko'rish
- Sotuvchi paneliga kirish

---

## ❌ Arizani Rad Etish

### Qadamlar:

1. **Arizani tanlang**
   - Kutilayotgan arizalar ro'yxatidan kerakli arizani toping
   - "Rad etish" tugmasini bosing

2. **Rad etish sababini ko'rsating** ⚠️ MAJBURIY
   - Rad etish sababini yozing
   - Masalan: "Telefon raqami noto'g'ri", "Korxona nomi aniq emas"
   - Bu maydon to'ldirilishi shart!

3. **Tasdiqlang**
   - "Rad etish" tugmasini bosing
   - Tizim avtomatik ravishda:
     - Ariza holatini "rad etilgan"ga o'zgartiradi
     - Rad etish sababini saqlaydi
     - Foydalanuvchiga xabar yuboradi

### Natija:

❌ Ariza rad etiladi va foydalanuvchi:
- Rad etish sababini ko'radi
- Ma'lumotlarni to'g'rilab, qayta ariza topshirishi mumkin

---

## 📊 Rol O'zgarishlari Tarixi

### Kirish:

1. Chap tarafdagi menyudan **"Rol o'zgarishlari tarixi"** bo'limini tanlang
2. Yoki to'g'ridan-to'g'ri `/admin/role-history` sahifasiga o'ting

### Ma'lumotlar:

Har bir rol o'zgarishida quyidagi ma'lumotlar ko'rsatiladi:
- **Foydalanuvchi** - Kim o'zgartirildi
- **Eski rol** → **Yangi rol**
- **O'zgartirdi** - Qaysi administrator o'zgartirdi
- **Sabab** - O'zgartirish sababi (masalan, "Seller application approved")
- **Sana va vaqt** - Qachon o'zgartirildi

### Filtrlar:

- **Barchasi** - Barcha rol o'zgarishlari
- **Sotuvchi bo'lganlar** - Faqat sotuvchiga aylantirilganlar
- **Admin bo'lganlar** - Faqat adminga aylantirilganlar

### Statistika:

- Jami o'zgarishlar soni
- Sotuvchi bo'lganlar soni
- Admin bo'lganlar soni

---

## 🔒 Xavfsizlik Qoidalari

### Sizning Huquqlaringiz:

✅ **Qila olasiz:**
- Barcha arizalarni ko'rish
- Arizalarni tasdiqlash
- Arizalarni rad etish
- Rol o'zgarishlari tarixini ko'rish
- Administrator izohi qo'shish

❌ **Qila olmaysiz:**
- Bir xil arizani ikki marta tasdiqlash
- Tasdiqlangan arizani qayta ko'rib chiqish
- Foydalanuvchi arizasini o'zgartirish

### Tizim Himoyasi:

🛡️ **Avtomatik Himoya:**
- Faqat adminlar arizalarni ko'rib chiqishi mumkin
- Foydalanuvchilar faqat o'z arizalarini ko'radi
- Bir foydalanuvchi faqat bitta kutilayotgan ariza topshirishi mumkin
- Barcha harakatlar tarixga yoziladi
- Rol o'zgarishlari audit logiga yoziladi

---

## 📝 Eng Ko'p Uchraydigan Savollar

### 1. Ariza topshirilgandan keyin foydalanuvchi uni o'zgartira oladimi?

❌ **Yo'q.** Ariza topshirilgandan keyin foydalanuvchi uni o'zgartira olmaydi. Agar ma'lumotlar noto'g'ri bo'lsa, arizani rad eting va sabab ko'rsating.

### 2. Bir foydalanuvchi nechta ariza topshirishi mumkin?

📌 **Faqat bitta kutilayotgan ariza.** Agar ariza rad etilsa, foydalanuvchi qayta ariza topshirishi mumkin.

### 3. Tasdiqlangandan keyin foydalanuvchi darhol sotuvchi bo'ladimi?

✅ **Ha.** Tizim avtomatik ravishda foydalanuvchi rolini "sotuvchi"ga o'zgartiradi va u darhol sotuvchi paneliga kirish huquqiga ega bo'ladi.

### 4. Rad etish sababini yozish majburiymi?

✅ **Ha.** Rad etish sababini yozish majburiy. Bu foydalanuvchiga nima noto'g'ri ekanligini tushunishga yordam beradi.

### 5. Tasdiqlangan arizani bekor qila olamanmi?

❌ **Yo'q.** Tasdiqlangan arizani bekor qilish mumkin emas. Agar xato qilgan bo'lsangiz, foydalanuvchi rolini "Foydalanuvchi Rollari" bo'limidan o'zgartirishingiz kerak.

### 6. Rol o'zgarishlari tarixi nima uchun kerak?

📊 **Audit uchun.** Barcha rol o'zgarishlari tarixga yoziladi. Bu:
- Kim, qachon, nima qilganini ko'rish
- Xatoliklarni topish
- Tizim xavfsizligini ta'minlash uchun kerak

---

## ⚠️ Muhim Eslatmalar

1. **Diqqat bilan tekshiring**
   - Arizani tasdiqlashdan oldin barcha ma'lumotlarni diqqat bilan tekshiring
   - Telefon raqami to'g'ri formatda ekanligini tekshiring
   - Korxona nomi aniq va tushunarli ekanligini tekshiring

2. **Rad etish sababini aniq yozing**
   - Foydalanuvchi nima qilishi kerakligini tushunishi uchun aniq sabab yozing
   - Masalan: "Telefon raqami noto'g'ri formatda" yoki "Korxona nomi juda qisqa"

3. **Tez javob bering**
   - Foydalanuvchilar arizalariga tez javob kutishadi
   - Kutilayotgan arizalarni muntazam tekshiring

4. **Rol o'zgarishlarini kuzatib boring**
   - Vaqti-vaqti bilan rol o'zgarishlari tarixini ko'rib chiqing
   - Shubhali harakatlarni aniqlang

---

## 🆘 Yordam

Agar muammo yuzaga kelsa:

1. **Arizalar ko'rinmayapti?**
   - Sahifani yangilang (F5)
   - Admin hisobingiz bilan kirganingizni tekshiring

2. **Tasdiqlash ishlamayapti?**
   - Ariza holati "kutilmoqda" ekanligini tekshiring
   - Brauzer konsolini tekshiring (F12)

3. **Rol o'zgarmayapti?**
   - Rol o'zgarishlari tarixini tekshiring
   - Foydalanuvchi profilini tekshiring

4. **Boshqa muammolar?**
   - Brauzer konsolini tekshiring (F12)
   - Ma'lumotlar bazasi migratsiyalari qo'llanilganligini tekshiring

---

## 📞 Texnik Ma'lumotlar

### Sahifalar:
- Arizalar ro'yxati: `/admin/seller-applications`
- Rol o'zgarishlari: `/admin/role-history`

### Ma'lumotlar Bazasi:
- Arizalar jadvali: `seller_applications`
- Rol o'zgarishlari jadvali: `role_change_logs`

### Backend Funksiyalar:
- `approve_seller_application()` - Arizani tasdiqlash
- `reject_seller_application()` - Arizani rad etish
- `get_pending_seller_applications()` - Kutilayotgan arizalarni olish

---

**Oxirgi Yangilanish**: 2026-02-10
**Versiya**: 1.0
**Holat**: Ishlab chiqarishga tayyor ✅
