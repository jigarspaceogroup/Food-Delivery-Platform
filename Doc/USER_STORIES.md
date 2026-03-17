# User Stories Document

## Food Delivery Platform - White-Label Solution

| Field | Detail |
|---|---|
| **Project Name** | Food Delivery Platform |
| **Document Type** | User Stories (Product Backlog) |
| **Source Document** | PROJECT_SCOPE.md v1.1 |
| **Total Stories** | 120 |
| **Document Version** | v1.0 |
| **Date** | March 2026 |

---

## Personas

| Persona | Description |
|---|---|
| **Customer (Guest)** | An unregistered user browsing the restaurant menu on the Android app or web interface |
| **Customer (Registered)** | A registered user who can place orders, track deliveries, and manage their account |
| **Driver** | A delivery driver using the Android app to manage assigned deliveries |
| **Restaurant Admin** | A restaurant owner or manager using the web dashboard to manage operations |
| **Restaurant Marketing Manager** | A restaurant staff member focused on promotions, campaigns, and customer engagement |

---

## Priority Definitions

| Priority | Definition |
|---|---|
| **P0** | Must-have for MVP launch. Blocking if missing. |
| **P1** | Important for MVP. Should be included but launch is possible without it. |
| **P2** | Nice-to-have. Can be deferred to a post-launch sprint if needed. |

---

## Screen Reference Prefixes

| Prefix | Application |
|---|---|
| **SCR-C-** | Customer App (Android + Web) |
| **SCR-D-** | Driver App (Android) |
| **SCR-R-** | Restaurant Web Dashboard |

---

## Table of Contents

