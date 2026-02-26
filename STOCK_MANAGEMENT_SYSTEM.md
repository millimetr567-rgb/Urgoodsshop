# URGOODS - Stock Management System Documentation

## Overview

Complete stock (qoldiq) management system implementation for URGOODS marketplace ensuring accurate product availability, preventing overselling, and providing clear stock visibility to users.

---

## ✅ Implementation Status

### 1. Admin Panel - Stock Management ✅
- **Stock quantity field** added to product creation/edit form
- **Real-time stock status** display (Mavjud, Kam qoldi, Tugagan)
- **Validation**: Stock must be integer ≥ 0
- **Immediate updates** when admin changes stock
- **Uzbek UI messages** for all stock operations

### 2. Frontend - Stock Visibility ✅
- **Product cards** show stock status:
  - Stock > 10: "Mavjud" (green)
  - Stock ≤ 10: "Kam qoldi (X dona)" (orange)
  - Stock = 0: "Tugagan" (red)
- **Add to cart button** disabled when stock = 0
- **Button text** changes to "Tugagan" when out of stock

### 3. Cart - Quantity Limits ✅
- **Stock validation** before adding to cart
- **Quantity selector** max = available stock
- **Stock warnings** displayed in cart
- **Uzbek error messages** when exceeding stock
- **Plus button** disabled when at stock limit

### 4. Order & Stock Synchronization ✅
- **Atomic stock reduction** using database transactions
- **Race condition prevention** with row-level locking
- **Server-side validation** before order creation
- **Automatic stock reduction** on successful order
- **Order rejection** if insufficient stock
- **Uzbek success/error messages**

### 5. Backend Rules ✅
- **Database transaction** for all stock operations
- **Row-level locking** (FOR UPDATE) prevents race conditions
- **Never trust frontend** - all validation server-side
- **Atomic operations** via PostgreSQL functions

### 6. Real-time Updates ✅
- **Product cards** update after stock changes
- **Cart** reflects current stock levels
- **Admin panel** shows live stock status
- **No stale data** - always fresh from database

---

## 🔧 Technical Implementation

### Database Functions

#### 1. `reduce_product_stock()`
Atomically reduces product stock with row-level locking.

```sql
CREATE OR REPLACE FUNCTION reduce_product_stock(
  p_product_id UUID,
  p_quantity INTEGER
)
RETURNS TABLE(
  success BOOLEAN,
  message TEXT,
  new_stock INTEGER
)
```

**Features**:
- Row-level locking (`FOR UPDATE`)
- Stock validation before reduction
- Returns success status and new stock level
- Uzbek error messages

**Usage**:
```sql
SELECT * FROM reduce_product_stock(
  '123e4567-e89b-12d3-a456-426614174000',
  5
);
```

#### 2. `restore_product_stock()`
Restores stock when order is cancelled.

```sql
CREATE OR REPLACE FUNCTION restore_product_stock(
  p_product_id UUID,
  p_quantity INTEGER
)
RETURNS BOOLEAN
```

#### 3. `get_stock_status()`
Returns stock status text for display.

```sql
CREATE OR REPLACE FUNCTION get_stock_status(p_stock_quantity INTEGER)
RETURNS TEXT
```

Returns:
- "Tugagan" if stock = 0
- "Kam qoldi" if stock ≤ 10
- "Mavjud" if stock > 10

#### 4. `create_order_with_stock_reduction()`
Creates order and reduces stock atomically.

```sql
CREATE OR REPLACE FUNCTION create_order_with_stock_reduction(
  p_user_id UUID,
  p_seller_id UUID,
  p_items JSONB,
  p_total_amount NUMERIC,
  p_currency TEXT,
  p_mahalla TEXT,
  p_delivery_address TEXT,
  p_phone TEXT,
  p_customer_name TEXT DEFAULT NULL,
  p_customer_email TEXT DEFAULT NULL
)
RETURNS TABLE(
  success BOOLEAN,
  message TEXT,
  order_id UUID,
  failed_products JSONB
)
```

