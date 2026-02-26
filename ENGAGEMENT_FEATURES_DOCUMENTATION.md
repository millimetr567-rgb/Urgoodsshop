# URGOODS - Engagement, Trust, Urgency & Revenue Features

## 📋 Overview

Complete implementation of high-impact engagement, trust-building, urgency-creating, and revenue-boosting features for the URGOODS marketplace platform. All user-facing content is in **UZBEK language** as required.

---

## ✅ Implementation Status

### 1. TRUST & SOCIAL PROOF FEATURES ✅

#### ⭐ Product & Seller Ratings
- **Product Ratings**: Users can rate products 1-5 stars after purchase
- **Seller Ratings**: Users can rate sellers based on their experience
- **Reviews**: Optional text reviews with ratings
- **Display**: Ratings shown on product cards and detail pages
- **Uzbek UI**:
  - "Baholash" (Rate)
  - "Izoh qoldirish" (Leave review)
  - "Sotuvchi reytingi" (Seller rating)
- **Automatic Calculation**: Average ratings updated automatically via triggers

#### 🛡 Verified Seller Badge
- **Admin Control**: Admins can mark sellers as verified
- **Badge Display**: "Tasdiqlangan sotuvchi" badge shown on:
  - Product cards (blue checkmark icon)
  - Product detail pages
  - Seller profiles
- **Purpose**: Increases trust and conversion rate

### 2. REVENUE & MONETIZATION FEATURES ✅

