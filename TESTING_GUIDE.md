# URGOODS Bug Fixes - Quick Testing Guide

## How to Test Issue 1: Product Creation

### Test Case 1: Create New Product Successfully
1. Login as admin
2. Navigate to Admin → Mahsulotlar
3. Click "Yangi mahsulot" button
4. Fill in all required fields:
   - Mahsulot nomi: "Test Product"
   - Narx: 100000
   - Kategoriya: Select any category
   - Upload at least one image
5. Click "O'zgarishlarni saqlash"
6. **Expected**: Success toast "Yangi mahsulot muvaffaqiyatli qo'shildi"
7. **Expected**: Redirected to products list
8. **Expected**: New product appears in list

### Test Case 2: Validation - Missing Name
1. Try to save product without entering name
2. **Expected**: Error toast "Mahsulot nomi majburiy maydon"

### Test Case 3: Validation - Invalid Price
1. Enter name but set price to 0 or negative
2. **Expected**: Error toast "Narx 0 dan katta bo'lishi kerak"

### Test Case 4: Validation - Missing Category
1. Enter name and price but don't select category
2. **Expected**: Error toast "Kategoriyani tanlang"

### Test Case 5: Validation - No Images
1. Fill all required fields but don't upload images
2. **Expected**: Warning toast "Kamida bitta rasm yuklash tavsiya etiladi"
3. **Expected**: Product still saves (warning, not error)

### Test Case 6: Discount Calculation
1. Create product with:
   - Price: 100000
   - Discount: 20%
2. Save product
3. View product in database or frontend
4. **Expected**: discounted_price = 80000 (calculated automatically)

### Test Case 7: Admin Creates Product for Another Seller
1. Login as admin
2. Create product (seller_id will be admin's ID)
3. **Expected**: Product saves successfully
4. **Expected**: No RLS policy error

---

## How to Test Issue 2: Category Logo Updates

### Test Case 1: View Category Logos
1. Navigate to /categories page
2. **Expected**: Categories with logos show uploaded images (not emojis)
3. **Expected**: Categories without logos show emoji fallback
4. **Expected**: Each category has colored border matching its theme

### Test Case 2: Update Category Logo
1. Login as admin
2. Navigate to Admin → Kategoriyalar
3. Click edit on any category
4. Upload new logo image
5. Save changes
6. **Expected**: Success toast "Kategoriya muvaffaqiyatli yangilandi"
7. Open /categories page in NEW TAB
8. **Expected**: New logo appears immediately

### Test Case 3: Manual Refresh
1. Have /categories page open
2. In another tab, update a category logo as admin
3. Return to /categories tab
4. Click the refresh button (↻ icon in top-right)
5. **Expected**: Button spins during loading
6. **Expected**: Updated logo appears after refresh

### Test Case 4: Auto-Refresh on Tab Focus
1. Have /categories page open
2. Switch to another tab
3. Update a category logo as admin
4. Switch BACK to /categories tab
5. **Expected**: Page automatically refreshes
6. **Expected**: Updated logo appears without manual refresh

### Test Case 5: Inactive Categories Hidden
1. Login as admin
2. Navigate to Admin → Kategoriyalar
3. Toggle a category to inactive
4. Open /categories page (not logged in or as regular user)
5. **Expected**: Inactive category does NOT appear in list
6. Login as admin and check admin panel
7. **Expected**: Inactive category still visible in admin panel

### Test Case 6: Image Load Error Handling
1. Edit a category and set logo_url to invalid URL
2. View /categories page
3. **Expected**: Emoji fallback appears instead of broken image
4. **Expected**: No console errors or broken image icon

### Test Case 7: Cache Busting
1. Upload logo for category
2. Note the image URL in browser DevTools
3. Update the same category with different logo
4. Refresh /categories page
5. Check image URL in DevTools
6. **Expected**: URL has different ?v= parameter
7. **Expected**: New image loads (not cached old image)

---

## Quick Verification Commands

### Check Database Schema
```sql
-- Verify is_active column exists
SELECT column_name, data_type, column_default 
FROM information_schema.columns 
WHERE table_name = 'products' AND column_name = 'is_active';

-- Verify admin policy exists
SELECT policyname, cmd, qual 
FROM pg_policies 
WHERE tablename = 'products' AND policyname LIKE '%admin%';

-- Check generated column
SELECT column_name, is_generated, generation_expression 
FROM information_schema.columns 
WHERE table_name = 'products' AND column_name = 'discounted_price';
```

### Check Frontend Console
Open browser DevTools (F12) and look for:
- ✅ No errors when creating products
- ✅ Success logs: "Product insert success"
- ✅ Category refresh logs when switching tabs
- ✅ Image URLs have ?v= parameter

---

## Common Issues & Solutions

### Issue: "Cannot insert into generated column"
**Cause**: Frontend trying to insert discounted_price
**Solution**: Already fixed - discounted_price removed from insert data

### Issue: "RLS policy violation"
**Cause**: Missing admin policy
**Solution**: Already fixed - admin policy added in migration

### Issue: Logo doesn't update after change
**Cause**: Browser cache
**Solution**: Already fixed - cache busting with ?v= parameter

### Issue: Old logo still shows
**Cause**: Page not refreshed
**Solution**: Already fixed - auto-refresh on tab focus + manual refresh button

---

## Success Criteria

### Issue 1 (Product Creation)
- ✅ Admin can create products without errors
- ✅ All validation messages are specific and clear
- ✅ Discounted price calculates automatically
- ✅ Images upload successfully
- ✅ Products appear in list immediately

### Issue 2 (Category Logos)
- ✅ Logos display on categories page
- ✅ Logo updates reflect after refresh
- ✅ Manual refresh button works
- ✅ Auto-refresh on tab focus works
- ✅ Cache busting prevents stale images
- ✅ Inactive categories are hidden

---

## Rollback Plan (If Needed)

### To Rollback Database Changes
```sql
-- Remove admin policy
DROP POLICY IF EXISTS "Admins can manage all products" ON products;

-- Remove is_active column
ALTER TABLE products DROP COLUMN IF EXISTS is_active;

-- Remove index
DROP INDEX IF EXISTS idx_products_is_active;
```

### To Rollback Frontend Changes
```bash
# Revert to previous commit
git revert HEAD

# Or restore specific files
git checkout HEAD~1 -- src/pages/admin/AdminProductEditPage.tsx
git checkout HEAD~1 -- src/pages/CategoriesPage.tsx
```

---

## Contact & Support

If issues persist after fixes:
1. Check browser console for errors (F12)
2. Check Supabase logs for database errors
3. Verify migrations applied: `supabase migration list`
4. Check RLS policies: Query pg_policies table
5. Clear browser cache completely (Ctrl+Shift+Delete)

---

## Next Steps

After verifying fixes work:
1. ✅ Test in production environment
2. ✅ Monitor error logs for 24 hours
3. ✅ Gather user feedback
4. ✅ Update user documentation
5. ✅ Train admin users on new features (refresh button, validation messages)
