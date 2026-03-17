# Screen Inventory

## Food Delivery Platform - Complete Screen/View Catalog

| Field | Detail |
|---|---|
| **Total Screens** | 66 |
| **Customer App (Android + Web)** | 28 screens (SCR-C-001 to SCR-C-028) |
| **Driver App (Android)** | 10 screens (SCR-D-001 to SCR-D-010) |
| **Restaurant Dashboard (Web)** | 28 screens (SCR-R-001 to SCR-R-028) |
| **Source** | PRD.md Sections 6.1-6.24 and Section 7 |
| **Last Updated** | March 2026 |

---

## Table of Contents

1. [Customer App Screens](#1-customer-app-screens)
   - [Authentication & Onboarding](#11-authentication--onboarding) (SCR-C-001 to SCR-C-005)
   - [Menu & Discovery](#12-menu--discovery) (SCR-C-006 to SCR-C-009)
   - [Cart & Checkout](#13-cart--checkout) (SCR-C-010 to SCR-C-013)
   - [Order Tracking & History](#14-order-tracking--history) (SCR-C-014 to SCR-C-018)
   - [Offers & Addresses](#15-offers--addresses) (SCR-C-019 to SCR-C-021)
   - [Profile & Settings](#16-profile--settings) (SCR-C-022 to SCR-C-028)
2. [Driver App Screens](#2-driver-app-screens) (SCR-D-001 to SCR-D-010)
3. [Restaurant Dashboard Screens](#3-restaurant-dashboard-screens)
   - [Auth & Dashboard](#31-auth--dashboard) (SCR-R-001 to SCR-R-002)
   - [Menu Management](#32-menu-management) (SCR-R-003 to SCR-R-005)
   - [Order Processing](#33-order-processing) (SCR-R-006 to SCR-R-007)
   - [Driver Management](#34-driver-management) (SCR-R-008 to SCR-R-011)
   - [Business Settings & Payments](#35-business-settings--payments) (SCR-R-012 to SCR-R-013)
   - [Marketing & Promotions](#36-marketing--promotions) (SCR-R-014 to SCR-R-017)
   - [Reports & Analytics](#37-reports--analytics) (SCR-R-018 to SCR-R-020)
   - [Customer & Support](#38-customer--support) (SCR-R-021 to SCR-R-024)
   - [Platform Configuration](#39-platform-configuration) (SCR-R-025 to SCR-R-028)
4. [Navigation Structure](#4-navigation-structure)
5. [Screen-to-Feature Mapping](#5-screen-to-feature-mapping)
6. [Screen State Summary](#6-screen-state-summary)

---

## 1. Customer App Screens

### 1.1 Authentication & Onboarding

---

#### SCR-C-001: Splash Screen

| Property | Detail |
|---|---|
| **Module** | Authentication |
| **Purpose** | App entry point with restaurant branding |
| **Accessible By** | All users |
| **User Stories** | US-CUST-AUTH-001 |
| **PRD Section** | 6.1 |
| **Nav Entry Point** | App launch |

**Layout:**
- Full screen with restaurant logo (centered)
- Brand colors background
- Loading indicator at bottom
- Duration: 2-3 seconds or until initial data loads

**States:**
- Loading (default)
- Error (network unavailable -- show retry button)

**Navigates To:**
- Onboarding (SCR-C-002) on first launch
- Login (SCR-C-003) if not authenticated
- Home (SCR-C-006) if authenticated session exists

---

#### SCR-C-002: Onboarding Screens

| Property | Detail |
|---|---|
| **Module** | Authentication |
| **Purpose** | Introduce app features on first launch |
| **Accessible By** | New users (first launch only) |
| **User Stories** | US-CUST-AUTH-001 |
| **PRD Section** | 6.1 |
| **Nav Entry Point** | After splash, first launch only |

**Layout:**
- Swipeable carousel with 2-3 slides
- Each slide: illustration, headline, description
- Dot indicators at bottom
- "Skip" button at top-right
- "Next" button at bottom
- Final slide: "Get Started" button

**States:**
- First launch only (skipped on subsequent opens)

**Navigates To:**
- Login (SCR-C-003) on "Get Started" or "Skip"

---

#### SCR-C-003: Login Screen

| Property | Detail |
|---|---|
| **Module** | Authentication |
| **Purpose** | User authentication |
| **Accessible By** | Unauthenticated users |
| **User Stories** | US-CUST-AUTH-001, US-CUST-AUTH-002, US-CUST-AUTH-003 |
| **PRD Section** | 6.1 |
| **Nav Entry Point** | After onboarding / session expired |

**Layout:**
- Restaurant logo at top
- "Welcome Back" heading
- Phone/email input field (text, required, validation: valid phone or email format)
- Password field (password type, required, min 8 chars)
- "Login" button (primary)
- Divider "or continue with"
- Google login button (with icon)
- Facebook login button (with icon)
- "Forgot Password?" link
- "New here? Register" link

**States:**
- Default
- Loading (button shows spinner)
- Error (field-level validation messages)
- Network Error (toast)

**Form Fields:**
- Phone/Email (text, required)
- Password (password, required, min 8 chars)

**Navigates To:**
- OTP Verification (SCR-C-004) if OTP required
- Home (SCR-C-006) on successful login
- Registration (SCR-C-005) via "Register" link

---

#### SCR-C-004: OTP Verification Screen

| Property | Detail |
|---|---|
| **Module** | Authentication |
| **Purpose** | Verify phone/email via OTP code |
| **Accessible By** | Users during registration/login |
| **User Stories** | US-CUST-AUTH-001 |
| **PRD Section** | 6.1 |
| **Nav Entry Point** | From Login or Registration |

**Layout:**
- "Verify Your Account" heading
- Subtitle showing where OTP was sent (masked phone/email)
- 6 individual digit input fields (auto-advance on entry)
- Countdown timer for OTP expiry
- "Resend OTP" link (disabled until timer ends)
- "Verify" button (primary)

**States:**
- Default
- Countdown active
- OTP expired (show resend)
- Invalid OTP (shake animation on fields, error text)
- Success (brief checkmark animation, then redirect)

**Navigates To:**
- Home (SCR-C-006) on successful verification
- Back to Login (SCR-C-003) on cancel

---

#### SCR-C-005: Registration Screen

| Property | Detail |
|---|---|
| **Module** | Authentication |
| **Purpose** | New account creation |
| **Accessible By** | Unauthenticated users |
| **User Stories** | US-CUST-AUTH-001, US-CUST-AUTH-002 |
| **PRD Section** | 6.1 |
| **Nav Entry Point** | From Login screen |

**Layout:**
- "Create Account" heading
- Full name field (text, required)
- Phone number field (tel, required, +966 prefix pre-filled)
- Email field (email, optional)
- Password field (password, required, min 8 chars, show/hide toggle)
- "Register" button (primary)
- Terms & privacy policy checkbox (required)
- Social login buttons

**States:**
- Default
- Validation errors
- Loading
- Success

**Form Fields:**
- Full Name (text, required)
- Phone Number (tel, required, +966 prefix)
- Email (email, optional)
- Password (password, required, min 8 chars)
- Terms checkbox (required)

**Navigates To:**
- OTP Verification (SCR-C-004) on successful registration
- Login (SCR-C-003) via "Already have account?" link

---

### 1.2 Menu & Discovery

---

#### SCR-C-006: Home Screen

| Property | Detail |
|---|---|
| **Module** | Menu Browse & Search |
| **Purpose** | Main landing page with menu discovery |
| **Accessible By** | All users (guest + registered) |
| **User Stories** | US-CUST-MENU-001, US-CUST-MENU-005 |
| **PRD Section** | 6.2 |
| **Nav Entry Point** | Bottom tab: Home |

**Layout:**
- Top section: Restaurant logo/name, location selector (if multi-branch), search bar
- Promotional banner carousel (auto-scroll, tappable)
- "Popular Items" horizontal scrollable section
- Category grid/list
- Bottom navigation bar (Home, Offers, Cart with badge, Orders, Profile)

**States:**
- Loading (skeleton)
- Loaded
- Error (retry button)
- Restaurant Closed (banner)

**Interactions:**
- Pull-to-refresh to reload menu
- Scroll down to see full category list

**Navigates To:**
- Search (SCR-C-008) via search bar
- Menu Category (SCR-C-007) via category tap
- Product Detail (SCR-C-009) via item tap
- Branch Map (SCR-C-026) via location selector
- Offers (SCR-C-019) / Cart (SCR-C-010) / Order History (SCR-C-015) / Profile (SCR-C-022) via bottom nav

---

#### SCR-C-007: Menu Category Screen

| Property | Detail |
|---|---|
| **Module** | Menu Browse & Search |
| **Purpose** | Browse items within a category |
| **Accessible By** | All users |
| **User Stories** | US-CUST-MENU-001, US-CUST-MENU-002 |
| **PRD Section** | 6.2 |
| **Nav Entry Point** | From Home screen category tap |

**Layout:**
- Category name as header with back button
- Subcategory chips (horizontal scroll, if applicable)
- Item list (vertical scroll)
- Each item card: image (left), name + short description (center), price (right), "Add" button

**States:**
- Loading
- Loaded
- Empty ("No items in this category")
- Error

**Interactions:**
- Tap item card to go to detail
- Tap "Add" for quick add (default options)
- Long-press for quick-view modal

**Navigates To:**
- Product Detail (SCR-C-009) via item tap
- Back to Home (SCR-C-006)

---

#### SCR-C-008: Search Screen

| Property | Detail |
|---|---|
| **Module** | Menu Browse & Search |
| **Purpose** | Search and filter menu items |
| **Accessible By** | All users |
| **User Stories** | US-CUST-MENU-002, US-CUST-MENU-003, US-CUST-MENU-004 |
| **PRD Section** | 6.2 |
| **Nav Entry Point** | From Home screen search bar |

**Layout:**
- Search bar (auto-focused)
- Auto-suggest dropdown (max 5 items)
- Search results list (same card format as category screen)
- Filter button
- Sort button
- Results count indicator

**States:**
- Empty (recent searches shown)
- Typing (auto-suggest appears)
- Results loaded
- No results ("No items found. Try a different search.")
- Error

**Filter Modal:**
- Price range slider
- Availability toggle
- Dietary checkboxes (Vegetarian, Vegan, Gluten-free, Spicy, Halal-certified)
- Apply/Clear buttons

**Sort Options:**
- Relevance (default), Price Low-High, Price High-Low, Popularity, Rating, Newest

**Navigates To:**
- Product Detail (SCR-C-009) via item tap
- Back to Home (SCR-C-006)

---

#### SCR-C-009: Product Detail Screen

| Property | Detail |
|---|---|
| **Module** | Product Details & Customization |
| **Purpose** | View full item info and customize before adding to cart |
| **Accessible By** | All users |
| **User Stories** | US-CUST-MENU-006, US-CUST-MENU-007, US-CUST-MENU-008 |
| **PRD Section** | 6.3 |
| **Nav Entry Point** | From any menu list (category, search, popular, favorites) |

**Layout:**
- Hero image carousel (swipeable, full-width)
- Back button overlay on image
- Favorite (heart) icon overlay on image
- Item name (large text)
- Price (large, bold)
- Description text
- Nutrition info (collapsible section: calories, protein, carbs, fat)
- Allergy warnings (icon badges: nuts, dairy, gluten, etc.)
- Variant groups (each with label and options as chips/toggles)
- Special Instructions text field
- Quantity selector (+/- with number)
- "Add to Cart" button with live total price
- Sticky bottom bar with quantity and add button

**States:**
- Loading (skeleton)
- Loaded
- Unavailable (grayed, disabled add button)
- Added to cart (brief success animation)

**Form Fields:**
- Special Instructions (textarea, optional, max 200 chars)
- Variant selections (radio for single-select groups, checkbox for multi-select groups)
- Quantity (number, min 1, max 99)

**Navigates To:**
- Back to previous list
- Cart (SCR-C-010) after adding item (optional auto-navigate)

---

### 1.3 Cart & Checkout

---

#### SCR-C-010: Cart Screen

| Property | Detail |
|---|---|
| **Module** | Shopping Cart & Checkout |
| **Purpose** | Review and manage cart items |
| **Accessible By** | All users (checkout requires auth) |
| **User Stories** | US-CUST-CART-001 through US-CUST-CART-005 |
| **PRD Section** | 6.4 |
| **Nav Entry Point** | Bottom tab: Cart |

**Layout:**
- Cart header with item count
- Item list (each row: image thumbnail, name, customization summary, quantity +/-, line total, swipe-to-delete or X button)
- Upsell section ("You might also like..." horizontal scroll of item cards)
- Promo code field with "Apply" button
- Order summary (Subtotal, Discount, VAT, Delivery Fee, Total)
- "Proceed to Checkout" button (disabled if below minimum order)

**States:**
- Items in cart (default)
- Empty cart ("Your cart is empty. Browse the menu!" with CTA button)
- Loading
- Promo applied (green badge showing discount)
- Promo error (red text below field)

**Interactions:**
- Swipe left on item to reveal delete
- Tap +/- for quantity
- Tap item name to go back to product detail for editing

**Navigates To:**
- Checkout (SCR-C-011) via "Proceed to Checkout"
- Product Detail (SCR-C-009) via item tap
- Login (SCR-C-003) if guest attempts checkout

---

#### SCR-C-011: Checkout Screen

| Property | Detail |
|---|---|
| **Module** | Shopping Cart & Checkout |
| **Purpose** | Complete order placement |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-CART-006 through US-CUST-CART-011 |
| **PRD Section** | 6.4 |
| **Nav Entry Point** | From Cart screen |

**Layout:**
- Single scrollable page
- Progress indicator at top (Address > Time > Payment > Review)
- Order Type toggle (Delivery/Pickup)
- Address section (saved address cards, "Add New" button, or branch selector for pickup)
- Delivery Time section (ASAP radio, Schedule radio with date/time picker)
- Payment Method section (saved cards, Mada, Google Pay, STC Pay, COD as selectable cards with icons)
- Order Summary section (itemized list, all fees, grand total)
- "Place Order" button (fixed at bottom)
- Terms text ("By placing this order, you agree to our Terms")

**States:**
- Default
- Validation errors (highlighted sections)
- Processing payment (full-screen loader with "Processing your order...")
- Error (payment failed modal with retry option)

**Form Fields:**
- Delivery/Pickup (radio toggle)
- Address (selection or map pin-drop)
- Schedule date (date picker, only future dates during operating hours)
- Schedule time (time picker, 15-min slots)
- Payment method (radio selection)
- Promo code (text input)

**Navigates To:**
- Order Confirmation (SCR-C-012) on success
- Address Add/Edit (SCR-C-021) via "Add New Address"
- Back to Cart (SCR-C-010)

---

#### SCR-C-012: Order Confirmation Screen

| Property | Detail |
|---|---|
| **Module** | Shopping Cart & Checkout |
| **Purpose** | Confirm successful order placement |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-CART-011 |
| **PRD Section** | 6.4 |
| **Nav Entry Point** | From Checkout on success |

**Layout:**
- Success checkmark animation
- "Order Confirmed!" heading
- Order number (large, prominent)
- ETA display
- Order summary (collapsed, expandable)
- "Track Order" button (primary)
- "Continue Shopping" button (secondary)
- Confetti animation (brief)

**States:**
- Default (success). Terminal state; back button goes to home.

**Navigates To:**
- Order Tracking (SCR-C-014) via "Track Order"
- Home (SCR-C-006) via "Continue Shopping" or back button

---

#### SCR-C-013: Payment Method Selection

| Property | Detail |
|---|---|
| **Module** | Payment Processing |
| **Purpose** | Select and process payment method |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-PAY-001 through US-CUST-PAY-007 |
| **PRD Section** | 6.5 |
| **Nav Entry Point** | Within Checkout (SCR-C-011) |

**Layout:**
- Payment section within checkout screen
- Each method as a tappable card: icon (Visa/MC/Mada/Google Pay/STC Pay/Cash), name, last 4 digits (for saved cards)
- Radio button for selection
- "Add New Card" option
- Selected method highlighted with checkmark

**States:**
- Default (methods listed)
- Card input (Stripe Elements form)
- Processing (spinner on button)
- Error (red text below method)
- Success (redirect to confirmation)

**Payment Methods:**
- Credit/Debit Card (via Stripe)
- Mada (via Stripe)
- Google Pay (via Stripe)
- STC Pay (via Stripe or separate SDK)
- Cash on Delivery

---

### 1.4 Order Tracking & History

---

#### SCR-C-014: Order Tracking Screen

| Property | Detail |
|---|---|
| **Module** | Real-Time Order Tracking |
| **Purpose** | Track active order in real-time with GPS |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-TRACK-001 through US-CUST-TRACK-004 |
| **PRD Section** | 6.6 |
| **Nav Entry Point** | From Order Confirmation or Order Detail |

**Layout:**
- Status timeline (horizontal or vertical) at top with stage icons and labels
- Current stage highlighted/animated
- ETA display prominently below timeline
- Map section (Google Maps) showing: restaurant pin, customer pin, driver pin (moving), route line
- Driver info card: driver name, photo, vehicle info, rating
- "Call Driver" and "Message Driver" buttons
- Order summary (collapsible)
- "Help" button for support

**Status Stages:**
Order Placed > Confirmed > Preparing > Ready for Pickup > Driver Picked Up > On the Way > Delivered

**States:**
- Waiting for confirmation (pulsing "Waiting for restaurant...")
- Confirmed (checkmark animation)
- Preparing (kitchen icon)
- Ready (bag icon)
- On the Way (map visible, driver moving)
- Delivered (success animation, rating prompt)
- Error (Socket.io disconnected: "Reconnecting...")

**Interactions:**
- Tap driver card to see more details
- Tap Call/Message for direct contact
- Pinch/zoom on map
- Tap "View Order" to expand summary
- Pull down for manual refresh as backup

**Real-time Updates:**
- Socket.io for order status and driver location
- Driver location pin updates every 10-15 seconds with smooth animation
- ETA recalculates on significant driver movement (>200m)

**Navigates To:**
- Rating (SCR-C-018) after delivery
- Home (SCR-C-006) via back
- Support via "Help" button

---

#### SCR-C-015: Order History Screen

| Property | Detail |
|---|---|
| **Module** | Order History & Ratings |
| **Purpose** | View past orders |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-TRACK-005 |
| **PRD Section** | 6.7 |
| **Nav Entry Point** | Bottom tab: Orders |

**Layout:**
- "My Orders" heading
- Tab filters: Active / Completed / Cancelled
- Order list (each card: date, order #, items preview, total, status badge, reorder button)
- Infinite scroll pagination (20 orders per page)

**States:**
- Loading (skeleton)
- Orders loaded
- Empty ("No orders yet. Start ordering!" with browse CTA)
- Error

**Navigates To:**
- Order Detail (SCR-C-016) via order tap
- Order Tracking (SCR-C-014) via active order tap
- Home (SCR-C-006) via browse CTA

---

#### SCR-C-016: Order Detail Screen

| Property | Detail |
|---|---|
| **Module** | Order History & Ratings |
| **Purpose** | View full order details |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-TRACK-005, US-CUST-TRACK-006 |
| **PRD Section** | 6.7 |
| **Nav Entry Point** | From Order History |

**Layout:**
- Order # and date at top
- Status timeline (completed)
- Items list with customizations and individual prices
- Price breakdown (subtotal, discount, VAT, delivery fee, total)
- Delivery address
- Payment method
- Driver info (name, rating)
- Timestamps (placed, confirmed, picked up, delivered)
- "Reorder" button
- "View Receipt" button
- "Rate Items" button (if within 7-day rating window)

**States:**
- Loaded
- Reorder processing
- Receipt loading

**Navigates To:**
- Receipt (SCR-C-017) via "View Receipt"
- Rating (SCR-C-018) via "Rate Items"
- Cart (SCR-C-010) via "Reorder" (items added to cart)
- Back to Order History (SCR-C-015)

---

#### SCR-C-017: Receipt Screen

| Property | Detail |
|---|---|
| **Module** | Order History & Ratings |
| **Purpose** | View VAT-compliant receipt |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-TRACK-007 |
| **PRD Section** | 6.7 |
| **Nav Entry Point** | From Order Detail |

**Layout:**
- Restaurant name and logo
- "TAX INVOICE" heading
- Receipt number
- Date and time
- VAT Registration Number
- Itemized list (name, qty, unit price, line total)
- Subtotal
- Discount (if any)
- VAT (15%)
- Delivery Fee
- Grand Total
- Payment method
- "Download PDF" button
- "Share" button

**States:**
- Loaded
- Downloading PDF
- Share sheet

**Navigates To:**
- Back to Order Detail (SCR-C-016)

---

#### SCR-C-018: Rating Screen

| Property | Detail |
|---|---|
| **Module** | Order History & Ratings |
| **Purpose** | Rate delivered items and delivery experience |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-TRACK-008 |
| **PRD Section** | 6.7 |
| **Nav Entry Point** | From Order Detail or post-delivery prompt |

**Layout:**
- "Rate Your Order" heading
- Order summary
- For each item: item name, star rating (1-5, tappable), optional text review field
- Overall delivery rating (1-5 stars)
- "Submit" button

**States:**
- Default
- Partially filled
- Submitted (thank you message)
- Already rated (shows existing ratings, editable)

**Constraints:**
- Rating window: 7 days after delivery
- Review text: max 500 characters per item
- One rating per item per order (can be updated)

**Navigates To:**
- Back to Order Detail (SCR-C-016) or Home (SCR-C-006)

---

### 1.5 Offers & Addresses

---

#### SCR-C-019: Offers Screen

| Property | Detail |
|---|---|
| **Module** | Offers & Promotions |
| **Purpose** | View available promotions and apply |
| **Accessible By** | All users (apply requires auth) |
| **User Stories** | US-CUST-MISC-001, US-CUST-MISC-002 |
| **PRD Section** | 6.8 |
| **Nav Entry Point** | Bottom tab: Offers |

**Layout:**
- "Offers" heading
- Introductory offer banner (for new users, prominent styling)
- Offer cards list (each: image/illustration, title, description, discount badge, "Apply" button, expiry countdown)
- Categories filter (if offers are category-specific)

**States:**
- Loading
- Offers available
- No offers ("No offers right now. Check back soon!")
- Error

**Navigates To:**
- Cart (SCR-C-010) with promo auto-applied via "Apply"
- Home (SCR-C-006) / Menu if cart is empty and offer applied
- Login (SCR-C-003) if guest tries to apply

---

#### SCR-C-020: Address List Screen

| Property | Detail |
|---|---|
| **Module** | Address Management |
| **Purpose** | Manage saved addresses |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-MISC-003 |
| **PRD Section** | 6.9 |
| **Nav Entry Point** | From Profile or Checkout |

**Layout:**
- "My Addresses" heading
- Address cards (each: label icon, label name, address text, "Default" badge if default, edit/delete buttons)
- "Add New Address" button
- Swipe to delete with confirmation

**States:**
- Loading
- Addresses listed
- Empty ("No saved addresses. Add one!")
- Error

**Constraints:**
- Maximum 10 saved addresses per user
- One address must be default

**Navigates To:**
- Address Add/Edit (SCR-C-021) via "Add New" or edit button
- Back to Profile (SCR-C-022) or Checkout (SCR-C-011)

---

#### SCR-C-021: Address Add/Edit Screen

| Property | Detail |
|---|---|
| **Module** | Address Management |
| **Purpose** | Add or edit a delivery address via map pin-drop |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-MISC-003, US-CUST-MISC-004, US-CUST-MISC-005, US-CUST-MISC-006 |
| **PRD Section** | 6.9 |
| **Nav Entry Point** | From Address List or Checkout |

**Layout:**
- Google Map (top half of screen, draggable pin)
- Address fields below map:
  - Street (text, auto-filled via reverse geocoding)
  - District (text, auto-filled)
  - City (text, auto-filled)
  - Postal Code (text, auto-filled)
  - Apartment/Floor (text, optional)
  - Building Name (text, optional)
  - Delivery Instructions (textarea, optional, max 200 chars)
- Label selector (Home/Work/Other chips, custom text input for Other)
- "Set as Default" toggle
- "Save Address" button

**States:**
- Loading map
- Map loaded with pin
- Geocoding in progress (spinner on fields)
- Fields filled
- Validation errors
- Saving

**Form Validations:**
- Street (required)
- City (required)
- Label (required)

**Navigates To:**
- Back to Address List (SCR-C-020) or Checkout (SCR-C-011) on save

---

### 1.6 Profile & Settings

---

#### SCR-C-022: Profile Screen

| Property | Detail |
|---|---|
| **Module** | Notifications & Settings |
| **Purpose** | View and manage user profile |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-AUTH-001 |
| **PRD Section** | 6.10 |
| **Nav Entry Point** | Bottom tab: Profile |

**Layout:**
- User avatar/initials
- Name
- Phone/Email
- "Edit Profile" button
- Quick links: My Orders, My Addresses, Payment Methods, Favorites, Loyalty Points
- Settings link
- Logout button

**States:**
- Loaded
- Loading

**Navigates To:**
- Order History (SCR-C-015) via "My Orders"
- Address List (SCR-C-020) via "My Addresses"
- Settings (SCR-C-023) via Settings link
- Favorites (SCR-C-027) via "Favorites"
- Loyalty (SCR-C-025) via "Loyalty Points"

---

#### SCR-C-023: Settings Screen

| Property | Detail |
|---|---|
| **Module** | Notifications & Settings |
| **Purpose** | App preferences and account settings |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-MISC-007, US-CUST-MISC-008 |
| **PRD Section** | 6.10 |
| **Nav Entry Point** | From Profile |

**Layout:**
- Language section (Arabic/English toggle or radio)
- Notifications section (toggles: Order Updates, Promotions, Announcements)
- Account section (Change Password, Payment Methods, Delete Account)
- About section (Version, Terms, Privacy Policy, Contact Us)

**States:**
- Loaded
- Saving (when toggling)
- Error

**Navigates To:**
- Language (SCR-C-028) within settings
- Back to Profile (SCR-C-022)

---

#### SCR-C-024: Notifications Screen

| Property | Detail |
|---|---|
| **Module** | Notifications & Settings |
| **Purpose** | View notification history |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-MISC-007 |
| **PRD Section** | 6.10 |
| **Nav Entry Point** | From Profile or notification bell |

**Layout:**
- "Notifications" heading
- List of notifications (each: icon, title, body, timestamp, read/unread indicator)
- Tap to open related screen (order detail, offer, etc.)

**States:**
- Loading
- Notifications listed
- Empty ("No notifications yet")
- Error

**Navigates To:**
- Order Detail (SCR-C-016) for order notifications
- Offers (SCR-C-019) for promo notifications
- Order Tracking (SCR-C-014) for delivery notifications

---

#### SCR-C-025: Loyalty Screen

| Property | Detail |
|---|---|
| **Module** | Loyalty Program |
| **Purpose** | View loyalty points and history |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-MISC-009 |
| **PRD Section** | 6.11 |
| **Nav Entry Point** | From Profile |

**Layout:**
- Current balance (large number with "Points" label)
- Equivalent value in SAR
- "Redeem at Checkout" CTA
- Earning history (list: date, order #, points earned/redeemed, balance)
- Program rules summary (how to earn, how to redeem, expiry policy)

**States:**
- Loading
- Loaded
- No points yet ("Start earning! Place your first order.")
- Program not configured (hidden or "Coming soon")

**Navigates To:**
- Cart/Checkout (SCR-C-010/SCR-C-011) via "Redeem at Checkout"
- Back to Profile (SCR-C-022)

---

#### SCR-C-026: Branch Map Screen

| Property | Detail |
|---|---|
| **Module** | Menu Browse & Search |
| **Purpose** | View restaurant branches on map |
| **Accessible By** | All users |
| **User Stories** | US-CUST-CART-008 |
| **PRD Section** | 6.4 (referenced) |
| **Nav Entry Point** | From Home location selector |

**Layout:**
- Google Map with branch location pins
- Branch detail cards (name, address, distance, operating hours)
- Curbside pickup toggle per branch
- "Select This Branch" button

**States:**
- Loading map
- Branches displayed
- No branches nearby
- Error

**Navigates To:**
- Home (SCR-C-006) with selected branch context
- Checkout (SCR-C-011) if selecting pickup location

---

#### SCR-C-027: Favorites Screen

| Property | Detail |
|---|---|
| **Module** | Menu Browse & Search |
| **Purpose** | View saved favorite items |
| **Accessible By** | Registered users |
| **User Stories** | US-CUST-MENU-008 |
| **PRD Section** | 6.3 (referenced) |
| **Nav Entry Point** | From Profile |

**Layout:**
- "My Favorites" heading
- Favorited item cards (image, name, price, availability badge)
- Remove from favorites button per item
- "Add to Cart" quick action

**States:**
- Loading
- Favorites listed
- Empty ("No favorites yet. Browse the menu and save items you love!")
- Error

**Navigates To:**
- Product Detail (SCR-C-009) via item tap
- Cart (SCR-C-010) via "Add to Cart"
- Home (SCR-C-006) via browse CTA

---

#### SCR-C-028: Language Selection

| Property | Detail |
|---|---|
| **Module** | Notifications & Settings |
| **Purpose** | Switch app language (Arabic/English) |
| **Accessible By** | All users |
| **User Stories** | US-CUST-MISC-008 |
| **PRD Section** | 6.10 |
| **Nav Entry Point** | Within Settings (SCR-C-023) |

**Layout:**
- Arabic/English selection (radio buttons or large toggles)
- Preview of how text will appear in selected language
- "Apply" button

**States:**
- Current language highlighted
- Switching (app reloads in new language)

**Navigates To:**
- Settings (SCR-C-023) after language change applied

---

## 2. Driver App Screens

---

#### SCR-D-001: Driver Login Screen

| Property | Detail |
|---|---|
| **Module** | Authentication & Profile |
| **Purpose** | Driver authentication with restaurant credentials |
| **Accessible By** | Unauthenticated drivers |
| **User Stories** | US-DRV-001 |
| **PRD Section** | 6.12 |
| **Nav Entry Point** | App launch |

**Layout:**
- Restaurant logo and name
- "Driver Login" heading
- Username/ID field (text, required)
- Password field (password, required, show/hide toggle)
- "Login" button (primary)
- "Forgot Password? Contact Restaurant" text link

**States:**
- Default
- Loading
- Error (invalid credentials)
- Account inactive error

**Navigates To:**
- Driver Dashboard (SCR-D-002) on success

---

#### SCR-D-002: Driver Home/Dashboard

| Property | Detail |
|---|---|
| **Module** | Availability & Orders |
| **Purpose** | Main driver hub with availability toggle and orders |
| **Accessible By** | Authenticated drivers |
| **User Stories** | US-DRV-003, US-DRV-004 |
| **PRD Section** | 6.13 |
| **Nav Entry Point** | After login / main screen |

**Layout:**
- Availability toggle (large, prominent: green=Online, gray=Offline)
- Current status indicator
- Active delivery card (if any: order #, customer name, address, status, navigate button)
- Stats summary (today's deliveries, earnings if applicable)
- New assignment notification card (slides in from top)
- Queue of upcoming assignments

**States:**
- Offline (toggle off, no orders)
- Online waiting (toggle on, no current orders, "Waiting for orders..." message)
- Active delivery (current order card visible)
- New assignment (notification card with Accept/Decline)
- Multiple queued (list of assigned orders)

**Interactions:**
- Toggle availability
- Tap assignment for details
- Accept/Decline buttons on new assignments
- Tap active order for navigation

**Navigates To:**
- Order Detail (SCR-D-003) via order tap
- Navigation (SCR-D-004) via "Navigate" button
- Profile (SCR-D-008) / Performance (SCR-D-007) / Support (SCR-D-009) / Settings (SCR-D-010) via drawer/menu

---

#### SCR-D-003: Order Detail (Driver)

| Property | Detail |
|---|---|
| **Module** | Availability & Orders |
| **Purpose** | View assigned delivery details |
| **Accessible By** | Authenticated drivers |
| **User Stories** | US-DRV-005, US-DRV-006 |
| **PRD Section** | 6.13 |
| **Nav Entry Point** | From Dashboard or push notification |

**Layout:**
- Order # and time placed
- Items list with quantities and customizations
- Customer info (name, phone -- masked until accepted)
- Delivery address with map preview
- Special delivery instructions
- Distance and estimated time
- Accept/Decline buttons (for new assignments)
- "Navigate" button (for accepted orders)
- "Call Customer" and "Message Customer" buttons

**States:**
- New assignment (accept/decline visible)
- Accepted (navigate and contact visible)
- Picked up (navigation to customer active)
- Completed

**Navigates To:**
- Navigation (SCR-D-004) via "Navigate"
- Delivery Confirmation (SCR-D-005) on arrival
- Issue Report (SCR-D-006) via "Report Issue"
- Dashboard (SCR-D-002) on decline/complete

---

#### SCR-D-004: Navigation Screen

| Property | Detail |
|---|---|
| **Module** | Navigation & Delivery |
| **Purpose** | Turn-by-turn GPS navigation to customer |
| **Accessible By** | Authenticated drivers (active delivery) |
| **User Stories** | US-DRV-007 |
| **PRD Section** | 6.14 |
| **Nav Entry Point** | From Order Detail or Dashboard |

**Layout:**
- Full-screen Google Maps with turn-by-turn navigation overlay
- Route highlighted in blue
- Current location (blue dot)
- Destination pin
- Bottom card: ETA, distance remaining, customer name and address
- "Call Customer" quick action
- "End Navigation" button

**States:**
- Navigating (active turn-by-turn)
- Arrived (destination reached, prompt to confirm)
- GPS lost ("Reconnecting...")

**Interactions:**
- Tap bottom card to expand for full address/instructions
- Tap call button for customer contact

**Real-time:**
- Location shared every 10-15 seconds via Socket.io
- Route updates dynamically with Google Maps Directions API

**Navigates To:**
- Delivery Confirmation (SCR-D-005) on arrival
- Order Detail (SCR-D-003) via back

---

#### SCR-D-005: Delivery Confirmation Screen

| Property | Detail |
|---|---|
| **Module** | Navigation & Delivery |
| **Purpose** | Confirm order delivered to customer |
| **Accessible By** | Authenticated drivers (active delivery) |
| **User Stories** | US-DRV-008, US-DRV-009 |
| **PRD Section** | 6.14 |
| **Nav Entry Point** | From Navigation on arrival |

**Layout:**
- "Confirm Delivery" heading
- Order summary (order #, items count)
- Customer name
- "Did you collect cash?" (COD only, with amount field)
- "Confirm Delivery" button (large, primary)
- "Report Issue" button (secondary, if there's a problem)

**States:**
- Default
- COD input
- Confirming (loading)
- Confirmed (success animation, redirect to dashboard)
- Error

**Form Fields (COD):**
- Amount collected (number, required for COD, pre-filled with order total)

**Navigates To:**
- Dashboard (SCR-D-002) on confirmation
- Issue Report (SCR-D-006) via "Report Issue"

---

#### SCR-D-006: Issue Report Screen

| Property | Detail |
|---|---|
| **Module** | Communication & Reporting |
| **Purpose** | Report delivery problems |
| **Accessible By** | Authenticated drivers |
| **User Stories** | US-DRV-011 |
| **PRD Section** | 6.15 |
| **Nav Entry Point** | From delivery screens |

**Layout:**
- "Report an Issue" heading
- Order # reference
- Issue category selector (radio buttons or list):
  - Customer Unavailable
  - Wrong Address
  - Order Damaged
  - Cannot Access Location
  - Vehicle Problem
  - Other
- Notes field (textarea, optional, max 500 chars)
- Photo attachment button (camera or gallery)
- "Submit Report" button
- "Cancel" link

**States:**
- Default
- Uploading photo (progress)
- Submitting (loading)
- Submitted (confirmation message: "The restaurant has been notified")
- Error

**Navigates To:**
- Back to delivery screen on submit/cancel

---

#### SCR-D-007: Performance Screen

| Property | Detail |
|---|---|
| **Module** | Communication & Reporting |
| **Purpose** | View delivery statistics and ratings |
| **Accessible By** | Authenticated drivers |
| **User Stories** | US-DRV-012 |
| **PRD Section** | 6.15 |
| **Nav Entry Point** | From Dashboard drawer/menu |

**Layout:**
- Summary cards at top: Total Deliveries, Completion Rate, Average Rating
- Period selector (Today / This Week / This Month)
- Detailed stats: deliveries per day chart, average delivery time, on-time rate, customer ratings breakdown (5-star distribution)

**States:**
- Loading
- Loaded
- No data ("Complete your first delivery to see stats")

**Navigates To:**
- Dashboard (SCR-D-002) via back

---

#### SCR-D-008: Driver Profile Screen

| Property | Detail |
|---|---|
| **Module** | Authentication & Profile |
| **Purpose** | Manage driver profile and documents |
| **Accessible By** | Authenticated drivers |
| **User Stories** | US-DRV-002 |
| **PRD Section** | 6.12 |
| **Nav Entry Point** | From Dashboard drawer/menu |

**Layout:**
- Driver photo/avatar
- Name
- Phone
- Email
- Vehicle section (type, license plate)
- Documents section (list of uploaded docs with status badges: Approved, Pending, Expired)
- "Edit Profile" button
- "Upload Document" button
- "Change Password" section

**States:**
- Loaded
- Editing (form mode)
- Uploading document (progress bar)
- Error

**Form Fields:**
- Name (text, required)
- Phone (tel, required)
- Email (email, optional)
- Vehicle Type (dropdown: motorcycle, car, bicycle)
- License Plate (text, required)
- Document upload (file picker: camera, gallery, files; accepted: JPG, PNG, PDF; max 5MB)

**Navigates To:**
- Dashboard (SCR-D-002) via back

---

#### SCR-D-009: Support Screen

| Property | Detail |
|---|---|
| **Module** | Communication & Reporting |
| **Purpose** | Contact restaurant support |
| **Accessible By** | Authenticated drivers |
| **User Stories** | US-DRV-013 |
| **PRD Section** | 6.15 |
| **Nav Entry Point** | From Dashboard drawer/menu |

**Layout:**
- Simple chat-like interface
- Message bubbles (driver on right, restaurant on left)
- Text input field at bottom
- "Send" button

**States:**
- Loading messages
- Messages loaded
- Empty ("Need help? Send a message to the restaurant.")
- Error

**Real-time:**
- Socket.io for real-time message updates

**Navigates To:**
- Dashboard (SCR-D-002) via back

---

#### SCR-D-010: Driver Settings Screen

| Property | Detail |
|---|---|
| **Module** | Communication & Reporting |
| **Purpose** | App preferences |
| **Accessible By** | Authenticated drivers |
| **User Stories** | US-DRV-002 |
| **PRD Section** | 6.15 |
| **Nav Entry Point** | From Dashboard drawer/menu |

**Layout:**
- Language toggle (Arabic/English)
- Notification preferences
- GPS accuracy mode (High/Standard)
- About (app version)
- Logout button

**States:**
- Loaded
- Saving

**Navigates To:**
- Login (SCR-D-001) via Logout
- Dashboard (SCR-D-002) via back

---

## 3. Restaurant Dashboard Screens

### 3.1 Auth & Dashboard

---

#### SCR-R-001: Dashboard Login

| Property | Detail |
|---|---|
| **Module** | Dashboard & Auth |
| **Purpose** | Admin authentication |
| **Accessible By** | Unauthenticated admins |
| **User Stories** | US-REST-001 |
| **PRD Section** | 6.16 |
| **Nav Entry Point** | Dashboard URL |

**Layout:**
- Centered login card
- Restaurant logo above
- Email field (email, required)
- Password field (password, required, show/hide)
- "Login" button (primary)
- "Forgot Password?" link

**States:**
- Default
- Loading
- Error (invalid credentials)
- Locked (too many attempts -- 5 failures = 30-min lock)

**Navigates To:**
- Main Dashboard (SCR-R-002) on success

---

#### SCR-R-002: Main Dashboard

| Property | Detail |
|---|---|
| **Module** | Dashboard & Auth |
| **Purpose** | Business overview and KPIs |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-002 |
| **PRD Section** | 6.16 |
| **Nav Entry Point** | After login / sidebar: Dashboard |

**Layout:**
- Left sidebar navigation (persistent)
- Top bar with restaurant name, admin name, notifications bell, language toggle
- Main content area with:
  - KPI cards row (4-5 cards: Today's Orders, Today's Revenue, Active Orders, Available Drivers, Pending Issues -- with trend arrows)
  - Charts row (Revenue trend line chart, Order volume bar chart)
  - Top-selling items list
  - Recent activity feed
  - Quick action buttons (View Order Board, Manage Menu, Send Notification)

**Sidebar Items:**
Dashboard, Orders, Menu, Drivers, Customers, Promotions, Reports, Support, Settings

**States:**
- Loading (skeleton)
- Loaded
- Error (connection lost banner with retry)

**Real-time:**
- Socket.io for order count and driver status updates
- Charts refresh every 5 minutes

**Navigates To:**
- All sidebar destinations (SCR-R-003 through SCR-R-028)

---

### 3.2 Menu Management

---

#### SCR-R-003: Menu List Screen

| Property | Detail |
|---|---|
| **Module** | Menu Management |
| **Purpose** | View and manage all menu items |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-003, US-REST-007 |
| **PRD Section** | 6.17 |
| **Nav Entry Point** | Sidebar: Menu |

**Layout:**
- "Menu Management" heading
- Search bar
- Category filter dropdown
- Availability filter (All/Available/Unavailable)
- "Add New Item" button
- Items table: Image thumbnail, Name (AR/EN), Category, Price, Availability toggle, Actions (Edit, Delete)
- Bulk action toolbar (on selection)
- Pagination

**States:**
- Loading
- Items listed
- Empty ("No menu items yet. Add your first item!")
- Search no results

**Navigates To:**
- Menu Item Form (SCR-R-004) via "Add New" or Edit
- Category Manager (SCR-R-005)

---

#### SCR-R-004: Menu Item Form

| Property | Detail |
|---|---|
| **Module** | Menu Management |
| **Purpose** | Add or edit a menu item |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-003, US-REST-004, US-REST-005 |
| **PRD Section** | 6.17 |
| **Nav Entry Point** | From Menu List |

**Layout:**
Tabbed form with 4 tabs:

**Basic Info Tab:**
- Name AR (text, required)
- Name EN (text, required)
- Description AR (textarea)
- Description EN (textarea)
- Category (dropdown, required)
- Price (number, required, min 0.01)
- Availability toggle

**Variants Tab:**
- Variant groups list with "Add Group" button
- Each group: Group Name (AR/EN), Required toggle, Options list (name, price modifier, add/remove)

**Nutrition Tab:**
- Calories (number)
- Protein (number)
- Carbs (number)
- Fat (number)
- Allergy tags (multi-select checkboxes: Nuts, Dairy, Gluten, Eggs, Soy, Shellfish, Sesame)

**Images Tab:**
- Drag-and-drop upload area
- Image thumbnails with reorder and delete
- Max 5 images, max 5MB each, accepted: JPG, PNG, WebP

**States:**
- New item (empty form)
- Edit item (pre-filled)
- Saving (loading)
- Validation errors
- Image uploading

**Navigates To:**
- Back to Menu List (SCR-R-003) on save/cancel

---

#### SCR-R-005: Category Manager

| Property | Detail |
|---|---|
| **Module** | Menu Management |
| **Purpose** | Manage menu categories hierarchy |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-004 |
| **PRD Section** | 6.17 |
| **Nav Entry Point** | From Menu section |

**Layout:**
- Category tree (drag-and-drop sortable)
- Each row: Icon/image, Name (AR/EN), Item count, Actions (Edit, Delete)
- "Add Category" button
- Add/edit modal: Name AR (text, required), Name EN (text, required), Parent Category (dropdown, optional), Icon/Image upload, Display Order (number)

**States:**
- Loading
- Loaded
- Empty
- Drag in progress
- Delete confirmation modal

**Constraints:**
- Maximum 2-level hierarchy (category > subcategory)

**Navigates To:**
- Back to Menu List (SCR-R-003)

---

### 3.3 Order Processing

---

#### SCR-R-006: Order Board

| Property | Detail |
|---|---|
| **Module** | Order Processing |
| **Purpose** | Kanban board for real-time order management |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-008, US-REST-009 |
| **PRD Section** | 6.18 |
| **Nav Entry Point** | Sidebar: Orders |

**Layout:**
- Kanban board with drag-and-drop columns:
  - New (red highlight for urgency)
  - Preparing (yellow)
  - Ready (green)
  - Out for Delivery (blue)
  - Delivered (gray)
- Each order card: Order #, customer name, items count, total, time since placed, payment method badge (COD/Card)
- Sound toggle for alerts
- Filter by status, date, payment method
- Real-time badge count on sidebar "Orders" item

**States:**
- Loading
- Active orders displayed
- No orders ("No active orders right now")
- Connection lost ("Reconnecting...")

**Interactions:**
- Click card to open detail
- Drag card between columns (with validation)
- Double-click for quick accept

**Real-time:**
- Socket.io for new orders and status changes
- Audible alert on new orders (configurable)

**Navigates To:**
- Order Detail (SCR-R-007) via card click

---

#### SCR-R-007: Order Detail (Restaurant)

| Property | Detail |
|---|---|
| **Module** | Order Processing |
| **Purpose** | Full order view with management actions |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-009, US-REST-010, US-REST-011, US-REST-012 |
| **PRD Section** | 6.18 |
| **Nav Entry Point** | From Order Board |

**Layout:**
- Order # and timestamp
- Status badge
- Customer section (name, phone, email, address with map, delivery instructions)
- Items table (name, customizations, quantity, unit price, line total)
- Price breakdown (subtotal, discount, VAT, delivery fee, total)
- Payment method and status
- Driver assignment section (assigned driver or "Assign Driver" button)
- Status action buttons (Accept, Reject, Mark Ready, Cancel)
- Preparation time input
- Order timeline (all status changes with timestamps)

**States:**
- New order (accept/reject buttons)
- Accepted (preparation timer)
- Ready (assign driver)
- Out for delivery (driver tracking)
- Delivered (completed)
- Cancelled

**Navigates To:**
- Driver selection modal for assignment
- Back to Order Board (SCR-R-006)

---

### 3.4 Driver Management

---

#### SCR-R-008: Driver List

| Property | Detail |
|---|---|
| **Module** | Driver Management |
| **Purpose** | Manage driver accounts |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-013 |
| **PRD Section** | 6.19 |
| **Nav Entry Point** | Sidebar: Drivers |

**Layout:**
- "Driver Management" heading
- "Add Driver" button
- Search bar
- Drivers table: Name, Phone, Vehicle, Status (Online/Offline badge), Active Deliveries, Avg Rating, Actions (Edit, Deactivate/Activate)
- Filters: Status (All/Online/Offline)
- Pagination

**States:**
- Loading
- Drivers listed
- Empty ("No drivers registered. Add your first driver!")
- Search no results

**Navigates To:**
- Driver Form (SCR-R-009) via "Add Driver" or Edit
- Driver Map (SCR-R-010)
- Delivery Zones (SCR-R-011)

---

#### SCR-R-009: Driver Form

| Property | Detail |
|---|---|
| **Module** | Driver Management |
| **Purpose** | Add or edit driver account |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-013 |
| **PRD Section** | 6.19 |
| **Nav Entry Point** | From Driver List |

**Layout:**
- "Add/Edit Driver" heading
- Form fields:
  - Name (text, required)
  - Phone (tel, required)
  - Email (email, optional)
  - Vehicle Type (dropdown: Motorcycle, Car, Bicycle, required)
  - License Plate (text, required)
  - Password (password, required for new, optional for edit)
- "Save" and "Cancel" buttons

**States:**
- New (empty form)
- Edit (pre-filled)
- Saving
- Validation errors

**Navigates To:**
- Back to Driver List (SCR-R-008) on save/cancel

---

#### SCR-R-010: Driver Map

| Property | Detail |
|---|---|
| **Module** | Driver Management |
| **Purpose** | Real-time driver location tracking on map |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-015 |
| **PRD Section** | 6.19 |
| **Nav Entry Point** | From Drivers section |

**Layout:**
- Full-width Google Map showing all online drivers
- Driver pins with name tooltips
- Filter: Show All Drivers / Busy Drivers / Available Drivers
- Click pin for driver detail popup: name, phone, current order (if any), status
- Side panel option: list of drivers with live status

**States:**
- Loading map
- Map loaded with drivers
- No online drivers
- Connection lost

**Real-time:**
- Driver positions update every 10-15 seconds via Socket.io

**Navigates To:**
- Driver detail popup on pin click

---

#### SCR-R-011: Delivery Zones Screen

| Property | Detail |
|---|---|
| **Module** | Driver Management / Settings |
| **Purpose** | Define delivery coverage areas with zone-based fees |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-018 |
| **PRD Section** | 6.19, 6.20 |
| **Nav Entry Point** | From Drivers section or Settings |

**Layout:**
- Google Map with polygon drawing tools
- List of defined zones (name, fee, color on map)
- Edit zone: name, delivery fee (SAR), polygon coordinates
- Delete zone with confirmation

**States:**
- Loading
- Zones displayed
- No zones ("Define your first delivery zone")
- Drawing mode

**Navigates To:**
- Back to Driver List (SCR-R-008) or Settings (SCR-R-012)

---

### 3.5 Business Settings & Payments

---

#### SCR-R-012: Business Settings

| Property | Detail |
|---|---|
| **Module** | Business Settings & Configuration |
| **Purpose** | Configure operating parameters |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-017 through US-REST-021 |
| **PRD Section** | 6.20 |
| **Nav Entry Point** | Sidebar: Settings |

**Layout:**
Settings navigation tabs: General, Operating Hours, Order Settings, Tax, Payment

- **General:** Restaurant name, description, contact info
- **Operating Hours:** Weekly grid with time pickers per day, closed toggle, split-hours support
- **Order Settings:** Minimum order amount (number, SAR), default preparation time (number, minutes)
- **Tax:** VAT rate (number, %), VAT registration number (text)
- "Save" button per section

**States:**
- Loading
- Loaded
- Saving
- Saved (success toast)
- Validation errors

**Navigates To:**
- Delivery Zones (SCR-R-011) for zone configuration
- Branding (SCR-R-025), System (SCR-R-026), Notifications (SCR-R-027), Loyalty (SCR-R-028) via sub-navigation

---

#### SCR-R-013: Payment Records

| Property | Detail |
|---|---|
| **Module** | Business Settings & Configuration |
| **Purpose** | View financial transactions and reconciliation |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-022 |
| **PRD Section** | 6.20 |
| **Nav Entry Point** | From Settings |

**Layout:**
- "Payment Records" heading
- Date range filter
- Payment method filter
- Status filter (Completed, Pending, Failed, Refunded)
- Transactions table: Date, Order #, Amount, Method, Status, Actions (View, Refund for eligible)
- Export button (CSV/Excel)
- Summary cards: Total Revenue, Total Refunds, Net Revenue

**States:**
- Loading
- Transactions listed
- Empty
- Filtered no results
- Exporting

**Navigates To:**
- Order Detail (SCR-R-007) via Order # link

---

### 3.6 Marketing & Promotions

---

#### SCR-R-014: Promo Manager

| Property | Detail |
|---|---|
| **Module** | Marketing & Promotions |
| **Purpose** | Manage promotional codes |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-025 |
| **PRD Section** | 6.21 |
| **Nav Entry Point** | Sidebar: Promotions |

**Layout:**
- "Promotions" heading
- Tabs: Promo Codes / Push Notifications / Email Campaigns
- Promo codes list: Code, Type, Value, Usage (used/limit), Status (Active/Expired/Scheduled), Date range, Actions (Edit, Deactivate, Delete)
- "Create Promo" button
- Filters: Status, Date range

**States:**
- Loading
- Codes listed
- Empty
- Filtered no results

**Navigates To:**
- Promo Form (SCR-R-015) via "Create Promo" or Edit
- Push Notification Manager (SCR-R-016) via tab
- Email Campaign Manager (SCR-R-017) via tab

---

#### SCR-R-015: Promo Form

| Property | Detail |
|---|---|
| **Module** | Marketing & Promotions |
| **Purpose** | Create or edit a promotional code |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-025 |
| **PRD Section** | 6.21 |
| **Nav Entry Point** | From Promo Manager |

**Layout:**
- "Create/Edit Promotion" heading
- Code field (text, required, with "Auto-generate" button)
- Discount Type (radio: Percentage, Fixed Amount)
- Discount Value (number, required)
- Minimum Order (number, optional)
- Maximum Discount for percentage type (number, optional)
- Usage Limit (number, optional, 0=unlimited)
- Per-User Limit (number, default 1)
- Start Date (date picker, required)
- End Date (date picker, required)
- Target Audience (radio: All, New Customers, Segment)
- Applicable Items/Categories (multi-select, optional)
- "Save" and "Cancel" buttons

**States:**
- New
- Edit
- Saving
- Validation errors

**Navigates To:**
- Back to Promo Manager (SCR-R-014) on save/cancel

---

#### SCR-R-016: Push Notification Manager

| Property | Detail |
|---|---|
| **Module** | Marketing & Promotions |
| **Purpose** | Send push notification campaigns |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-026 |
| **PRD Section** | 6.21 |
| **Nav Entry Point** | From Promotions tab |

**Layout:**
- "Push Notifications" heading
- History list: Title, Audience size, Sent date, Delivery rate
- "New Notification" button
- Form: Title AR (text, required), Title EN (text, required), Body AR (textarea, required), Body EN (textarea, required), Image (upload, optional), Target (radio: All, Segment, Specific), Schedule (radio: Now, Later with datetime picker)
- Preview pane (mobile mockup)
- "Send" button with confirmation dialog

**States:**
- History loaded
- Empty
- Form open
- Previewing
- Sending
- Sent confirmation

**Navigates To:**
- Back to Promo Manager (SCR-R-014)

---

#### SCR-R-017: Email Campaign Manager

| Property | Detail |
|---|---|
| **Module** | Marketing & Promotions |
| **Purpose** | Send email marketing campaigns |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-027 |
| **PRD Section** | 6.21 |
| **Nav Entry Point** | From Promotions tab |

**Layout:**
- "Email Campaigns" heading
- History list: Subject, Audience, Sent date, Open rate
- "New Campaign" button
- Form: Subject AR (text, required), Subject EN (text, required), Body AR (rich text editor), Body EN (rich text editor), Target Audience, Schedule
- "Preview" and "Send" buttons

**States:**
- History loaded
- Empty
- Form open
- Previewing
- Sending
- Sent

**Navigates To:**
- Back to Promo Manager (SCR-R-014)

---

### 3.7 Reports & Analytics

---

#### SCR-R-018: Sales Reports

| Property | Detail |
|---|---|
| **Module** | Reporting & Analytics |
| **Purpose** | Sales and revenue analytics |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-028 |
| **PRD Section** | 6.22 |
| **Nav Entry Point** | Sidebar: Reports |

**Layout:**
- "Sales Reports" heading
- Date range selector (preset buttons + custom range picker)
- KPI cards: Total Revenue (SAR), Order Count, Avg Order Value, Top Payment Method
- Charts: Revenue trend (line), Order volume (bar), Revenue by payment (pie)
- Transactions table (sortable, filterable)
- Export buttons (CSV, PDF)
- VAT toggle (Include/Exclude VAT)

**States:**
- Loading
- Report loaded
- No data
- Exporting
- Export ready

**Navigates To:**
- Customer Analytics (SCR-R-019) / Popular Items (SCR-R-020) via sub-navigation

---

#### SCR-R-019: Customer Analytics

| Property | Detail |
|---|---|
| **Module** | Reporting & Analytics |
| **Purpose** | Customer behavior insights |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-029 |
| **PRD Section** | 6.22 |
| **Nav Entry Point** | From Reports section |

**Layout:**
- "Customer Analytics" heading
- Date range selector
- KPI cards: Total Customers, New (period), Returning Rate (%), Avg Lifetime Value
- Charts: New vs returning (stacked bar), Order frequency distribution (histogram), Top customers (table)
- Segment filters

**States:**
- Loading
- Loaded
- No data

**Navigates To:**
- Customer Detail (SCR-R-022) via top customers table

---

#### SCR-R-020: Popular Items

| Property | Detail |
|---|---|
| **Module** | Reporting & Analytics |
| **Purpose** | Menu item performance analysis |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-030 |
| **PRD Section** | 6.22 |
| **Nav Entry Point** | From Reports section |

**Layout:**
- "Popular Items" heading
- Date range selector
- Category filter
- Items ranking table: Rank, Item Name, Orders Count, Revenue, Trend arrow (up/down/stable)
- Chart: Top 10 items bar chart
- Period comparison toggle

**States:**
- Loading
- Loaded
- No data

**Navigates To:**
- Menu Item Form (SCR-R-004) via item click (to edit)

---

### 3.8 Customer & Support

---

#### SCR-R-021: Customer List

| Property | Detail |
|---|---|
| **Module** | Customer Support Management |
| **Purpose** | View all registered customers |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-024 |
| **PRD Section** | 6.23 |
| **Nav Entry Point** | Sidebar: Customers |

**Layout:**
- "Customers" heading
- Search bar (name, phone, email)
- Customer table: Name, Phone, Email, Registered Date, Total Orders, Total Spent, Last Order, Actions (View)
- Filters: Registration date range, order count range
- Pagination
- Export button

**States:**
- Loading
- Customers listed
- Empty
- Search no results

**Navigates To:**
- Customer Detail (SCR-R-022) via View

---

#### SCR-R-022: Customer Detail

| Property | Detail |
|---|---|
| **Module** | Customer Support Management |
| **Purpose** | Individual customer view with full history |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-024 |
| **PRD Section** | 6.23 |
| **Nav Entry Point** | From Customer List |

**Layout:**
- Customer profile card (name, phone, email, registration date, avatar)
- Tabs: Orders | Loyalty | Support | Addresses
- **Orders tab:** Order history table
- **Loyalty tab:** Points balance, transaction history
- **Support tab:** Related tickets
- **Addresses tab:** Saved addresses

**States:**
- Loading
- Loaded

**Navigates To:**
- Order Detail (SCR-R-007) via order click
- Ticket Detail (SCR-R-024) via ticket click
- Back to Customer List (SCR-R-021)

---

#### SCR-R-023: Support Tickets

| Property | Detail |
|---|---|
| **Module** | Customer Support Management |
| **Purpose** | Manage support requests |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-031 |
| **PRD Section** | 6.23 |
| **Nav Entry Point** | Sidebar: Support |

**Layout:**
- "Support" heading
- Ticket list: Ticket #, Customer Name, Subject, Status badge, Date, Priority
- Status filters (All/Open/In Progress/Resolved/Closed)
- Sort by date or priority
- "View" button per ticket

**States:**
- Loading
- Tickets listed
- Empty ("No support tickets")
- Filtered no results

**Navigates To:**
- Ticket Detail (SCR-R-024) via View

---

#### SCR-R-024: Ticket Detail

| Property | Detail |
|---|---|
| **Module** | Customer Support Management |
| **Purpose** | View and respond to a support ticket |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-031 |
| **PRD Section** | 6.23 |
| **Nav Entry Point** | From Support Tickets |

**Layout:**
- Ticket # and status badge
- Customer info card (name, phone, email)
- Order reference (if linked, clickable to order detail)
- Conversation thread (messages with timestamps, sender labels)
- Reply text area
- Status update dropdown (Open > In Progress > Resolved > Closed)
- "Send Reply" button
- "Close Ticket" button

**States:**
- Loading
- Loaded
- Replying (sending)
- Reply sent
- Closing

**Navigates To:**
- Order Detail (SCR-R-007) via order reference
- Back to Support Tickets (SCR-R-023)

---

### 3.9 Platform Configuration

---

#### SCR-R-025: Branding Configuration

| Property | Detail |
|---|---|
| **Module** | Platform Configuration & Branding |
| **Purpose** | Customize white-label branding |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-032 |
| **PRD Section** | 6.24 |
| **Nav Entry Point** | From Settings |

**Layout:**
- "Branding" heading
- Logo upload (preview, drag-and-drop)
- Favicon upload
- Splash image upload
- Color picker section: Primary (hex input + picker), Secondary (hex input + picker), Background (hex input + picker)
- App Name (text, max 30 chars)
- Tagline (text, max 60 chars)
- Live preview panel (shows a mockup of the app with current settings)
- "Save" button

**States:**
- Loading
- Loaded
- Saving
- Saved (success)
- Validation errors

**Constraints:**
- Logo: Max 2MB, accepted: PNG, SVG
- App Name: Max 30 characters

**Navigates To:**
- Back to Settings

---

#### SCR-R-026: System Settings

| Property | Detail |
|---|---|
| **Module** | Platform Configuration & Branding |
| **Purpose** | System-level configuration |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-033 |
| **PRD Section** | 6.24 |
| **Nav Entry Point** | From Settings |

**Layout:**
- "System Settings" heading
- Sections:
  - General (time zone, currency, date format)
  - Integrations (API keys display -- masked, connection status badges for Google Maps, Stripe, Firebase)
  - Maintenance Mode toggle (shows "Under maintenance" to customers)
- "Save" button per section

**States:**
- Loading
- Loaded
- Saving
- Saved

**Navigates To:**
- Back to Settings

---

#### SCR-R-027: Notification Settings

| Property | Detail |
|---|---|
| **Module** | Platform Configuration & Branding |
| **Purpose** | Configure admin alert preferences |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-033 |
| **PRD Section** | 6.24 |
| **Nav Entry Point** | From Settings |

**Layout:**
- "Notification Preferences" heading
- Event types table: Event Name, Dashboard Alert (toggle), Email (toggle), SMS (toggle)
- Rows: New Order, Order Cancellation, Low Stock Alert, New Support Ticket, New Customer Registration, Driver Issue Report
- Sound selection dropdown for dashboard alerts
- "Save" button

**States:**
- Loading
- Loaded
- Saving
- Saved

**Navigates To:**
- Back to Settings

---

#### SCR-R-028: Loyalty Configuration

| Property | Detail |
|---|---|
| **Module** | Platform Configuration & Branding |
| **Purpose** | Configure loyalty program rules |
| **Accessible By** | Authenticated admins |
| **User Stories** | US-REST-033, US-CUST-MISC-009 |
| **PRD Section** | 6.24 |
| **Nav Entry Point** | From Settings |

**Layout:**
- "Loyalty Program" heading
- Enable/Disable toggle (prominent)
- If enabled:
  - Points per SAR (number, e.g., "1 point per X SAR spent")
  - Redemption rate (number, e.g., "X points = 1 SAR discount")
  - Minimum points to redeem (number)
  - Maximum redemption per order (% slider)
  - Points expiry (months, or "Never")
- Program summary text (auto-generated from settings)
- "Save" button

**States:**
- Loading
- Loaded
- Saving
- Saved
- Disabled (grayed out fields)

**Navigates To:**
- Back to Settings

---

## 4. Navigation Structure

### Customer App (Android + Web) -- Bottom Tab Navigation

```
Customer App
|
+-- Splash Screen (SCR-C-001)
+-- Onboarding (SCR-C-002) [first launch only]
+-- Login / Register
|   +-- Login (SCR-C-003)
|   +-- OTP Verification (SCR-C-004)
|   +-- Register (SCR-C-005)
|
+-- Main App (Bottom Tab Navigation)
|   +-- Home Tab
|   |   +-- Home (SCR-C-006)
|   |   +-- Menu Category (SCR-C-007)
|   |   +-- Search (SCR-C-008)
|   |   +-- Product Detail (SCR-C-009)
|   |   +-- Branch Map (SCR-C-026)
|   |
|   +-- Offers Tab
|   |   +-- Offers (SCR-C-019)
|   |
|   +-- Cart Tab
|   |   +-- Cart (SCR-C-010)
|   |   +-- Checkout (SCR-C-011)
|   |   +-- Payment (SCR-C-013) [within checkout]
|   |   +-- Order Confirmation (SCR-C-012)
|   |
|   +-- Orders Tab
|   |   +-- Order History (SCR-C-015)
|   |   +-- Order Detail (SCR-C-016)
|   |   +-- Receipt (SCR-C-017)
|   |   +-- Ratings (SCR-C-018)
|   |   +-- Order Tracking (SCR-C-014) [active orders]
|   |
|   +-- Profile Tab
|       +-- Profile (SCR-C-022)
|       +-- Settings (SCR-C-023)
|       +-- Notifications (SCR-C-024)
|       +-- Address List (SCR-C-020)
|       +-- Address Add/Edit (SCR-C-021)
|       +-- Favorites (SCR-C-027)
|       +-- Loyalty (SCR-C-025)
|       +-- Language (SCR-C-028) [within settings]
```

### Driver App (Android) -- Drawer/Tab Navigation

```
Driver App
|
+-- Login (SCR-D-001)
|
+-- Main App (Drawer/Tab Navigation)
|   +-- Home / Dashboard (SCR-D-002)
|   +-- Order Detail (SCR-D-003)
|   +-- Navigation (SCR-D-004)
|   +-- Delivery Confirmation (SCR-D-005)
|   +-- Issue Report (SCR-D-006)
|   +-- Performance (SCR-D-007)
|   +-- Profile (SCR-D-008)
|   +-- Support (SCR-D-009)
|   +-- Settings (SCR-D-010)
```

### Restaurant Dashboard (Web) -- Left Sidebar Navigation

```
Restaurant Dashboard
|
+-- Login (SCR-R-001)
|
+-- Main Dashboard (Left Sidebar Navigation)
|   +-- Dashboard Home (SCR-R-002)
|   |
|   +-- Orders
|   |   +-- Order Board (SCR-R-006)
|   |   +-- Order Detail (SCR-R-007)
|   |
|   +-- Menu
|   |   +-- Menu List (SCR-R-003)
|   |   +-- Menu Item Form (SCR-R-004)
|   |   +-- Category Manager (SCR-R-005)
|   |
|   +-- Drivers
|   |   +-- Driver List (SCR-R-008)
|   |   +-- Driver Form (SCR-R-009)
|   |   +-- Driver Map (SCR-R-010)
|   |   +-- Delivery Zones (SCR-R-011)
|   |
|   +-- Customers
|   |   +-- Customer List (SCR-R-021)
|   |   +-- Customer Detail (SCR-R-022)
|   |
|   +-- Promotions
|   |   +-- Promo Manager (SCR-R-014)
|   |   +-- Promo Form (SCR-R-015)
|   |   +-- Push Notification Manager (SCR-R-016)
|   |   +-- Email Campaign Manager (SCR-R-017)
|   |
|   +-- Reports
|   |   +-- Sales Reports (SCR-R-018)
|   |   +-- Customer Analytics (SCR-R-019)
|   |   +-- Popular Items (SCR-R-020)
|   |
|   +-- Support
|   |   +-- Support Tickets (SCR-R-023)
|   |   +-- Ticket Detail (SCR-R-024)
|   |
|   +-- Settings
|       +-- Business Settings (SCR-R-012)
|       +-- Payment Records (SCR-R-013)
|       +-- Branding Config (SCR-R-025)
|       +-- System Settings (SCR-R-026)
|       +-- Notification Settings (SCR-R-027)
|       +-- Loyalty Config (SCR-R-028)
```

---

## 5. Screen-to-Feature Mapping

### Customer App Feature Coverage

| Feature | Screens | FR Reference |
|---|---|---|
| Guest Browsing | SCR-C-006, SCR-C-007, SCR-C-008, SCR-C-009 | FR-001 |
| Registration & Auth | SCR-C-003, SCR-C-004, SCR-C-005 | FR-002 to FR-006 |
| Menu Browse & Search | SCR-C-006, SCR-C-007, SCR-C-008 | FR-007 to FR-012 |
| Product Detail & Customize | SCR-C-009 | FR-013, FR-014, FR-015 |
| Favorites | SCR-C-009, SCR-C-027 | FR-015 |
| Cart Management | SCR-C-010 | FR-016 to FR-020 |
| Delivery/Pickup Options | SCR-C-011, SCR-C-026 | FR-021 to FR-025 |
| Address Management | SCR-C-020, SCR-C-021 | FR-026 to FR-028 |
| Checkout | SCR-C-011, SCR-C-012 | FR-029, FR-030 |
| Payment Processing | SCR-C-013 | FR-031 to FR-037 |
| Order Tracking | SCR-C-014 | FR-038 to FR-041 |
| Notifications | SCR-C-024 | FR-042 to FR-045 |
| Order History | SCR-C-015, SCR-C-016 | FR-046, FR-047 |
| Receipts | SCR-C-017 | FR-048 |
| Ratings & Reviews | SCR-C-018 | FR-049 |
| Offers & Promos | SCR-C-019 | FR-050 to FR-052 |
| Multi-Language | SCR-C-028 | FR-053 to FR-055 |
| Loyalty | SCR-C-025 | FR-056 |
| Profile & Settings | SCR-C-022, SCR-C-023 | General |

### Driver App Feature Coverage

| Feature | Screens | FR Reference |
|---|---|---|
| Driver Auth | SCR-D-001 | FR-057 |
| Profile & Documents | SCR-D-008 | FR-058, FR-059 |
| Availability & Shifts | SCR-D-002 | FR-060, FR-061 |
| Order Viewing | SCR-D-003 | FR-062 |
| Accept/Decline | SCR-D-002, SCR-D-003 | FR-063, FR-064 |
| GPS Navigation | SCR-D-004 | FR-065 |
| Real-time Location | SCR-D-004 | FR-066 |
| Delivery Confirmation | SCR-D-005 | FR-067 |
| Customer Communication | SCR-D-003, SCR-D-004 | FR-068, FR-069 |
| Issue Reporting | SCR-D-006 | FR-070 |
| Performance Stats | SCR-D-007 | FR-071 |
| Restaurant Support | SCR-D-009 | FR-072 |
| Settings | SCR-D-010 | General |

### Restaurant Dashboard Feature Coverage

| Feature | Screens | FR Reference |
|---|---|---|
| Admin Auth | SCR-R-001 | FR-073 |
| Dashboard Overview | SCR-R-002 | FR-074 |
| Menu CRUD | SCR-R-003, SCR-R-004 | FR-075 to FR-078 |
| Category Management | SCR-R-005 | FR-079 |
| Variant Configuration | SCR-R-004 | FR-080 |
| Pricing | SCR-R-004 | FR-081 |
| Availability Control | SCR-R-003 | FR-082, FR-083 |
| Order Reception | SCR-R-006 | FR-084 |
| Order Processing | SCR-R-006, SCR-R-007 | FR-085 to FR-088 |
| Driver Management | SCR-R-008, SCR-R-009 | FR-089 |
| Driver Assignment | SCR-R-007 | FR-090 |
| Driver Tracking | SCR-R-010 | FR-091 |
| Delivery Zones | SCR-R-011 | FR-092, FR-093 |
| Business Config | SCR-R-012 | FR-092, FR-094 |
| Payment Records | SCR-R-013 | FR-095 |
| Promo Engine | SCR-R-014, SCR-R-015 | FR-025 (promos) |
| Push Notifications | SCR-R-016 | FR-026 (push) |
| Email Marketing | SCR-R-017 | FR-027 (email) |
| Sales Reports | SCR-R-018 | FR-028 (reports) |
| Customer Analytics | SCR-R-019 | FR-029 (analytics) |
| Popular Items | SCR-R-020 | FR-030 (analysis) |
| Customer Database | SCR-R-021, SCR-R-022 | FR-096 |
| Support Tickets | SCR-R-023, SCR-R-024 | FR-096 (support) |
| Branding | SCR-R-025 | White-label config |
| System Settings | SCR-R-026, SCR-R-027 | System config |
| Loyalty Config | SCR-R-028 | FR-056 (loyalty rules) |

---

## 6. Screen State Summary

### Total Screen Count by Module

| Module | Customer | Driver | Restaurant | Total |
|---|---|---|---|---|
| Authentication | 5 | 1 | 1 | **7** |
| Menu/Discovery | 4 | -- | 3 | **7** |
| Cart/Checkout | 4 | -- | -- | **4** |
| Order Tracking | 1 | -- | -- | **1** |
| Order History | 4 | -- | -- | **4** |
| Order Processing | -- | 2 | 2 | **4** |
| Delivery/Navigation | -- | 2 | -- | **2** |
| Offers/Promos | 1 | -- | 4 | **5** |
| Address Management | 2 | -- | -- | **2** |
| Profile/Settings | 4 | 3 | -- | **7** |
| Driver Management | -- | -- | 4 | **4** |
| Reports/Analytics | -- | 1 | 3 | **4** |
| Customer/Support | -- | 1 | 4 | **5** |
| Platform Config | 1 | -- | 4 | **5** |
| Communication | -- | 1 | -- | **1** |
| Loyalty | 1 | -- | 1 | **2** |
| Branch/Map | 1 | -- | -- | **1** |
| Favorites | 1 | -- | -- | **1** |
| Payment | 1 | -- | 1 | **2** |
| **Total** | **28** | **10** | **28** | **66** |

### Screens Requiring Real-Time (Socket.io)

| Screen ID | Screen Name | Real-time Feature |
|---|---|---|
| SCR-C-014 | Order Tracking | Order status + driver GPS location |
| SCR-D-002 | Driver Dashboard | New order assignments |
| SCR-D-004 | Navigation | Location sharing (emit) |
| SCR-D-009 | Driver Support | Chat messages |
| SCR-R-002 | Main Dashboard | Order counts, driver status |
| SCR-R-006 | Order Board | New orders, status changes |
| SCR-R-010 | Driver Map | Driver location pins |

### Screens Requiring Google Maps Integration

| Screen ID | Screen Name | Maps Feature |
|---|---|---|
| SCR-C-014 | Order Tracking | Driver location on map, route |
| SCR-C-021 | Address Add/Edit | Pin-drop, reverse geocoding |
| SCR-C-026 | Branch Map | Branch location pins |
| SCR-D-004 | Navigation | Turn-by-turn navigation |
| SCR-R-010 | Driver Map | Real-time driver positions |
| SCR-R-011 | Delivery Zones | Polygon drawing, zone display |

### Screens Requiring Payment Integration (Stripe)

| Screen ID | Screen Name | Payment Feature |
|---|---|---|
| SCR-C-013 | Payment Method Selection | Card input (Stripe Elements), Google Pay, Mada, STC Pay |
| SCR-R-013 | Payment Records | Transaction records, refund processing |

---

*Last Updated: March 2026*
*Source: PRD.md Sections 6.1-6.24 and Section 7*
*Total: 66 screens across 3 applications*
