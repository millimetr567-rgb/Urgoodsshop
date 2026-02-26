# URGOODS - Tezkor Qo'llanma (Quick Reference)

## 🎯 Asosiy O'zgarishlar

### ✅ Qoldiq (Stock) Olib Tashlandi
- Admin panelda qoldiq maydoni yo'q
- Mahsulotlar ro'yxatida qoldiq ko'rinmaydi
- Database'da deprecated (ishlatilmaydi)

### ✅ Qat'iy Validatsiya
- Barcha majburiy maydonlar tekshiriladi
- Aniq o'zbekcha xato xabarlari
- Frontend + Backend validatsiya

### ✅ Kategoriya Logotipi Avtomatik Yangilanadi
- Admin logotip yangilasa, avtomatik ko'rinadi
- Yangilash tugmasi qo'shildi
- Kesh muammosi hal qilindi

---

## 📝 Mahsulot Qo'shish Qoidalari

### Majburiy Maydonlar
1. **Mahsulot nomi** - Kamida 3 ta belgi
2. **Kategoriya** - Ro'yxatdan tanlash
3. **Narx** - 0 dan katta raqam
4. **Rasm** - Kamida 1 ta rasm

### Ixtiyoriy Maydonlar
- Tavsif (description)
- Qisqa tavsif (short_description)
- Chegirma (0-100%)
- Rang (card_color_accent)
- Badge turi

---

## ⚠️ Xato Xabarlari

| Xato | Sabab | Yechim |
|------|-------|--------|
| "Mahsulot nomi majburiy maydon" | Nom kiritilmagan | Mahsulot nomini kiriting |
| "Mahsulot nomi kamida 3 ta belgidan iborat bo'lishi kerak" | Nom juda qisqa | 3 yoki undan ko'p belgi kiriting |
| "Kategoriya tanlanmagan" | Kategoriya tanlanmagan | Ro'yxatdan kategoriya tanlang |
| "Narx noto'g'ri formatda..." | Narx 0 yoki manfiy | Musbat raqam kiriting |
| "Kamida bitta rasm yuklash majburiy" | Rasm yuklanmagan | Rasm yuklang |
| "Chegirma 0 dan 100 gacha bo'lishi kerak" | Chegirma noto'g'ri | 0-100 oralig'ida kiriting |

---

## 🔄 Kategoriya Logotipini Yangilash

### Qadamlar:
1. Admin panelga kiring
2. "Kategoriyalar" bo'limiga o'ting
3. Kategoriyani tahrirlang
4. Yangi logotip yuklang
5. Saqlang

### Natija:
- ✅ "Kategoriya logotipi yangilandi" xabari
- ✅ Asosiy menyuda avtomatik ko'rinadi
- ✅ Yangilash tugmasini bosish mumkin

---

## 🛠️ Muammolarni Hal Qilish

### Mahsulot Saqlanmaydi
1. Barcha majburiy maydonlar to'ldirilganini tekshiring
2. Xato xabarini diqqat bilan o'qing
3. Brauzer konsolini tekshiring (F12)
4. Admin sifatida kirganingizni tasdiqlang

### Logotip Yangilanmaydi
1. Yangilash tugmasini bosing (↻)
2. Sahifani yangilang (F5)
3. Brauzer keshini tozalang (Ctrl+Shift+Delete)
4. Boshqa brauzerda sinab ko'ring

### Xato Xabari Inglizcha
1. Bu backend xatosi
2. Xabar tarjima qilinishi kerak
3. Konsolda to'liq xato ko'ring
4. Texnik yordam so'rang

---

## 📊 Validatsiya Oqimi

```
Forma to'ldirish
    ↓
Frontend tekshiruvi
    ├─ Xato? → O'zbekcha xabar ❌
    └─ To'g'ri? → Backend'ga yuborish ✅
        ↓
    Backend tekshiruvi
        ├─ Xato? → O'zbekcha xabar ❌
        └─ To'g'ri? → Saqlash ✅
            ↓
        "Mahsulot muvaffaqiyatli qo'shildi" ✅
```

---

## 🎨 Kategoriya Ranglari

Kategoriya tahrirlashda rang tanlash mumkin:
- Rang kategoriya kartasining chegarasida ko'rinadi
- Hex format: #8B5CF6 (default)
- Rang tanlash uchun color picker ishlatiladi