#### 💸 Commission System
- **Flexible Configuration**:
  - Percentage-based commission (e.g., 5%)
  - Fixed amount commission (e.g., 10,000 so'm)
- **Scope Options**:
  - Apply to all orders
  - Apply to specific categories
  - Apply to specific sellers
- **Admin Panel**: Full commission management interface
- **Uzbek UI**:
  - "Komissiya foizi" (Commission percentage)
  - "Sotuvchidan olinadigan summa" (Amount taken from seller)
- **Automatic Calculation**: Commission calculated on order completion

#### 🚀 Premium Seller Plan
- **Benefits**:
  - Products appear higher in listings
  - Highlighted product cards with golden ring
  - "TOP sotuvchi" badge with crown icon
  - Premium badge on all products
- **Admin Control**:
  - Set premium duration (days)
  - Automatic expiration tracking
- **Uzbek UI**:
  - "Premium sotuvchi" (Premium seller)
  - "TOP sotuvchi" (TOP seller)
- **Visual Enhancement**: Golden gradient badges and card borders

### 3. URGENCY & PSYCHOLOGICAL TRIGGERS ✅

#### ⏳ Low Stock Warning
- **Threshold**: When stock ≤ 10
- **Display**: Animated warning badge
- **Uzbek Text**:
  - "Kam qoldi" (Running low)
  - "Faqat X dona qoldi" (Only X items left)
- **Style**: Orange color with pulse animation
- **Purpose**: Creates urgency and FOMO

#### 👀 Live Interest Indicator
- **Social Activity Hints**:
  - "Hozir bu mahsulotni X kishi ko'ryapti" (X people viewing now)
  - "Bugun X marta sotib olindi" (Sold X times today)
- **Tracking**: Real-time view and purchase counts
- **Display**: Shown on product cards when activity > threshold
- **Purpose**: Increases urgency and social proof

### 4. SMART NOTIFICATIONS ✅

#### 🔔 Price Drop Notification
- **Trigger**: When favorited/viewed product price drops
- **Delivery**: In-app notification system
- **Uzbek Text**:
  - "Siz ko'rgan mahsulot arzonlashdi" (Product you viewed got cheaper)
- **Data Tracking**: Price history table tracks all changes

#### 🔁 Repeat Purchase Reminder
- **Trigger**: Time-based after previous purchase
- **Recommendation**: Products user bought before
- **Uzbek Text**:
  - "Siz oldin xarid qilgan mahsulot yana mavjud" (Product you bought before is available again)
- **Purpose**: Increases repeat purchases

### 5. DELIVERY & ORDER EXPERIENCE ✅

#### 🚚 Order Status Tracking
- **Statuses** (Uzbek):
  - "Yig'ilmoqda" (Being prepared)
  - "Yo'lda" (On the way)
  - "Yetkazildi" (Delivered)
- **Visibility**: User profile and order history
- **Real-time Updates**: Status changes reflected immediately

#### 🕒 Delivery Time Estimation
- **Display**: "Taxminiy yetkazish vaqti: 1–2 soat"
- **Purpose**: Sets expectations and builds trust

### 6. USER RETENTION FEATURES ✅

#### 🎁 Bonus / Cashback System
- **Earning Opportunities**:
  - First order bonus
  - Frequent buyer rewards
  - Special promotions
- **Usage**: Bonus usable on next orders
- **Uzbek UI**:
  - "Bonus balans" (Bonus balance)
  - "Bonus ishlatish" (Use bonus)
- **Tracking**: Complete transaction history

#### ❤️ Favorite Sellers
- **Follow System**: Users can follow favorite sellers
- **Notifications**: Alert when seller adds new products
- **Uzbek UI**:
  - "Sevimli sotuvchilar" (Favorite sellers)
  - "Yangi mahsulot qo'shildi" (New product added)
- **Purpose**: Builds seller-customer relationships

### 7. ADMIN & SAFETY AUTOMATION ✅

#### 🚫 Smart Moderation
- **Auto-Flagging**:
  - Extremely low prices (< 30% of category average)
  - Unusual discounts (> 70%)
  - Suspicious patterns
- **Admin Approval**: Required before publishing flagged products
- **Uzbek UI**:
  - "Tekshiruv talab qilinadi" (Review required)
- **Workflow**: Admin can approve or reject flagged products

---

## 🗄️ Database Schema

### New Tables Created

1. **product_ratings**
   - Product ratings and reviews
   - Linked to users and orders
   - Automatic average calculation

2. **seller_ratings**
   - Seller ratings and reviews
   - Aggregated from order experiences

3. **commission_settings**
   - Flexible commission configuration
   - Supports percentage and fixed amounts

4. **notifications**
   - In-app notification system
   - Multiple notification types

5. **price_history**
   - Tracks all price changes
   - Enables price drop alerts

6. **bonus_transactions**
   - Complete bonus/cashback history
   - Tracks earned, spent, and expired bonuses

7. **favorite_sellers**
   - User-seller follow relationships
   - Enables personalized notifications

8. **moderation_flags**
   - Auto-flagged products
   - Admin review workflow

9. **product_views**
   - Real-time view tracking
   - Enables "X people viewing" feature

### Enhanced Tables

1. **products**
   - `average_rating` - Product rating (0-5)
   - `rating_count` - Number of ratings
   - `views_today` - Daily view count
   - `purchases_today` - Daily purchase count
   - `moderation_status` - pending/approved/rejected
   - `requires_review` - Auto-flagged indicator

2. **profiles**
   - `average_rating` - Seller rating (0-5)
   - `rating_count` - Number of ratings
   - `is_verified_seller` - Verification badge
   - `is_premium_seller` - Premium status
   - `premium_expires_at` - Premium expiration
   - `bonus_balance` - User bonus points

3. **orders**
   - `commission_amount` - Calculated commission
   - `commission_type` - percentage/fixed

---

## 🎨 UI/UX Enhancements

### Product Card Enhancements

```tsx
// Verified seller badge
{product.seller?.is_verified_seller && (
  <BadgeCheck className="h-3 w-3 text-blue-500" />
)}

// Premium seller badge
{product.seller?.is_premium_seller && (
  <Crown className="h-3 w-3 text-amber-500" />
)}

// Product rating
{product.rating_count > 0 && (
  <div className="flex items-center gap-1">
    <Star className="h-3 w-3 fill-amber-400 text-amber-400" />
    <span>{product.average_rating.toFixed(1)}</span>
    <span>({product.rating_count})</span>
  </div>
)}

// Low stock warning (animated)
{product.stock_quantity <= 10 && (
  <p className="text-orange-500 animate-pulse">
    ⚠️ Kam qoldi ({product.stock_quantity} dona)
  </p>
)}

// Live interest indicators
{product.views_today > 5 && (
  <div className="flex items-center gap-1">
    <Eye className="h-3 w-3" />
    <span>{product.views_today} kishi ko'rdi</span>
  </div>
)}

{product.purchases_today > 0 && (
  <div className="flex items-center gap-1 text-green-600">
    <ShoppingBag className="h-3 w-3" />
    <span>Bugun {product.purchases_today} marta sotildi</span>
  </div>
)}

// Premium seller card highlight
<Card className={`${
  product.seller?.is_premium_seller ? 'ring-2 ring-amber-400/50' : ''
}`}>
```

### Admin Panel Pages

1. **Commission Management** (`/admin/commission`)
   - Create/edit commission settings
   - Toggle active/inactive
   - View commission history

2. **Seller Management** (`/admin/sellers`)
   - Verify sellers
   - Grant premium status
   - View seller ratings
   - Set premium duration

3. **Moderation Queue** (`/admin/moderation`)
   - Review auto-flagged products
   - Approve or reject
   - View flag reasons
   - Track resolution history

---

## 📊 API Functions

### Ratings & Reviews

```typescript
// Create product rating
createProductRating({
  productId: string,
  userId: string,
  orderId?: string,
  rating: number, // 1-5
  review?: string
})

// Get product ratings
getProductRatings(productId: string)

// Create seller rating
createSellerRating({
  sellerId: string,
  userId: string,
  orderId?: string,
  rating: number,
  review?: string
})

// Get seller ratings
getSellerRatings(sellerId: string)
```

### Notifications

```typescript
// Get user notifications
getUserNotifications(userId: string)

// Mark as read
markNotificationAsRead(notificationId: string)

// Mark all as read
markAllNotificationsAsRead(userId: string)

// Create notification
createNotification({
  userId: string,
  type: NotificationType,
  title: string,
  message: string,
  data?: any
})
```

### Favorite Sellers

```typescript
// Add favorite seller
addFavoriteSeller(userId: string, sellerId: string)

// Remove favorite seller
removeFavoriteSeller(userId: string, sellerId: string)

// Get favorite sellers
getFavoriteSellers(userId: string)

// Check if favorite
isFavoriteSeller(userId: string, sellerId: string)
```

### Bonus System

```typescript
// Get bonus balance
getBonusBalance(userId: string)

// Get bonus transactions
getBonusTransactions(userId: string)

// Award bonus points
awardBonusPoints(
  userId: string,
  amount: number,
  reason: string,
  orderId?: string
)
```

### Product Views

```typescript
// Track product view
trackProductView(
  productId: string,
  userId?: string,
  sessionId?: string
)

// Get views today
getProductViewsToday(productId: string)
```

### Commission (Admin)

```typescript
// Get commission settings
getCommissionSettings()

// Create commission setting
createCommissionSetting({
  commissionType: 'percentage' | 'fixed',
  commissionValue: number,
  appliesTo: 'all' | 'category' | 'seller',
  targetId?: string
})

// Update commission setting
updateCommissionSetting(id: string, updates: {...})

// Calculate order commission
calculateOrderCommission(orderId: string)
```

### Seller Management (Admin)

```typescript
// Update seller status
updateSellerStatus(sellerId: string, {
  isVerified?: boolean,
  isPremium?: boolean,
  premiumExpiresAt?: string | null
})
```

### Moderation (Admin)

```typescript
// Get moderation flags
getModerationFlags(resolved: boolean = false)

// Resolve moderation flag
resolveModerationFlag(
  flagId: string,
  resolvedBy: string,
  action: 'approve' | 'reject'
)
```

---

## 🔄 Automatic Processes

### Database Triggers

1. **Update Product Rating**
   - Automatically recalculates average rating when new rating added
   - Updates rating count

2. **Update Seller Rating**
   - Automatically recalculates seller average rating
   - Updates rating count

3. **Check Suspicious Pricing**
   - Auto-flags products with >70% discount
   - Auto-flags products with price <30% of category average
   - Sets moderation status to 'pending'

### Database Functions

1. **calculate_order_commission()**
   - Finds applicable commission setting
   - Calculates commission amount
   - Updates order record

2. **award_bonus_points()**
   - Adds bonus transaction
   - Updates user balance

3. **track_product_view()**
   - Records view event
   - Updates product view count

---

## 🎯 Expected Results

### User Trust Increases
- ✅ Verified seller badges build credibility
- ✅ Ratings and reviews provide social proof
- ✅ Premium sellers stand out as reliable

### Conversion Rate Improves
- ✅ Urgency indicators drive immediate action
- ✅ Live interest creates FOMO
- ✅ Low stock warnings prompt quick decisions

### Repeat Purchases Grow
- ✅ Bonus system incentivizes returns
- ✅ Favorite sellers build loyalty
- ✅ Price drop notifications bring users back

### Revenue Becomes Scalable
- ✅ Commission system generates platform revenue
- ✅ Premium seller plans create recurring income
- ✅ Increased conversions boost transaction volume

### Platform Feels Modern
- ✅ Uzum/Temu-style engagement features
- ✅ Real-time activity indicators
- ✅ Smooth animations and transitions
- ✅ Professional, trustworthy design

---

## 🚀 Usage Examples

### For Users

1. **Viewing Products**
   - See verified seller badges
   - Check product and seller ratings
   - Notice low stock warnings
   - See how many people are viewing/buying

2. **Making Purchases**
   - Earn bonus points on first order
   - Use bonus balance for discounts
   - Rate products after delivery

3. **Following Sellers**
   - Add sellers to favorites
   - Get notified of new products
   - Build trusted seller network

4. **Receiving Notifications**
   - Price drop alerts
   - Repeat purchase reminders
   - Order status updates

### For Sellers

1. **Building Trust**
   - Get verified by admin
   - Accumulate positive ratings
   - Upgrade to premium status

2. **Premium Benefits**
   - Products ranked higher
   - Golden badge on all listings
   - Increased visibility

3. **Managing Products**
   - Auto-moderation for pricing
   - Commission automatically calculated
   - Real-time view tracking

### For Admins

1. **Commission Management**
   - Set platform-wide commission
   - Create category-specific rates
   - Set seller-specific rates

2. **Seller Management**
   - Verify trusted sellers
   - Grant premium status
   - Set premium duration

3. **Moderation**
   - Review auto-flagged products
   - Approve legitimate deals
   - Reject suspicious listings

---

## 📈 Performance Considerations

### Database Indexes
- All foreign keys indexed
- Rating queries optimized
- View tracking indexed by date
- Notification queries optimized

### Caching Strategy
- Ratings cached on product objects
- View counts updated in batches
- Commission settings cached

### Real-time Updates
- Triggers for automatic calculations
- Efficient query patterns
- Minimal database round-trips

---

## 🔐 Security Features

### Data Validation
- Rating values constrained (1-5)
- Commission values validated
- User permissions enforced

### RLS Policies
- Users can only rate their own orders
- Users can only view their own notifications
- Admins have full access to moderation

### Auto-Moderation
- Prevents fraudulent pricing
- Flags suspicious discounts
- Requires admin approval

---

## 🎨 Design Principles

### Uzbek Language First
- All user-facing text in Uzbek
- Natural, conversational tone
- Culturally appropriate messaging

### Non-Intrusive
- Subtle animations
- Professional color scheme
- Clear visual hierarchy

### Mobile-Optimized
- Touch-friendly elements
- Responsive layouts
- Fast loading times

### Trust-Building
- Clear seller information
- Transparent pricing
- Reliable status indicators

---

## 📝 Uzbek UI Text Reference

### Trust & Social Proof
- "Baholash" - Rate
- "Izoh qoldirish" - Leave review
- "Sotuvchi reytingi" - Seller rating
- "Tasdiqlangan sotuvchi" - Verified seller

### Revenue & Monetization
- "Komissiya foizi" - Commission percentage
- "Sotuvchidan olinadigan summa" - Amount taken from seller
- "Premium sotuvchi" - Premium seller
- "TOP sotuvchi" - TOP seller

### Urgency & Triggers
- "Kam qoldi" - Running low
- "Faqat X dona qoldi" - Only X items left
- "Hozir bu mahsulotni X kishi ko'ryapti" - X people viewing now
- "Bugun X marta sotib olindi" - Sold X times today

### Notifications
- "Siz ko'rgan mahsulot arzonlashdi" - Product you viewed got cheaper
- "Siz oldin xarid qilgan mahsulot yana mavjud" - Product you bought before is available again

### Delivery & Orders
- "Yig'ilmoqda" - Being prepared
- "Yo'lda" - On the way
- "Yetkazildi" - Delivered
- "Taxminiy yetkazish vaqti" - Estimated delivery time

### User Retention
- "Bonus balans" - Bonus balance
- "Bonus ishlatish" - Use bonus
- "Sevimli sotuvchilar" - Favorite sellers
- "Yangi mahsulot qo'shildi" - New product added

### Admin & Safety
- "Tekshiruv talab qilinadi" - Review required

---

## ✅ Final Checklist

### Database
- [x] All tables created
- [x] Indexes added
- [x] Triggers configured
- [x] Functions implemented
- [x] RLS policies set

### Backend
- [x] API functions created
- [x] Type definitions added
- [x] Validation implemented
- [x] Error handling added

### Frontend
- [x] Product card enhanced
- [x] Admin pages created
- [x] Routes configured
- [x] UI components styled

### Features
- [x] Ratings & reviews
- [x] Verified seller badges
- [x] Commission system
- [x] Premium seller plans
- [x] Low stock warnings
- [x] Live interest indicators
- [x] Notification system
- [x] Bonus/cashback system
- [x] Favorite sellers
- [x] Smart moderation

### Quality
- [x] All text in Uzbek
- [x] TypeScript compiles
- [x] Lint passes
- [x] Non-breaking changes
- [x] Documentation complete

---

**Status**: ✅ FULLY IMPLEMENTED  
**Version**: 1.0  
**Date**: 2026-02-10  
**Platform**: URGOODS Marketplace - Urgut District  
**Language**: Uzbek (UI) / English (Technical)

---

## 🎉 Result

The URGOODS marketplace now has a complete suite of engagement, trust, urgency, and revenue features that rival major platforms like Uzum Market and Temu, while maintaining the local Urgut district focus and Uzbek language throughout.
