# URGOODS - Extended Admin Panel

## Overview
The admin panel has been significantly extended with comprehensive product management, category controls with logo upload, and a special animated promotions section - all in Uzbek language.

## New Features

### 1. Full Product Management (Mahsulotlar Boshqaruvi)
**Location:** `/admin/products/edit/:id` and `/admin/products/new`

Admins can now fully edit every aspect of products:

#### Basic Information
- Mahsulot nomi (Product name)
- Qisqa tavsif (Short description) - appears on product cards
- To'liq tavsif (Full description)
- Narx (Price)
- Chegirma foizi (Discount percentage)
- Qoldiq/Stock (Inventory)
- Kategoriya (Category selection)
- Mahsulot holati (Active/Inactive status)

#### Product Images
- Upload multiple images
- Remove images
- First image is automatically marked as "Asosiy" (Main)
- 1MB file size limit with validation
- Supports PNG, JPG formats

#### Product Card Customization
- **Kartochka rang aksenti** - Color accent picker with hex input
- **Badge turi** - Badge type selection:
  - Yo'q (None)
  - Chegirma (Discount)
  - TOP
  - Aksiya (Promotion)
- **Kartochka animatsiyasi** - Toggle card animation on/off

### 2. Category & Logo Management (Kategoriyalar va Logotiplar)
**Location:** `/admin/categories-manage`

Complete category management system:

#### Category Controls
- **Kategoriya nomi** - Category name in Uzbek
- **Kategoriya logotipi** - Logo upload (SVG, PNG, max 1MB)
- **Rang mavzusi** - Color theme picker
- **Kategoriya faolligi** - Active/Inactive toggle
- **Tartib** - Display order (drag handle for future sorting)

#### Features
- Visual logo preview
- Color theme display with color swatch
- Quick toggle for active/inactive status
- Edit and delete functionality
- Logo appears on product cards, filters, and admin panel

### 3. Promotions Management (Aksiyadagi Tovarlar)
**Location:** `/admin/promotions`

Dedicated section for managing special promotions:

#### Promotion Controls
- **Mahsulot** - Select product from dropdown
- **Aksiya sarlavhasi** - Promotion title
- **Badge matni** - Custom badge text (default: "AKSIYA")
- **Chegirma %** - Discount percentage
- **Boshlanish vaqti** - Start date/time picker
- **Tugash vaqti** - End date/time picker
- **Kartochka uslubi** - Card style selection:
  - Oddiy (Default)
  - Keng (Wide)
  - Maxsus (Featured)
- **Aksiya holati** - Active/Inactive toggle

#### Promotion Display
- Shows product image thumbnail
- Displays time remaining with clock icon
- Shows all promotion details in organized grid
- Quick edit and delete actions
- Drag handle for reordering (display_order)

### 4. Promotions Carousel (Frontend Component)
**Location:** Home page, auto-imported

Special animated carousel for promotions:

#### Visual Design
- **Wide format cards** with gradient backgrounds
- **Large discount badges** with pulse animation
- **Prominent badge text** with bounce animation
- **Timer display** showing time remaining
- **Price comparison** - original vs discounted price

#### Animation Behavior
- Auto-slides every 4 seconds
- Smooth transitions between promotions
- **Pause on hover** - stops auto-slide when user hovers
- **Mobile swipe support** - touch-friendly navigation
- Dot indicators for navigation
- Previous/Next buttons

#### Features
- Fetches active promotions from database
- Real-time countdown timer
- Click to navigate to product detail page
- Responsive design (mobile-first)

## Database Schema Updates

### Products Table - New Fields
```sql
- card_color_accent TEXT DEFAULT '#8B5CF6'
- badge_type TEXT (none/discount/top/promotion)
- card_animation_enabled BOOLEAN DEFAULT true
- short_description TEXT
- image_order INTEGER[]
```

### Categories Table - New Fields
```sql
- logo_url TEXT
- color_theme TEXT DEFAULT '#8B5CF6'
- display_order INTEGER DEFAULT 0
- is_active BOOLEAN DEFAULT true
```

### Promotions Table (New)
```sql
- id UUID PRIMARY KEY
- product_id UUID REFERENCES products
- title TEXT NOT NULL
- badge_text TEXT DEFAULT 'AKSIYA'
- discount_percentage INTEGER NOT NULL
- start_date TIMESTAMPTZ NOT NULL
- end_date TIMESTAMPTZ NOT NULL
- is_active BOOLEAN DEFAULT true
- display_order INTEGER DEFAULT 0
- card_style TEXT (default/wide/featured)
- created_at, updated_at TIMESTAMPTZ
```

