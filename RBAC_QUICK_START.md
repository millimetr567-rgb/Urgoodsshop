# RBAC System - Quick Start Guide

## 🚀 For Administrators

### Accessing Role Management

1. Log in as an administrator
2. Navigate to **Admin Panel** → **Foydalanuvchi Rollari**
3. Or go directly to: `/admin/users/roles`

### Changing a User's Role

**Step-by-Step:**

1. **Find the User**
   - Use the search box to find user by name, phone, or email
   - Or scroll through the user list

2. **Open Role Dialog**
   - Click **"Rolni o'zgartirish"** button on the user card
   - Note: You cannot change your own role (button will be disabled)

3. **Select New Role**
   - Current role is displayed at the top
   - Choose from dropdown:
     - **Foydalanuvchi** - Regular user (can only purchase)
     - **Sotuvchi** - Seller (can add products and view orders)
     - **Administrator** - Admin (full system control)

4. **Add Reason (Optional)**
   - Enter reason in the text area
   - Example: "Sotuvchi sifatida ro'yxatdan o'tish so'rovi"

5. **Confirm Change**
   - Review the change preview
   - Click **"Tasdiqlash"** to confirm
   - Or **"Bekor qilish"** to cancel

6. **Success**
   - You'll see: "Foydalanuvchi roli yangilandi"
   - Or: "Foydalanuvchi sotuvchiga aylantirildi" (if changed to seller)

### Viewing Role Change History

**For All Users:**
1. Click **"Rol o'zgarishlari tarixi"** button at the top
2. View complete history of all role changes

**For Specific User:**
1. Find the user in the list
2. Click **"Tarix"** button on their card
3. View that user's role change history

**History Shows:**
- Who changed the role
- Old role → New role
- When it was changed
- Reason (if provided)

---

## 🔐 Security Rules

### What You CAN Do

✅ Change any other user's role  
✅ Promote users to seller or admin  
✅ Demote sellers or admins to regular users  
✅ View complete role change history  
✅ Add reasons for role changes  

### What You CANNOT Do

❌ **Change Your Own Role**
- Error: "Siz o'z rolingizni o'zgartira olmaysiz"
- Reason: Prevents accidental self-demotion

❌ **Downgrade the Last Admin**
- Error: "Oxirgi administratorni pasaytirib bo'lmaydi"
- Reason: Prevents system lockout

❌ **Use Invalid Roles**
- Error: "Noto'g'ri rol"
- Reason: Only user/seller/admin are valid

---

## 📊 Understanding the Dashboard

### Statistics Cards

1. **Jami Foydalanuvchilar** - Total users in system
2. **Administrator** - Number of admins (red badge)
3. **Sotuvchi** - Number of sellers (blue badge)
4. **Foydalanuvchi** - Number of regular users (gray badge)

### User Cards

Each user card shows:
- **Name** and **Username**
- **Current Role** (with colored badge)
- **Contact Info** (phone, email)
- **Mahalla** (if set)
- **Registration Date**
- **Seller Info** (if applicable):
  - Verified badge
  - Premium badge
  - Rating

### Search

- Search by name, username, phone, or email
- Results filter in real-time
- Case-insensitive

---

## 🎯 Common Scenarios

### Scenario 1: User Requests Seller Access

**Steps:**
1. Find user in the list
2. Click "Rolni o'zgartirish"
3. Select "Sotuvchi"
4. Add reason: "Sotuvchi sifatida ro'yxatdan o'tish so'rovi"
5. Confirm

**Result:**
- User can now access seller panel
- User can add products
- User can view their orders
- Message: "Foydalanuvchi sotuvchiga aylantirildi"

### Scenario 2: Promote User to Admin

**Steps:**
1. Find trusted user
2. Click "Rolni o'zgartirish"
3. Select "Administrator"
4. Add reason: "Yangi admin tayinlash"
5. Confirm

**Result:**
- User gets full admin access
- User can manage all system functions
- User can change other users' roles

### Scenario 3: Demote Seller to Regular User

**Steps:**
1. Find seller
2. Click "Rolni o'zgartirish"
3. Select "Foydalanuvchi"
4. Add reason: "Sotuvchi faoliyatini to'xtatish"
5. Confirm

**Result:**
- User loses seller access
- User can only browse and purchase
- Products remain but cannot be edited

### Scenario 4: Review Role Changes

**Steps:**
1. Click "Rol o'zgarishlari tarixi"
2. Review all changes
3. Check who made changes and when
4. Verify reasons provided

**Use Cases:**
- Audit trail for compliance
- Investigate unauthorized changes
- Track admin activity

---

## ⚠️ Important Notes

### Before Changing Roles

1. **Verify User Identity**
   - Confirm you have the right user
   - Check phone/email to be sure

2. **Consider Impact**
   - Seller → User: Loses product management
   - Admin → User: Loses all admin access
   - User → Admin: Gets full system control

3. **Add Clear Reason**
   - Helps with future audits
   - Provides context for changes
   - Optional but recommended

### After Changing Roles

1. **User May Need to Refresh**
   - Role change is immediate
   - User might need to reload page
   - Consider notifying user

2. **Check Audit Log**
   - Verify change was recorded
   - Confirm correct old/new roles
   - Review reason if added

3. **Monitor User Activity**
   - Ensure user has correct access
   - Watch for any issues
   - Be ready to revert if needed

---

## 🐛 Troubleshooting

### Problem: Cannot Change Role

**Possible Causes:**
1. Trying to change your own role
2. Trying to downgrade last admin
3. Not logged in as admin

**Solutions:**
- Ask another admin to change your role
- Promote another user to admin first
- Verify you're logged in as admin

### Problem: User Not Found

**Possible Causes:**
1. User doesn't exist
2. Search query too specific
3. User was deleted

**Solutions:**
- Try different search terms
- Check username spelling
- Verify user exists in system

### Problem: Role Change Not Working

**Possible Causes:**
1. Network error
2. Database issue
3. Permission problem

**Solutions:**
- Check internet connection
- Try again in a few moments
- Contact system administrator

---

## 📞 Support

If you encounter issues:

1. **Check Error Message**
   - Read the Uzbek error message
   - Follow suggested actions

2. **Review Documentation**
   - See `RBAC_DOCUMENTATION.md` for details
   - Check security rules

3. **Contact Support**
   - Provide user details
   - Include error message
   - Describe what you were trying to do

---

## ✅ Best Practices

### Do's

✅ Add reasons for role changes  
✅ Review history regularly  
✅ Verify user identity before changes  
✅ Keep at least 2 admins  
✅ Document important changes  

### Don'ts

❌ Change roles without verification  
❌ Remove all admins  
❌ Make changes without reason  
❌ Share admin credentials  
❌ Change roles while user is active  

---

**Quick Reference Version**: 1.0  
**Last Updated**: 2026-02-10  
**Platform**: URGOODS Marketplace  
**Admin UI Language**: Uzbek
