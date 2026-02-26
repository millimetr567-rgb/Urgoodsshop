# URGOODS - Quick Reference Guide for New Features

## 🚀 For Developers

### New Database Tables
```sql
product_ratings         -- Product ratings & reviews
seller_ratings          -- Seller ratings & reviews
commission_settings     -- Commission configuration
notifications           -- In-app notifications
price_history           -- Price change tracking
bonus_transactions      -- Bonus/cashback history
favorite_sellers        -- User-seller follows
moderation_flags        -- Auto-flagged products
product_views           -- View tracking
```

### New API Functions (src/db/api.ts)
```typescript
// Ratings
createProductRating()
getProductRatings()
createSellerRating()
getSellerRatings()

// Notifications
getUserNotifications()
markNotificationAsRead()
createNotification()

// Favorite Sellers
addFavoriteSeller()
removeFavoriteSeller()
getFavoriteSellers()

// Bonus System
getBonusBalance()
awardBonusPoints()
getBonusTransactions()

// Product Views
trackProductView()
getProductViewsToday()

// Commission (Admin)
getCommissionSettings()
createCommissionSetting()
calculateOrderCommission()

// Seller Management (Admin)
updateSellerStatus()

// Moderation (Admin)
getModerationFlags()
resolveModerationFlag()
```

### New Admin Pages
```
/admin/commission    - Commission management
/admin/sellers       - Seller verification & premium
/admin/moderation    - Auto-flagged products review
```

### Enhanced Components
```
ProductCard.tsx      - Now shows ratings, badges, urgency indicators
```

---

## 👨‍💼 For Admins

### Commission Management
1. Go to `/admin/commission`
2. Click "Yangi Sozlama" (New Setting)
3. Choose:
   - **Foiz (%)** - Percentage of order amount
   - **Qat'iy Summa** - Fixed amount per order
4. Set value and scope (all/category/seller)
5. Save

**Example**: 5% commission on all orders
- Type: Foiz (%)
- Value: 5
- Applies to: Barcha Buyurtmalarga

### Seller Verification
1. Go to `/admin/sellers`
2. Find seller
3. Click "Tasdiqlash" (Verify)
4. Blue checkmark badge appears on all their products

### Premium Seller
1. Go to `/admin/sellers`
2. Find seller
3. Click "Premium berish" (Grant Premium)
4. Set duration (days)
5. Seller gets:
   - Golden crown badge
   - Products ranked higher
   - Golden ring on product cards

### Moderation Queue
1. Go to `/admin/moderation`
2. Review auto-flagged products:
   - **Past Narx** - Price too low
   - **Yuqori Chegirma** - Discount too high
3. Click "Tasdiqlash" (Approve) or "Rad etish" (Reject)

**Auto-Flagging Rules**:
- Discount > 70% → Flagged
- Price < 30% of category average → Flagged

---

## 👤 For Users

### Viewing Products
**What You'll See**:
- ⭐ Product rating (e.g., 4.5 ★ (23))
- 🛡 "Tasdiqlangan sotuvchi" badge (verified)
- 👑 "TOP sotuvchi" badge (premium)
- ⚠️ "Kam qoldi (5 dona)" - Low stock warning
- 👀 "12 kishi ko'rdi" - People viewing now
- 🛍 "Bugun 8 marta sotildi" - Sold today

### Rating Products
1. Complete an order
2. Go to order history
3. Click "Baholash" (Rate)
4. Select 1-5 stars
5. Optionally add review text
6. Submit

### Following Sellers
1. Visit seller profile
2. Click "Sevimli sotuvchilarga qo'shish"
3. Get notified when they add new products

### Using Bonuses
1. Check "Bonus balans" in profile
2. Earn bonuses from:
   - First order
   - Frequent purchases
   - Special promotions
3. Use bonuses at checkout

### Notifications
Check notification icon for:
- 🔔 Price drops on favorited products
- 🔁 Repeat purchase reminders
- 📦 Order status updates
- 🆕 New products from favorite sellers

---

## 🎨 UI Elements Reference

### Badges
```
✅ Tasdiqlangan sotuvchi  - Blue checkmark (verified)
👑 TOP sotuvchi           - Golden crown (premium)
⚠️ Kam qoldi              - Orange warning (low stock)
```

### Ratings Display
```
⭐ 4.5 (23)              - Product rating
Sotuvchi: ⭐ 4.8        - Seller rating
```

### Live Indicators
```
👀 12 kishi ko'rdi                    - People viewing
🛍 Bugun 8 marta sotildi             - Sold today
```

### Premium Seller Highlight
```
Golden ring around product card
Golden gradient badge
```

---

## 🔧 Technical Details

### Database Triggers
- `trigger_update_product_rating` - Auto-updates product average rating
- `trigger_update_seller_rating` - Auto-updates seller average rating
- `trigger_check_suspicious_pricing` - Auto-flags suspicious products