**Features**:
- Pre-validates ALL products have sufficient stock
- Locks all product rows before creating order
- Creates order only if all products available
- Reduces stock for each product atomically
- Returns detailed error info if any product fails
- Transaction rollback on any failure

**Flow**:
```
1. Lock all product rows (FOR UPDATE)
2. Validate each product has sufficient stock
3. If any fails → return error with details
4. Create order record
5. Reduce stock for each product
6. Commit transaction
7. Return success with order_id
```

---

## 📊 Stock Validation Flow

### Adding to Cart

```
User clicks "Add to Cart"
    ↓
Frontend: Check if stock > 0
    ├─ No → Button disabled, show "Tugagan" ❌
    └─ Yes → Call addToCart() ✅
        ↓
    Backend: Check current stock
        ├─ Stock = 0 → "Mahsulot tugagan" ❌
        ├─ Stock < quantity → "Mavjud miqdordan ortiq..." ❌
        └─ Stock ≥ quantity → Add to cart ✅
            ↓
        Check existing cart quantity
            ├─ Total > stock → Error ❌
            └─ Total ≤ stock → Success ✅
```

### Updating Cart Quantity

```
User changes quantity in cart
    ↓
Frontend: Check if new quantity ≤ stock
    ├─ No → Show error, don't update ❌
    └─ Yes → Call updateCartItemQuantity() ✅
        ↓
    Backend: Validate against current stock
        ├─ Quantity > stock → Error ❌
        └─ Quantity ≤ stock → Update ✅
```

### Placing Order

```
User clicks "Buyurtma berish"
    ↓
Frontend: Collect order data
    ↓
Backend: create_order_with_stock_reduction()
    ↓
Lock ALL product rows (FOR UPDATE)
    ↓
Validate EACH product stock
    ├─ Any insufficient → Rollback, return errors ❌
    └─ All sufficient → Continue ✅
        ↓
    Create order record
        ↓
    Reduce stock for each product
        ↓
    Commit transaction
        ↓
    Return success ✅
```

---

## 🎯 Stock Status Display

### Product Card

```tsx
{product.stock_quantity === 0 ? (
  <p className="text-xs text-destructive font-medium">Tugagan</p>
) : product.stock_quantity <= 10 ? (
  <p className="text-xs text-orange-500 font-medium">
    Kam qoldi ({product.stock_quantity} dona)
  </p>
) : (
  <p className="text-xs text-green-600 font-medium">Mavjud</p>
)}
```

### Cart Item

```tsx
{product.stock_quantity === 0 && (
  <p className="text-xs text-destructive font-medium">Tugagan</p>
)}
{product.stock_quantity > 0 && product.stock_quantity < item.quantity && (
  <p className="text-xs text-orange-500 font-medium">
    Faqat {product.stock_quantity} dona mavjud
  </p>
)}
{product.stock_quantity > 0 && product.stock_quantity <= 10 && (
  <p className="text-xs text-orange-500 font-medium">
    Kam qoldi ({product.stock_quantity} dona)
  </p>
)}
```

### Admin Product List

```tsx
<p className={`font-medium ${
  product.stock_quantity === 0 ? 'text-destructive' : 
  product.stock_quantity <= 10 ? 'text-orange-500' : 
  'text-green-600'
}`}>
  {product.stock_quantity === 0 && 'Tugagan'}
  {product.stock_quantity > 0 && product.stock_quantity <= 10 && 
    `Kam qoldi (${product.stock_quantity})`}
  {product.stock_quantity > 10 && 
    `Mavjud (${product.stock_quantity})`}
</p>
```

---

## 🔒 Race Condition Prevention

### Problem
Two users try to buy the last item simultaneously:
1. User A checks stock: 1 available ✅
2. User B checks stock: 1 available ✅
3. User A places order: stock reduced to 0 ✅
4. User B places order: stock reduced to -1 ❌ **OVERSOLD!**

### Solution: Row-Level Locking