### Database Function
- `get_active_promotions()` - Returns active promotions with product details and time remaining

## Admin Navigation Updates

### Header Dropdown Menu
Admin users now see expanded menu with quick access to:
- Admin bosh sahifa (Dashboard)
- Kategoriyalar (Categories)
- Mahsulotlar (Products)
- Aksiyalar (Promotions)
- Buyurtmalar (Orders)
- Sotuvchilar (Sellers)
- Mahallalar (Mahallas)

### Admin Dashboard
New quick action cards for:
- Kategoriyalar - Category and logo management
- Aksiyalar - Promotions management

## UI/UX Features

### Design Principles
- **Minimal and professional** - Clean, focused interface
- **Fast performance** - Optimized queries and loading
- **Dark mode support** - Consistent with app theme
- **Drag & drop ready** - GripVertical icons for future sorting
- **Mobile responsive** - Works on all screen sizes

### Uzbek Language
All UI text is in Uzbek:
- Form labels and placeholders
- Button text
- Success/error messages
- Section headings
- Help text

### User Feedback
- Toast notifications for all actions
- Loading states during operations
- Confirmation dialogs for destructive actions
- Visual feedback on hover/focus

## File Structure

```
src/
├── pages/admin/
│   ├── AdminProductEditPage.tsx (NEW)
│   ├── AdminCategoriesManagePage.tsx (NEW)
│   ├── AdminPromotionsPage.tsx (NEW)
│   └── AdminProductsPage.tsx (UPDATED - added edit button)
├── components/
│   └── promotions/
│       └── PromotionsCarousel.tsx (NEW)
├── types/
│   └── types.ts (UPDATED - added Promotion type, updated Product & Category)
└── routes.tsx (UPDATED - added new routes)
```

## Usage Instructions

### For Admins

#### Managing Products
1. Navigate to Admin → Mahsulotlar
2. Click "Yangi mahsulot" to create or "Tahrirlash" to edit
3. Fill in all required fields (marked with *)
4. Upload product images (drag multiple files)
5. Customize card appearance (color, badge, animation)
6. Click "O'zgarishlarni saqlash"

#### Managing Categories
1. Navigate to Admin → Kategoriyalar
2. Click "Kategoriya qo'shish"
3. Enter category name
4. Upload logo (SVG or PNG)
5. Choose color theme
6. Toggle active status
7. Click "Qo'shish"

#### Managing Promotions
1. Navigate to Admin → Aksiyalar
2. Click "Aksiyaga qo'shish"
3. Select product from dropdown
4. Enter promotion title and badge text
5. Set discount percentage
6. Choose start and end dates
7. Select card style (wide recommended)
8. Click "Qo'shish"

### For Users
- Promotions automatically appear on home page
- Carousel auto-rotates every 4 seconds
- Hover to pause and read details
- Click to view product
- Timer shows time remaining

## Technical Notes

### Image Upload
- All images stored in Supabase Storage bucket: `app-9inj10nzkjr5_product_images`
- 1MB size limit enforced
- Automatic validation and error handling
- Public URLs generated for display

### RLS Policies
- Promotions: Public can view active, admins can manage all
- Products/Categories: Existing policies maintained
- Admin-only access enforced on all management pages

### Performance
- Promotions fetched via optimized RPC function
- Includes product details in single query
- Indexed on active status and dates
- Efficient carousel rendering

## Future Enhancements (Ready for Implementation)

1. **Drag & Drop Reordering**
   - GripVertical icons already in place
   - display_order field exists in database
   - Can implement with react-beautiful-dnd

2. **Bulk Operations**
   - Multi-select products
   - Batch activate/deactivate
   - Bulk category assignment

3. **Advanced Filtering**
   - Filter by multiple categories
   - Date range filters
   - Stock level alerts

4. **Analytics**
   - Promotion performance metrics
   - Click-through rates
   - Conversion tracking

## Conclusion

The extended admin panel provides complete control over the marketplace with:
- ✅ Full product editing with visual customization
- ✅ Category management with logo upload
- ✅ Special promotions section with animated carousel
- ✅ All UI in Uzbek language
- ✅ Professional, fast, mobile-responsive design
- ✅ Ready for commercial use in Urgut district