### Database Functions
- `calculate_order_commission()` - Calculates commission for order
- `award_bonus_points()` - Awards bonus to user
- `track_product_view()` - Records product view
- `reduce_product_stock()` - Atomically reduces stock (existing)

### Automatic Processes
1. **Rating Calculation**: Instant via triggers
2. **Commission Calculation**: On order completion
3. **Price Monitoring**: On product create/update
4. **View Tracking**: Real-time on page view

---

## 📊 Data Flow Examples

### Rating a Product
```
User rates product (1-5 stars)
    ↓
Insert into product_ratings
    ↓
Trigger: update_product_rating
    ↓
Calculate AVG(rating) and COUNT(*)
    ↓
Update products table
    ↓
Product card shows new rating
```

### Creating Order with Commission
```
User places order
    ↓
Order created in database
    ↓
Function: calculate_order_commission()
    ↓
Find applicable commission setting
    ↓
Calculate amount (percentage or fixed)
    ↓
Update order.commission_amount
    ↓
Admin sees commission in order details
```

### Auto-Moderation
```
Admin creates/edits product
    ↓
Trigger: check_suspicious_pricing
    ↓
Check discount > 70%?
Check price < 30% of category avg?
    ↓
If yes: Create moderation_flag
    ↓
Set product.moderation_status = 'pending'
    ↓
Product hidden until admin approves
    ↓
Admin reviews in /admin/moderation
    ↓
Approve → Product visible
Reject → Product hidden
```

---

## 🎯 Best Practices

### For Admins
1. **Verify Trusted Sellers**: Only verify sellers with good track record
2. **Monitor Moderation Queue**: Check daily for flagged products
3. **Set Reasonable Commission**: Balance platform revenue with seller satisfaction
4. **Grant Premium Strategically**: Reward top-performing sellers

### For Sellers
1. **Build Trust**: Accumulate positive ratings
2. **Price Fairly**: Avoid triggering auto-moderation
3. **Maintain Stock**: Keep products available
4. **Engage Customers**: Respond to reviews

### For Users
1. **Rate Honestly**: Help other buyers make decisions
2. **Follow Favorite Sellers**: Get notified of new products
3. **Use Bonuses**: Save money on purchases
4. **Check Ratings**: Look for verified and highly-rated sellers

---

## 🐛 Troubleshooting

### Product Not Showing
**Possible Causes**:
- Moderation status = 'pending'
- Auto-flagged for suspicious pricing
- Stock quantity = 0

**Solution**: Check `/admin/moderation` and approve if legitimate

### Commission Not Calculating
**Possible Causes**:
- No active commission setting
- Commission setting not applicable to order

**Solution**: Create/activate commission setting in `/admin/commission`

### Ratings Not Updating
**Possible Causes**:
- Database trigger not firing
- User not authorized to rate

**Solution**: Check database logs and user permissions

---

## 📈 Monitoring & Analytics

### Key Metrics to Track
1. **Conversion Rate**: Before/after urgency indicators
2. **Average Order Value**: Impact of bonus system
3. **Repeat Purchase Rate**: Effectiveness of notifications
4. **Seller Ratings**: Overall platform trust
5. **Commission Revenue**: Platform earnings

### Database Queries
```sql
-- Total commission earned
SELECT SUM(commission_amount) FROM orders 
WHERE status = 'completed';

-- Average product rating
SELECT AVG(average_rating) FROM products 
WHERE rating_count > 0;

-- Most viewed products today
SELECT name, views_today FROM products 
ORDER BY views_today DESC LIMIT 10;

-- Premium sellers count
SELECT COUNT(*) FROM profiles 
WHERE is_premium_seller = true 
AND premium_expires_at > NOW();
```

---

## 🔐 Security Considerations

### RLS Policies
- Users can only rate their own orders
- Users can only view their own notifications
- Admins have full moderation access

### Data Validation
- Ratings constrained to 1-5
- Commission values must be positive
- Stock quantities must be non-negative

### Auto-Moderation
- Prevents fraudulent pricing
- Requires admin approval for suspicious products
- Protects platform reputation

---

## 🚀 Future Enhancements

### Potential Additions
1. **Email Notifications**: Send price drops via email
2. **SMS Alerts**: Critical order updates
3. **Advanced Analytics**: Seller performance dashboard
4. **Bulk Operations**: Batch verify sellers
5. **Scheduled Promotions**: Time-based premium plans
6. **Review Moderation**: Flag inappropriate reviews
7. **Seller Tiers**: Bronze/Silver/Gold levels
8. **Loyalty Program**: Points for frequent buyers

---

**Quick Reference Version**: 1.0  
**Last Updated**: 2026-02-10  
**Platform**: URGOODS Marketplace
