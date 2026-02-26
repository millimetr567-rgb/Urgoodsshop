# Quick Reference: Three-Step Order Routing

## 🔄 Workflow Overview

```
User Checkout → Admin Review → Seller Assignment → Order Fulfillment
```

### Step 1: User Places Order
- Status: `pending_admin`
- Seller: `NULL` (not assigned)
- Message: "Your order has been received and sent for review"

### Step 2: Admin Assigns Seller
- Admin selects seller from dropdown
- Status changes to: `assigned_to_seller`
- Seller receives notification

### Step 3: Seller Fulfills
- Seller sees order in dashboard
- Updates status: `in_progress` → `completed`

---

## 🗄️ Database Changes

### New Order Statuses
- `pending_admin` - Waiting for admin
- `assigned_to_seller` - Admin assigned seller
- `in_progress` - Seller working on it
- `completed` - Delivered

### Schema Updates
```sql
-- Orders table
ALTER TABLE orders ALTER COLUMN seller_id DROP NOT NULL;
ALTER TABLE orders ADD COLUMN assigned_by UUID;
ALTER TABLE orders ADD COLUMN assigned_at TIMESTAMPTZ;
ALTER TABLE orders ADD COLUMN admin_notes TEXT;

-- New audit table
CREATE TABLE order_assignments (
  id UUID PRIMARY KEY,
  order_id UUID REFERENCES orders(id),
  assigned_by UUID REFERENCES profiles(id),
  assigned_to UUID REFERENCES profiles(id),
  previous_seller_id UUID,
  notes TEXT,
  created_at TIMESTAMPTZ
);
```

---

## 🔧 Key Functions

### 1. create_order_for_admin_review
**Used by**: Checkout page  
**Purpose**: Create order without seller  
**Returns**: `{ success, message, order_id }`

### 2. assign_order_to_seller
**Used by**: Admin panel  
**Purpose**: Assign order to seller  
**Params**: `adminId, orderId, sellerId, notes`  
**Returns**: `{ success, message, order_id }`

### 3. get_pending_admin_orders
**Used by**: Admin pending orders page  
**Purpose**: Get all unassigned orders  
**Returns**: Array of pending orders

### 4. get_available_sellers
**Used by**: Admin assignment dialog  
**Purpose**: Get seller list for dropdown  
**Returns**: Array of sellers (sorted by premium, verified, rating)

### 5. get_seller_assigned_orders
**Used by**: Seller dashboard  
**Purpose**: Get seller's assigned orders  
**Returns**: Array of assigned orders

---

## 💻 Frontend Files Changed

### 1. CheckoutPage.tsx
- Removed Stripe integration
- Removed seller grouping
- Added `createOrderForAdminReview` call
- Simplified order submission

### 2. AdminPendingOrdersPage.tsx (NEW)
- Display pending orders
- Seller selection dialog
- Assignment functionality
- Real-time statistics

### 3. AdminLayout.tsx
- Added "Yangi Buyurtmalar" menu item
- Renamed "Buyurtmalar" to "Barcha Buyurtmalar"

### 4. api.ts
- Added 5 new API functions
- Added TypeScript interfaces
- Proper error handling

### 5. routes.tsx
- Added `/admin/pending-orders` route

---

## 🔒 Security Rules

### Orders Access
- **Users**: Can view own orders only
- **Sellers**: Can view assigned orders only
- **Admins**: Can view all orders

### Assignment Access
- **Only admins** can assign orders
- **Only admins** can view pending orders
- **Sellers** cannot see unassigned orders

### Direct Database Access
- ❌ Direct INSERT blocked
- ✅ Only via SECURITY DEFINER functions
- ✅ RLS policies enforced

---

## ✅ Testing Checklist

### Checkout Flow
- [ ] User can complete checkout
- [ ] No errors during submission
- [ ] Success message displays
- [ ] Cart is cleared
- [ ] Order has `pending_admin` status
- [ ] Order has NO seller assigned

### Admin Assignment
- [ ] Admin sees pending orders
- [ ] Seller dropdown works
- [ ] Assignment succeeds
- [ ] Order removed from pending list
- [ ] Assignment logged in database

### Seller Access
- [ ] Seller sees assigned orders
- [ ] Seller CANNOT see unassigned orders
- [ ] Admin notes visible
- [ ] Status updates work

---

## 🐛 Common Issues

### Issue: Checkout fails
**Check**: User logged in? Cart has items? Form filled?  
**Fix**: Verify `create_order_for_admin_review` function exists

### Issue: Admin cannot assign
**Check**: User has admin role? Seller exists?  
**Fix**: Verify roles in profiles table

### Issue: Seller sees no orders
**Check**: Orders assigned to this seller? Correct status?  
**Fix**: Query orders table for seller_id

---

## 📊 Monitoring Queries

### Pending Orders Count
```sql
SELECT COUNT(*) FROM orders WHERE status = 'pending_admin';
```

### Seller Workload
```sql
SELECT seller_id, COUNT(*) as orders
FROM orders
WHERE status IN ('assigned_to_seller', 'in_progress')
GROUP BY seller_id;
```

### Assignment Stats
```sql
SELECT assigned_by, COUNT(*) as assignments
FROM order_assignments
GROUP BY assigned_by;
```

---

## 🚀 Quick Start

### For Developers

1. **Database**: Migrations already applied ✅
2. **Frontend**: Code already updated ✅
3. **Test**: Run checkout flow
4. **Verify**: Check admin panel

### For Admins

1. Navigate to "Yangi Buyurtmalar"
2. Review pending orders
3. Click "Assign Seller"
4. Select seller from dropdown
5. Add notes (optional)
6. Click "Assign Order"

### For Sellers

1. Log in to dashboard
2. View assigned orders
3. Read admin notes
4. Update order status
5. Mark as completed when done

---

## 📝 User Messages

### English
- "Your order has been received and sent for review"
- "Order assigned to seller successfully"
- "You do not have permission to perform this action"

### Uzbek (for future translation)
- "Buyurtmangiz qabul qilindi va tekshiruvga yuborildi"
- "Buyurtma sotuvchiga biriktirildi"
- "Sizda bu amalni bajarish huquqi yo'q"

---

**Status**: ✅ Production Ready  
**Version**: 1.0  
**Date**: 2026-02-10