```sql
-- Lock the product row
SELECT stock_quantity INTO current_stock
FROM products
WHERE id = p_product_id
FOR UPDATE;  -- This locks the row until transaction completes

-- Now only ONE transaction can proceed at a time
IF current_stock < p_quantity THEN
  -- Insufficient stock
  RETURN error;
END IF;

-- Reduce stock
UPDATE products
SET stock_quantity = stock_quantity - p_quantity
WHERE id = p_product_id;
```

**How it works**:
1. `FOR UPDATE` locks the row
2. Other transactions wait until lock is released
3. Only one transaction can check and reduce stock at a time
4. Prevents overselling completely

---

## 📝 API Functions

### Frontend API (`src/db/api.ts`)

#### `addToCart(userId, productId, quantity)`
Adds product to cart with stock validation.

```typescript
export const addToCart = async (
  userId: string, 
  productId: string, 
  quantity: number = 1
) => {
  // Check product stock
  const { data: product } = await supabase
    .from('products')
    .select('stock_quantity, name')
    .eq('id', productId)
    .single();

  if (product.stock_quantity === 0) {
    throw new Error('Mahsulot tugagan');
  }

  if (product.stock_quantity < quantity) {
    throw new Error(
      `Mavjud miqdordan ortiq qo'shib bo'lmaydi. ` +
      `Faqat ${product.stock_quantity} dona mavjud`
    );
  }

  // Check existing cart item
  const { data: existingItem } = await supabase
    .from('cart_items')
    .select('quantity')
    .eq('user_id', userId)
    .eq('product_id', productId)
    .maybeSingle();

  const newQuantity = existingItem 
    ? existingItem.quantity + quantity 
    : quantity;

  if (newQuantity > product.stock_quantity) {
    throw new Error(
      `Mavjud miqdordan ortiq qo'shib bo'lmaydi. ` +
      `Faqat ${product.stock_quantity} dona mavjud`
    );
  }

  // Add to cart
  const { data, error } = await supabase
    .from('cart_items')
    .upsert({ 
      user_id: userId, 
      product_id: productId, 
      quantity: newQuantity 
    })
    .select()
    .maybeSingle();

  if (error) throw error;
  return data;
};
```

#### `updateCartItemQuantity(cartItemId, quantity)`
Updates cart item quantity with stock validation.

```typescript
export const updateCartItemQuantity = async (
  cartItemId: string, 
  quantity: number
) => {
  // Get cart item with product info
  const { data: cartItem } = await supabase
    .from('cart_items')
    .select('product_id, products(stock_quantity, name)')
    .eq('id', cartItemId)
    .single();

  const product = cartItem.products;

  if (quantity > product.stock_quantity) {
    throw new Error(
      `Mavjud miqdordan ortiq qo'shib bo'lmaydi. ` +
      `Faqat ${product.stock_quantity} dona mavjud`
    );
  }

  // Update quantity
  const { data, error } = await supabase
    .from('cart_items')
    .update({ quantity })
    .eq('id', cartItemId)
    .select()
    .maybeSingle();

  if (error) throw error;
  return data;
};
```

#### `createOrderWithStockReduction(orderData)`
Creates order with atomic stock reduction.

```typescript
export const createOrderWithStockReduction = async (orderData: {
  userId: string;
  sellerId: string;
  items: any[];
  totalAmount: number;
  currency: string;
  mahalla: string;
  deliveryAddress: string;
  phone: string;
  customerName?: string;
  customerEmail?: string;
}) => {
  const { data, error } = await supabase.rpc(
    'create_order_with_stock_reduction',
    {
      p_user_id: orderData.userId,
      p_seller_id: orderData.sellerId,
      p_items: orderData.items,
      p_total_amount: orderData.totalAmount,
      p_currency: orderData.currency,
      p_mahalla: orderData.mahalla,
      p_delivery_address: orderData.deliveryAddress,
      p_phone: orderData.phone,
      p_customer_name: orderData.customerName || null,
      p_customer_email: orderData.customerEmail || null,
    }
  );

  if (error) throw error;

  const result = data[0];

  if (!result.success) {
    const failedProducts = result.failed_products || [];
    if (failedProducts.length > 0) {
      const firstFailed = failedProducts[0];
      throw new Error(
        firstFailed.reason || 'Mahsulot miqdori yetarli emas'
      );
    }
    throw new Error(
      result.message || 'Buyurtmani yaratishda xatolik yuz berdi'
    );
  }

  return {
    success: true,
    orderId: result.order_id,
    message: result.message,
  };
};
```

