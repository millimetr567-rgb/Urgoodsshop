# URGOODS - Mahsulot Soni Boshqaruvi (Qoldiq Tizimi)

## 📋 Umumiy Ma'lumot

URGOODS marketplace uchun to'liq mahsulot soni (qoldiq) boshqaruv tizimi. Mahsulotlar miqdori har doim aniq, foydalanuvchilarga ko'rinadi va buyurtmalar bilan sinxronlashtirilgan.

---

## ✅ Asosiy Imkoniyatlar

### 1. Admin Panel - Mahsulot Sonini Boshqarish
- ✅ Mahsulot qo'shish/tahrirlashda "Mahsulot soni" maydoni
- ✅ Jonli holat ko'rsatish (Mavjud, Kam qoldi, Tugagan)
- ✅ Faqat butun sonlar, 0 dan katta yoki teng
- ✅ O'zgarishlar darhol qo'llaniladi
- ✅ Barcha xabarlar o'zbekcha

### 2. Foydalanuvchi - Mahsulot Holati
- ✅ Mahsulot kartasida aniq holat:
  - 10 dan ko'p: "Mavjud" (yashil)
  - 10 va undan kam: "Kam qoldi (X dona)" (to'q sariq)
  - 0: "Tugagan" (qizil)
- ✅ Tugagan mahsulotda tugma o'chirilgan
- ✅ Tugma matni "Tugagan" ga o'zgaradi

### 3. Savatcha - Miqdor Cheklovi
- ✅ Savatchaga qo'shishdan oldin tekshirish
- ✅ Maksimal miqdor = mavjud mahsulot soni
- ✅ Savatchada ogohlantirish xabarlari
- ✅ O'zbekcha xato xabarlari
- ✅ + tugma chegara bo'yicha o'chiriladi

### 4. Buyurtma - Avtomatik Kamaytirish
- ✅ Buyurtma berilganda mahsulot soni avtomatik kamayadi
- ✅ Ikki kishi bir vaqtda oxirgi mahsulotni ololmaydi
- ✅ Server tomonida tekshirish
- ✅ Yetarli bo'lmasa buyurtma rad etiladi
- ✅ Aniq o'zbekcha xabarlar

---

## 🎯 Mahsulot Holati Ko'rsatkichlari

### Mahsulot Kartasida

| Mahsulot Soni | Ko'rinish | Rang | Tugma |
|---------------|-----------|------|-------|
| 0 | "Tugagan" | Qizil | O'chirilgan |
| 1-10 | "Kam qoldi (X dona)" | To'q sariq | Faol |
| 11+ | "Mavjud" | Yashil | Faol |

### Savatchada

| Holat | Xabar | Rang |
|-------|-------|------|
| Mahsulot tugagan | "Tugagan" | Qizil |
| Savatchadagi miqdor > mavjud | "Faqat X dona mavjud" | To'q sariq |
| Kam qoldi | "Kam qoldi (X dona)" | To'q sariq |

### Admin Panelda

| Mahsulot Soni | Ko'rinish | Rang |
|---------------|-----------|------|
| 0 | "Tugagan" | Qizil |
| 1-10 | "Kam qoldi (X)" | To'q sariq |
| 11+ | "Mavjud (X)" | Yashil |

---

## 📝 Admin Uchun Qo'llanma

### Mahsulot Qo'shish

1. Admin panelga kiring
2. "Mahsulotlar" → "Yangi mahsulot qo'shish"
3. Barcha maydonlarni to'ldiring
4. **"Mahsulot soni"** maydoniga mavjud miqdorni kiriting
   - Faqat butun sonlar (1, 2, 3, ...)
   - 0 dan katta yoki teng
   - Manfiy son kiritib bo'lmaydi
5. Saqlang

**Holat ko'rsatkichi**:
- 0 dona: "Mahsulot tugagan"
- 1-10 dona: "Kam qoldi (X dona)"
- 11+ dona: "Mavjud"

### Mahsulot Sonini Yangilash

1. "Mahsulotlar" ro'yxatidan mahsulotni tanlang
2. "Tahrirlash" tugmasini bosing
3. "Mahsulot soni" maydonini o'zgartiring
4. Saqlang

**Xabar**: "Mahsulot soni yangilandi"

### Mahsulotlar Ro'yxatida

Har bir mahsulot uchun ko'rinadi:
- Mahsulot nomi
- Narx
- Chegirma (agar bor bo'lsa)
- **Mahsulot soni** (rangli ko'rsatkich bilan)
- Kategoriya
- Ko'rishlar soni

---

## 👤 Foydalanuvchi Uchun Qo'llanma

### Mahsulotni Ko'rish

1. Mahsulotlar sahifasiga o'ting
2. Har bir mahsulot kartasida holat ko'rinadi:
   - **Mavjud** (yashil) - xarid qilish mumkin
   - **Kam qoldi (X dona)** (to'q sariq) - tezroq xarid qiling
   - **Tugagan** (qizil) - xarid qilib bo'lmaydi

### Savatchaga Qo'shish

1. Mahsulot kartasida "Savatchaga qo'shish" tugmasini bosing
2. Agar mahsulot tugagan bo'lsa:
   - Tugma o'chirilgan
   - "Tugagan" yozuvi ko'rinadi
3. Agar mavjud bo'lsa:
   - Savatchaga qo'shiladi
   - "Savatchaga qo'shildi" xabari chiqadi

### Savatchada Miqdorni O'zgartirish

1. Savatchaga o'ting
2. Har bir mahsulot uchun + va - tugmalari bor
3. **+ tugma**:
   - Mahsulot soni yetarli bo'lsa faol
   - Chegara bo'yicha o'chirilgan
4. **- tugma**:
   - 1 donadan ko'p bo'lsa faol
   - 1 dona bo'lsa o'chirilgan

**Ogohlantirish**:
- Agar savatchadagi miqdor mavjud miqdordan ko'p bo'lsa:
  - "Faqat X dona mavjud" xabari ko'rinadi
  - + tugma o'chirilgan

### Buyurtma Berish

1. Savatchada "Buyurtmani rasmiylashtirish" tugmasini bosing
2. Manzil va telefon raqamni kiriting
3. "Buyurtma berish" tugmasini bosing
4. Tizim mahsulot sonini tekshiradi:
   - **Yetarli bo'lsa**: 
     - Buyurtma qabul qilinadi
     - Mahsulot soni avtomatik kamayadi
     - "Buyurtma qabul qilindi" xabari
   - **Yetarli bo'lmasa**:
     - Buyurtma rad etiladi
     - "Mahsulot miqdori yetarli emas" xabari

---

## ⚠️ Xato Xabarlari va Yechimlar

### "Mahsulot tugagan"
**Sabab**: Mahsulot soni 0 ga teng  
**Yechim**: Boshqa mahsulot tanlang yoki keyinroq qaytib keling

### "Mahsulot miqdori yetarli emas"
**Sabab**: Buyurtma berayotganda mahsulot soni yetarli emas  
**Yechim**: Savatchadagi miqdorni kamaytiring

### "Mavjud miqdordan ortiq qo'shib bo'lmaydi. Faqat X dona mavjud"
**Sabab**: Savatchaga ko'p miqdor qo'shmoqchisiz  
**Yechim**: Faqat mavjud miqdorda qo'shing

### "Mahsulot soni butun son va 0 dan katta yoki teng bo'lishi kerak"
**Sabab**: Admin noto'g'ri qiymat kiritdi  
**Yechim**: Faqat butun sonlar kiriting (0, 1, 2, 3, ...)

---

## 🔒 Xavfsizlik va Ishonchlilik

### Ikki Kishi Bir Vaqtda Xarid Qilsa

**Holat**: Mahsulot 1 dona qoldi, 2 kishi bir vaqtda xarid qilmoqchi

**Tizim harakati**:
1. Birinchi kishi buyurtma beradi → Muvaffaqiyatli ✅
2. Mahsulot soni 0 ga kamayadi
3. Ikkinchi kishi buyurtma beradi → Rad etiladi ❌
4. Xabar: "Mahsulot miqdori yetarli emas"

**Natija**: Hech qachon ortiqcha sotilmaydi!

### Server Tomonida Tekshirish

Barcha tekshiruvlar server tomonida amalga oshiriladi:
- Frontend faqat ko'rinish uchun
- Backend haqiqiy tekshirish
- Ma'lumotlar bazasi yakuniy nazorat

**Natija**: Xavfsiz va ishonchli tizim!

---

## 📊 Misol Stsenariylar

### Stsenariy 1: Oddiy Xarid

1. Mahsulot: "Telefon", Soni: 10
2. Foydalanuvchi savatchaga 2 ta qo'shadi
3. Buyurtma beradi
4. **Natija**: 
   - Buyurtma qabul qilindi ✅
   - Mahsulot soni: 10 → 8

### Stsenariy 2: Oxirgi Mahsulot

1. Mahsulot: "Kitob", Soni: 1
2. Foydalanuvchi savatchaga 1 ta qo'shadi
3. Buyurtma beradi
4. **Natija**:
   - Buyurtma qabul qilindi ✅
   - Mahsulot soni: 1 → 0
   - Holat: "Tugagan"
   - Boshqa foydalanuvchilar xarid qila olmaydi

### Stsenariy 3: Yetarli Emas

1. Mahsulot: "Sumka", Soni: 3
2. Foydalanuvchi savatchaga 5 ta qo'shmoqchi
3. **Natija**:
   - Xato: "Mavjud miqdordan ortiq qo'shib bo'lmaydi. Faqat 3 dona mavjud" ❌
   - Savatchaga qo'shilmadi

### Stsenariy 4: Admin Mahsulot Qo'shadi

1. Admin yangi mahsulot qo'shadi
2. Mahsulot soni: 50
3. Saqlaydi
4. **Natija**:
   - Mahsulot ro'yxatida ko'rinadi
   - Holat: "Mavjud (50)" (yashil)
   - Foydalanuvchilar xarid qilishlari mumkin

### Stsenariy 5: Mahsulot Tugayapti

1. Mahsulot: "Daftar", Soni: 15
2. Foydalanuvchilar xarid qilishadi
3. Soni 8 ga tushadi
4. **Natija**:
   - Holat: "Kam qoldi (8 dona)" (to'q sariq)
   - Admin ogohlantirish ko'radi
5. Soni 0 ga tushadi
6. **Natija**:
   - Holat: "Tugagan" (qizil)
   - Xarid qilib bo'lmaydi

---

## 🎨 Rang Kodlari

| Holat | Rang | Hex Kod | Ishlatilish |
|-------|------|---------|-------------|
| Mavjud | Yashil | #16a34a | 11+ dona |
| Kam qoldi | To'q sariq | #f97316 | 1-10 dona |
| Tugagan | Qizil | #dc2626 | 0 dona |

---

## 💡 Maslahatlar

### Admin Uchun

1. **Muntazam tekshiring**: Mahsulotlar sonini har kuni tekshiring
2. **Kam qolgan mahsulotlar**: To'q sariq rangdagi mahsulotlarni to'ldiring
3. **Aniq miqdor**: Har doim aniq miqdor kiriting
4. **Tugagan mahsulotlar**: Tugagan mahsulotlarni yangilang yoki o'chiring

### Foydalanuvchi Uchun

1. **Tezroq xarid qiling**: "Kam qoldi" ko'rsangiz, tezroq xarid qiling
2. **Savatchangizni tekshiring**: Buyurtma berishdan oldin mahsulotlar mavjudligini tekshiring
3. **Tugagan mahsulotlar**: Tugagan mahsulotlar uchun keyinroq qaytib keling

---

## 📞 Yordam

### Savol: Mahsulot savatchaga qo'shilmayapti
**Javob**: 
1. Mahsulot tugagan bo'lishi mumkin
2. Savatchada allaqachon maksimal miqdor bor
3. Xato xabarini o'qing

### Savol: Buyurtma qabul qilinmayapti
**Javob**:
1. Mahsulot soni yetarli emasligini tekshiring
2. Savatchadagi miqdorni kamaytiring
3. Xato xabarini diqqat bilan o'qing

### Savol: Admin mahsulot sonini o'zgartira olmayapti
**Javob**:
1. Faqat butun sonlar kiriting
2. Manfiy son kiritib bo'lmaydi
3. Sahifani yangilang va qayta urinib ko'ring

---

## ✅ Tekshirish Ro'yxati

### Mahsulot Qo'shish
- [ ] Mahsulot nomi kiritilgan
- [ ] Kategoriya tanlangan
- [ ] Narx kiritilgan
- [ ] Rasm yuklangan
- [ ] **Mahsulot soni kiritilgan** (butun son, ≥ 0)
- [ ] Saqlash tugmasi bosilgan

### Xarid Qilish
- [ ] Mahsulot mavjud ("Mavjud" yoki "Kam qoldi")
- [ ] Savatchaga qo'shildi
- [ ] Miqdor to'g'ri
- [ ] Manzil va telefon kiritilgan
- [ ] Buyurtma berildi

### Admin Tekshiruvi
- [ ] Barcha mahsulotlar soni to'g'ri
- [ ] Tugagan mahsulotlar yangilangan
- [ ] Kam qolgan mahsulotlar to'ldirilgan
- [ ] Yangi mahsulotlar qo'shilgan

---

## 🎉 Natijalar

### Oldin ❌
- Mahsulot soni noaniq
- Ortiqcha sotilish
- Foydalanuvchilar chalkashib qolishardi
- Buyurtmalar rad etilardi

### Keyin ✅
- Mahsulot soni har doim aniq
- Hech qachon ortiqcha sotilmaydi
- Foydalanuvchilar aniq ko'rishadi
- Buyurtmalar muvaffaqiyatli

---

## 📚 Qo'shimcha Hujjatlar

1. **STOCK_MANAGEMENT_SYSTEM.md** - Texnik hujjat (inglizcha)
2. **VALIDATSIYA_VA_TUZATISHLAR.md** - Validatsiya tizimi
3. **TECHNICAL_VALIDATION_DOCUMENTATION.md** - Texnik ma'lumotlar

---

**Holat**: ✅ To'liq Ishga Tayyor  
**Versiya**: 3.0  
**Sana**: 2026-02-10  
**Platforma**: URGOODS Marketplace - Urgut tumani