---

## 📸 Rasm Yuklash

### Qoidalar:
- Maksimal hajm: 1MB
- Format: JPG, PNG
- Kamida 1 ta rasm majburiy
- Ko'p rasm yuklash mumkin

### Rasmni O'chirish:
- Rasm ustidagi X tugmasini bosing
- Tasdiqlash kerak emas
- Darhol o'chiriladi

---

## 🔐 Ruxsatlar

### Admin:
- ✅ Barcha mahsulotlarni ko'rish
- ✅ Barcha mahsulotlarni tahrirlash
- ✅ Yangi mahsulot qo'shish
- ✅ Mahsulotni o'chirish
- ✅ Kategoriyalarni boshqarish

### Sotuvchi:
- ✅ Faqat o'z mahsulotlarini ko'rish
- ✅ Faqat o'z mahsulotlarini tahrirlash
- ✅ Yangi mahsulot qo'shish
- ❌ Kategoriyalarni boshqarish

### Foydalanuvchi:
- ✅ Faqat mavjud mahsulotlarni ko'rish
- ❌ Tahrirlash
- ❌ Qo'shish
- ❌ O'chirish

---

## 💡 Maslahatlar

### Mahsulot Qo'shishda:
1. Avval barcha ma'lumotlarni tayyorlang
2. Rasmlarni oldindan tayyorlang (1MB dan kichik)
3. Kategoriyani to'g'ri tanlang
4. Narxni diqqat bilan kiriting
5. Chegirma kerak bo'lsa, foizda kiriting

### Kategoriya Boshqarishda:
1. Logotip hajmi kichik bo'lsin (tez yuklanadi)
2. Rang kategoriya mazmuniga mos bo'lsin
3. Nom qisqa va tushunarli bo'lsin
4. Nofaol kategoriyalarni o'chirib qo'ying

---

## 📞 Yordam

### Texnik Muammo:
1. Brauzer konsolini tekshiring (F12)
2. Xato xabarini to'liq o'qing
3. Sahifani yangilang
4. Qayta urinib ko'ring

### Savol:
1. Ushbu qo'llanmani o'qing
2. VALIDATSIYA_VA_TUZATISHLAR.md ni ko'ring
3. TECHNICAL_VALIDATION_DOCUMENTATION.md ni o'qing
4. Texnik yordam so'rang

---

## ✅ Tekshirish Ro'yxati

### Mahsulot Qo'shishdan Oldin:
- [ ] Admin sifatida kirganman
- [ ] Mahsulot nomi tayyorman (3+ belgi)
- [ ] Kategoriya tanladim
- [ ] Narx kiritdim (musbat raqam)
- [ ] Kamida 1 ta rasm yuklab oldim
- [ ] Chegirma kerak bo'lsa, 0-100 oralig'ida

### Kategoriya Yangilashdan Oldin:
- [ ] Admin sifatida kirganman
- [ ] Yangi logotip tayyorman (1MB dan kichik)
- [ ] Rang tanladim (ixtiyoriy)
- [ ] Kategoriya nomi to'g'ri

---

## 🎉 Muvaffaqiyat Mezonlari

### Mahsulot Qo'shish:
- ✅ "Mahsulot muvaffaqiyatli qo'shildi" xabari
- ✅ Mahsulotlar ro'yxatiga o'tish
- ✅ Yangi mahsulot ro'yxatda ko'rinadi

### Kategoriya Yangilash:
- ✅ "Kategoriya logotipi yangilandi" xabari
- ✅ Kategoriyalar sahifasida yangi logotip
- ✅ Yangilash tugmasi ishlaydi

---

## 📚 Qo'shimcha Hujjatlar

1. **VALIDATSIYA_VA_TUZATISHLAR.md** - O'zbekcha to'liq qo'llanma
2. **TECHNICAL_VALIDATION_DOCUMENTATION.md** - Texnik hujjat (inglizcha)
3. **BUG_FIXES_DOCUMENTATION.md** - Xatolarni tuzatish tarixi
4. **TESTING_GUIDE.md** - Test qilish qo'llanmasi

---

**Versiya**: 2.0  
**Sana**: 2026-02-10  
**Holat**: ✅ Ishga Tayyor