---

## 🎨 UI Components

### Admin Product Edit Form

```tsx
<div className="space-y-2">
  <Label htmlFor="stock">Mahsulot soni *</Label>
  <Input
    id="stock"
    type="number"
    min="0"
    step="1"
    value={product.stock_quantity}
    onChange={(e) => setProduct({ 
      ...product, 
      stock_quantity: parseInt(e.target.value) || 0 
    })}
    placeholder="Mavjud mahsulotlar soni"
  />
  <p className="text-sm text-muted-foreground">
    {product.stock_quantity === 0 && 'Mahsulot tugagan'}
    {product.stock_quantity > 0 && product.stock_quantity <= 10 && 
      `Kam qoldi (${product.stock_quantity} dona)`}
    {product.stock_quantity > 10 && 'Mavjud'}
  </p>
</div>
```

### Product Card Button

```tsx
<Button
  className="w-full"
  onClick={handleAddToCart}
  disabled={loading || product.stock_quantity === 0}
>
  <ShoppingCart className="mr-2 h-4 w-4" />
  {product.stock_quantity === 0 ? 'Tugagan' : 'Savatchaga qo\'shish'}
</Button>
```

### Cart Quantity Controls

```tsx
<div className="flex items-center gap-2 border rounded">
  <Button
    variant="ghost"
    size="icon"
    onClick={() => handleUpdateQuantity(item.id, item.quantity - 1, product.stock_quantity)}
    disabled={item.quantity <= 1}
  >
    <Minus className="h-4 w-4" />
  </Button>
  <span className="w-8 text-center">{item.quantity}</span>
  <Button
    variant="ghost"
    size="icon"
    onClick={() => handleUpdateQuantity(item.id, item.quantity + 1, product.stock_quantity)}
    disabled={item.quantity >= product.stock_quantity || product.stock_quantity === 0}
  >
    <Plus className="h-4 w-4" />
  </Button>
</div>
```

---

## 🧪 Testing Scenarios

### Test 1: Add to Cart with Sufficient Stock
1. Product has stock = 10
2. User adds 5 to cart
3. **Expected**: Success, cart shows 5 items

### Test 2: Add to Cart with Insufficient Stock
1. Product has stock = 3
2. User tries to add 5 to cart
3. **Expected**: Error "Mavjud miqdordan ortiq qo'shib bo'lmaydi. Faqat 3 dona mavjud"

### Test 3: Add to Cart When Out of Stock
1. Product has stock = 0
2. User clicks "Add to Cart"
3. **Expected**: Button disabled, shows "Tugagan"

### Test 4: Increase Quantity in Cart
1. Cart has 2 items, product stock = 5
2. User clicks + button
3. **Expected**: Quantity increases to 3

### Test 5: Increase Quantity Beyond Stock
1. Cart has 5 items, product stock = 5
2. User clicks + button
3. **Expected**: Button disabled, can't increase

### Test 6: Race Condition Test
1. Product has stock = 1
2. User A starts checkout
3. User B starts checkout simultaneously
4. **Expected**: Only ONE order succeeds, other gets "Mahsulot miqdori yetarli emas"

### Test 7: Admin Updates Stock
1. Admin changes stock from 10 to 5
2. User has 8 items in cart
3. User tries to checkout
4. **Expected**: Error "Mahsulot miqdori yetarli emas"