1. [Customer - Authentication](#1-customer---authentication-fr-001-to-fr-007)
2. [Customer - Menu and Search](#2-customer---menu-and-search-fr-008-to-fr-015)
3. [Customer - Cart and Checkout](#3-customer---cart-and-checkout-fr-016-to-fr-026)
4. [Customer - Payment](#4-customer---payment-fr-027-to-fr-033)
5. [Customer - Order Tracking and History](#5-customer---order-tracking-and-history-fr-034-to-fr-041)
6. [Customer - Offers, Addresses and Settings](#6-customer---offers-addresses-and-settings-fr-042-to-fr-050)
7. [Driver App](#7-driver-app-fr-051-to-fr-063)
8. [Restaurant Dashboard](#8-restaurant-dashboard-fr-064-to-fr-096)
9. [Cross-Cutting Stories](#9-cross-cutting-stories)

---

## 1. Customer - Authentication (FR-001 to FR-007)

### US-CUST-AUTH-001: Guest Menu Browsing
**As a** guest user, **I want to** browse the full restaurant menu, view item details, and see prices without creating an account, **so that** I can evaluate the restaurant offerings before committing to registration.

**Priority:** P0
**Scope Req:** FR-001
**Screens:** SCR-C-001 (Home), SCR-C-002 (Menu), SCR-C-003 (Item Detail)

**Acceptance Criteria:**
- **Given** a user opens the app for the first time without an account, **When** the app loads, **Then** the full menu with categories, items, images, descriptions, and prices is displayed without any login prompt or registration wall.
- **Given** a guest user is browsing the menu, **When** they tap on a menu item, **Then** the full product detail page is shown including images, description, pricing, nutrition info, and customization options.
- **Given** a guest user attempts to add an item to the cart or proceed to checkout, **When** they tap "Add to Cart" or "Checkout", **Then** a registration/login prompt is displayed with options for OTP, social login, and phone/email registration.

---

### US-CUST-AUTH-002: OTP Registration
**As a** new user, **I want to** register using SMS or email OTP verification, **so that** I can create a secure account quickly with minimal effort.

**Priority:** P0
**Scope Req:** FR-002
**Screens:** SCR-C-004 (Registration), SCR-C-005 (OTP Verification)

**Acceptance Criteria:**
- **Given** a user selects OTP registration and enters their phone number or email, **When** they tap "Send OTP", **Then** an OTP is sent within 60 seconds and the verification input screen is displayed.
- **Given** a user receives an OTP, **When** they enter the correct code within the timeout window, **Then** their account is created and they are logged in automatically.
- **Given** a user enters an incorrect OTP, **When** they submit the code, **Then** an error message is displayed and they can retry. After the OTP expires, a "Resend OTP" option becomes available.

---

### US-CUST-AUTH-003: Social Login with Google
**As a** new or returning user, **I want to** sign in using my Google account, **so that** I can register or log in with a single tap without creating a new password.

**Priority:** P1
**Scope Req:** FR-003
**Screens:** SCR-C-004 (Registration), SCR-C-006 (Login)

**Acceptance Criteria:**
- **Given** a user is on the registration or login screen, **When** they tap the "Continue with Google" button, **Then** the Google OAuth flow is initiated and the user can select their Google account.
- **Given** a user completes Google authentication for the first time, **When** the OAuth flow succeeds, **Then** a new account is created using the Google profile data (name, email) and the user is logged in.
- **Given** a returning user taps "Continue with Google", **When** the OAuth flow succeeds and an account already exists for that Google identity, **Then** the user is logged into their existing account with all previous data intact.

---

### US-CUST-AUTH-004: Social Login with Facebook
**As a** new or returning user, **I want to** sign in using my Facebook account, **so that** I can register or log in conveniently using an existing social account.

**Priority:** P1
**Scope Req:** FR-003
**Screens:** SCR-C-004 (Registration), SCR-C-006 (Login)

**Acceptance Criteria:**
- **Given** a user is on the registration or login screen, **When** they tap the "Continue with Facebook" button, **Then** the Facebook OAuth flow is initiated and the user can authorize the application.
- **Given** a user completes Facebook authentication for the first time, **When** the OAuth flow succeeds, **Then** a new account is created using the Facebook profile data (name, email) and the user is logged in.
- **Given** a returning user taps "Continue with Facebook", **When** the OAuth flow succeeds and an account already exists for that Facebook identity, **Then** the user is logged into their existing account with all previous data intact.

---

### US-CUST-AUTH-005: Phone or Email Registration
**As a** new user, **I want to** register with my phone number or email address as an alternative to OTP or social login, **so that** I have a traditional registration option if I prefer.

**Priority:** P0
**Scope Req:** FR-004
**Screens:** SCR-C-004 (Registration)

**Acceptance Criteria:**
- **Given** a user is on the registration screen, **When** they choose to register with phone or email, **Then** a form is displayed requesting phone/email, name, and password with clear validation messages.
- **Given** a user fills in valid registration details, **When** they submit the form, **Then** a verification step (email link or SMS code) is initiated to confirm the contact information.
- **Given** a user completes verification, **When** the verification succeeds, **Then** the account is created, the user is logged in, and redirected to the home screen or their previous browsing context.

---

### US-CUST-AUTH-006: Minimized Signup Flow
**As a** new user, **I want to** complete registration with the fewest possible form fields, **so that** I experience minimal friction and can start ordering quickly.

**Priority:** P0
**Scope Req:** FR-005
**Screens:** SCR-C-004 (Registration)

**Acceptance Criteria:**
- **Given** a user initiates registration, **When** the signup form is displayed, **Then** only essential fields are required (name, phone or email, verification) with all other profile data deferred to later.
- **Given** a user completes the minimal signup, **When** they submit the form, **Then** they are immediately logged in and can proceed to place orders without completing additional profile fields.
- **Given** a user registered with minimal fields, **When** they navigate to their profile later, **Then** they can optionally complete additional information such as delivery address, dietary preferences, and payment methods.

---

### US-CUST-AUTH-007: Arabic-Friendly Registration Interface
**As a** Saudi Arabian user, **I want to** complete the entire registration flow in Arabic with proper RTL layout, **so that** I can register comfortably in my native language.

**Priority:** P0
**Scope Req:** FR-006
**Screens:** SCR-C-004 (Registration), SCR-C-005 (OTP Verification), SCR-C-006 (Login)

**Acceptance Criteria:**
- **Given** a user has their device language set to Arabic or has selected Arabic in the app, **When** they open any registration or login screen, **Then** all labels, buttons, placeholders, error messages, and instructions are displayed in Arabic with correct RTL text alignment.
- **Given** a user is viewing the registration form in Arabic, **When** they interact with form fields, **Then** the layout is right-to-left with form labels aligned to the right, input fields flowing correctly, and navigation elements positioned according to RTL conventions.
- **Given** a user encounters a validation error during Arabic registration, **When** the error is displayed, **Then** the error message is in Arabic, grammatically correct, and positioned appropriately within the RTL layout.

---

### US-CUST-AUTH-008: Profile Completion
**As a** registered user, **I want to** complete my profile by adding delivery addresses via map pin-drop, payment preferences, and dietary restrictions, **so that** I have a personalized experience and faster checkout in the future.

**Priority:** P1
**Scope Req:** FR-007
**Screens:** SCR-C-007 (Profile), SCR-C-008 (Address Management), SCR-C-009 (Payment Preferences)

**Acceptance Criteria:**
- **Given** a registered user navigates to their profile, **When** the profile screen loads, **Then** sections for personal info, delivery addresses, payment methods, and dietary restrictions are displayed with clear edit capabilities.
- **Given** a user wants to add a delivery address, **When** they tap "Add Address", **Then** a map interface with pin-drop functionality is displayed allowing them to select a precise location, add a label (Home, Work, etc.), and save the address.
- **Given** a user sets dietary restrictions (e.g., vegetarian, gluten-free, halal), **When** they save their preferences, **Then** the preferences are stored and can be used for menu filtering and item recommendations.

---

## 2. Customer - Menu and Search (FR-008 to FR-015)

### US-CUST-MENU-001: Category Browsing
**As a** customer, **I want to** browse the restaurant menu organized by categories and subcategories, **so that** I can quickly find the type of food I am looking for.

**Priority:** P0
**Scope Req:** FR-008
**Screens:** SCR-C-002 (Menu), SCR-C-010 (Category View)

**Acceptance Criteria:**
- **Given** a customer opens the menu screen, **When** the menu loads, **Then** all top-level categories (e.g., Appetizers, Main Course, Beverages, Desserts) are displayed with icons or images.
- **Given** a customer taps on a top-level category, **When** the category has subcategories, **Then** the subcategories are displayed and the customer can drill down further to view items within each subcategory.
- **Given** a customer is browsing a category, **When** items are displayed, **Then** each item shows its name, thumbnail image, price, and a brief description with a clear option to view full details.

---

### US-CUST-MENU-002: Advanced Search with Auto-Suggest
**As a** customer, **I want to** search the menu with auto-suggest functionality, **so that** I can find specific items quickly without browsing through categories.

**Priority:** P0
**Scope Req:** FR-009
**Screens:** SCR-C-011 (Search), SCR-C-002 (Menu)

**Acceptance Criteria:**
- **Given** a customer taps the search bar on the menu screen, **When** they begin typing after entering 2 or more characters, **Then** auto-suggest results appear in real time showing matching menu items, categories, and ingredients.
- **Given** a customer types a search query, **When** they submit the search, **Then** relevant results are returned within 2 seconds, ranked by relevance, and display item name, image, price, and category.
- **Given** a customer searches for a term with no matching results, **When** the search completes, **Then** a "No results found" message is displayed along with suggestions for popular items or alternative search terms.

---

### US-CUST-MENU-003: Menu Filtering
**As a** customer, **I want to** filter menu items by price range, availability, and dietary preferences, **so that** I can narrow down the menu to items that match my criteria.

**Priority:** P1
**Scope Req:** FR-010
**Screens:** SCR-C-012 (Filter Panel), SCR-C-002 (Menu)

**Acceptance Criteria:**
- **Given** a customer is viewing the menu or search results, **When** they tap the filter icon, **Then** a filter panel is displayed with options for price range (slider or input), availability status, and dietary preferences (e.g., vegetarian, vegan, gluten-free, halal).
- **Given** a customer applies one or more filters, **When** they confirm the filter selection, **Then** the menu items are immediately filtered to show only items matching all selected criteria, with a count of matching items displayed.
- **Given** a customer has active filters applied, **When** they view the menu, **Then** active filter indicators are visible (e.g., chips or badges) and each can be individually removed to reset that specific filter.

---

### US-CUST-MENU-004: Menu Sorting
**As a** customer, **I want to** sort menu items by different criteria such as price, popularity, and name, **so that** I can organize the menu view according to my preference.

**Priority:** P1
**Scope Req:** FR-011
**Screens:** SCR-C-002 (Menu)

**Acceptance Criteria:**
- **Given** a customer is viewing menu items in a category or search results, **When** they tap the sort control, **Then** sorting options are displayed including: Price (low to high), Price (high to low), Popularity, Name (A-Z / Arabic equivalent), and Newest.
- **Given** a customer selects a sort option, **When** the sort is applied, **Then** the menu items are reordered immediately according to the selected criterion and the active sort is indicated in the UI.
- **Given** a customer has both filters and sorting active, **When** items are displayed, **Then** the items are filtered first and then sorted within the filtered results, ensuring both filter and sort work together correctly.

---

### US-CUST-MENU-005: Popular Items Section
**As a** customer, **I want to** see a dedicated section for popular and trending menu items, **so that** I can discover what other customers are ordering and make quick decisions.

**Priority:** P1
**Scope Req:** FR-012
**Screens:** SCR-C-001 (Home), SCR-C-002 (Menu)

**Acceptance Criteria:**
- **Given** a customer opens the home screen or menu, **When** the page loads, **Then** a "Popular Items" or "Trending Now" section is prominently displayed showing the most-ordered items with images, names, prices, and order counts or ratings.
- **Given** the popular items section is displayed, **When** the customer taps on a popular item, **Then** the full product detail page for that item is opened.
- **Given** the restaurant has recently updated their menu, **When** the popular items section loads, **Then** the items reflect actual ordering data and are dynamically updated based on recent order frequency.

---

### US-CUST-MENU-006: Product Detail View
**As a** customer, **I want to** view a detailed product page with images, descriptions, pricing, and nutrition/allergy information, **so that** I can make an informed decision before adding the item to my cart.

**Priority:** P0
**Scope Req:** FR-013
**Screens:** SCR-C-003 (Item Detail)

**Acceptance Criteria:**
- **Given** a customer taps on a menu item from any listing, **When** the product detail page loads, **Then** it displays high-quality images (with swipe gallery if multiple), item name, full description, price, and available customization options.
- **Given** a product has nutrition and allergy information configured, **When** the detail page is viewed, **Then** the nutrition data (calories, macros) and allergen warnings (nuts, dairy, gluten, etc.) are clearly displayed in a dedicated section.
- **Given** a customer is viewing a product detail page, **When** they scroll through the page, **Then** an "Add to Cart" button remains visible (sticky at the bottom) with the current price reflecting any selected customizations.

---

### US-CUST-MENU-007: Item Customization
**As a** customer, **I want to** customize menu items by selecting size, toppings, spice level, and adding special instructions using clear icons and toggles, **so that** I can personalize my order to my preferences.

**Priority:** P0
**Scope Req:** FR-014
**Screens:** SCR-C-003 (Item Detail), SCR-C-013 (Customization Panel)

**Acceptance Criteria:**
- **Given** a customer is on a product detail page for a customizable item, **When** the customization options load, **Then** each option group (size, toppings, spice level, extras) is displayed with clear icons, toggles, or radio buttons with individual pricing for each option.
- **Given** a customer selects customization options, **When** they toggle or select an option, **Then** the total price updates in real time to reflect the cost of all selected customizations.
- **Given** a customer wants to add special instructions, **When** they tap the "Special Instructions" field, **Then** a free-text input is available where they can type custom requests (e.g., "extra sauce on the side", "no onions") with a reasonable character limit.

---

### US-CUST-MENU-008: Save Favorite Items
**As a** registered customer, **I want to** save menu items as favorites for quick access, **so that** I can easily reorder items I enjoy without searching for them again.

**Priority:** P1
**Scope Req:** FR-015
**Screens:** SCR-C-003 (Item Detail), SCR-C-014 (Favorites)

**Acceptance Criteria:**
- **Given** a registered customer is viewing a menu item, **When** they tap the heart/favorite icon, **Then** the item is added to their favorites list and the icon state changes to indicate it is saved.
- **Given** a customer has saved favorite items, **When** they navigate to the Favorites section in the app, **Then** all favorited items are displayed in a list with images, names, prices, and a direct "Add to Cart" option.
- **Given** a customer wants to remove a favorite, **When** they tap the favorite icon on an already-favorited item, **Then** the item is removed from their favorites and the icon reverts to its default state.

---

## 3. Customer - Cart and Checkout (FR-016 to FR-026)

### US-CUST-CART-001: Cart Management
**As a** customer, **I want to** add, remove, and edit items in my cart with inline quantity controls, **so that** I can easily manage my order before checkout.

**Priority:** P0
**Scope Req:** FR-016
**Screens:** SCR-C-015 (Cart)

**Acceptance Criteria:**
- **Given** a customer adds an item from the menu, **When** they tap "Add to Cart", **Then** the item (with selected customizations) is added to the cart and a cart badge updates to show the total number of items.
- **Given** a customer is viewing the cart, **When** they adjust the quantity using inline plus/minus controls, **Then** the item quantity updates immediately and the cart subtotal, VAT, and total recalculate in real time.
- **Given** a customer wants to remove an item from the cart, **When** they tap the remove/delete button or reduce quantity to zero, **Then** the item is removed from the cart with a brief undo option, and all totals are recalculated.

---

### US-CUST-CART-002: Promo Code Application
**As a** customer, **I want to** apply a promotional or discount code to my cart, **so that** I can receive the associated discount on my order.

**Priority:** P0
**Scope Req:** FR-017
**Screens:** SCR-C-015 (Cart), SCR-C-016 (Checkout)

**Acceptance Criteria:**
- **Given** a customer is viewing the cart or checkout screen, **When** they tap the "Apply Promo Code" field and enter a valid code, **Then** the discount is applied and the order summary updates to show the discount amount and the new total.
- **Given** a customer enters an invalid or expired promo code, **When** they submit the code, **Then** a clear error message is displayed explaining why the code cannot be applied (e.g., "Code expired", "Minimum order not met", "Invalid code").
- **Given** a customer has successfully applied a promo code, **When** they view the order summary, **Then** the promo code name and discount amount are displayed as a line item in the fee breakdown, and a "Remove" option is available to unapply it.

---

### US-CUST-CART-003: VAT Display in Cart
**As a** customer, **I want to** see VAT calculations displayed upfront in my cart totals, **so that** I know the exact tax amount before proceeding to checkout.

**Priority:** P0
**Scope Req:** FR-018
**Screens:** SCR-C-015 (Cart), SCR-C-016 (Checkout)

**Acceptance Criteria:**
- **Given** a customer has items in their cart, **When** the cart totals are displayed, **Then** the VAT amount is shown as a separate line item (e.g., "VAT (15%): SAR X.XX") calculated on the subtotal after any discounts.
- **Given** a customer adds or removes items from the cart, **When** the cart updates, **Then** the VAT amount recalculates in real time and the updated VAT is immediately visible.
- **Given** the restaurant has configured a specific VAT rate in the dashboard, **When** VAT is calculated in the cart, **Then** the calculation uses the restaurant-configured rate (defaulting to 15% per Saudi regulations) and the rate percentage is displayed alongside the amount.

---

### US-CUST-CART-004: Upsell Prompts
**As a** customer, **I want to** see relevant "Frequently Ordered Together" suggestions based on my cart items, **so that** I can discover complementary items and enhance my order.

**Priority:** P1
**Scope Req:** FR-019
**Screens:** SCR-C-015 (Cart), SCR-C-003 (Item Detail)

**Acceptance Criteria:**
- **Given** a customer has items in their cart, **When** they view the cart, **Then** a "Frequently Ordered Together" or "You Might Also Like" section is displayed below the cart items showing 2-4 relevant suggestions based on rule-based associations.
- **Given** the upsell section is displayed, **When** the customer taps "Add" on a suggested item, **Then** the item is added to the cart immediately and the totals recalculate without navigating away from the cart.
- **Given** a customer is viewing a product detail page, **When** complementary items exist for that product, **Then** a related items section is shown below the product details with a one-tap add-to-cart option for each suggestion.

---

### US-CUST-CART-005: Delivery and Pickup Toggle
**As a** customer, **I want to** switch between home delivery and restaurant pickup for my order, **so that** I can choose the fulfillment method that is most convenient for me.

**Priority:** P0
**Scope Req:** FR-020
**Screens:** SCR-C-016 (Checkout), SCR-C-015 (Cart)

**Acceptance Criteria:**
- **Given** a customer is on the cart or checkout screen, **When** they toggle between "Delivery" and "Pickup", **Then** the order summary updates to reflect the appropriate fees (delivery fee added for delivery, removed for pickup) and the relevant address or branch selection fields are shown.
- **Given** a customer selects "Pickup", **When** the pickup option is active, **Then** the delivery fee is removed from the total, the address selection is hidden, and the branch/location selector is displayed.
- **Given** a customer selects "Delivery", **When** the delivery option is active, **Then** the delivery address field is displayed (with saved addresses or map pin-drop) and the zone-based delivery fee is calculated and added to the order total.

---

### US-CUST-CART-006: Order Scheduling
**As a** customer, **I want to** schedule my delivery or pickup for a future date and time, **so that** I can plan my meal in advance and receive it when I want.

**Priority:** P1
**Scope Req:** FR-021
**Screens:** SCR-C-016 (Checkout)

**Acceptance Criteria:**
- **Given** a customer is on the checkout screen, **When** they tap the scheduling option, **Then** a date and time picker is displayed showing available time slots based on the restaurant's operating hours.
- **Given** a customer selects a future date and time, **When** they confirm the schedule, **Then** the selected delivery/pickup time is displayed in the order summary and the order is marked as "Scheduled" rather than "ASAP".
- **Given** the restaurant is currently closed but has future operating hours, **When** a customer attempts to place an order, **Then** the scheduling option is presented as the default with the nearest available time slot pre-selected.

---

### US-CUST-CART-007: ETA Display
**As a** customer, **I want to** see the estimated delivery or pickup time for my order, **so that** I know approximately when to expect my food.

**Priority:** P0
**Scope Req:** FR-022
**Screens:** SCR-C-016 (Checkout), SCR-C-015 (Cart)

**Acceptance Criteria:**
- **Given** a customer has selected a delivery address and has items in the cart, **When** the ETA is calculated, **Then** an estimated delivery time range (e.g., "30-45 minutes") is displayed on the cart and checkout screens.
- **Given** a customer switches between delivery and pickup, **When** the fulfillment mode changes, **Then** the ETA recalculates to reflect the different times (pickup is typically shorter than delivery).
- **Given** the restaurant has set preparation times and a zone-based delivery model, **When** the ETA is calculated, **Then** it factors in preparation time plus estimated travel time based on the customer's delivery zone.

---

### US-CUST-CART-008: Branch Map with Pickup Option
**As a** customer, **I want to** see a map showing restaurant branches with curbside pickup options, **so that** I can select the most convenient branch for pickup.

**Priority:** P1
**Scope Req:** FR-023
**Screens:** SCR-C-017 (Branch Map)

**Acceptance Criteria:**
- **Given** a customer selects the "Pickup" option, **When** the branch map loads, **Then** all restaurant branches are displayed as pins on a Google Maps interface with branch names, addresses, and distance from the customer's current location.
- **Given** a customer taps on a branch pin on the map, **When** the branch details appear, **Then** the branch address, operating hours, phone number, and a "Select This Branch" button are displayed.
- **Given** a customer selects a branch for pickup, **When** they confirm the selection, **Then** the branch is set as the pickup location, the order summary updates with the branch name, and curbside pickup instructions are shown if available.

---

### US-CUST-CART-009: Address Selection at Checkout
**As a** customer, **I want to** select from my saved delivery addresses or add a new address via map pin-drop during checkout, **so that** I can specify where my order should be delivered quickly.

**Priority:** P0
**Scope Req:** FR-024
**Screens:** SCR-C-016 (Checkout), SCR-C-008 (Address Management)

**Acceptance Criteria:**
- **Given** a customer is on the checkout screen with delivery selected, **When** the address section loads, **Then** saved addresses are listed with labels (Home, Work, etc.) and a default address is pre-selected if set.
- **Given** a customer wants to add a new address at checkout, **When** they tap "Add New Address", **Then** a map interface with pin-drop opens allowing them to select a location, enter details, and save it for future use.
- **Given** a customer selects a delivery address, **When** the address is confirmed, **Then** the system validates the address is within the restaurant's delivery zone and the delivery fee updates based on the zone. If outside the zone, an error message is displayed.

---

### US-CUST-CART-010: One-Page Checkout
**As a** customer, **I want to** complete the entire checkout process on a single scrollable page with a progress indicator, **so that** I can review and confirm my order efficiently without navigating between multiple screens.

**Priority:** P0
**Scope Req:** FR-025
**Screens:** SCR-C-016 (Checkout)

**Acceptance Criteria:**
- **Given** a customer proceeds to checkout, **When** the checkout page loads, **Then** a single scrollable page displays all checkout sections: delivery/pickup selection, address, order summary, payment method, and a progress indicator showing the current step.
- **Given** a customer fills in all required checkout fields, **When** they scroll through the page, **Then** each section validates inline and the progress indicator updates as sections are completed.
- **Given** a customer has a default address and saved payment method, **When** they reach the checkout page, **Then** these defaults are pre-filled, minimizing the fields they need to interact with and allowing a fast checkout experience.

---

### US-CUST-CART-011: Fee Transparency
**As a** customer, **I want to** see a comprehensive order summary showing all fees including subtotal, VAT, delivery fee, and any discounts, **so that** I understand exactly what I am paying and there are no hidden charges.

**Priority:** P0
**Scope Req:** FR-026
**Screens:** SCR-C-016 (Checkout), SCR-C-015 (Cart)

**Acceptance Criteria:**
- **Given** a customer is on the cart or checkout screen, **When** the order summary is displayed, **Then** it shows a complete fee breakdown: subtotal (items), discount (if any), delivery fee (if delivery), VAT amount, and total payable.
- **Given** a customer has applied a promo code and selected delivery, **When** the fee summary is displayed, **Then** the discount line item shows the promo code name and amount deducted, the delivery fee shows the zone-based fee, and the VAT is calculated on the post-discount subtotal.
- **Given** a customer changes any aspect of the order (items, delivery mode, address, promo code), **When** the order summary updates, **Then** all fee lines recalculate and update in real time, and the total is always accurate and current.

---

## 4. Customer - Payment (FR-027 to FR-033)

### US-CUST-PAY-001: Credit and Debit Card Payment
**As a** customer, **I want to** pay for my order using a credit or debit card, **so that** I can complete my purchase with a standard card payment.

**Priority:** P0
**Scope Req:** FR-027
**Screens:** SCR-C-018 (Payment Selection), SCR-C-019 (Card Entry)

**Acceptance Criteria:**
- **Given** a customer is on the payment step of checkout, **When** they select "Credit/Debit Card" as the payment method, **Then** a secure card entry form (Stripe Elements) is displayed for entering card number, expiry, CVV, and cardholder name.
- **Given** a customer enters valid card details, **When** they submit the payment, **Then** the payment is processed through Stripe, and upon success, the order is confirmed with a confirmation screen displaying the order number.
- **Given** a customer enters invalid card details or the payment is declined, **When** the payment fails, **Then** a clear error message is displayed (e.g., "Card declined", "Invalid card number") and the customer can retry with the same or different card.

---

### US-CUST-PAY-002: Mada Card Payment
**As a** Saudi customer, **I want to** pay using my Mada debit card, **so that** I can use the local Saudi payment network I trust for everyday transactions.

**Priority:** P0
**Scope Req:** FR-028
**Screens:** SCR-C-018 (Payment Selection), SCR-C-019 (Card Entry)

**Acceptance Criteria:**
- **Given** a customer is on the payment step, **When** they select "Mada" as the payment method, **Then** the Mada card entry form is displayed via Stripe (which supports Mada natively in Saudi Arabia).
- **Given** a customer enters their Mada card details, **When** they submit the payment, **Then** the transaction is processed through Stripe's Mada integration and the customer receives a confirmation upon successful payment.
- **Given** a Mada payment fails due to insufficient funds or network error, **When** the error occurs, **Then** the customer receives an Arabic-localized error message explaining the issue with a retry option.

---

### US-CUST-PAY-003: Google Pay
**As a** customer with Google Pay set up on my device, **I want to** pay using Google Pay, **so that** I can complete my purchase with a single tap without entering card details.

**Priority:** P1
**Scope Req:** FR-029
**Screens:** SCR-C-018 (Payment Selection)

**Acceptance Criteria:**
- **Given** a customer has Google Pay configured on their Android device, **When** they view the payment options at checkout, **Then** a "Google Pay" button is displayed as a payment method.
- **Given** a customer taps the Google Pay button, **When** the Google Pay sheet appears, **Then** the order total is pre-filled and the customer can authenticate and pay using their saved Google Pay cards.
- **Given** Google Pay is not configured on the device, **When** the payment options are displayed, **Then** the Google Pay option is either hidden or shown as disabled with a prompt to set up Google Pay.

---

### US-CUST-PAY-004: STC Pay
**As a** Saudi customer, **I want to** pay using my STC Pay digital wallet, **so that** I can use my preferred local mobile payment method.

**Priority:** P1
**Scope Req:** FR-030
**Screens:** SCR-C-018 (Payment Selection)

**Acceptance Criteria:**
- **Given** a customer is on the payment step, **When** they select "STC Pay" as the payment method, **Then** the STC Pay payment flow is initiated (redirect or in-app SDK integration).
- **Given** a customer completes the STC Pay authorization, **When** the payment is confirmed, **Then** the order is placed successfully and the customer receives an order confirmation with the payment method noted as STC Pay.
- **Given** a customer cancels the STC Pay flow or the payment fails, **When** they return to the checkout, **Then** the order is not placed, the customer is returned to the payment selection step, and an appropriate error message is displayed.

---

### US-CUST-PAY-005: Cash on Delivery
**As a** customer, **I want to** select Cash on Delivery (COD) as my payment method, **so that** I can pay with cash when my order arrives.

**Priority:** P0
**Scope Req:** FR-031
**Screens:** SCR-C-018 (Payment Selection)

**Acceptance Criteria:**
- **Given** a customer is on the payment step and COD is enabled by the restaurant, **When** they select "Cash on Delivery", **Then** no additional payment information is required and the order can be placed immediately.
- **Given** a customer places a COD order, **When** the order is confirmed, **Then** the confirmation screen clearly indicates the payment method as "Cash on Delivery" and shows the total amount due in cash.
- **Given** COD is selected for a pickup order, **When** the customer confirms, **Then** the order summary indicates payment will be collected at the restaurant at the time of pickup.

---

### US-CUST-PAY-006: Saved Payment Cards
**As a** registered customer, **I want to** save my payment cards for future use, **so that** I can check out faster on subsequent orders without re-entering card details.

**Priority:** P1
**Scope Req:** FR-032
**Screens:** SCR-C-019 (Card Entry), SCR-C-009 (Payment Preferences)

**Acceptance Criteria:**
- **Given** a customer is entering card details during checkout, **When** they check the "Save this card for future use" option, **Then** the card is tokenized and stored securely via Stripe (no raw card data stored on the platform) and the last 4 digits are saved for display.
- **Given** a customer has saved cards, **When** they reach the payment step on a future order, **Then** their saved cards are displayed as selectable options showing card brand icon and last 4 digits.
- **Given** a customer wants to manage their saved cards, **When** they navigate to Payment Preferences in their profile, **Then** they can view all saved cards, set a default card, and delete cards they no longer want saved.

---

### US-CUST-PAY-007: Quick Payment Selection
**As a** customer, **I want to** quickly select my payment method from a clear, easy-to-use interface, **so that** I can complete checkout with minimal taps.

**Priority:** P1
**Scope Req:** FR-033
**Screens:** SCR-C-018 (Payment Selection)

**Acceptance Criteria:**
- **Given** a customer reaches the payment step at checkout, **When** the payment options load, **Then** all available payment methods (saved cards, Mada, Google Pay, STC Pay, COD) are displayed as distinct, tappable options with recognizable icons and labels.
- **Given** a customer has a default payment method set, **When** the payment step loads, **Then** the default method is pre-selected and the customer can proceed without additional taps unless they wish to change.
- **Given** a customer taps on a different payment method, **When** they select it, **Then** the payment method switches immediately with appropriate UI (e.g., card entry form for new card, or confirmation for COD) without a full page reload.

---

## 5. Customer - Order Tracking and History (FR-034 to FR-041)

### US-CUST-TRACK-001: Order Status Tracking
**As a** customer, **I want to** track my order through each stage from confirmation to delivery, **so that** I know exactly where my order is in the process.

**Priority:** P0
**Scope Req:** FR-034
**Screens:** SCR-C-020 (Order Tracking)

**Acceptance Criteria:**
- **Given** a customer has placed an order, **When** they navigate to the order tracking screen, **Then** a visual progress indicator shows the current stage: Order Confirmed, Preparing, Ready for Pickup, Out for Delivery, Delivered.
- **Given** the restaurant updates the order status (e.g., from "Preparing" to "Ready"), **When** the status changes, **Then** the tracking screen updates in real time via Socket.io without requiring a manual refresh.
- **Given** a customer is not on the tracking screen when a status change occurs, **When** the status updates, **Then** a push notification is sent to the customer informing them of the new status.

---

### US-CUST-TRACK-002: Live GPS Driver Tracking
**As a** customer, **I want to** see the driver's live location on a map during delivery, **so that** I can monitor the driver's approach and be ready to receive my order.

**Priority:** P0
**Scope Req:** FR-035
**Screens:** SCR-C-020 (Order Tracking), SCR-C-021 (Live Map)

**Acceptance Criteria:**
- **Given** a customer's order status is "Out for Delivery", **When** they view the tracking screen, **Then** a Google Maps view is displayed showing the driver's real-time location as a moving pin, with the delivery address marked.
- **Given** the driver is en route, **When** the driver's location updates, **Then** the map pin moves smoothly to the new position with location updates occurring at minimum every 10-15 seconds.
- **Given** the driver's location is being tracked, **When** the customer views the map, **Then** the estimated remaining delivery time updates dynamically based on the driver's current position and route.

---

### US-CUST-TRACK-003: Driver Contact
**As a** customer, **I want to** call or message the driver directly from the tracking screen, **so that** I can communicate delivery instructions or resolve any issues.

**Priority:** P0
**Scope Req:** FR-036
**Screens:** SCR-C-020 (Order Tracking)

**Acceptance Criteria:**
- **Given** a customer's order is assigned to a driver, **When** they view the tracking screen, **Then** the driver's name and contact options (call button, message button) are displayed.
- **Given** a customer taps the call button, **When** the call is initiated, **Then** a phone call is placed to the driver directly (or via a masked/proxy number for privacy).
- **Given** a customer taps the message button, **When** the messaging interface opens, **Then** the customer can send text messages to the driver for coordination purposes (e.g., "I'm at the gate", "Call when you arrive").

---

### US-CUST-TRACK-004: Push Notifications for Order Updates
**As a** customer, **I want to** receive push notifications for order confirmation, status changes, and delivery alerts, **so that** I stay informed about my order even when not actively using the app.

**Priority:** P0
**Scope Req:** FR-037
**Screens:** System-level (Push Notifications)

**Acceptance Criteria:**
- **Given** a customer has placed an order and has push notifications enabled, **When** the order status changes at any stage, **Then** a push notification is delivered to the customer's device within seconds of the status change.
- **Given** the driver is approaching the delivery location, **When** the driver is within a close proximity, **Then** the customer receives a "Your driver is nearby" push notification.
- **Given** the order is delivered, **When** the driver confirms delivery, **Then** the customer receives a "Your order has been delivered" notification with an option to rate the experience.

---

### US-CUST-TRACK-005: Order History
**As a** a registered customer, **I want to** view my complete past order history, **so that** I can review previous orders, track spending, and reference past meals.

**Priority:** P0
**Scope Req:** FR-038
**Screens:** SCR-C-022 (Order History), SCR-C-023 (Order Detail)

**Acceptance Criteria:**
- **Given** a registered customer navigates to the Order History section, **When** the history loads, **Then** all past orders are displayed in reverse chronological order showing order date, items summary, total amount, and order status.
- **Given** a customer taps on a past order in the history, **When** the order detail opens, **Then** the full order details are shown including all items with customizations, fee breakdown, payment method, delivery address, and timestamps.
- **Given** a customer has many past orders, **When** they scroll through the history, **Then** the list loads incrementally (pagination or infinite scroll) and remains performant.

---

### US-CUST-TRACK-006: Reorder Function
**As a** registered customer, **I want to** reorder a previous order with one click, **so that** I can quickly place the same order again without rebuilding it from scratch.

**Priority:** P1
**Scope Req:** FR-039
**Screens:** SCR-C-022 (Order History), SCR-C-023 (Order Detail)

**Acceptance Criteria:**
- **Given** a customer is viewing their order history, **When** they see a past order, **Then** a "Reorder" button is prominently displayed next to each order.
- **Given** a customer taps "Reorder", **When** the reorder is initiated, **Then** all items from the previous order (with their customizations) are added to the cart. If any item is no longer available, the customer is notified of the specific unavailable items.
- **Given** items from a previous order have changed in price, **When** the reorder populates the cart, **Then** the current prices are used and the customer can review the updated totals before proceeding to checkout.

---

### US-CUST-TRACK-007: VAT-Compliant Receipts
**As a** customer, **I want to** generate and view VAT-compliant receipts for my completed orders, **so that** I have proper documentation for my purchases that meets Saudi tax requirements.

**Priority:** P0
**Scope Req:** FR-040
**Screens:** SCR-C-023 (Order Detail)

**Acceptance Criteria:**
- **Given** a customer views a completed order in their history, **When** they tap "View Receipt", **Then** a VAT-compliant receipt is displayed showing restaurant name, tax registration number, order items, subtotal, VAT amount (with rate), total, payment method, and date/time.
- **Given** a customer is viewing a receipt, **When** they tap "Download" or "Share", **Then** the receipt is available as a PDF that can be saved to the device or shared via standard sharing options.
- **Given** the receipt is generated, **When** the VAT details are displayed, **Then** the receipt complies with Saudi ZATCA (Zakat, Tax and Customs Authority) requirements for simplified tax invoices including QR code if required.

---

### US-CUST-TRACK-008: Item Ratings and Reviews
**As a** customer, **I want to** rate and review individual menu items I have ordered, **so that** I can share my feedback and help other customers make informed decisions.

**Priority:** P2
**Scope Req:** FR-041
**Screens:** SCR-C-024 (Rating/Review), SCR-C-003 (Item Detail)

**Acceptance Criteria:**
- **Given** a customer has received a delivered order, **When** they view the order detail or receive the post-delivery prompt, **Then** they can rate each item on a star scale (1-5) and optionally write a text review.
- **Given** a customer submits a rating and review, **When** the review is saved, **Then** the rating contributes to the item's overall average rating displayed on the menu and a confirmation is shown.
- **Given** other customers view a menu item, **When** ratings and reviews exist, **Then** the item's average rating, total number of reviews, and individual review comments are visible on the product detail page.

---

## 6. Customer - Offers, Addresses and Settings (FR-042 to FR-050)

### US-CUST-OFFER-001: Offers Tab
**As a** customer, **I want to** see a dedicated tab showing all available offers with one-tap apply, **so that** I can easily discover and use discounts on my orders.

**Priority:** P1
**Scope Req:** FR-042
**Screens:** SCR-C-025 (Offers Tab)

**Acceptance Criteria:**
- **Given** a customer navigates to the Offers tab, **When** the offers load, **Then** all active offers are displayed showing the offer title, description, discount amount/percentage, expiry date, and any conditions (e.g., minimum order).
- **Given** a customer finds an offer they want to use, **When** they tap "Apply" on the offer, **Then** the promo code or discount is automatically added to their cart and they are redirected to the menu or cart if items are already present.
- **Given** an offer has conditions (e.g., minimum order amount, specific items only), **When** the customer taps "Apply", **Then** the condition is clearly stated and the offer is applied only when all conditions are met during checkout.

---

### US-CUST-OFFER-002: Introductory Offers for New Customers
**As a** new customer, **I want to** receive introductory discount offers upon first registration, **so that** I am incentivized to place my first order.

**Priority:** P1
**Scope Req:** FR-043
**Screens:** SCR-C-025 (Offers Tab), SCR-C-001 (Home)

**Acceptance Criteria:**
- **Given** a user has just completed registration, **When** they land on the home screen for the first time, **Then** a welcome banner or popup displays the introductory offer (e.g., "20% off your first order") with a clear call-to-action.
- **Given** a new customer views the Offers tab, **When** the offers load, **Then** the introductory offer is highlighted prominently at the top of the offers list, marked as "New Customer Special" or similar.
- **Given** a new customer applies the introductory offer, **When** they proceed to checkout, **Then** the discount is applied correctly to their first order, and the offer is marked as used and cannot be reapplied on subsequent orders.

---

### US-CUST-ADDR-001: Multiple Saved Addresses
**As a** registered customer, **I want to** save multiple delivery addresses with custom labels, **so that** I can quickly select the right address for each order.

**Priority:** P0
**Scope Req:** FR-044
**Screens:** SCR-C-008 (Address Management)

**Acceptance Criteria:**
- **Given** a customer navigates to Address Management, **When** the address list loads, **Then** all saved addresses are displayed with their labels (Home, Work, etc.), full address text, and edit/delete options.
- **Given** a customer taps "Add New Address", **When** the address form opens, **Then** they can enter the address details including a custom label, street address, building/apartment number, and additional delivery instructions.
- **Given** a customer has multiple saved addresses, **When** they proceed to checkout with delivery selected, **Then** all saved addresses are presented as selectable options, making address selection a single-tap action.

---

### US-CUST-ADDR-002: Map Pin-Drop for Addresses
**As a** customer, **I want to** add delivery addresses using a map pin-drop interface, **so that** I can precisely mark my location on the map for accurate deliveries.

**Priority:** P0
**Scope Req:** FR-045
**Screens:** SCR-C-026 (Map Pin-Drop)

**Acceptance Criteria:**
- **Given** a customer is adding a new address, **When** they select the map pin-drop option, **Then** a full-screen Google Maps interface is displayed centered on their current GPS location with a draggable pin.
- **Given** a customer moves the pin on the map, **When** they position it on their desired location, **Then** the address text auto-populates via reverse geocoding and the customer can confirm or manually adjust the address details.
- **Given** a customer confirms a pin-drop location, **When** they save the address, **Then** the GPS coordinates and the resolved address are stored, and the address appears in their saved addresses with the correct location.

---

### US-CUST-ADDR-003: Default Delivery Address
**As a** customer, **I want to** set one of my saved addresses as the default delivery address, **so that** it is automatically selected during checkout saving me time.

**Priority:** P1
**Scope Req:** FR-046
**Screens:** SCR-C-008 (Address Management), SCR-C-016 (Checkout)

**Acceptance Criteria:**
- **Given** a customer has multiple saved addresses, **When** they view the address management screen, **Then** they can mark one address as the default by tapping a "Set as Default" option, and the default address is visually distinguished.
- **Given** a customer has set a default address, **When** they proceed to checkout with delivery, **Then** the default address is automatically pre-selected in the address field.
- **Given** a customer changes their default address, **When** they set a new default, **Then** the previous default is unmarked and the new default is used for all future checkouts.

---

### US-CUST-ADDR-004: Postal System Integration
**As a** customer, **I want to** benefit from integration with the official Saudi postal system for accurate addressing, **so that** my delivery address is precise and recognized by the postal infrastructure.

**Priority:** P2
**Scope Req:** FR-047
**Screens:** SCR-C-026 (Map Pin-Drop), SCR-C-008 (Address Management)

**Acceptance Criteria:**
- **Given** a customer is entering a delivery address, **When** they type in the address field, **Then** auto-complete suggestions from the Saudi postal system (SPL) are provided for recognized addresses including postal codes.
- **Given** a customer uses map pin-drop, **When** the address is reverse-geocoded, **Then** the system attempts to match the location with a registered postal address for accuracy.
- **Given** a postal system match is found, **When** the address is saved, **Then** the postal code and standardized address format are included in the saved address data.

---

### US-CUST-SET-001: Notification Preferences
**As a** customer, **I want to** control which types of notifications I receive and how frequently, **so that** I only get the notifications that are relevant and useful to me.

**Priority:** P1
**Scope Req:** FR-048
**Screens:** SCR-C-027 (Settings - Notifications)

**Acceptance Criteria:**
- **Given** a customer navigates to notification preferences in settings, **When** the preferences load, **Then** toggle controls are displayed for each notification category: Order Updates, Promotions/Offers, Delivery Alerts, and General Announcements.
- **Given** a customer disables a notification category, **When** they save preferences, **Then** push notifications of that category are no longer sent to the customer's device.
- **Given** a customer re-enables a previously disabled category, **When** they save, **Then** notifications of that category resume immediately.

---

### US-CUST-SET-002: Language Toggle
**As a** customer, **I want to** switch between Arabic and English within the app, **so that** I can use the app in my preferred language.

**Priority:** P0
**Scope Req:** FR-049
**Screens:** SCR-C-027 (Settings - Language)

**Acceptance Criteria:**
- **Given** a customer navigates to language settings, **When** they toggle between Arabic and English, **Then** the entire app interface switches to the selected language including all labels, buttons, menus, notifications, and content.
- **Given** a customer switches from English to Arabic, **When** the language changes, **Then** the entire layout switches to RTL with all text, navigation, and interactive elements correctly mirrored.
- **Given** a customer sets a language preference, **When** they close and reopen the app, **Then** the app loads in the last selected language without requiring the user to set it again.

---

### US-CUST-LOYAL-001: Basic Loyalty Program
**As a** registered customer, **I want to** earn and redeem cashback or points on my orders, **so that** I am rewarded for my loyalty and incentivized to order more.

**Priority:** P1
**Scope Req:** FR-050
**Screens:** SCR-C-028 (Loyalty/Rewards)

**Acceptance Criteria:**
- **Given** the restaurant has configured a loyalty program via the dashboard, **When** a registered customer places an order, **Then** points or cashback are earned based on the restaurant-defined rules (e.g., 1 point per SAR spent) and the earned amount is displayed on the order confirmation.
- **Given** a customer has accumulated redeemable points or cashback, **When** they proceed to checkout, **Then** an option to redeem available rewards is shown with the equivalent discount amount, and applying it reduces the order total.
- **Given** a customer wants to check their loyalty balance, **When** they navigate to the Loyalty/Rewards section, **Then** their current points balance, earning history, and redemption history are displayed.

---

## 7. Driver App (FR-051 to FR-063)

### US-DRV-AUTH-001: Driver Login
**As a** driver, **I want to** log in using credentials provided by the restaurant, **so that** I can access the driver app and start receiving delivery assignments.

**Priority:** P0
**Scope Req:** FR-051
**Screens:** SCR-D-001 (Login)

**Acceptance Criteria:**
- **Given** a driver has received login credentials from the restaurant, **When** they enter their username/ID and password on the login screen, **Then** the credentials are validated and the driver is granted access to the driver app dashboard.
- **Given** a driver enters incorrect credentials, **When** they submit the login form, **Then** an error message is displayed indicating invalid credentials with a retry option.
- **Given** a driver has logged in previously, **When** they open the app, **Then** their session persists (JWT-based) and they are taken directly to the dashboard without re-entering credentials, until the session expires or they log out.

---

### US-DRV-PROF-001: Driver Profile Management
**As a** driver, **I want to** manage my profile including contact information, vehicle details, and document storage, **so that** my information is up to date and the restaurant has my current details.

**Priority:** P1
**Scope Req:** FR-052
**Screens:** SCR-D-002 (Profile)

**Acceptance Criteria:**
- **Given** a driver navigates to their profile, **When** the profile loads, **Then** their contact information, vehicle details (type, plate number, model), and uploaded documents are displayed.
- **Given** a driver wants to update their vehicle details, **When** they edit and save the information, **Then** the updated details are stored and visible to the restaurant via the dashboard.
- **Given** a driver needs to upload documents (license, vehicle registration, ID), **When** they tap "Upload Document", **Then** they can take a photo or select a file, the document is uploaded to secure cloud storage (S3), and its status is shown as "Pending Review" until the restaurant approves it.

---

### US-DRV-AVAIL-001: Availability Toggle
**As a** driver, **I want to** set my availability status to online or offline, **so that** the restaurant knows when I am available to receive delivery assignments.

**Priority:** P0
**Scope Req:** FR-053
**Screens:** SCR-D-003 (Dashboard)

**Acceptance Criteria:**
- **Given** a driver is on the dashboard, **When** they toggle the availability switch to "Online", **Then** their status is updated to available in real time and the restaurant can assign them deliveries.
- **Given** a driver toggles to "Offline", **When** the status changes, **Then** they stop receiving new delivery assignments and the restaurant dashboard reflects their offline status.
- **Given** a driver has an active delivery in progress, **When** they attempt to go offline, **Then** a warning is displayed that they have an active delivery and they must complete it before going fully offline, or the system completes the current delivery before setting them offline.

---

### US-DRV-AVAIL-002: Shift Management
**As a** driver, **I want to** manage my work schedule and submit leave requests, **so that** the restaurant can plan delivery coverage accordingly.

**Priority:** P2
**Scope Req:** FR-054
**Screens:** SCR-D-004 (Shift Schedule)

**Acceptance Criteria:**
- **Given** a driver navigates to the Shift Management section, **When** the schedule loads, **Then** their assigned shifts are displayed in a calendar or list view showing dates, start times, and end times.
- **Given** a driver wants to request time off, **When** they submit a leave request with dates and reason, **Then** the request is sent to the restaurant admin for approval and the driver can see its pending status.
- **Given** a restaurant admin approves or denies a leave request, **When** the decision is made, **Then** the driver receives a notification with the outcome and their schedule is updated accordingly.

---

### US-DRV-ORDER-001: Order Assignment View
**As a** driver, **I want to** view my assigned deliveries with full order details and customer information, **so that** I have all the information I need to complete the delivery.

**Priority:** P0
**Scope Req:** FR-055
**Screens:** SCR-D-005 (Order Details)

**Acceptance Criteria:**
- **Given** a driver receives a new delivery assignment, **When** they view the assignment, **Then** the order details are displayed including order number, list of items (with quantities and customizations), restaurant branch address, customer name, customer delivery address, and any special delivery instructions.
- **Given** a driver is viewing an assigned delivery, **When** they review the customer information, **Then** the customer's name, delivery address (with map preview), and contact options (call/message) are accessible.
- **Given** a driver has multiple assigned deliveries, **When** they view their dashboard, **Then** all active assignments are listed in priority order with status indicators (e.g., "Pickup Ready", "In Transit").

---

### US-DRV-ORDER-002: Accept or Decline Delivery Requests
**As a** driver, **I want to** accept or decline incoming delivery requests, **so that** I can manage my workload and only take deliveries I can handle.

**Priority:** P0
**Scope Req:** FR-056
**Screens:** SCR-D-003 (Dashboard), SCR-D-005 (Order Details)

**Acceptance Criteria:**
- **Given** a new delivery request is assigned to an online driver, **When** the notification arrives, **Then** the request displays a summary (pickup location, delivery address, estimated distance, order value) with prominent "Accept" and "Decline" buttons.
- **Given** a driver taps "Accept", **When** the acceptance is confirmed, **Then** the order is assigned to them, the restaurant is notified, and the driver sees the full order details with navigation to the restaurant.
- **Given** a driver taps "Decline", **When** the decline is confirmed, **Then** the order is returned to the unassigned pool for reassignment, and the driver's decline is logged for performance tracking.

---

### US-DRV-NAV-001: GPS Navigation to Customer
**As a** driver, **I want to** use built-in GPS navigation to the customer's delivery location, **so that** I can find the most efficient route and deliver promptly.

**Priority:** P0
**Scope Req:** FR-057
**Screens:** SCR-D-006 (Navigation)

**Acceptance Criteria:**
- **Given** a driver has accepted a delivery, **When** they tap "Navigate" on the order screen, **Then** turn-by-turn navigation is launched (via Google Maps integration) from the restaurant to the customer's delivery address.
- **Given** the driver completes restaurant pickup, **When** they start the delivery leg, **Then** the navigation automatically updates to route from the current location to the customer's address.
- **Given** the driver is following navigation, **When** traffic conditions change, **Then** the route recalculates to provide the optimal path based on current conditions.

---

### US-DRV-NAV-002: Real-Time Location Sharing
**As a** driver, **I want to** share my live location with the restaurant and customer during delivery, **so that** they can track my progress in real time.

**Priority:** P0
**Scope Req:** FR-058
**Screens:** SCR-D-006 (Navigation), Background Service

**Acceptance Criteria:**
- **Given** a driver has an active delivery, **When** their location changes, **Then** the updated GPS coordinates are sent to the server via Socket.io at minimum every 10-15 seconds.
- **Given** the driver's location is being shared, **When** the customer views the tracking screen, **Then** they see the driver's pin moving in real time on the map.
- **Given** the driver's location is being shared, **When** the restaurant admin views the driver tracking on the dashboard, **Then** they see the driver's current position on the delivery map.

---

### US-DRV-DEL-001: Delivery Confirmation
**As a** driver, **I want to** confirm successful delivery completion, **so that** the order lifecycle is closed and all parties are notified.

**Priority:** P0
**Scope Req:** FR-059
**Screens:** SCR-D-007 (Delivery Confirmation)

**Acceptance Criteria:**
- **Given** a driver has arrived at the delivery location and handed over the order, **When** they tap "Confirm Delivery", **Then** the order status is updated to "Delivered", the customer receives a delivery confirmation notification, and the restaurant dashboard reflects the completed delivery.
- **Given** the delivery is a COD order, **When** the driver confirms delivery, **Then** the driver is prompted to confirm that cash was collected along with the amount, and this is logged in the order record.
- **Given** a driver confirms delivery, **When** the confirmation is processed, **Then** the driver's active delivery list is updated, their completed delivery count increments, and they become available for new assignments (if still online).

---

### US-DRV-COMM-001: Customer Communication
**As a** driver, **I want to** call or message the customer directly, **so that** I can coordinate the delivery (e.g., get building access instructions, confirm arrival).

**Priority:** P0
**Scope Req:** FR-060
**Screens:** SCR-D-005 (Order Details)

**Acceptance Criteria:**
- **Given** a driver has an active delivery, **When** they view the order details, **Then** call and message buttons are displayed for contacting the customer.
- **Given** a driver taps the call button, **When** the call connects, **Then** a direct phone call is placed to the customer (or via a privacy-preserving proxy number).
- **Given** a driver taps the message button, **When** the messaging interface opens, **Then** the driver can send text messages to the customer and receive replies within the app.

---

### US-DRV-ISSUE-001: Issue Reporting
**As a** driver, **I want to** report problems such as customer unavailability, order damage, or address issues, **so that** the restaurant is informed and can take appropriate action.

**Priority:** P1
**Scope Req:** FR-061
**Screens:** SCR-D-008 (Issue Reporting)

**Acceptance Criteria:**
- **Given** a driver encounters a problem during delivery, **When** they tap "Report Issue" on the active order, **Then** a form is displayed with issue categories (Customer Unavailable, Wrong Address, Order Damaged, Safety Concern, Other) and a free-text description field.
- **Given** a driver fills in the issue report, **When** they submit it, **Then** the report is sent to the restaurant dashboard in real time with a timestamp and the driver's current location, and the restaurant admin receives a notification.
- **Given** a driver reports "Customer Unavailable", **When** the report is submitted, **Then** the system starts a configurable wait timer and provides instructions on next steps (e.g., "Wait 5 minutes, then contact restaurant support").

---

### US-DRV-PERF-001: Performance Dashboard
**As a** driver, **I want to** view my delivery statistics, completion rates, and customer ratings, **so that** I can track my performance and identify areas for improvement.

**Priority:** P2
**Scope Req:** FR-062
**Screens:** SCR-D-009 (Performance)

**Acceptance Criteria:**
- **Given** a driver navigates to the Performance section, **When** the dashboard loads, **Then** key metrics are displayed including total deliveries, deliveries today, average delivery time, completion rate, and average customer rating.
- **Given** a driver wants to review their performance over time, **When** they select a date range, **Then** the metrics update to reflect the selected period with trend indicators (improving/declining).
- **Given** a driver has customer ratings, **When** they view the ratings section, **Then** individual delivery ratings and any written feedback are accessible.

---

### US-DRV-SUPP-001: Restaurant Support Channel
**As a** driver, **I want to** communicate directly with restaurant support, **so that** I can get help with issues that require restaurant intervention.

**Priority:** P1
**Scope Req:** FR-063
**Screens:** SCR-D-010 (Support)

**Acceptance Criteria:**
- **Given** a driver needs assistance from the restaurant, **When** they navigate to the Support section, **Then** a communication channel is available (in-app chat or direct call option) to reach restaurant support staff.
- **Given** a driver sends a support message, **When** the message is sent, **Then** the restaurant dashboard receives the message in the support management section with the driver's details and active order context.
- **Given** restaurant support responds to a driver's message, **When** the response is sent, **Then** the driver receives the response as a push notification and can view it in the support chat within the app.

---

## 8. Restaurant Dashboard (FR-064 to FR-096)

### US-REST-AUTH-001: Admin Login
**As a** restaurant admin, **I want to** securely log into the web dashboard, **so that** I can access the management tools and control restaurant operations.

**Priority:** P0
**Scope Req:** FR-064
**Screens:** SCR-R-001 (Login)

**Acceptance Criteria:**
- **Given** a restaurant admin navigates to the dashboard URL, **When** they enter valid credentials (email/username and password), **Then** they are authenticated and redirected to the main dashboard overview.
- **Given** an admin enters incorrect credentials, **When** they attempt to login, **Then** an error message is displayed without revealing which credential was wrong, and the account is locked after a configurable number of failed attempts.
- **Given** an admin is authenticated, **When** their session is active, **Then** the session is managed via JWT with automatic refresh, and the admin is logged out after a period of inactivity for security.

---

### US-REST-DASH-001: Dashboard Overview
**As a** restaurant admin, **I want to** see a control panel with real-time orders overview, sales metrics, and operational status at a glance, **so that** I can monitor the business performance and current operations from a single screen.

**Priority:** P0
**Scope Req:** FR-065
**Screens:** SCR-R-002 (Dashboard)

**Acceptance Criteria:**
- **Given** an admin logs in, **When** the dashboard loads, **Then** the overview displays today's order count, revenue, active orders, pending orders, available drivers, and key performance indicators.
- **Given** a new order is placed, **When** the dashboard is open, **Then** the order count and pending orders update in real time via Socket.io without manual refresh, and an audio/visual notification alerts the admin.
- **Given** an admin views the dashboard during operating hours, **When** they review operational status, **Then** the number of online drivers, average preparation time, and current order pipeline are visible.

---

### US-REST-MENU-001: Menu Item CRUD
**As a** restaurant admin, **I want to** add, edit, and delete menu items with images, descriptions, pricing, and nutrition/allergy information, **so that** I can maintain an accurate and appealing menu for customers.

**Priority:** P0
**Scope Req:** FR-066
**Screens:** SCR-R-003 (Menu Management), SCR-R-004 (Item Editor)

**Acceptance Criteria:**
- **Given** an admin navigates to Menu Management, **When** they click "Add New Item", **Then** a form is displayed for entering item name (Arabic and English), description, price, category, images (upload to S3), nutrition information, and allergen tags.
- **Given** an admin edits an existing menu item, **When** they save the changes, **Then** the updates are reflected immediately on the customer app and web interface without requiring an app update or cache clear.
- **Given** an admin deletes a menu item, **When** they confirm the deletion, **Then** the item is removed from the menu (soft-deleted to preserve order history), and any active cart containing that item is notified of the change.

---

### US-REST-MENU-002: Category Management
**As a** restaurant admin, **I want to** create and manage hierarchical menu categories and subcategories, **so that** the menu is well-organized and easy for customers to navigate.

**Priority:** P0
**Scope Req:** FR-067
**Screens:** SCR-R-005 (Category Management)

**Acceptance Criteria:**
- **Given** an admin navigates to Category Management, **When** they view the category list, **Then** all categories are displayed in a hierarchical tree structure showing parent categories and their subcategories.
- **Given** an admin creates a new category, **When** they enter the category name (Arabic and English), optional image, display order, and parent category (for subcategories), **Then** the category is created and visible in the menu structure.
- **Given** an admin reorders categories, **When** they drag-and-drop or set display order numbers, **Then** the category order updates on the customer-facing menu immediately.

---

### US-REST-MENU-003: Item Variants Configuration
**As a** restaurant admin, **I want to** configure item variants (sizes, toppings, modifications) with individual pricing, **so that** customers can customize their orders with correctly priced options.

**Priority:** P0
**Scope Req:** FR-068
**Screens:** SCR-R-004 (Item Editor)

**Acceptance Criteria:**
- **Given** an admin is editing a menu item, **When** they navigate to the Variants section, **Then** they can add variant groups (e.g., "Size", "Toppings", "Spice Level") and individual options within each group with names (Arabic/English) and additional price.
- **Given** an admin configures a variant group as "required" (e.g., Size), **When** a customer views the item on the app, **Then** the customer must select an option from that group before adding to cart.
- **Given** an admin sets variant pricing, **When** a customer selects that variant, **Then** the additional cost is added to the base price and the total is displayed correctly on the customer app.

---

### US-REST-MENU-004: Pricing Management
**As a** restaurant admin, **I want to** set and manage menu item prices including bulk discounts and promotional pricing, **so that** I can control my pricing strategy effectively.

**Priority:** P0
**Scope Req:** FR-069
**Screens:** SCR-R-004 (Item Editor), SCR-R-006 (Pricing)

**Acceptance Criteria:**
- **Given** an admin is editing a menu item, **When** they set the price, **Then** the price is stored in SAR and displayed to customers with proper currency formatting.
- **Given** an admin wants to set promotional pricing, **When** they configure a promotional price with start and end dates, **Then** the discounted price is shown to customers during the promotional period with the original price struck through.
- **Given** an admin changes a price, **When** the price update is saved, **Then** active customer carts are updated with the new price on their next refresh or checkout attempt, and the customer is notified of the price change.

---

### US-REST-MENU-005: Availability Control
**As a** restaurant admin, **I want to** toggle menu item availability in real time and manage stock levels, **so that** customers only see items that are currently available.

**Priority:** P0
**Scope Req:** FR-070
**Screens:** SCR-R-003 (Menu Management), SCR-R-007 (Availability)

**Acceptance Criteria:**
- **Given** an admin views the menu management screen, **When** they toggle an item's availability switch, **Then** the item is immediately marked as unavailable on the customer app (grayed out or hidden) without deleting it from the menu.
- **Given** an admin sets stock levels for an item, **When** orders reduce the stock to zero, **Then** the item is automatically marked as unavailable and the admin is notified.
- **Given** an item was marked unavailable, **When** the admin toggles it back to available, **Then** the item immediately reappears as orderable on the customer app.

---

### US-REST-ORDER-001: Order Reception
**As a** restaurant admin, **I want to** receive incoming orders with real-time notifications, **so that** I can respond to new orders immediately and keep preparation times low.

**Priority:** P0
**Scope Req:** FR-071
**Screens:** SCR-R-008 (Order Management)

**Acceptance Criteria:**
- **Given** the dashboard is open and the restaurant is within operating hours, **When** a new order is placed by a customer, **Then** the order appears in the "New Orders" section within seconds via Socket.io, accompanied by an audio notification and visual alert.
- **Given** a new order arrives, **When** the admin views the order, **Then** the full order details are shown including items, customizations, special instructions, customer name, delivery/pickup selection, payment method, and estimated totals.
- **Given** multiple orders arrive simultaneously, **When** the admin views the order queue, **Then** orders are listed in chronological order with clear status indicators and time elapsed since placement.

---

### US-REST-ORDER-002: Order Accept or Reject
**As a** restaurant admin, **I want to** accept or reject incoming orders based on kitchen capacity, **so that** I only commit to orders I can fulfill within a reasonable time.

**Priority:** P0
**Scope Req:** FR-072
**Screens:** SCR-R-008 (Order Management)

**Acceptance Criteria:**
- **Given** a new order appears in the queue, **When** the admin reviews it, **Then** "Accept" and "Reject" buttons are prominently displayed alongside the order details.
- **Given** the admin accepts an order, **When** they click "Accept", **Then** the order status changes to "Preparing", the customer receives a notification that their order has been accepted, and a preparation timer begins.
- **Given** the admin rejects an order, **When** they click "Reject" and provide a reason, **Then** the customer is notified of the rejection with the reason, any payment is voided or flagged for refund, and the order is moved to a "Rejected" archive.

---

### US-REST-ORDER-003: Preparation Time Setting
**As a** restaurant admin, **I want to** set estimated preparation times for each order, **so that** customers and drivers have accurate expectations for when the order will be ready.

**Priority:** P1
**Scope Req:** FR-073
**Screens:** SCR-R-008 (Order Management)

**Acceptance Criteria:**
- **Given** an admin accepts an order, **When** the acceptance flow completes, **Then** the admin can set an estimated preparation time (in minutes) via a quick-select (15, 20, 30, 45, 60 min) or custom input.
- **Given** a preparation time is set, **When** it is saved, **Then** the customer's ETA updates to reflect the preparation time plus delivery time, and the driver receives the estimated pickup time.
- **Given** the preparation is taking longer than estimated, **When** the admin updates the preparation time, **Then** the customer and driver are notified of the revised timeline.

---

### US-REST-ORDER-004: Kitchen Coordination
**As a** restaurant admin, **I want to** have tools for coordinating order preparation with kitchen staff, **so that** orders are prepared efficiently and on time.

**Priority:** P1
**Scope Req:** FR-074
**Screens:** SCR-R-008 (Order Management), SCR-R-009 (Kitchen View)

**Acceptance Criteria:**
- **Given** an order is in "Preparing" status, **When** the admin views the order management screen, **Then** the order displays item-by-item preparation details, special instructions highlighted, and a "Mark Ready" button.
- **Given** the kitchen has completed preparing an order, **When** the admin clicks "Mark Ready", **Then** the order status updates to "Ready for Pickup", the assigned driver is notified, and the customer sees the updated status.
- **Given** multiple orders are being prepared simultaneously, **When** the admin views the order list, **Then** orders are sortable by preparation time remaining, with overdue orders highlighted in red.

---

### US-REST-ORDER-005: Order Lifecycle Tracking
**As a** restaurant admin, **I want to** track orders through their entire lifecycle from placement to delivery, **so that** I have full visibility into every order's status and can intervene if needed.

**Priority:** P0
**Scope Req:** FR-075
**Screens:** SCR-R-008 (Order Management)

**Acceptance Criteria:**
- **Given** an admin views the order management section, **When** orders are displayed, **Then** they are organized by status columns or tabs: New, Preparing, Ready, Out for Delivery, Delivered, and Rejected/Cancelled.
- **Given** an admin clicks on any order, **When** the order detail opens, **Then** a complete timeline of all status changes is shown with timestamps, including who triggered each change.
- **Given** an order has been out for delivery for an unusually long time, **When** the admin reviews the order, **Then** the system highlights the delay and provides the driver's current location and contact information.

---

### US-REST-DRV-001: Driver Account Management
**As a** restaurant admin, **I want to** create and manage driver accounts, **so that** drivers can log into the driver app and receive delivery assignments.

**Priority:** P0
**Scope Req:** FR-076
**Screens:** SCR-R-010 (Driver Management)

**Acceptance Criteria:**
- **Given** an admin navigates to Driver Management, **When** they click "Add Driver", **Then** a form is presented to enter driver name, phone number, email, vehicle details, and generate login credentials (username/ID and initial password).
- **Given** an admin creates a driver account, **When** the account is saved, **Then** the driver can log into the driver app with the provided credentials and the driver appears in the restaurant's driver list.
- **Given** an admin wants to deactivate a driver, **When** they toggle the driver's status to inactive, **Then** the driver can no longer log in or receive assignments, and any current session is terminated.

---

### US-REST-DRV-002: Driver Assignment
**As a** restaurant admin, **I want to** assign deliveries to available drivers, **so that** orders are dispatched efficiently to the right driver.

**Priority:** P0
**Scope Req:** FR-077
**Screens:** SCR-R-008 (Order Management), SCR-R-010 (Driver Management)

**Acceptance Criteria:**
- **Given** an order is in "Ready for Pickup" status, **When** the admin clicks "Assign Driver", **Then** a list of currently online and available drivers is displayed with their names, current location, and active delivery count.
- **Given** the admin selects a driver for assignment, **When** they confirm the assignment, **Then** the driver receives a push notification with the order details, the order status updates, and the driver appears as assigned on the order.
- **Given** no drivers are currently available, **When** the admin attempts to assign a driver, **Then** a message indicates no available drivers and the admin can choose to wait or manually contact a driver.

---

### US-REST-DRV-003: Driver GPS Tracking
**As a** restaurant admin, **I want to** monitor driver locations in real time on a map, **so that** I can track active deliveries and manage operations efficiently.

**Priority:** P0
**Scope Req:** FR-078
**Screens:** SCR-R-011 (Driver Map)

**Acceptance Criteria:**
- **Given** an admin navigates to the Driver Map section, **When** the map loads, **Then** all online drivers are displayed as pins on a Google Maps interface with their current locations and status (Available, On Delivery).
- **Given** a driver is on an active delivery, **When** their location updates, **Then** the pin moves on the admin's map in real time showing the delivery progress.
- **Given** an admin clicks on a driver pin, **When** the driver details appear, **Then** the driver's name, current delivery details (if any), contact information, and a timeline of their recent activity are shown.

---

### US-REST-DRV-004: Driver Performance Monitoring
**As a** restaurant admin, **I want to** track driver metrics and performance, **so that** I can identify top performers and address any performance issues.

**Priority:** P2
**Scope Req:** FR-079
**Screens:** SCR-R-012 (Driver Performance)

**Acceptance Criteria:**
- **Given** an admin navigates to Driver Performance, **When** the report loads, **Then** a table and/or charts display each driver's key metrics: total deliveries, average delivery time, completion rate, acceptance rate, and average customer rating.
- **Given** an admin selects a specific driver, **When** the driver's detail view opens, **Then** a detailed performance breakdown is shown with historical trends over selectable time periods.
- **Given** the admin wants to compare drivers, **When** they view the performance overview, **Then** drivers are rankable and sortable by any metric for easy comparison.

---

### US-REST-SET-001: Operating Hours Configuration
**As a** restaurant admin, **I want to** set business operating hours and days, **so that** customers can only place orders during open hours and see accurate availability.

**Priority:** P0
**Scope Req:** FR-080
**Screens:** SCR-R-013 (Business Settings)

**Acceptance Criteria:**
- **Given** an admin navigates to Operating Hours settings, **When** the form loads, **Then** they can set opening and closing times for each day of the week, including the option to mark specific days as closed.
- **Given** the restaurant is outside operating hours, **When** a customer opens the app, **Then** a clear message indicates the restaurant is currently closed with the next opening time displayed, and only scheduled orders (for future times) are allowed.
- **Given** the admin updates operating hours, **When** the changes are saved, **Then** the new hours take effect immediately and are reflected on the customer app.

---

### US-REST-SET-002: Delivery Zone Configuration
**As a** restaurant admin, **I want to** define delivery coverage areas on a map, **so that** I can control which locations I deliver to and manage zone-based delivery logistics.

**Priority:** P0
**Scope Req:** FR-081
**Screens:** SCR-R-014 (Delivery Zones)

**Acceptance Criteria:**
- **Given** an admin navigates to Delivery Zone settings, **When** the zone editor loads, **Then** a Google Maps interface is displayed where the admin can draw polygon zones to define delivery areas.
- **Given** an admin draws a delivery zone, **When** they save the zone, **Then** the zone boundary is stored and used to validate customer delivery addresses. Addresses outside all zones are rejected at checkout.
- **Given** multiple delivery zones are configured, **When** the admin views the map, **Then** each zone is displayed with a distinct color, its name, and the associated delivery fee.

---

### US-REST-SET-003: Minimum Order Configuration
**As a** restaurant admin, **I want to** set minimum order amounts, **so that** small orders that are not economically viable for delivery are prevented.

**Priority:** P1
**Scope Req:** FR-082
**Screens:** SCR-R-013 (Business Settings)

**Acceptance Criteria:**
- **Given** an admin navigates to Minimum Order settings, **When** they set a minimum order amount (in SAR), **Then** the amount is saved and enforced during customer checkout.
- **Given** a customer's cart total is below the minimum order amount, **When** they attempt to proceed to checkout, **Then** a message indicates the minimum order requirement and the additional amount needed to meet it.
- **Given** the admin changes the minimum order amount, **When** the update is saved, **Then** the new minimum is enforced immediately for all new checkout attempts.

---

### US-REST-SET-004: Delivery Fee Configuration
**As a** restaurant admin, **I want to** configure zone-based delivery fees by defining zones on a map with different fees per zone, **so that** delivery charges accurately reflect the distance and operational costs for each area.

**Priority:** P0
**Scope Req:** FR-083
**Screens:** SCR-R-014 (Delivery Zones)

**Acceptance Criteria:**
- **Given** an admin has defined delivery zones, **When** they edit a zone, **Then** they can set a specific delivery fee (in SAR) for that zone.
- **Given** a customer enters a delivery address during checkout, **When** the address is geocoded, **Then** the system identifies which delivery zone the address falls in and applies the corresponding zone-based delivery fee to the order total.
- **Given** different zones have different fees, **When** a customer changes their delivery address to a different zone, **Then** the delivery fee in the order summary recalculates immediately to reflect the new zone's fee.

---

### US-REST-SET-005: Tax Settings
**As a** restaurant admin, **I want to** configure VAT and tax rates for the platform, **so that** all orders are taxed correctly in compliance with Saudi regulations.

**Priority:** P0
**Scope Req:** FR-084
**Screens:** SCR-R-013 (Business Settings)

**Acceptance Criteria:**
- **Given** an admin navigates to Tax Settings, **When** the settings load, **Then** they can set the VAT rate (defaulting to 15% per Saudi regulations) and configure whether prices displayed are inclusive or exclusive of VAT.
- **Given** the admin sets the VAT rate, **When** a customer views cart totals, **Then** the VAT is calculated using the configured rate and displayed as a separate line item in the order summary.
- **Given** the admin enters their tax registration number, **When** receipts are generated, **Then** the tax registration number is included on all VAT-compliant receipts.

---

### US-REST-PAY-001: Payment Processing
**As a** restaurant admin, **I want to** process and track all payment transactions, **so that** I have a complete financial record of all orders.

**Priority:** P0
**Scope Req:** FR-085
**Screens:** SCR-R-015 (Payment Management)

**Acceptance Criteria:**
- **Given** an admin navigates to Payment Management, **When** the transaction list loads, **Then** all transactions are displayed with order ID, customer name, amount, payment method, status (successful, pending, failed), and timestamp.
- **Given** an admin wants to review a specific transaction, **When** they click on a transaction, **Then** the full transaction details are shown including Stripe payment ID, order items, fee breakdown, and any refund status.
- **Given** an admin wants to review financial summaries, **When** they select a date range, **Then** aggregated totals are displayed broken down by payment method (Card, Mada, Google Pay, STC Pay, COD).

---

### US-REST-PAY-002: Refund Management (Technical Failures Only)
**As a** restaurant admin, **I want to** process refunds for technical and payment failures such as stuck payments or double charges, **so that** customers are not charged incorrectly due to system errors.

**Priority:** P1
**Scope Req:** FR-086
**Screens:** SCR-R-015 (Payment Management)

**Acceptance Criteria:**
- **Given** a transaction has a technical issue (stuck payment, double charge, payment processed but order failed), **When** the admin identifies the issue, **Then** a "Refund" button is available on the transaction detail page.
- **Given** the admin initiates a refund, **When** they confirm the refund with a reason (technical failure category), **Then** the refund is processed through Stripe, the transaction status updates to "Refunded", and the customer is notified.
- **Given** this is a technical-only refund system, **When** the admin views refund options, **Then** only technical/payment failure categories are available (e.g., "Duplicate Charge", "Payment Stuck", "System Error") and general order-dispute refunds are not supported in Phase 1.

---

### US-REST-CUST-001: Customer Database
**As a** restaurant admin, **I want to** view customer registrations and information, **so that** I have visibility into my customer base and can understand my audience.

**Priority:** P1
**Scope Req:** FR-087
**Screens:** SCR-R-016 (Customer Management)

**Acceptance Criteria:**
- **Given** an admin navigates to Customer Management, **When** the customer list loads, **Then** all registered customers are displayed with name, phone, email, registration date, total orders, and total spend.
- **Given** an admin wants to find a specific customer, **When** they use the search or filter function, **Then** they can search by name, phone, or email and filter by registration date range or order count.
- **Given** an admin clicks on a customer record, **When** the customer detail opens, **Then** the customer's order history, saved addresses, and account status are visible.

---

### US-REST-PROMO-001: Promo Engine
**As a** restaurant admin, **I want to** create discount codes and promotional campaigns, **so that** I can attract new customers and incentivize repeat orders.

**Priority:** P1
**Scope Req:** FR-088
**Screens:** SCR-R-017 (Promotions)

**Acceptance Criteria:**
- **Given** an admin navigates to the Promotions section, **When** they click "Create Promotion", **Then** a form is displayed for entering promo code, discount type (percentage or fixed amount), minimum order requirement, usage limits (total and per customer), validity dates, and applicable items/categories.
- **Given** an admin creates a promo code, **When** the promo is saved and active, **Then** customers can apply the code at checkout and the discount is calculated and applied correctly according to the configured rules.
- **Given** an admin views existing promotions, **When** the list loads, **Then** all promotions are shown with their code, type, discount amount, usage count, status (active/expired/paused), and options to edit, pause, or delete.

---

### US-REST-PROMO-002: Push Notification Management
**As a** restaurant admin, **I want to** send targeted push notifications to customers, **so that** I can communicate promotions, updates, and announcements directly to customer devices.

**Priority:** P1
**Scope Req:** FR-089
**Screens:** SCR-R-018 (Notification Center)

**Acceptance Criteria:**
- **Given** an admin navigates to the Notification Center, **When** they click "Send Notification", **Then** a form is displayed for composing the notification title, body, optional image, and selecting the target audience (all customers, new customers, inactive customers, or custom segment).
- **Given** an admin composes a notification, **When** they submit it, **Then** the push notification is sent via Firebase Cloud Messaging to the targeted customer devices and a delivery report is generated.
- **Given** the notification content can be in Arabic or English, **When** the admin composes the message, **Then** they can create bilingual content or select the target language and the notification is delivered in the appropriate language based on customer preferences.

---

### US-REST-PROMO-003: Email Marketing
**As a** restaurant marketing manager, **I want to** create and send email marketing campaigns to customers, **so that** I can promote offers, share news, and maintain customer engagement via email.

**Priority:** P2
**Scope Req:** FR-090
**Screens:** SCR-R-019 (Email Campaigns)

**Acceptance Criteria:**
- **Given** an admin or marketing manager navigates to Email Campaigns, **When** they create a new campaign, **Then** they can design the email with a template editor, set subject line, preview the content, and select recipient lists.
- **Given** a campaign is ready, **When** they click "Send" or schedule for a future date/time, **Then** the emails are delivered to the selected recipients via the integrated email service provider.
- **Given** a campaign has been sent, **When** the admin views the campaign report, **Then** basic metrics are shown including delivery count, open rate, and click rate.

---

### US-REST-REPORT-001: Sales Reports
**As a** restaurant admin, **I want to** generate detailed sales and revenue reports, **so that** I can understand my financial performance and make data-driven business decisions.

**Priority:** P0
**Scope Req:** FR-091
**Screens:** SCR-R-020 (Reports - Sales)

**Acceptance Criteria:**
- **Given** an admin navigates to Sales Reports, **When** they select a date range, **Then** a report is generated showing total revenue, number of orders, average order value, revenue by payment method, and revenue by day/week/month.
- **Given** a sales report is generated, **When** the admin reviews it, **Then** the data is presented in both tabular and chart formats (line chart for trends, bar chart for comparisons).
- **Given** an admin wants to export a report, **When** they click "Export", **Then** the report is downloadable as a CSV or PDF file with all displayed data included.

---

### US-REST-REPORT-002: Customer Analytics
**As a** restaurant admin, **I want to** view customer behavior and segment analytics, **so that** I can understand my customer base, identify trends, and tailor my offerings.

**Priority:** P2
**Scope Req:** FR-092
**Screens:** SCR-R-021 (Reports - Customers)

**Acceptance Criteria:**
- **Given** an admin navigates to Customer Analytics, **When** the analytics load, **Then** key metrics are displayed: total registered customers, new customers (this period), returning customers, customer retention rate, and average order frequency.
- **Given** the admin reviews customer segments, **When** they view the segment breakdown, **Then** customers are categorized into segments (e.g., New, Active, At Risk, Dormant) based on order frequency and recency.
- **Given** the admin wants to drill into a segment, **When** they click on a segment, **Then** the individual customers in that segment are listed with their last order date, total orders, and total spend.

---

### US-REST-REPORT-003: Popular Items Analysis
**As a** restaurant admin, **I want to** track and analyze trending and popular menu items, **so that** I can make informed decisions about menu composition, pricing, and inventory.

**Priority:** P1
**Scope Req:** FR-093
**Screens:** SCR-R-022 (Reports - Popular Items)

**Acceptance Criteria:**
- **Given** an admin navigates to Popular Items analysis, **When** the report loads, **Then** menu items are ranked by total orders, revenue generated, and customer ratings for the selected time period.
- **Given** the admin selects a time period, **When** the data updates, **Then** the ranking reflects orders and revenue within that specific period, allowing trend analysis over different timeframes.
- **Given** the admin wants to understand item performance by category, **When** they filter by category, **Then** the popular items within that category are shown with their relative contribution to total category revenue.

---

### US-REST-SUPP-001: Customer Support Management
**As a** restaurant admin, **I want to** handle customer inquiries, complaints, and support requests, **so that** customer issues are resolved promptly and customer satisfaction is maintained.

**Priority:** P1
**Scope Req:** FR-094
**Screens:** SCR-R-023 (Support Management)

**Acceptance Criteria:**
- **Given** a customer or driver submits a support request, **When** the admin views the Support Management section, **Then** all open support tickets are listed with requester name, issue type, priority, submission time, and status.
- **Given** an admin opens a support ticket, **When** they view the details, **Then** the full conversation history, related order details, and customer/driver information are displayed with a reply interface.
- **Given** an admin resolves a support issue, **When** they mark the ticket as resolved, **Then** the requester is notified, the ticket is archived, and the resolution time is tracked for performance metrics.

---

### US-REST-CONFIG-001: Branding Configuration
**As a** restaurant admin, **I want to** configure white-label branding elements including logo, colors, and brand name, **so that** the customer app and web interface reflect my restaurant's brand identity.

**Priority:** P1
**Scope Req:** FR-095
**Screens:** SCR-R-024 (Branding Settings)

**Acceptance Criteria:**
- **Given** an admin navigates to Branding Configuration, **When** the settings load, **Then** they can upload a logo, set primary and secondary brand colors, configure the brand name, and preview how the branding appears on the customer app.
- **Given** an admin uploads a new logo and sets brand colors, **When** they save the configuration, **Then** the branding is applied across the customer app, web interface, receipts, and notifications.
- **Given** an admin wants to preview branding changes, **When** they make changes in the branding editor, **Then** a live preview shows how the changes will appear on key screens (home, menu, checkout) before saving.

---

### US-REST-CONFIG-002: Notification Configuration
**As a** restaurant admin, **I want to** set up and configure system notification preferences, **so that** I control which notifications are sent, their content, and their triggers.

**Priority:** P1
**Scope Req:** FR-096
**Screens:** SCR-R-025 (Notification Settings)

**Acceptance Criteria:**
- **Given** an admin navigates to Notification Configuration, **When** the settings load, **Then** a list of all system notification types is displayed (Order Confirmation, Status Updates, Delivery Alerts, Promotional, etc.) with toggle controls and customizable message templates.
- **Given** an admin edits a notification template, **When** they modify the title and body text (in Arabic and English), **Then** the updated template is used for all future notifications of that type.
- **Given** an admin disables a notification type, **When** they toggle it off, **Then** notifications of that type are no longer sent to customers, and a warning is shown if disabling critical notifications (e.g., order confirmation).

---

## 9. Cross-Cutting Stories

### US-CROSS-LANG-001: Multi-Language Toggle (Arabic and English)
**As a** user of any app (Customer, Driver, or Restaurant Dashboard), **I want to** switch the interface language between Arabic and English at any time, **so that** I can use the platform in my preferred language.

**Priority:** P0
**Scope Req:** NFR-008, NFR-009
**Screens:** All screens across all applications

**Acceptance Criteria:**
- **Given** a user accesses any application, **When** they change the language setting, **Then** all UI elements, labels, buttons, navigation items, messages, and system text switch to the selected language immediately without requiring an app restart.
- **Given** a user selects Arabic, **When** the language changes, **Then** all text content displays professional Arabic translations that are grammatically correct, culturally appropriate, and use proper Saudi Arabic conventions.
- **Given** a user selects English after using Arabic, **When** the switch occurs, **Then** the language reverts to English completely with no leftover Arabic text fragments, and vice versa.

---

### US-CROSS-RTL-001: RTL Layout Support
**As a** user viewing the platform in Arabic, **I want to** have the entire interface rendered in a proper right-to-left layout, **so that** the experience feels natural and consistent with Arabic reading direction.

**Priority:** P0
**Scope Req:** NFR-009, NFR-010
**Screens:** All screens across all applications

**Acceptance Criteria:**
- **Given** the language is set to Arabic, **When** any screen renders, **Then** the layout is fully mirrored: navigation menus are on the right, text aligns right, progress bars fill from right to left, and scrolling directions are reversed where appropriate.
- **Given** the platform displays icons with directional meaning (arrows, back buttons, forward buttons), **When** RTL mode is active, **Then** directional icons are mirrored (e.g., back arrow points right instead of left) and non-directional icons remain unchanged.
- **Given** the platform includes forms, tables, and data entry fields, **When** RTL mode is active, **Then** form labels are right-aligned, table columns flow right-to-left, input text entry starts from the right, and all interactive elements are positioned per RTL conventions.

---

### US-CROSS-RT-001: Real-Time Order Updates via Socket.io
**As a** user of any role (Customer, Driver, or Restaurant Admin), **I want to** receive real-time order status updates without refreshing the page, **so that** I always see the current state of orders instantly.

**Priority:** P0
**Scope Req:** NFR-001
**Screens:** SCR-C-020 (Customer Tracking), SCR-D-003 (Driver Dashboard), SCR-R-008 (Restaurant Orders)

**Acceptance Criteria:**
- **Given** a Socket.io connection is established when a user opens the app or dashboard, **When** an order status changes (e.g., restaurant accepts order, driver picks up, delivery confirmed), **Then** all connected users related to that order see the updated status within 2-3 seconds without manual refresh.
- **Given** a user loses network connectivity momentarily, **When** the connection is restored, **Then** the Socket.io client automatically reconnects and fetches the latest order state to ensure no updates were missed.
- **Given** multiple orders are active simultaneously, **When** status updates occur on different orders, **Then** each update is delivered to the correct users and reflected on the correct order without cross-contamination of data.

---

### US-CROSS-RT-002: Real-Time GPS Tracking via Socket.io
**As a** customer or restaurant admin, **I want to** see driver locations update on the map in real time, **so that** I can accurately track delivery progress.

**Priority:** P0
**Scope Req:** NFR-001, FR-035, FR-058, FR-078
**Screens:** SCR-C-021 (Customer Live Map), SCR-R-011 (Restaurant Driver Map)

**Acceptance Criteria:**
- **Given** a driver has an active delivery and location sharing is enabled, **When** the driver's position changes, **Then** GPS coordinates are transmitted via Socket.io at minimum every 10-15 seconds and the map pin updates smoothly on all connected viewers.
- **Given** a customer is viewing the live delivery map, **When** the driver's location updates, **Then** the map smoothly animates the driver pin movement (not abrupt jumps) and the ETA recalculates based on the new position.
- **Given** the driver enters an area with poor GPS signal, **When** location updates become unreliable, **Then** the system handles stale data gracefully by showing the last known position with a "Location updating..." indicator rather than displaying inaccurate positions.

---

### US-CROSS-PUSH-001: Push Notification Delivery
**As a** customer or driver, **I want to** receive push notifications on my Android device for critical events, **so that** I am alerted even when the app is not in the foreground.

**Priority:** P0
**Scope Req:** FR-037, FR-089
**Screens:** System-level (Firebase Cloud Messaging)

**Acceptance Criteria:**
- **Given** a critical event occurs (order confirmed, status change, driver assigned, delivery approaching, delivery completed), **When** the event is triggered, **Then** a push notification is delivered to the relevant user's Android device via Firebase Cloud Messaging within seconds.
- **Given** a user receives a push notification, **When** they tap on it, **Then** the app opens directly to the relevant screen (e.g., tapping an order status notification opens the order tracking screen).
- **Given** notifications must support both languages, **When** a push notification is sent, **Then** the notification content is delivered in the user's preferred language (Arabic or English) as set in their app preferences.

---

### US-CROSS-PUSH-002: Segmented and Localized Notifications
**As a** restaurant admin, **I want to** send notifications that are targeted to specific customer segments and localized in the correct language, **so that** my communication is relevant and personalized.

**Priority:** P1
**Scope Req:** FR-089, NFR-008
**Screens:** SCR-R-018 (Notification Center)

**Acceptance Criteria:**
- **Given** an admin creates a push notification campaign, **When** they select a target segment (e.g., new customers, inactive customers), **Then** the notification is sent only to customers in that segment.
- **Given** the admin creates notification content in both Arabic and English, **When** the notification is dispatched, **Then** each customer receives the notification in their preferred language setting.
- **Given** a notification includes rich content (image, action buttons), **When** it is delivered to an Android device, **Then** the rich notification renders correctly with the image and action buttons functional.

---

### US-CROSS-BRAND-001: White-Label Branding Application
**As a** restaurant admin, **I want to** have my brand identity (logo, colors, name) consistently applied across all customer-facing touchpoints, **so that** the platform feels like my own branded app rather than a generic platform.

**Priority:** P1
**Scope Req:** FR-095
**Screens:** All customer-facing screens (SCR-C-*), Receipts, Push Notifications

**Acceptance Criteria:**
- **Given** the restaurant admin has configured branding (logo, primary color, secondary color, brand name) in the dashboard, **When** a customer opens the app or web interface, **Then** the configured logo appears in the header/splash screen, the primary color is applied to buttons, headers, and accent elements, and the brand name appears in the app title and relevant locations.
- **Given** branding is configured, **When** a receipt is generated for a customer, **Then** the receipt includes the restaurant's logo, brand name, and uses the brand's color scheme.
- **Given** a push notification is sent, **When** it arrives on the customer's device, **Then** the notification icon and app name reflect the white-label branding, not a generic platform identity.

---

### US-CROSS-SEC-001: Secure Authentication and Data Protection
**As a** user of any role, **I want to** have my data protected with encryption and secure authentication mechanisms, **so that** my personal and financial information is safe.

**Priority:** P0
**Scope Req:** NFR-004, NFR-005, NFR-006, NFR-007
**Screens:** All screens handling sensitive data

**Acceptance Criteria:**
- **Given** a user transmits any data (login credentials, payment info, personal details), **When** the data is sent to the server, **Then** it is encrypted in transit via TLS/HTTPS and sensitive data is encrypted at rest in the database.
- **Given** a user authenticates, **When** the login succeeds, **Then** a JWT token is issued with appropriate expiration, and subsequent API calls are authenticated via the token with automatic refresh before expiry.
- **Given** a user enters payment information, **When** card data is processed, **Then** the platform complies with PCI DSS by using Stripe's PCI-compliant SDKs and never stores raw card data on the platform's servers.

---

### US-CROSS-SEC-002: Saudi Regulatory Compliance
**As a** restaurant operating in Saudi Arabia, **I want to** ensure the platform complies with Saudi Arabian regulations including PDPL, CITC, and ZATCA requirements, **so that** the business operates legally.

**Priority:** P0
**Scope Req:** NFR-007, C-001, C-003
**Screens:** All screens, Receipts, Data storage

**Acceptance Criteria:**
- **Given** the platform stores personal customer data, **When** data is collected and stored, **Then** it complies with the Saudi Personal Data Protection Law (PDPL) including consent, purpose limitation, and data minimization.
- **Given** VAT-compliant receipts are required, **When** any order is completed, **Then** the receipt meets ZATCA requirements including the restaurant's VAT registration number, itemized VAT, and QR code if mandated.
- **Given** data is hosted in the cloud, **When** the infrastructure is deployed, **Then** all data is stored in the AWS Bahrain region to maintain data residency within or near Saudi Arabia.

---

### US-CROSS-PERF-001: Fast and Responsive User Experience
**As a** user of any app, **I want to** experience fast load times and responsive interactions, **so that** using the platform feels smooth and does not cause frustration.

**Priority:** P0
**Scope Req:** NFR-002, NFR-003
**Screens:** All screens across all applications

**Acceptance Criteria:**
- **Given** a user performs a search or loads a menu page, **When** the request is sent, **Then** results are returned within 2 seconds under normal network conditions.
- **Given** the platform is under load with multiple concurrent users, **When** users interact with the system, **Then** the horizontally scalable microservices architecture maintains consistent response times without degradation.
- **Given** a user is on a slow network connection, **When** pages load, **Then** optimistic UI patterns and loading indicators provide feedback, and the app gracefully handles slow responses without freezing or crashing.

---

### US-CROSS-LOYAL-CONFIG-001: Loyalty Program Configuration
**As a** restaurant admin, **I want to** configure the loyalty program rules including points per SAR spent and redemption rates, **so that** I can customize the loyalty program to fit my business model.

**Priority:** P1
**Scope Req:** FR-050
**Screens:** SCR-R-026 (Loyalty Settings)

**Acceptance Criteria:**
- **Given** an admin navigates to Loyalty Settings, **When** the configuration form loads, **Then** they can set the earning rate (e.g., 1 point per 10 SAR), redemption rate (e.g., 100 points = 5 SAR discount), and minimum points for redemption.
- **Given** an admin saves the loyalty configuration, **When** customers place orders, **Then** points are earned according to the configured earning rate and displayed correctly in the customer app.
- **Given** an admin wants to disable the loyalty program, **When** they toggle it off, **Then** the loyalty section is hidden in the customer app and no points are earned or redeemable until re-enabled.

---

### US-CROSS-WEB-001: Customer Web Interface
**As a** customer, **I want to** access the restaurant menu, browse items, and place orders through a web browser in addition to the Android app, **so that** I can order from any device without installing the app.

**Priority:** P1
**Scope Req:** Deliverable #2
**Screens:** SCR-C-WEB-001 (Web Home), SCR-C-WEB-002 (Web Menu), SCR-C-WEB-003 (Web Checkout)

**Acceptance Criteria:**
- **Given** a customer opens the restaurant's web URL in any modern browser, **When** the page loads, **Then** a responsive, mobile-friendly web interface is displayed with the restaurant's white-label branding, full menu browsing, and ordering capabilities.
- **Given** a customer browses the menu on the web, **When** they interact with items, **Then** the same item details, customization options, and pricing are available as on the Android app.
- **Given** a customer completes checkout on the web, **When** payment is processed, **Then** the order flows into the same restaurant dashboard order queue and follows the identical order lifecycle as mobile app orders.

---

## Appendix A: Story Summary by Module

| Module | Story Range | Count | P0 | P1 | P2 |
|---|---|---|---|---|---|
| Customer - Authentication | US-CUST-AUTH-001 to 008 | 8 | 5 | 3 | 0 |
| Customer - Menu and Search | US-CUST-MENU-001 to 008 | 8 | 4 | 4 | 0 |
| Customer - Cart and Checkout | US-CUST-CART-001 to 011 | 11 | 7 | 4 | 0 |
| Customer - Payment | US-CUST-PAY-001 to 007 | 7 | 3 | 4 | 0 |
| Customer - Order Tracking | US-CUST-TRACK-001 to 008 | 8 | 5 | 1 | 2 |
| Customer - Offers/Addresses/Settings | US-CUST-OFFER/ADDR/SET/LOYAL-001 to 009 | 9 | 3 | 5 | 1 |
| Driver App | US-DRV-*-001 to 013 | 13 | 8 | 3 | 2 |
| Restaurant Dashboard | US-REST-*-001 to 033 | 33 | 16 | 13 | 4 |
| Cross-Cutting | US-CROSS-*-001 to 013 | 13 | 6 | 5 | 0 |
| **Total** | | **110** | **57** | **42** | **9** |

## Appendix B: FR to User Story Mapping

| FR ID | User Story ID |
|---|---|
| FR-001 | US-CUST-AUTH-001 |
| FR-002 | US-CUST-AUTH-002 |
| FR-003 | US-CUST-AUTH-003, US-CUST-AUTH-004 |
| FR-004 | US-CUST-AUTH-005 |
| FR-005 | US-CUST-AUTH-006 |
| FR-006 | US-CUST-AUTH-007 |
| FR-007 | US-CUST-AUTH-008 |
| FR-008 | US-CUST-MENU-001 |
| FR-009 | US-CUST-MENU-002 |
| FR-010 | US-CUST-MENU-003 |
| FR-011 | US-CUST-MENU-004 |
| FR-012 | US-CUST-MENU-005 |
| FR-013 | US-CUST-MENU-006 |
| FR-014 | US-CUST-MENU-007 |
| FR-015 | US-CUST-MENU-008 |
| FR-016 | US-CUST-CART-001 |
| FR-017 | US-CUST-CART-002 |
| FR-018 | US-CUST-CART-003 |
| FR-019 | US-CUST-CART-004 |
| FR-020 | US-CUST-CART-005 |
| FR-021 | US-CUST-CART-006 |
| FR-022 | US-CUST-CART-007 |
| FR-023 | US-CUST-CART-008 |
| FR-024 | US-CUST-CART-009 |
| FR-025 | US-CUST-CART-010 |
| FR-026 | US-CUST-CART-011 |
| FR-027 | US-CUST-PAY-001 |
| FR-028 | US-CUST-PAY-002 |
| FR-029 | US-CUST-PAY-003 |
| FR-030 | US-CUST-PAY-004 |
| FR-031 | US-CUST-PAY-005 |
| FR-032 | US-CUST-PAY-006 |
| FR-033 | US-CUST-PAY-007 |
| FR-034 | US-CUST-TRACK-001 |
| FR-035 | US-CUST-TRACK-002, US-CROSS-RT-002 |
| FR-036 | US-CUST-TRACK-003 |
| FR-037 | US-CUST-TRACK-004, US-CROSS-PUSH-001 |
| FR-038 | US-CUST-TRACK-005 |
| FR-039 | US-CUST-TRACK-006 |
| FR-040 | US-CUST-TRACK-007 |
| FR-041 | US-CUST-TRACK-008 |
| FR-042 | US-CUST-OFFER-001 |
| FR-043 | US-CUST-OFFER-002 |
| FR-044 | US-CUST-ADDR-001 |
| FR-045 | US-CUST-ADDR-002 |
| FR-046 | US-CUST-ADDR-003 |
| FR-047 | US-CUST-ADDR-004 |
| FR-048 | US-CUST-SET-001 |
| FR-049 | US-CUST-SET-002 |
| FR-050 | US-CUST-LOYAL-001, US-CROSS-LOYAL-CONFIG-001 |
| FR-051 | US-DRV-AUTH-001 |
| FR-052 | US-DRV-PROF-001 |
| FR-053 | US-DRV-AVAIL-001 |
| FR-054 | US-DRV-AVAIL-002 |
| FR-055 | US-DRV-ORDER-001 |
| FR-056 | US-DRV-ORDER-002 |
| FR-057 | US-DRV-NAV-001 |
| FR-058 | US-DRV-NAV-002, US-CROSS-RT-002 |
| FR-059 | US-DRV-DEL-001 |
| FR-060 | US-DRV-COMM-001 |
| FR-061 | US-DRV-ISSUE-001 |
| FR-062 | US-DRV-PERF-001 |
| FR-063 | US-DRV-SUPP-001 |
| FR-064 | US-REST-AUTH-001 |
| FR-065 | US-REST-DASH-001 |
| FR-066 | US-REST-MENU-001 |
| FR-067 | US-REST-MENU-002 |
| FR-068 | US-REST-MENU-003 |
| FR-069 | US-REST-MENU-004 |
| FR-070 | US-REST-MENU-005 |
| FR-071 | US-REST-ORDER-001 |
| FR-072 | US-REST-ORDER-002 |
| FR-073 | US-REST-ORDER-003 |
| FR-074 | US-REST-ORDER-004 |
| FR-075 | US-REST-ORDER-005 |
| FR-076 | US-REST-DRV-001 |
| FR-077 | US-REST-DRV-002 |
| FR-078 | US-REST-DRV-003, US-CROSS-RT-002 |
| FR-079 | US-REST-DRV-004 |
| FR-080 | US-REST-SET-001 |
| FR-081 | US-REST-SET-002 |
| FR-082 | US-REST-SET-003 |
| FR-083 | US-REST-SET-004 |
| FR-084 | US-REST-SET-005 |
| FR-085 | US-REST-PAY-001 |
| FR-086 | US-REST-PAY-002 |
| FR-087 | US-REST-CUST-001 |
| FR-088 | US-REST-PROMO-001 |
| FR-089 | US-REST-PROMO-002, US-CROSS-PUSH-002 |
| FR-090 | US-REST-PROMO-003 |
| FR-091 | US-REST-REPORT-001 |
| FR-092 | US-REST-REPORT-002 |
| FR-093 | US-REST-REPORT-003 |
| FR-094 | US-REST-SUPP-001 |
| FR-095 | US-REST-CONFIG-001, US-CROSS-BRAND-001 |
| FR-096 | US-REST-CONFIG-002 |

---

*Document generated from PROJECT_SCOPE.md v1.1. All 96 functional requirements (FR-001 through FR-096) are mapped to user stories with full acceptance criteria. Cross-cutting stories cover multi-language, RTL, real-time updates, push notifications, white-label branding, security, compliance, performance, and the customer web interface.*