### Test 8: Stock Display
1. Product stock = 15
2. **Expected**: Shows "Mavjud" (green)
3. Admin reduces to 5
4. **Expected**: Shows "Kam qoldi (5 dona)" (orange)
5. Admin reduces to 0
6. **Expected**: Shows "Tugagan" (red), button disabled

---

## 📋 Error Messages (Uzbek)

| Scenario | Message |
|----------|---------|
| Out of stock | "Mahsulot tugagan" |
| Insufficient stock | "Mahsulot miqdori yetarli emas" |
| Exceeding available | "Mavjud miqdordan ortiq qo'shib bo'lmaydi. Faqat X dona mavjud" |
| Stock updated | "Mahsulot soni yangilandi" |
| Order accepted | "Buyurtma qabul qilindi" |
| Cart updated | "Mahsulot miqdori yangilandi" |
| Product not found | "Mahsulot topilmadi" |
| Invalid stock | "Mahsulot soni butun son va 0 dan katta yoki teng bo'lishi kerak" |

---

## 🔐 Security Considerations

### 1. Never Trust Frontend
- All stock validation happens server-side
- Frontend checks are for UX only
- Backend always re-validates before committing

### 2. Atomic Operations
- All stock operations use database transactions
- Either all succeed or all rollback
- No partial updates

### 3. Row-Level Locking
- `FOR UPDATE` prevents concurrent modifications
- Ensures only one transaction modifies stock at a time
- Prevents race conditions completely

### 4. Validation at Multiple Levels
- Frontend: Immediate feedback
- API layer: Business logic validation
- Database: Constraint enforcement
- Database function: Atomic validation

---

## 📈 Performance Considerations

### Database Indexes
```sql
-- Index for stock queries
CREATE INDEX idx_products_stock_quantity 
ON products(stock_quantity) 
WHERE stock_quantity > 0;
```

### Query Optimization
- Use `FOR UPDATE` only when necessary (during order placement)
- Regular stock checks use simple SELECT queries
- Batch operations where possible

### Caching Strategy
- Don't cache stock quantities (always fetch fresh)
- Cache product details (name, images, etc.)
- Invalidate cart cache after stock changes

---

## 🚀 Future Enhancements

### 1. Low Stock Alerts
- Notify admin when stock ≤ threshold
- Email/SMS notifications
- Dashboard widget

### 2. Stock History
- Track all stock changes
- Audit log for admin actions
- Analytics on stock movement

### 3. Automatic Reordering
- Set reorder point
- Automatic purchase orders
- Supplier integration

### 4. Reserved Stock
- Reserve stock during checkout process
- Release after timeout
- Prevent cart abandonment issues

### 5. Bulk Stock Updates
- CSV import/export
- Batch update operations
- Stock reconciliation tools

---

## ✅ Checklist

### Admin Panel
- [x] Stock quantity field in product form
- [x] Stock validation (integer ≥ 0)
- [x] Real-time stock status display
- [x] Uzbek UI messages
- [x] Stock display in product list

### Frontend
- [x] Stock status on product cards
- [x] Conditional button states
- [x] Stock-based button text
- [x] Color-coded stock indicators

### Cart
- [x] Stock validation before adding
- [x] Quantity limits enforced
- [x] Stock warnings displayed
- [x] Plus/minus button states
- [x] Uzbek error messages

### Orders
- [x] Atomic stock reduction function
- [x] Race condition prevention
- [x] Server-side validation
- [x] Transaction rollback on failure
- [x] Detailed error reporting

### Backend
- [x] Database functions created
- [x] Row-level locking implemented
- [x] Constraints added
- [x] Indexes created
- [x] Permissions granted

### Testing
- [x] Lint passes
- [x] TypeScript compiles
- [x] No console errors
- [x] All migrations applied

---

## 📞 Support

For issues or questions:
1. Check error messages in browser console
2. Verify stock quantities in admin panel
3. Test with different stock levels
4. Check database logs for transaction errors

---

**Status**: ✅ FULLY IMPLEMENTED  
**Version**: 3.0  
**Date**: 2026-02-10  
**Platform**: URGOODS Marketplace - Urgut District
