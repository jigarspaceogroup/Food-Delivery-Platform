# Product Requirements Document (PRD)

# Food Delivery Platform - White-Label Solution

---

| Field | Detail |
|---|---|
| **Product Name** | Food Delivery Platform (White-Label) |
| **Version** | v1.0 MVP |
| **Document Status** | Draft |
| **Last Updated** | March 16, 2026 |
| **Authors** | Nael Mattar (Product Owner), Space-O Technologies (Vendor) |
| **Stakeholders** | Nael Mattar (Client), Space-O Technologies (Development), Restaurant Operations Team, QA Team |
| **Based On** | PROJECT_SCOPE.md v1.1, SOW dated 28th August 2025 |

---

## 1. Overview

### 1.1 Product Summary

The Food Delivery Platform is a comprehensive white-label food delivery solution designed for individual restaurants operating in the Saudi Arabian market. The platform enables restaurants to manage their own branded food delivery operations, eliminating dependency on third-party commission-based platforms such as Talabat and HungerStation.

The platform consists of three interconnected applications:

1. **Customer Application** (Android via React Native + Lightweight Web via React.js) -- Enables customers to browse menus, place orders, make payments, and track deliveries in real time.
2. **Driver Application** (Android via React Native) -- Enables delivery personnel to receive assignments, navigate to customers, and confirm deliveries.
3. **Restaurant Dashboard** (Web via React.js) -- Enables restaurant administrators to manage menus, process orders, assign drivers, run promotions, and view analytics.

### 1.2 Document Purpose

This PRD translates the project scope into detailed, developer-ready requirements. It covers user stories with acceptance criteria, feature specifications with screen-level detail, data models, API integrations, non-functional requirements, and release strategy. This document serves as the single source of truth for design, development, QA, and stakeholder alignment.

### 1.3 Technology Stack Summary

| Layer | Technology |
|---|---|
| Customer Mobile App | React Native (Android) |
| Customer Web App | React.js (lightweight) |
| Driver Mobile App | React Native (Android) |
| Restaurant Dashboard | React.js (responsive) |
| Backend API | Node.js / Express.js |
| Database | PostgreSQL |
| Real-Time Communication | Socket.io |
| Authentication | Firebase Authentication (OTP/phone), JWT |
| Push Notifications | Firebase Cloud Messaging (FCM) |
| Payments | Stripe (credit/debit, Mada, Google Pay), STC Pay |
| Maps & Navigation | Google Maps API |
| File Storage | AWS S3 |
| Cloud Hosting | AWS (Bahrain region, me-south-1) |
| Containerization | Docker |
| CI/CD | To be determined during development |

---

## 2. Problem Statement

### 2.1 Market Problem

Restaurants in Saudi Arabia currently rely heavily on third-party food delivery platforms such as Talabat and HungerStation to reach customers. These platforms charge commissions ranging from 15% to 30% per order, significantly reducing restaurant profit margins. Additionally, restaurants on these platforms:

- **Lose ownership of customer relationships** -- Customer data belongs to the platform, not the restaurant.
- **Have limited branding control** -- The restaurant's identity is subordinated to the platform's brand.
- **Cannot control the delivery experience** -- Quality of delivery is at the mercy of the platform's driver pool.
- **Face competitive disadvantage** -- Restaurants are listed alongside competitors, making differentiation difficult.
- **Have no direct communication channel** -- Marketing and promotions must go through the platform's systems.

### 2.2 User Problems

**For Customers:**
- Inconsistent delivery experiences across different platform providers
- Limited visibility into order preparation status
- Generic loyalty programs that do not build restaurant-specific brand affinity
- Language and cultural UX issues with international platforms operating in Saudi Arabia

**For Restaurants:**
- High commission fees (15-30%) eroding margins on every order
- No direct access to customer data for marketing and retention
- Inability to customize the ordering and delivery experience to match brand identity
- Dependence on third-party platforms for a critical revenue channel
- Limited control over delivery zone definitions, fee structures, and operational parameters

**For Drivers:**
- Working under third-party platforms with limited direct restaurant relationship
- Inconsistent assignment and tracking systems
- No direct communication channel with the restaurant they serve

### 2.3 Opportunity

By building an owned, white-label food delivery platform, restaurants can:
- Eliminate 15-30% commission fees, recovering significant margin
- Own customer relationships and data
- Control the entire ordering and delivery experience under their brand
- Build direct loyalty and retention programs
- Scale the platform across multiple branch locations
- Achieve competitive feature parity with established apps (Maestro, Herfy, Albaik)

---

## 3. Product Vision & Goals

### 3.1 Product Vision

To empower individual restaurant brands in Saudi Arabia with a fully owned, white-label food delivery platform that provides a seamless ordering experience for customers, efficient delivery management for drivers, and comprehensive operational control for restaurant operators -- all without third-party commission overhead.

### 3.2 Strategic Goals

| # | Goal | Description |
|---|---|---|
| G-001 | Eliminate Third-Party Dependency | Provide a complete alternative to Talabat/HungerStation for direct restaurant-to-customer ordering |
| G-002 | Customer Ownership | Give restaurants full ownership of customer data, relationships, and communication channels |
| G-003 | Brand Control | Enable restaurants to present a fully branded ordering experience (white-label) |
| G-004 | Operational Efficiency | Streamline order processing, delivery management, and kitchen coordination through a unified dashboard |
| G-005 | Market Localization | Deliver a best-in-class Arabic/RTL experience tailored to the Saudi market |
| G-006 | Payment Flexibility | Support all major Saudi payment methods (Mada, STC Pay, Google Pay, credit/debit, COD) |
| G-007 | Real-Time Experience | Provide real-time order tracking and GPS-based delivery monitoring |
| G-008 | Scalable Architecture | Build a platform that can be deployed across multiple restaurant brands and branch locations |
| G-009 | Customer Conversion | Optimize guest-to-registered-customer conversion through minimized signup friction |
| G-010 | Data-Driven Operations | Provide restaurants with comprehensive analytics and reporting for business decisions |

### 3.3 Key Performance Indicators (KPIs)

| KPI | Target | Measurement |
|---|---|---|
| Successful Google Play Store Deployment | All apps published and approved | Binary |
| Payment Processing Success Rate | All 5 payment methods (Mada, Google Pay, STC Pay, credit/debit, COD) processing correctly | Transaction success rate > 99% |
| Real-Time GPS Tracking Uptime | GPS tracking functional for all active deliveries | Tracking availability > 99.5% |
| Arabic/RTL Interface Quality | Pass comprehensive localization testing | Zero critical RTL/Arabic bugs at launch |
| Guest Browse-to-Registration Conversion | Operational conversion flow | Conversion rate tracked (baseline TBD) |
| VAT-Compliant Receipt Generation | 100% of completed orders generate compliant receipts | Audit compliance rate |
| PCI Compliance | Pass PCI DSS assessment | Binary |
| Order Completion Rate | Orders successfully delivered end-to-end | Target > 95% |
| Menu Search Response Time | Results returned quickly | < 2 seconds |
| OTP Delivery Time | OTP received promptly | < 60 seconds |
| GPS Location Update Frequency | Driver location refreshes on customer map | Every 10-15 seconds |

---

## 4. Target Users & Personas

### 4.1 Persona: Customer (End Consumer)

| Attribute | Detail |
|---|---|
| **Name** | Fatima Al-Rashidi (representative persona) |
| **Age Range** | 18-45 |
| **Location** | Saudi Arabia (urban areas: Riyadh, Jeddah, Dammam) |
| **Language** | Arabic (primary), English (secondary) |
| **Device** | Android smartphone (primary), Desktop/laptop browser (secondary) |
| **Tech Savviness** | Moderate to high; familiar with food delivery apps (Talabat, HungerStation, Jahez) |
| **Primary Goals** | Browse menus, place orders quickly, track deliveries, get deals |
| **Pain Points** | High delivery fees, slow apps, poor Arabic UX, lack of favorite restaurant loyalty |
| **Usage Pattern** | Mobile-first; orders 2-5 times per week; browses during lunch/dinner peaks |
| **Key Behaviors** | Compares prices, uses promo codes, saves favorite items, expects fast checkout |

### 4.2 Persona: Driver (Delivery Personnel)

| Attribute | Detail |
|---|---|
| **Name** | Ahmed Al-Dosari (representative persona) |
| **Age Range** | 20-40 |
| **Location** | Saudi Arabia (urban areas) |
| **Language** | Arabic (primary), basic English |
| **Device** | Android smartphone (mid-range, used while driving) |
| **Tech Savviness** | Low to moderate; needs simple, intuitive interface |
| **Primary Goals** | Receive delivery assignments, navigate to customers efficiently, complete deliveries, track performance |
| **Pain Points** | Confusing navigation, unclear delivery instructions, no direct restaurant support, difficulty reporting issues |
| **Usage Pattern** | On-the-go; uses app during entire shift (4-8 hours); one-hand operation while at stops |
| **Key Behaviors** | Checks availability toggle, accepts/declines orders quickly, uses built-in navigation, calls customers for unclear addresses |

### 4.3 Persona: Restaurant Admin (Business Operator)

| Attribute | Detail |
|---|---|
| **Name** | Khalid bin Nasser (representative persona) |
| **Age Range** | 25-55 |
| **Location** | Saudi Arabia |
| **Language** | Arabic (primary), English (business) |
| **Device** | Desktop computer (primary), tablet (secondary) |
| **Tech Savviness** | Moderate; familiar with web dashboards and POS systems |
| **Primary Goals** | Manage menu, process orders efficiently, assign drivers, monitor sales, run promotions |
| **Pain Points** | High platform commissions, lack of customer data ownership, limited operational control, manual reporting |
| **Usage Pattern** | Desktop-first; uses dashboard throughout business hours; peak usage during order rush hours |
| **Key Behaviors** | Monitors order board constantly, updates menu availability in real-time, reviews daily sales reports, manages driver schedules |

---

## 5. User Stories & Use Cases

All 96 functional requirements from the Project Scope Document are converted into user stories below. Each user story follows the format:

> **US-[MODULE]-[###]**: As a [persona], I want to [action], so that [benefit].

**Priority Levels:**
- **P0** -- Must-have for MVP launch. Blocking.
- **P1** -- Important for MVP but can be delivered in a fast-follow if needed.
- **P2** -- Nice-to-have for MVP. Can be deferred without blocking launch.

---

### 5.1 Customer Authentication & Registration (CUST-AUTH)

**US-CUST-AUTH-001: Guest Menu Browsing** (FR-001)
- **Priority:** P0
- As a **customer**, I want to browse the full restaurant menu, view items, and see prices without creating an account, so that I can decide what to order before committing to registration.
- **Acceptance Criteria:**
  - **Given** a user opens the app for the first time without logging in, **When** they land on the home screen, **Then** the full menu with categories, items, images, and prices is displayed.
  - **Given** a guest user is browsing, **When** they tap on any menu item, **Then** the full product detail page (images, description, price, nutrition info) is shown.
  - **Given** a guest user tries to add an item to the cart, **When** they tap "Add to Cart," **Then** the item is added to a local cart and they can continue browsing.
  - **Given** a guest user tries to proceed to checkout, **When** they tap "Checkout," **Then** they are prompted to register or log in before continuing.

**US-CUST-AUTH-002: OTP Registration** (FR-002)
- **Priority:** P0
- As a **customer**, I want to register using my phone number or email with OTP verification, so that my account is secure and verified.
- **Acceptance Criteria:**
  - **Given** a user taps "Register," **When** they enter a valid Saudi phone number or email address, **Then** an OTP code is sent via SMS or email within 60 seconds.
  - **Given** an OTP has been sent, **When** the user enters the correct OTP code, **Then** their account is created and they are logged in.
  - **Given** an OTP has been sent, **When** the OTP expires after the configured timeout, **Then** the user sees an expiry message and a "Resend OTP" button.
  - **Given** the user enters an incorrect OTP, **When** they submit it, **Then** an error message is shown and they can retry (up to 3 attempts before cooldown).

**US-CUST-AUTH-003: Social Login** (FR-003)
- **Priority:** P1
- As a **customer**, I want to log in using my Google or Facebook account, so that I can access the app quickly without creating a new password.
- **Acceptance Criteria:**
  - **Given** a user is on the login screen, **When** they tap "Continue with Google," **Then** the Google OAuth flow is initiated and upon success the user is logged in.
  - **Given** a user is on the login screen, **When** they tap "Continue with Facebook," **Then** the Facebook OAuth flow is initiated and upon success the user is logged in.
  - **Given** a social login is used for the first time, **When** login succeeds, **Then** a new account is created linked to that social provider.
  - **Given** a social login is used and the email matches an existing account, **When** login succeeds, **Then** the accounts are linked and the user accesses their existing data.

**US-CUST-AUTH-004: Phone/Email Registration** (FR-004)
- **Priority:** P0
- As a **customer**, I want to register with my phone number or email and a password, so that I have a direct login method independent of social providers.
- **Acceptance Criteria:**
  - **Given** a user selects phone/email registration, **When** they enter a valid phone number or email and a password meeting strength requirements, **Then** the registration form is accepted.
  - **Given** valid registration data is submitted, **When** OTP verification completes, **Then** the account is created and the user is logged in.
  - **Given** a phone number or email is already registered, **When** the user tries to register again, **Then** an error message suggests logging in instead.

**US-CUST-AUTH-005: Minimized Signup** (FR-005)
- **Priority:** P0
- As a **customer**, I want the signup process to require only essential information, so that I can start ordering quickly without filling out lengthy forms.
- **Acceptance Criteria:**
  - **Given** a user starts registration, **When** the registration form is displayed, **Then** only name, phone/email, and OTP verification are required (no address, payment, or other fields required at signup).
  - **Given** a user completes minimal registration, **When** they are logged in, **Then** they can immediately browse and add items to the cart.
  - **Given** a user has not added an address, **When** they attempt checkout, **Then** they are prompted to add a delivery address at that point.

**US-CUST-AUTH-006: Arabic-Friendly Interface** (FR-006)
- **Priority:** P0
- As a **customer**, I want the registration and login flow to fully support Arabic language and RTL layout, so that I can use the app comfortably in my native language.
- **Acceptance Criteria:**
  - **Given** the app language is set to Arabic, **When** the registration screen loads, **Then** all labels, placeholders, buttons, and error messages are displayed in Arabic with RTL alignment.
  - **Given** the app is in Arabic mode, **When** the user enters text in Arabic, **Then** text input fields correctly handle RTL text direction.
  - **Given** the app is in Arabic mode, **When** navigation elements are displayed, **Then** the layout mirrors correctly (back button on right, text right-aligned).

**US-CUST-AUTH-007: Profile Completion** (FR-007)
- **Priority:** P1
- As a **customer**, I want to complete my profile by adding delivery addresses, payment preferences, and dietary restrictions, so that my future orders are faster and personalized.
- **Acceptance Criteria:**
  - **Given** a logged-in user navigates to their profile, **When** they tap "Add Address," **Then** a map pin-drop interface is shown for selecting a delivery location.
  - **Given** a user is in profile settings, **When** they add payment preferences, **Then** their preferred payment method is saved for future checkouts.
  - **Given** a user is in profile settings, **When** they set dietary restrictions (e.g., vegetarian, halal-specific, allergies), **Then** these preferences are saved and can be used for menu filtering.

---

### 5.2 Customer Menu Browse & Search (CUST-MENU)

**US-CUST-MENU-001: Category Browsing** (FR-008)
- **Priority:** P0
- As a **customer**, I want to browse the menu organized by categories and subcategories, so that I can find items in a structured, intuitive way.
- **Acceptance Criteria:**
  - **Given** a user is on the menu screen, **When** categories are loaded, **Then** all active categories are displayed with names and optional icons/images.
  - **Given** a category has subcategories, **When** the user taps on a category, **Then** subcategories are shown, and tapping a subcategory shows its menu items.
  - **Given** a category has no subcategories, **When** the user taps on the category, **Then** menu items within that category are listed directly.
  - **Given** a category has zero available items, **When** the category list loads, **Then** the empty category is either hidden or shown with a "No items available" indicator.

**US-CUST-MENU-002: Advanced Search** (FR-009)
- **Priority:** P0
- As a **customer**, I want to search the menu with auto-suggest functionality, so that I can quickly find specific items without browsing through categories.
- **Acceptance Criteria:**
  - **Given** a user taps the search bar, **When** they type 2 or more characters, **Then** auto-suggest results appear in real time below the search bar.
  - **Given** search results are displayed, **When** the user taps on a suggestion, **Then** they are taken to that item's product detail page.
  - **Given** a user submits a search query, **When** results are fetched, **Then** results are returned within 2 seconds.
  - **Given** a user searches for a term with no matches, **When** results load, **Then** a "No items found" message is displayed with a suggestion to browse categories.

**US-CUST-MENU-003: Menu Filtering** (FR-010)
- **Priority:** P1
- As a **customer**, I want to filter menu items by price range, availability, and dietary preferences, so that I can narrow down options to what suits me.
- **Acceptance Criteria:**
  - **Given** a user is viewing a menu category or search results, **When** they tap "Filter," **Then** filter options for price range, availability (in stock), and dietary preferences (vegetarian, gluten-free, etc.) are shown.
  - **Given** filters are applied, **When** the results refresh, **Then** only items matching all selected filters are displayed.
  - **Given** filters result in zero items, **When** the filtered view loads, **Then** a message "No items match your filters" is shown with a "Clear Filters" button.

**US-CUST-MENU-004: Menu Sorting** (FR-011)
- **Priority:** P1
- As a **customer**, I want to sort menu items by different criteria, so that I can order the list in a way that helps me decide.
- **Acceptance Criteria:**
  - **Given** a user is viewing menu items, **When** they tap "Sort," **Then** options include: Price (low to high), Price (high to low), Popularity, Newest, and Rating.
  - **Given** a sort option is selected, **When** the list refreshes, **Then** items are reordered according to the selected criterion.

**US-CUST-MENU-005: Popular Items Section** (FR-012)
- **Priority:** P1
- As a **customer**, I want to see a "Popular Items" section on the home screen, so that I can quickly find trending dishes without searching.
- **Acceptance Criteria:**
  - **Given** a user is on the home screen, **When** the page loads, **Then** a "Popular Items" section is displayed showing the top-selling or most-ordered items.
  - **Given** the popular items section is visible, **When** the user taps on an item, **Then** they are taken to that item's product detail page.
  - **Given** the restaurant has no order history yet, **When** the popular section loads, **Then** it shows featured/recommended items instead or is hidden.

**US-CUST-MENU-006: Product Detail View** (FR-013)
- **Priority:** P0
- As a **customer**, I want to view detailed information about a menu item including images, description, pricing, and nutrition/allergy information, so that I can make an informed ordering decision.
- **Acceptance Criteria:**
  - **Given** a user taps on a menu item, **When** the product detail page loads, **Then** it displays: item image(s), name, description, price, nutrition information, and allergy warnings.
  - **Given** the product has multiple images, **When** the detail page loads, **Then** images are shown in a swipeable carousel.
  - **Given** the product has allergy information, **When** the detail page loads, **Then** allergens are clearly labeled with icons and text.

**US-CUST-MENU-007: Item Customization** (FR-014)
- **Priority:** P0
- As a **customer**, I want to customize menu items by selecting size, toppings, spice level, and adding special instructions, so that I get the order exactly as I want it.
- **Acceptance Criteria:**
  - **Given** a user is on a product detail page with customization options, **When** options load, **Then** each variant type (size, toppings, spice level) is displayed with clear icons and toggle controls.
  - **Given** a variant has additional cost, **When** the user selects it, **Then** the price updates in real time to reflect the total.
  - **Given** a user wants to add special instructions, **When** they tap the "Special Instructions" field, **Then** a free-text input is available (max 200 characters).
  - **Given** required customizations exist (e.g., must choose a size), **When** the user tries to add to cart without selecting, **Then** an error highlights the required field.

**US-CUST-MENU-008: Save Favorites** (FR-015)
- **Priority:** P1
- As a **customer**, I want to save menu items as favorites, so that I can quickly find and reorder items I like.
- **Acceptance Criteria:**
  - **Given** a logged-in user is on a product detail page or menu list, **When** they tap the heart/favorite icon, **Then** the item is added to their favorites list.
  - **Given** a user has saved favorites, **When** they navigate to the Favorites screen, **Then** all favorited items are listed with images, names, and prices.
  - **Given** a guest user tries to favorite an item, **When** they tap the favorite icon, **Then** they are prompted to log in or register.
  - **Given** a favorited item becomes unavailable, **When** the favorites list loads, **Then** the item is shown with an "Unavailable" badge.

---

### 5.3 Customer Cart & Checkout (CUST-CART)

**US-CUST-CART-001: Cart Management** (FR-016)
- **Priority:** P0
- As a **customer**, I want to add, remove, and edit items in my cart with inline quantity controls, so that I can adjust my order easily before checkout.
- **Acceptance Criteria:**
  - **Given** a user adds an item to the cart, **When** the cart is viewed, **Then** the item appears with name, customizations, quantity, and line total.
  - **Given** an item is in the cart, **When** the user taps +/- buttons, **Then** the quantity updates inline and the cart total recalculates instantly.
  - **Given** the user decreases quantity to zero, **When** the quantity reaches 0, **Then** the item is removed from the cart with a confirmation prompt.
  - **Given** the cart is empty, **When** the user views the cart, **Then** an empty state message is shown with a "Browse Menu" button.

**US-CUST-CART-002: Promo Code Application** (FR-017)
- **Priority:** P0
- As a **customer**, I want to apply a promo code to my order, so that I can receive a discount.
- **Acceptance Criteria:**
  - **Given** a user is in the cart or checkout screen, **When** they enter a valid promo code and tap "Apply," **Then** the discount is applied and the cart total is recalculated showing the discount amount.
  - **Given** an invalid or expired promo code is entered, **When** the user taps "Apply," **Then** an error message explains why the code is invalid (expired, minimum not met, not applicable).
  - **Given** a promo code has a minimum order requirement, **When** the cart subtotal is below the minimum, **Then** the code is rejected with a message showing the minimum amount needed.
  - **Given** a promo code is successfully applied, **When** the user removes items reducing the total below the minimum, **Then** the promo code is automatically removed with a notification.

**US-CUST-CART-003: VAT Display** (FR-018)
- **Priority:** P0
- As a **customer**, I want to see VAT calculations upfront in the cart total, so that I know the full cost before checkout.
- **Acceptance Criteria:**
  - **Given** a user has items in the cart, **When** the cart summary is displayed, **Then** the VAT amount (15%) is calculated and shown as a separate line item.
  - **Given** VAT is displayed, **When** the total is shown, **Then** the breakdown includes: Subtotal, Discount (if any), VAT (15%), Delivery Fee, and Grand Total.

**US-CUST-CART-004: Upsell Prompts** (FR-019)
- **Priority:** P1
- As a **customer**, I want to see "Frequently ordered together" suggestions, so that I can discover complementary items and have a better meal.
- **Acceptance Criteria:**
  - **Given** a user adds an item to the cart, **When** rule-based upsell rules match, **Then** a suggestion bar or modal shows complementary items (e.g., "Add a drink?" or "Customers also ordered...").
  - **Given** an upsell suggestion is shown, **When** the user taps "Add," **Then** the suggested item is added to the cart.
  - **Given** an upsell suggestion is shown, **When** the user taps "No thanks" or dismisses it, **Then** the suggestion disappears and does not reappear for that session.

**US-CUST-CART-005: Delivery/Pickup Toggle** (FR-020)
- **Priority:** P0
- As a **customer**, I want to toggle between home delivery and restaurant pickup, so that I can choose the most convenient option.
- **Acceptance Criteria:**
  - **Given** a user is on the cart or checkout screen, **When** they see the order type toggle, **Then** two options are available: "Delivery" and "Pickup."
  - **Given** the user selects "Delivery," **When** the toggle is set, **Then** the address selection and delivery fee sections are shown.
  - **Given** the user selects "Pickup," **When** the toggle is set, **Then** the delivery fee is removed, the address section is hidden, and branch selection is shown.

**US-CUST-CART-006: Order Scheduling** (FR-021)
- **Priority:** P1
- As a **customer**, I want to schedule a delivery or pickup for a future time, so that I can plan my meals in advance.
- **Acceptance Criteria:**
  - **Given** a user is on the checkout screen, **When** they see the delivery time option, **Then** they can choose "ASAP" or "Schedule for Later."
  - **Given** the user selects "Schedule for Later," **When** the date/time picker appears, **Then** only available time slots within operating hours are selectable.
  - **Given** a scheduled order is placed, **When** the order is confirmed, **Then** the confirmation shows the scheduled date and time.

**US-CUST-CART-007: ETA Display** (FR-022)
- **Priority:** P0
- As a **customer**, I want to see the estimated delivery or pickup time, so that I know when to expect my food.
- **Acceptance Criteria:**
  - **Given** a user has selected delivery with an address, **When** the checkout screen loads, **Then** an ETA is displayed (e.g., "Estimated delivery: 30-45 min").
  - **Given** a user has selected pickup, **When** the checkout screen loads, **Then** an estimated preparation time is displayed.
  - **Given** the restaurant is experiencing high volume, **When** ETA is calculated, **Then** the estimate reflects increased preparation times.

**US-CUST-CART-008: Branch Map** (FR-023)
- **Priority:** P1
- As a **customer**, I want to see a map of restaurant branches with a curbside pickup option, so that I can choose the nearest location for pickup.
- **Acceptance Criteria:**
  - **Given** a user selects "Pickup" as the order type, **When** the branch selection screen loads, **Then** a map is displayed showing all active restaurant branches with pins.
  - **Given** a map is displayed, **When** the user taps a branch pin, **Then** branch details (name, address, distance, operating hours) are shown.
  - **Given** a branch supports curbside pickup, **When** the branch details are shown, **Then** a "Curbside Pickup" toggle is available.

**US-CUST-CART-009: Address Selection** (FR-024)
- **Priority:** P0
- As a **customer**, I want to select from my saved delivery addresses or add a new one via map pin-drop, so that I can quickly specify where to deliver.
- **Acceptance Criteria:**
  - **Given** a user has saved addresses, **When** the address selection section loads at checkout, **Then** saved addresses are listed with labels (Home, Work, etc.) and the default is pre-selected.
  - **Given** the user wants a new address, **When** they tap "Add New Address," **Then** a map pin-drop interface opens.
  - **Given** the new address is outside the delivery zone, **When** the user selects it, **Then** an error message states the address is not within the delivery area.

**US-CUST-CART-010: One-Page Checkout** (FR-025)
- **Priority:** P0
- As a **customer**, I want to complete my entire checkout on a single page with a progress indicator, so that the process is fast and transparent.
- **Acceptance Criteria:**
  - **Given** a user taps "Checkout" from the cart, **When** the checkout page loads, **Then** all sections (delivery/pickup type, address, delivery time, payment method, order summary) are visible on a single scrollable page.
  - **Given** the checkout page is displayed, **When** the user scrolls, **Then** a progress indicator at the top shows which section they are on (e.g., Address > Payment > Review).
  - **Given** a required section is incomplete, **When** the user tries to place the order, **Then** the page scrolls to the incomplete section with validation errors highlighted.

**US-CUST-CART-011: Fee Transparency** (FR-026)
- **Priority:** P0
- As a **customer**, I want to see a comprehensive order summary showing all fees, so that there are no surprises at payment.
- **Acceptance Criteria:**
  - **Given** a user is on the checkout page, **When** the order summary section loads, **Then** it displays: Subtotal, Discount (if promo applied), VAT (15%), Delivery Fee (zone-based, or "Free" for pickup), and Grand Total.
  - **Given** the delivery fee varies by zone, **When** the fee is shown, **Then** it reflects the fee for the selected delivery zone.
  - **Given** the order qualifies for free delivery (promotion or minimum order met), **When** the summary loads, **Then** the delivery fee shows as "Free" with strikethrough of the original fee.

---

### 5.4 Customer Payment (CUST-PAY)

**US-CUST-PAY-001: Credit/Debit Card Payment** (FR-027)
- **Priority:** P0
- As a **customer**, I want to pay for my order using a credit or debit card, so that I can use my preferred payment method.
- **Acceptance Criteria:**
  - **Given** a user selects "Credit/Debit Card" as the payment method, **When** they enter valid card details (number, expiry, CVV), **Then** the payment is processed via Stripe and a confirmation is shown.
  - **Given** the card payment fails, **When** the error is returned, **Then** a clear error message is shown (e.g., "Card declined. Please try another card.").
  - **Given** the payment is processing, **When** the user waits, **Then** a loading indicator is shown and the "Place Order" button is disabled to prevent double submission.

**US-CUST-PAY-002: Mada Payment** (FR-028)
- **Priority:** P0
- As a **customer**, I want to pay using my Mada debit card, so that I can use Saudi Arabia's national payment network.
- **Acceptance Criteria:**
  - **Given** a user selects "Mada" as the payment method, **When** they enter their Mada card details, **Then** the payment is processed via Stripe's Mada integration.
  - **Given** a Mada payment succeeds, **When** the confirmation is shown, **Then** the receipt reflects Mada as the payment method.

**US-CUST-PAY-003: Google Pay** (FR-029)
- **Priority:** P1
- As a **customer**, I want to pay using Google Pay, so that I can check out quickly without entering card details.
- **Acceptance Criteria:**
  - **Given** a user has Google Pay set up on their device, **When** they select "Google Pay" at checkout, **Then** the Google Pay sheet appears for confirmation.
  - **Given** the user confirms Google Pay, **When** the payment processes, **Then** the order is placed and a confirmation is shown.
  - **Given** Google Pay is not available on the device, **When** the payment options load, **Then** the Google Pay option is hidden.

**US-CUST-PAY-004: STC Pay** (FR-030)
- **Priority:** P1
- As a **customer**, I want to pay using STC Pay, so that I can use my preferred Saudi digital wallet.
- **Acceptance Criteria:**
  - **Given** a user selects "STC Pay" as the payment method, **When** they initiate payment, **Then** the STC Pay flow is triggered (redirect or in-app).
  - **Given** the STC Pay payment is confirmed, **When** the response is received, **Then** the order is placed and a confirmation is shown.
  - **Given** STC Pay payment fails, **When** the error occurs, **Then** an error message is displayed and the user can select another payment method.

**US-CUST-PAY-005: Cash on Delivery** (FR-031)
- **Priority:** P0
- As a **customer**, I want to select Cash on Delivery (COD) as my payment method, so that I can pay when the food arrives.
- **Acceptance Criteria:**
  - **Given** a user selects "Cash on Delivery," **When** they place the order, **Then** the order is confirmed with payment status "Pending - COD."
  - **Given** a COD order is placed, **When** the driver delivers, **Then** the driver confirms cash collection and the order payment status updates to "Collected."

**US-CUST-PAY-006: Saved Cards** (FR-032)
- **Priority:** P1
- As a **customer**, I want to save my payment cards for future orders, so that I do not have to re-enter card details each time.
- **Acceptance Criteria:**
  - **Given** a user completes a card payment, **When** a "Save this card" checkbox is checked, **Then** the card (last 4 digits, brand) is saved to their account via Stripe tokenization.
  - **Given** a user has saved cards, **When** they check out again, **Then** saved cards are listed for quick selection.
  - **Given** a user wants to remove a saved card, **When** they go to payment settings and tap "Remove," **Then** the card is deleted from their saved methods.

**US-CUST-PAY-007: Quick Payment Selection** (FR-033)
- **Priority:** P1
- As a **customer**, I want a fast payment method selection UI, so that checkout is quick and seamless.
- **Acceptance Criteria:**
  - **Given** a user reaches the payment section of checkout, **When** payment methods load, **Then** all available methods (saved cards, Mada, Google Pay, STC Pay, COD) are shown as selectable options with icons.
  - **Given** the user has a default payment method, **When** checkout loads, **Then** the default method is pre-selected.
  - **Given** the user taps a payment method, **When** it is selected, **Then** a checkmark indicates the selection and the total updates if applicable.

---

### 5.5 Customer Order Tracking & History (CUST-TRACK)

**US-CUST-TRACK-001: Order Status Tracking** (FR-034)
- **Priority:** P0
- As a **customer**, I want to track my order through every stage (confirmed, preparing, picked up, on the way, delivered), so that I know exactly where my order is.
- **Acceptance Criteria:**
  - **Given** a user has placed an order, **When** they view the order, **Then** a status timeline shows: Order Confirmed > Preparing > Ready for Pickup > Driver Picked Up > On the Way > Delivered.
  - **Given** the order status changes, **When** the restaurant or driver updates it, **Then** the customer's tracking screen updates in real time via Socket.io.
  - **Given** the order is in "On the Way" status, **When** the tracking screen is open, **Then** the driver's live location is shown on a map.

**US-CUST-TRACK-002: Live GPS Tracking** (FR-035)
- **Priority:** P0
- As a **customer**, I want to see my driver's real-time location on a map, so that I can prepare for the delivery arrival.
- **Acceptance Criteria:**
  - **Given** a driver is en route to the customer, **When** the tracking map is displayed, **Then** the driver's position updates every 10-15 seconds.
  - **Given** the tracking map is shown, **When** the driver moves, **Then** the driver icon moves smoothly on the map (interpolated animation).
  - **Given** the driver's GPS is temporarily unavailable, **When** location updates stop, **Then** the last known position is shown with a "Location updating..." indicator.

**US-CUST-TRACK-003: Driver Contact** (FR-036)
- **Priority:** P0
- As a **customer**, I want to call or message my driver directly from the tracking screen, so that I can coordinate delivery details.
- **Acceptance Criteria:**
  - **Given** a driver has been assigned and the order is in transit, **When** the tracking screen is displayed, **Then** "Call Driver" and "Message Driver" buttons are visible.
  - **Given** the user taps "Call Driver," **When** the action triggers, **Then** the phone dialer opens with the driver's number.
  - **Given** the user taps "Message Driver," **When** the messaging interface opens, **Then** the user can send a text message to the driver.

**US-CUST-TRACK-004: Push Notifications for Orders** (FR-037)
- **Priority:** P0
- As a **customer**, I want to receive push notifications for order confirmation, status changes, and delivery alerts, so that I stay informed without keeping the app open.
- **Acceptance Criteria:**
  - **Given** an order is confirmed, **When** the restaurant accepts the order, **Then** a push notification "Your order has been confirmed!" is sent.
  - **Given** the order status changes, **When** each stage transition occurs, **Then** a corresponding push notification is sent (e.g., "Your order is being prepared," "Driver is on the way," "Your order has been delivered").
  - **Given** the driver is near the customer, **When** the driver is within a configured proximity, **Then** a "Driver is arriving" notification is sent.

**US-CUST-TRACK-005: Order History** (FR-038)
- **Priority:** P0
- As a **customer**, I want to view my complete past order history, so that I can review what I have ordered before.
- **Acceptance Criteria:**
  - **Given** a logged-in user navigates to "Order History," **When** the screen loads, **Then** all past orders are listed in reverse chronological order with date, items summary, total, and status.
  - **Given** the user taps on a past order, **When** the detail view opens, **Then** full order details are shown (items, customizations, prices, address, payment method, delivery time).
  - **Given** the user has no past orders, **When** the order history screen loads, **Then** an empty state message is shown: "No orders yet. Start ordering!"

**US-CUST-TRACK-006: Reorder Function** (FR-039)
- **Priority:** P1
- As a **customer**, I want a one-click reorder button on past orders, so that I can quickly repeat a previous order.
- **Acceptance Criteria:**
  - **Given** a user views a past order, **When** they tap "Reorder," **Then** all items from that order are added to the cart with the same customizations.
  - **Given** a reorder is triggered but some items are no longer available, **When** the cart is populated, **Then** available items are added and unavailable items are flagged with a message.
  - **Given** item prices have changed since the original order, **When** the reorder cart loads, **Then** current prices are used and the user is notified of any price changes.

**US-CUST-TRACK-007: VAT-Compliant Receipts** (FR-040)
- **Priority:** P0
- As a **customer**, I want to view and download VAT-compliant receipts for my orders, so that I have proper documentation for my purchases.
- **Acceptance Criteria:**
  - **Given** an order is completed, **When** the user views the order detail, **Then** a "View Receipt" button is available.
  - **Given** the user taps "View Receipt," **When** the receipt loads, **Then** it contains: restaurant name, VAT registration number, order date, itemized list with prices, VAT amount (15%), total, payment method, and receipt number.
  - **Given** the receipt is displayed, **When** the user taps "Download" or "Share," **Then** the receipt can be downloaded as PDF or shared.

**US-CUST-TRACK-008: Item Ratings & Reviews** (FR-041)
- **Priority:** P1
- As a **customer**, I want to rate and review individual menu items after delivery, so that I can share feedback and help other customers.
- **Acceptance Criteria:**
  - **Given** an order has been delivered, **When** the user views the order detail or receives a prompt, **Then** they can rate each item (1-5 stars) and write a text review.
  - **Given** a user submits a rating, **When** the review is saved, **Then** it is associated with the specific menu item and visible to the restaurant.
  - **Given** a user has already rated an item from a specific order, **When** they try to rate again, **Then** they can update their existing rating.

---

### 5.6 Customer Offers, Addresses & Settings (CUST-MISC)

**US-CUST-MISC-001: Offers Tab** (FR-042)
- **Priority:** P1
- As a **customer**, I want a dedicated offers tab showing all available promotions with one-tap apply, so that I never miss a deal.
- **Acceptance Criteria:**
  - **Given** a user navigates to the "Offers" tab, **When** the screen loads, **Then** all active promotions, discount codes, and special offers are listed with descriptions, expiry dates, and applicable conditions.
  - **Given** an offer is displayed, **When** the user taps "Apply" or "Use Now," **Then** the promo code is automatically applied and the user is directed to the menu or cart.
  - **Given** no offers are currently active, **When** the offers tab loads, **Then** an empty state says "No offers right now. Check back soon!"

**US-CUST-MISC-002: Introductory Offers** (FR-043)
- **Priority:** P1
- As a **new customer**, I want to receive introductory discount offers, so that I am incentivized to place my first order.
- **Acceptance Criteria:**
  - **Given** a user registers for the first time, **When** they log in, **Then** an introductory offer is displayed prominently (e.g., banner, modal) with the discount details.
  - **Given** an introductory offer is available, **When** the new user reaches checkout, **Then** the offer is auto-applied or easily applied with one tap.
  - **Given** the introductory offer has been used, **When** the user tries to use it again, **Then** it is marked as "Already used" and cannot be reapplied.

**US-CUST-MISC-003: Multiple Addresses** (FR-044)
- **Priority:** P0
- As a **customer**, I want to save multiple delivery addresses with labels, so that I can quickly switch between delivery locations.
- **Acceptance Criteria:**
  - **Given** a user navigates to "My Addresses," **When** the screen loads, **Then** all saved addresses are listed with labels (Home, Work, Other) and full address text.
  - **Given** the user taps "Add New Address," **When** the address form opens, **Then** they can enter address details and assign a label.
  - **Given** the user has multiple addresses, **When** they are at checkout, **Then** they can select any saved address.

**US-CUST-MISC-004: Map Pin-Drop** (FR-045)
- **Priority:** P0
- As a **customer**, I want to add a delivery address using a map pin-drop interface, so that I can precisely locate my delivery point.
- **Acceptance Criteria:**
  - **Given** a user taps "Add Address" or "Pin on Map," **When** the map loads, **Then** a draggable pin is placed at the user's current location (if GPS permission is granted).
  - **Given** the user drags the pin, **When** they release it, **Then** the address fields auto-populate via reverse geocoding.
  - **Given** GPS permission is denied, **When** the map loads, **Then** the pin defaults to a city center and the user can search for their address manually.

**US-CUST-MISC-005: Default Address** (FR-046)
- **Priority:** P1
- As a **customer**, I want to set a default delivery address, so that it is pre-selected at checkout for faster ordering.
- **Acceptance Criteria:**
  - **Given** a user has multiple saved addresses, **When** they tap "Set as Default" on an address, **Then** that address is marked as default.
  - **Given** a default address is set, **When** the user proceeds to checkout, **Then** the default address is pre-selected.

**US-CUST-MISC-006: Postal System Integration** (FR-047)
- **Priority:** P2
- As a **customer**, I want address fields to integrate with the official postal system, so that my address information is accurate and standardized.
- **Acceptance Criteria:**
  - **Given** a user is entering an address, **When** they type in the address field, **Then** auto-complete suggestions from the postal system API (Saudi Post/SPL) appear.
  - **Given** the postal API is unavailable, **When** the user enters an address, **Then** manual entry is available as a fallback with no error.

**US-CUST-MISC-007: Notification Preferences** (FR-048)
- **Priority:** P1
- As a **customer**, I want to control which types of notifications I receive and their frequency, so that I only get messages I care about.
- **Acceptance Criteria:**
  - **Given** a user navigates to "Notification Settings," **When** the screen loads, **Then** toggles are shown for: Order Updates, Promotions & Offers, General Announcements.
  - **Given** the user disables "Promotions & Offers," **When** a promotional push is sent, **Then** the user does not receive it.
  - **Given** the user disables all notifications, **When** order-critical updates occur, **Then** in-app notifications still appear when the app is open.

**US-CUST-MISC-008: Language Toggle** (FR-049)
- **Priority:** P0
- As a **customer**, I want to switch between Arabic and English at any time, so that I can use the app in my preferred language.
- **Acceptance Criteria:**
  - **Given** a user is on the settings screen, **When** they select a language (Arabic or English), **Then** the entire app interface switches to that language immediately.
  - **Given** the user switches to Arabic, **When** the interface reloads, **Then** the layout changes to RTL.
  - **Given** the user switches to English, **When** the interface reloads, **Then** the layout changes to LTR.

**US-CUST-MISC-009: Basic Loyalty Program** (FR-050)
- **Priority:** P1
- As a **customer**, I want to earn and redeem loyalty points/cashback on my orders, so that I am rewarded for my continued patronage.
- **Acceptance Criteria:**
  - **Given** a user places an order, **When** the order is delivered, **Then** loyalty points or cashback are credited to their account based on restaurant-configured rules (e.g., X points per SAR spent).
  - **Given** a user has accumulated points, **When** they are at checkout, **Then** they can see their points balance and choose to redeem points toward the order total.
  - **Given** the user navigates to the Loyalty screen, **When** it loads, **Then** their current balance, earning history, and redemption history are displayed.
  - **Given** the restaurant has not configured loyalty rules, **When** the loyalty section loads, **Then** it is hidden or shows "Coming soon."

---

### 5.7 Driver App (DRV)

**US-DRV-001: Driver Login** (FR-051)
- **Priority:** P0
- As a **driver**, I want to log in with credentials provided by the restaurant, so that I can access my delivery assignments.
- **Acceptance Criteria:**
  - **Given** a driver opens the app, **When** they enter their restaurant-provided username/ID and password, **Then** they are authenticated and see the driver dashboard.
  - **Given** invalid credentials are entered, **When** the driver taps "Login," **Then** an error message "Invalid credentials. Please contact your restaurant." is shown.
  - **Given** the driver's account has been deactivated, **When** they try to log in, **Then** a message "Your account is inactive. Contact the restaurant." is shown.

**US-DRV-002: Driver Profile** (FR-052)
- **Priority:** P0
- As a **driver**, I want to manage my profile with contact info, vehicle details, and document storage, so that my information is up to date for the restaurant.
- **Acceptance Criteria:**
  - **Given** a logged-in driver navigates to "Profile," **When** the screen loads, **Then** their name, phone, email, vehicle type, license plate, and uploaded documents are displayed.
  - **Given** the driver taps "Edit Profile," **When** they update contact info or vehicle details, **Then** changes are saved and synced with the restaurant dashboard.
  - **Given** the driver needs to upload a document (license, ID), **When** they tap "Upload Document," **Then** a camera/file picker opens and the document is uploaded to AWS S3.

**US-DRV-003: Availability Toggle** (FR-053)
- **Priority:** P0
- As a **driver**, I want to toggle my availability status between online and offline, so that the restaurant knows when I am ready to accept deliveries.
- **Acceptance Criteria:**
  - **Given** a logged-in driver is on the dashboard, **When** they see the availability toggle, **Then** it shows their current status (Online/Offline).
  - **Given** the driver toggles to "Online," **When** the status updates, **Then** they are visible to the restaurant for order assignment and their GPS location starts sharing.
  - **Given** the driver toggles to "Offline," **When** the status updates, **Then** they stop receiving new assignments and GPS sharing stops.

**US-DRV-004: Shift Management** (FR-054)
- **Priority:** P1
- As a **driver**, I want to manage my work schedule and submit leave requests, so that the restaurant can plan delivery coverage.
- **Acceptance Criteria:**
  - **Given** a driver navigates to "Shifts," **When** the screen loads, **Then** their scheduled shifts for the current and upcoming week are displayed.
  - **Given** the driver wants to request leave, **When** they submit a leave request with date and reason, **Then** the request is sent to the restaurant dashboard for approval.
  - **Given** a leave request is approved or denied, **When** the status changes, **Then** the driver receives a notification.

**US-DRV-005: Order Assignment View** (FR-055)
- **Priority:** P0
- As a **driver**, I want to view my assigned deliveries with full order and customer details, so that I have all the information needed for delivery.
- **Acceptance Criteria:**
  - **Given** a driver is online and assigned an order, **When** the assignment notification arrives, **Then** the order detail shows: order items, customer name, delivery address, special instructions, and estimated preparation time.
  - **Given** the driver views an assignment, **When** the detail screen loads, **Then** a map preview shows the route from restaurant to customer.
  - **Given** multiple orders are assigned, **When** the driver views their queue, **Then** orders are listed in priority/sequence order.

**US-DRV-006: Accept/Decline Orders** (FR-056)
- **Priority:** P0
- As a **driver**, I want to accept or decline delivery requests, so that I can manage my workload.
- **Acceptance Criteria:**
  - **Given** a new order assignment is received, **When** the notification appears, **Then** "Accept" and "Decline" buttons are prominently displayed.
  - **Given** the driver taps "Accept," **When** the action is confirmed, **Then** the order is assigned to them and the restaurant is notified.
  - **Given** the driver taps "Decline," **When** they optionally provide a reason, **Then** the order is returned to the restaurant for reassignment.
  - **Given** the driver does not respond within the configured timeout, **When** the timeout expires, **Then** the order is automatically returned for reassignment.

**US-DRV-007: GPS Navigation** (FR-057)
- **Priority:** P0
- As a **driver**, I want built-in GPS navigation to the customer's location, so that I can find the delivery address efficiently.
- **Acceptance Criteria:**
  - **Given** a driver has accepted an order, **When** they tap "Navigate," **Then** turn-by-turn navigation is initiated using Google Maps integration.
  - **Given** navigation is active, **When** the driver follows the route, **Then** real-time directions are displayed with distance and time remaining.
  - **Given** the customer's address is unclear, **When** the driver cannot locate it, **Then** a "Call Customer" button is accessible from the navigation screen.

**US-DRV-008: Real-Time Location Sharing** (FR-058)
- **Priority:** P0
- As a **driver**, I want my live location to be shared with the restaurant and customer, so that they can track my progress.
- **Acceptance Criteria:**
  - **Given** the driver is online and has an active delivery, **When** their location updates, **Then** the GPS position is sent to the server via Socket.io every 10-15 seconds.
  - **Given** location is being shared, **When** the customer opens the tracking screen, **Then** the driver's current position is displayed on the map.
  - **Given** location is being shared, **When** the restaurant views the driver map, **Then** the driver's position is visible in real time.

**US-DRV-009: Delivery Confirmation** (FR-059)
- **Priority:** P0
- As a **driver**, I want to confirm successful delivery completion, so that the order status is updated for the customer and restaurant.
- **Acceptance Criteria:**
  - **Given** the driver arrives at the customer's location, **When** they tap "Confirm Delivery," **Then** the order status is updated to "Delivered."
  - **Given** the order is COD, **When** the driver confirms delivery, **Then** they must also confirm cash collection amount.
  - **Given** delivery is confirmed, **When** the status updates, **Then** both the customer and restaurant receive notifications.

**US-DRV-010: Customer Communication** (FR-060)
- **Priority:** P0
- As a **driver**, I want to call or message the customer directly, so that I can coordinate delivery details (e.g., gate code, parking instructions).
- **Acceptance Criteria:**
  - **Given** a driver has an active delivery, **When** they view the order detail, **Then** "Call Customer" and "Message Customer" buttons are visible.
  - **Given** the driver taps "Call Customer," **When** the dialer opens, **Then** the customer's phone number is pre-filled.
  - **Given** the driver taps "Message Customer," **When** the messaging interface opens, **Then** they can send a text to the customer.

**US-DRV-011: Issue Reporting** (FR-061)
- **Priority:** P0
- As a **driver**, I want to report problems during delivery (customer unavailable, wrong address, order issues), so that the restaurant is informed and can take action.
- **Acceptance Criteria:**
  - **Given** a driver encounters a problem, **When** they tap "Report Issue," **Then** a form appears with issue categories (Customer Unavailable, Wrong Address, Order Damaged, Other).
  - **Given** an issue category is selected, **When** the driver adds optional details and submits, **Then** the report is sent to the restaurant dashboard.
  - **Given** the issue is "Customer Unavailable," **When** submitted, **Then** the restaurant is notified and can provide instructions (wait, return, leave at door).

**US-DRV-012: Performance Dashboard** (FR-062)
- **Priority:** P1
- As a **driver**, I want to view my delivery statistics, completion rates, and customer ratings, so that I can monitor my performance.
- **Acceptance Criteria:**
  - **Given** a driver navigates to "Performance," **When** the screen loads, **Then** it displays: total deliveries (today/week/month), completion rate, average delivery time, and average customer rating.
  - **Given** performance data is available, **When** the driver views it, **Then** trends are shown (e.g., improving/declining metrics).

**US-DRV-013: Restaurant Support Channel** (FR-063)
- **Priority:** P1
- As a **driver**, I want a direct communication channel with restaurant support, so that I can get help with issues during deliveries.
- **Acceptance Criteria:**
  - **Given** a driver is logged in, **When** they tap "Support" or "Contact Restaurant," **Then** a messaging/chat interface opens for direct communication with the restaurant.
  - **Given** the driver sends a support message, **When** submitted, **Then** the restaurant dashboard displays the message in the support queue.

---

### 5.8 Restaurant Web Dashboard (REST)

**US-REST-001: Admin Login** (FR-064)
- **Priority:** P0
- As a **restaurant admin**, I want to securely log in to the web dashboard, so that I can manage all restaurant operations.
- **Acceptance Criteria:**
  - **Given** an admin navigates to the dashboard URL, **When** they enter valid credentials (email/password), **Then** they are authenticated and see the main dashboard.
  - **Given** invalid credentials are entered, **When** login is attempted, **Then** an error message is shown without revealing which field is incorrect.
  - **Given** the session expires, **When** the admin performs an action, **Then** they are redirected to the login page with a "Session expired" message.

**US-REST-002: Dashboard Overview** (FR-065)
- **Priority:** P0
- As a **restaurant admin**, I want a control panel showing orders overview, sales metrics, and operational status, so that I have a quick summary of business health.
- **Acceptance Criteria:**
  - **Given** the admin logs in, **When** the dashboard loads, **Then** it displays: today's order count, today's revenue, active orders, available drivers, and pending issues.
  - **Given** the dashboard is open, **When** a new order comes in, **Then** the order count and active orders update in real time without page refresh.
  - **Given** the admin views the dashboard, **When** sales widgets load, **Then** charts show today's revenue trend, order volume by hour, and top-selling items.

**US-REST-003: Menu CRUD** (FR-066)
- **Priority:** P0
- As a **restaurant admin**, I want to add, edit, and delete menu items with images, descriptions, pricing, and nutrition/allergy info, so that the menu is always current.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Menu Management," **When** they click "Add New Item," **Then** a form opens with fields: name (AR/EN), description (AR/EN), category, price, images (upload), nutrition info, allergy tags, and availability toggle.
  - **Given** the admin edits an item, **When** they save changes, **Then** the updates are reflected in the customer app immediately.
  - **Given** the admin deletes an item, **When** they confirm deletion, **Then** the item is soft-deleted (hidden from menu) and existing orders referencing it remain intact.

**US-REST-004: Category Management** (FR-067)
- **Priority:** P0
- As a **restaurant admin**, I want to create and manage hierarchical menu categories and subcategories, so that the menu is well organized.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Categories," **When** they click "Add Category," **Then** they can enter a category name (AR/EN), assign a parent category (for subcategories), set display order, and upload an icon/image.
  - **Given** categories exist, **When** the admin reorders them via drag-and-drop, **Then** the display order updates in the customer app.
  - **Given** a category has items, **When** the admin tries to delete it, **Then** a warning shows "This category has X items. Reassign or delete items first."

**US-REST-005: Item Variants** (FR-068)
- **Priority:** P0
- As a **restaurant admin**, I want to configure size, topping, and modification variants with individual pricing, so that customers can customize their orders.
- **Acceptance Criteria:**
  - **Given** the admin is editing a menu item, **When** they navigate to the "Variants" tab, **Then** they can add variant groups (e.g., "Size," "Toppings") each with options (e.g., Small/Medium/Large) and individual prices.
  - **Given** a variant group is configured, **When** they set "Required" vs "Optional," **Then** customers must select from required groups before adding to cart.
  - **Given** a variant option has an extra cost, **When** the admin sets the price, **Then** the customer app shows the added cost next to the option.

**US-REST-006: Pricing Management** (FR-069)
- **Priority:** P0
- As a **restaurant admin**, I want to set prices, bulk discounts, and promotional pricing, so that I can control my pricing strategy.
- **Acceptance Criteria:**
  - **Given** the admin is editing a menu item, **When** they set a base price, **Then** the price is displayed to customers in SAR.
  - **Given** the admin wants to set promotional pricing, **When** they enter a discounted price with start/end dates, **Then** the discounted price is shown to customers during the active period with a strikethrough original price.
  - **Given** the admin wants bulk pricing, **When** they set quantity-based discounts, **Then** the discount applies automatically when customers order the qualifying quantity.

**US-REST-007: Availability Control** (FR-070)
- **Priority:** P0
- As a **restaurant admin**, I want to toggle item availability in real time and manage stock levels, so that customers only see items I can currently fulfill.
- **Acceptance Criteria:**
  - **Given** the admin views the menu list, **When** they toggle an item's availability switch, **Then** the item is immediately hidden or shown as "Unavailable" in the customer app.
  - **Given** an item has stock tracking enabled, **When** the stock reaches zero, **Then** the item is automatically marked as unavailable.
  - **Given** the admin re-enables an item, **When** the toggle is switched on, **Then** the item reappears in the customer menu immediately.

**US-REST-008: Order Reception** (FR-071)
- **Priority:** P0
- As a **restaurant admin**, I want to receive incoming orders with real-time notifications, so that I can begin processing immediately.
- **Acceptance Criteria:**
  - **Given** the dashboard is open, **When** a new order is placed, **Then** an audible alert sounds and a visual notification appears on the order board.
  - **Given** a new order notification appears, **When** the admin clicks on it, **Then** the full order details are displayed (items, customizations, customer info, delivery address, payment method).
  - **Given** the admin is on a different dashboard page, **When** a new order arrives, **Then** a persistent notification badge appears on the "Orders" tab with the count of new orders.

**US-REST-009: Order Accept/Reject** (FR-072)
- **Priority:** P0
- As a **restaurant admin**, I want to accept or reject orders based on capacity, so that I only commit to orders I can fulfill.
- **Acceptance Criteria:**
  - **Given** a new order is received, **When** the admin views it, **Then** "Accept" and "Reject" buttons are prominently displayed.
  - **Given** the admin clicks "Accept," **When** the order is accepted, **Then** the order status updates to "Confirmed" and the customer receives a notification.
  - **Given** the admin clicks "Reject," **When** they select a reason (e.g., "Out of stock," "Too busy," "Closing soon"), **Then** the order is cancelled and the customer receives a notification with the reason.

**US-REST-010: Preparation Time Setting** (FR-073)
- **Priority:** P1
- As a **restaurant admin**, I want to set estimated preparation times per order, so that customers and drivers have accurate expectations.
- **Acceptance Criteria:**
  - **Given** the admin accepts an order, **When** they set a preparation time (minutes), **Then** the ETA is updated for the customer and the driver is notified when to pick up.
  - **Given** a default preparation time is configured in settings, **When** an order is accepted without a custom time, **Then** the default time is used.

**US-REST-011: Kitchen Coordination** (FR-074)
- **Priority:** P1
- As a **restaurant admin**, I want tools for coordinating with kitchen staff on order status, so that orders are prepared and dispatched efficiently.
- **Acceptance Criteria:**
  - **Given** orders are being prepared, **When** the admin views the order board, **Then** orders are organized by status columns: New, Preparing, Ready for Pickup, Out for Delivery, Delivered.
  - **Given** an order is ready, **When** the admin moves it to "Ready for Pickup," **Then** the assigned driver receives a notification to pick up the order.

**US-REST-012: Order Lifecycle Tracking** (FR-075)
- **Priority:** P0
- As a **restaurant admin**, I want to track orders from placement through delivery, so that I have complete visibility into every order's progress.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Orders," **When** the order board loads, **Then** all active orders are displayed with current status, time elapsed, customer info, and assigned driver.
  - **Given** an order is in transit, **When** the admin clicks on it, **Then** the driver's current GPS location is shown on a map within the order detail.
  - **Given** the admin wants to view past orders, **When** they filter by date range or status, **Then** completed/cancelled orders are listed with full details.

**US-REST-013: Driver Account Management** (FR-076)
- **Priority:** P0
- As a **restaurant admin**, I want to create and manage driver accounts, so that I control who delivers for my restaurant.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Drivers," **When** they click "Add Driver," **Then** a form opens for: name, phone, email, vehicle type, license plate, and initial password.
  - **Given** a driver account is created, **When** the admin saves it, **Then** the driver can log in to the Driver app with those credentials.
  - **Given** the admin needs to deactivate a driver, **When** they toggle the account status, **Then** the driver cannot log in and is removed from available drivers.

**US-REST-014: Driver Assignment** (FR-077)
- **Priority:** P0
- As a **restaurant admin**, I want to assign deliveries to available drivers, so that orders are dispatched efficiently.
- **Acceptance Criteria:**
  - **Given** an order is ready for pickup, **When** the admin clicks "Assign Driver," **Then** a list of online/available drivers is shown with their current location and active delivery count.
  - **Given** the admin selects a driver, **When** they confirm the assignment, **Then** the driver receives a push notification with the order details.
  - **Given** no drivers are available, **When** the admin tries to assign, **Then** a message "No drivers currently available" is shown.

**US-REST-015: Driver GPS Tracking** (FR-078)
- **Priority:** P0
- As a **restaurant admin**, I want to monitor driver locations in real time on a map, so that I can manage deliveries and provide customer updates.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Driver Map," **When** the map loads, **Then** all online drivers are shown as pins/icons on the map with their current status.
  - **Given** drivers are moving, **When** their locations update, **Then** the map pins move in real time (every 10-15 seconds).
  - **Given** the admin clicks on a driver pin, **When** the detail opens, **Then** the driver's name, current delivery (if any), and contact info are shown.

**US-REST-016: Driver Performance Monitoring** (FR-079)
- **Priority:** P1
- As a **restaurant admin**, I want to track driver performance metrics, so that I can evaluate and improve delivery operations.
- **Acceptance Criteria:**
  - **Given** the admin views a driver's profile, **When** the performance section loads, **Then** it shows: total deliveries, average delivery time, completion rate, customer rating average, and issue reports.
  - **Given** the admin wants to compare drivers, **When** they view the driver list, **Then** key metrics are shown in columns for easy comparison.

**US-REST-017: Operating Hours Configuration** (FR-080)
- **Priority:** P0
- As a **restaurant admin**, I want to set business operating hours and days, so that customers can only order when we are open.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Business Settings," **When** they edit operating hours, **Then** they can set open/close times for each day of the week, including different hours per day.
  - **Given** operating hours are set, **When** a customer tries to order outside those hours, **Then** a message "Restaurant is currently closed. Opens at [time]" is shown.
  - **Given** the admin needs to close temporarily, **When** they toggle "Temporarily Closed," **Then** the restaurant appears as closed in the customer app immediately.

**US-REST-018: Delivery Zone Configuration** (FR-081)
- **Priority:** P0
- As a **restaurant admin**, I want to define delivery coverage areas on a map, so that customers know whether delivery is available to their address.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Delivery Zones," **When** the map loads, **Then** they can draw polygon zones on the map.
  - **Given** a zone is drawn, **When** the admin names it and sets parameters, **Then** the zone is saved and used for delivery validation.
  - **Given** a customer's address is outside all delivery zones, **When** they select delivery, **Then** they see "Delivery not available to this address."

**US-REST-019: Minimum Order Configuration** (FR-082)
- **Priority:** P0
- As a **restaurant admin**, I want to set minimum order amounts, so that small orders do not result in operational losses.
- **Acceptance Criteria:**
  - **Given** the admin sets a minimum order of X SAR, **When** a customer's cart is below the minimum, **Then** a message "Minimum order is X SAR. Add Y SAR more to proceed." is shown.
  - **Given** a minimum order is configured, **When** the customer meets the minimum, **Then** the checkout button is enabled.

**US-REST-020: Delivery Fee Configuration** (FR-083)
- **Priority:** P0
- As a **restaurant admin**, I want to configure zone-based delivery fees, so that fees reflect the distance and cost of delivery to different areas.
- **Acceptance Criteria:**
  - **Given** delivery zones are defined, **When** the admin edits a zone, **Then** they can set a specific delivery fee for that zone.
  - **Given** zone-based fees are configured, **When** a customer selects a delivery address, **Then** the fee corresponding to their zone is applied.
  - **Given** the admin wants to offer free delivery, **When** they set a zone fee to 0 or create a free delivery promotion, **Then** the delivery fee shows as "Free."

**US-REST-021: Tax Settings** (FR-084)
- **Priority:** P0
- As a **restaurant admin**, I want to configure VAT and tax rates, so that all orders are taxed correctly per Saudi regulations.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Tax Settings," **When** they set the VAT rate (default 15%), **Then** all order totals include VAT calculated at that rate.
  - **Given** the VAT registration number is entered, **When** receipts are generated, **Then** the VAT number appears on all receipts.

**US-REST-022: Payment Processing** (FR-085)
- **Priority:** P0
- As a **restaurant admin**, I want to process and track all transactions, so that I have a clear record of payments.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Payments," **When** the screen loads, **Then** all transactions are listed with: date, order ID, amount, payment method, and status (completed, pending, failed).
  - **Given** the admin filters by date range, **When** the filter is applied, **Then** only transactions within that range are shown.
  - **Given** the admin wants to export payment data, **When** they click "Export," **Then** a CSV/Excel file is downloaded.

**US-REST-023: Refund Management** (FR-086)
- **Priority:** P1
- As a **restaurant admin**, I want to process refunds for technical/payment failures (stuck payments, double charges), so that customers are not incorrectly charged.
- **Acceptance Criteria:**
  - **Given** a payment failure is identified (double charge, stuck payment), **When** the admin initiates a refund, **Then** the refund is processed via the original payment method through Stripe.
  - **Given** a refund is processed, **When** the customer checks their order, **Then** the payment status shows "Refunded" with the refund amount.
  - **Given** the refund scope, **When** the admin attempts a refund, **Then** only technical/payment failure reasons are available (no general order refund workflow in Phase 1).

**US-REST-024: Customer Database** (FR-087)
- **Priority:** P1
- As a **restaurant admin**, I want to view customer registrations and information, so that I understand my customer base.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Customers," **When** the screen loads, **Then** a list of all registered customers is shown with: name, phone, email, registration date, total orders, and total spent.
  - **Given** the admin clicks on a customer, **When** the detail view opens, **Then** their order history, addresses, and loyalty balance are displayed.
  - **Given** the admin wants to search, **When** they enter a name, phone, or email in the search bar, **Then** matching customers are filtered.

**US-REST-025: Promo Engine** (FR-088)
- **Priority:** P0
- As a **restaurant admin**, I want to create discount codes and promotional campaigns, so that I can attract and retain customers.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Promotions," **When** they click "Create Promo," **Then** a form opens with: code, discount type (percentage/fixed), amount, minimum order, usage limit, start/end dates, and target audience (all customers, new customers, specific segment).
  - **Given** a promo is created, **When** a customer applies the code, **Then** the discount is applied per the configured rules.
  - **Given** a promo reaches its usage limit or end date, **When** a customer tries to use it, **Then** the code is rejected with "This code has expired."

**US-REST-026: Push Notification Management** (FR-089)
- **Priority:** P1
- As a **restaurant admin**, I want to send targeted push notifications to customers, so that I can promote offers and engage customers.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Push Notifications," **When** they click "New Notification," **Then** a form opens with: title, body, image (optional), target audience (all, segment, specific customers), and schedule (send now or later).
  - **Given** the notification is sent, **When** customers receive it, **Then** it appears as a push notification on their Android device.
  - **Given** the admin wants to view history, **When** they view sent notifications, **Then** each shows send date, audience size, and delivery count.

**US-REST-027: Email Marketing** (FR-090)
- **Priority:** P2
- As a **restaurant admin**, I want to send email campaigns to customers, so that I can promote the restaurant through another channel.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Email Campaigns," **When** they click "New Campaign," **Then** a form opens with: subject, email body (rich text editor), target audience, and schedule.
  - **Given** the campaign is sent, **When** the emails are delivered, **Then** the admin can see delivery and open rates.

**US-REST-028: Sales Reports** (FR-091)
- **Priority:** P0
- As a **restaurant admin**, I want to generate detailed sales and revenue reports, so that I can analyze business performance.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Reports > Sales," **When** they select a date range, **Then** a report is generated showing: total revenue, order count, average order value, revenue by payment method, and revenue by time period (daily/weekly/monthly).
  - **Given** the report is displayed, **When** the admin clicks "Export," **Then** the data is downloadable as CSV or PDF.
  - **Given** the report includes charts, **When** it loads, **Then** visual graphs show trends over time.

**US-REST-029: Customer Analytics** (FR-092)
- **Priority:** P1
- As a **restaurant admin**, I want customer behavior and segment analytics, so that I can understand ordering patterns and target marketing.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Reports > Customers," **When** the analytics load, **Then** metrics include: new vs returning customers, order frequency distribution, average customer lifetime value, and top customers by spend.
  - **Given** segment data is available, **When** the admin views it, **Then** customers can be grouped by: order frequency, total spend, registration date.

**US-REST-030: Popular Items Analysis** (FR-093)
- **Priority:** P1
- As a **restaurant admin**, I want to track and analyze trending menu items, so that I can optimize my menu and stock.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Reports > Popular Items," **When** the analysis loads, **Then** a ranked list shows items by order count, revenue generated, and trend (rising/falling).
  - **Given** the data is available, **When** the admin selects a time range, **Then** the ranking adjusts to reflect that period.

**US-REST-031: Support Management** (FR-094)
- **Priority:** P1
- As a **restaurant admin**, I want to handle customer inquiries and complaints, so that I can provide good customer service.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Support," **When** the screen loads, **Then** all open support tickets are listed with: customer name, subject, status (Open, In Progress, Resolved), and date.
  - **Given** the admin clicks on a ticket, **When** the detail opens, **Then** the full conversation thread, order reference, and customer info are displayed.
  - **Given** the admin types a response, **When** they send it, **Then** the customer receives a notification.

**US-REST-032: Branding Configuration** (FR-095)
- **Priority:** P1
- As a **restaurant admin**, I want to configure white-label branding elements, so that the platform matches my restaurant's brand identity.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Branding," **When** the configuration page loads, **Then** they can upload: logo, favicon, set primary/secondary colors, app name, and splash screen image.
  - **Given** branding is updated, **When** customers open the app, **Then** the branding reflects the configured logo, colors, and name.

**US-REST-033: Notification Configuration** (FR-096)
- **Priority:** P1
- As a **restaurant admin**, I want to configure system notification preferences, so that I control how and when notifications are sent.
- **Acceptance Criteria:**
  - **Given** the admin navigates to "Notification Settings," **When** the page loads, **Then** they can configure: new order alerts (sound, email, SMS), driver assignment alerts, low stock alerts, and system alerts.
  - **Given** the admin disables email alerts for new orders, **When** a new order comes in, **Then** only the configured channels (e.g., dashboard sound) fire.

---

## 6. Feature Specifications

### 6.1 Customer Authentication & Registration

**Description:** Provides user registration, login, and profile management for customers on both the Android app and lightweight web interface. Supports guest browsing to reduce friction, OTP-based verification for security, social login for convenience, and minimized signup to maximize conversion. Full Arabic/RTL support throughout.

**User Stories Covered:** US-CUST-AUTH-001 through US-CUST-AUTH-007

**Detailed Requirements:**

**Registration Flow (Step-by-Step):**
1. User opens app for the first time and sees the splash screen with restaurant branding.
2. Onboarding carousel (2-3 slides) introduces key features (optional skip).
3. Home screen loads with full menu visible (guest mode).
4. When user attempts an action requiring authentication (checkout, favorites, order history), a registration/login modal appears.
5. Registration options presented: Phone/Email with OTP, Google Login, Facebook Login.
6. If Phone/Email: User enters phone number (Saudi format +966XXXXXXXXX) or email. OTP is sent via Firebase Auth. User enters 6-digit OTP. On success, user enters name (required) and password (optional for phone-only users). Account is created.
7. If Social Login: OAuth flow launches. On first login, account is created. On subsequent logins, existing account is accessed.
8. Post-registration, user is returned to their previous context (e.g., checkout).

**Business Rules:**
- Guest users can browse the full menu, view prices, and add items to a local cart.
- Registration is required for: checkout, favorites, order history, loyalty, ratings.
- OTP expires after 5 minutes. Maximum 3 attempts before 60-second cooldown.
- Phone numbers must be valid Saudi format (+966) or international format.
- Social login email conflicts: If the social login email matches an existing account, the accounts are linked.
- Deactivated accounts cannot log in and see a contact-restaurant message.

**Edge Cases:**
- User loses internet during OTP submission: Show retry option with the entered OTP preserved.
- OTP SMS not received: Provide "Resend OTP" after 60 seconds. Offer email OTP as fallback.
- Social login provider is down: Show error and suggest alternative login methods.
- User tries to register with an already-registered phone/email: Redirect to login with pre-filled identifier.

**UI/UX Requirements:**

**SCR-C-001: Splash Screen**
- Layout: Full screen with restaurant logo (centered), brand colors background, loading indicator at bottom.
- Duration: 2-3 seconds or until initial data loads.
- States: Loading (default), Error (network unavailable -- show retry button).

**SCR-C-002: Onboarding Screens**
- Layout: Swipeable carousel with 2-3 slides. Each slide has an illustration, headline, and description. Dot indicators at bottom. "Skip" button at top-right. "Next" button at bottom. Final slide has "Get Started" button.
- States: First launch only (skipped on subsequent opens).

**SCR-C-003: Login Screen**
- Layout: Restaurant logo at top. "Welcome Back" heading. Phone/email input field (text, required, validation: valid phone or email format). Password field (password type, required, min 8 chars). "Login" button (primary). Divider "or continue with." Google login button (with icon). Facebook login button (with icon). "Forgot Password?" link. "New here? Register" link.
- States: Default, Loading (button shows spinner), Error (field-level validation messages), Network Error (toast).

**SCR-C-004: OTP Verification Screen**
- Layout: "Verify Your Account" heading. Subtitle showing where OTP was sent (masked phone/email). 6 individual digit input fields (auto-advance on entry). Countdown timer for OTP expiry. "Resend OTP" link (disabled until timer ends). "Verify" button (primary).
- States: Default, Countdown active, OTP expired (show resend), Invalid OTP (shake animation on fields, error text), Success (brief checkmark animation, then redirect).

**SCR-C-005: Registration Screen**
- Layout: "Create Account" heading. Full name field (text, required). Phone number field (tel, required, +966 prefix pre-filled). Email field (email, optional). Password field (password, required, min 8 chars, show/hide toggle). "Register" button (primary). Terms & privacy policy checkbox (required). Social login buttons.
- States: Default, Validation errors, Loading, Success.

**Data Requirements:**
- CREATE: User account (name, phone, email, hashed password, auth provider, created_at)
- READ: User profile data, session token validation
- UPDATE: Profile fields (name, dietary restrictions, language preference)
- DELETE: Account deactivation (soft delete)

**Integration Points:**
- Firebase Authentication: OTP sending and verification, phone auth
- Google OAuth: Social login
- Facebook OAuth: Social login
- JWT: Session management after successful authentication

**Permissions/Roles:**
- Guest: Browse menu, view items, add to local cart
- Registered Customer: All guest permissions + checkout, favorites, order history, loyalty, ratings, profile management

---

### 6.2 Menu Browse & Search

**Description:** Enables customers to discover menu items through category navigation, search with auto-suggest, filtering by attributes, and sorting. Displays popular items and allows saving favorites. The menu reflects real-time availability as managed by the restaurant dashboard.

**User Stories Covered:** US-CUST-MENU-001 through US-CUST-MENU-008

**Detailed Requirements:**

**Category Browsing Flow:**
1. Home screen displays top-level categories as scrollable cards/chips.
2. Tapping a category shows its subcategories (if any) or directly lists items.
3. Each item in the list shows: thumbnail image, name, short description, price, and availability badge.
4. Tapping an item navigates to the Product Detail screen (Section 6.3).

**Search Flow:**
1. User taps the search bar at the top of the home or menu screen.
2. The keyboard opens and the search input is focused.
3. After typing 2+ characters, auto-suggest results appear in a dropdown (items matching name or description).
4. User can tap a suggestion to go to that item, or press search to see full results.
5. Full search results page shows matching items in a list/grid with the same card format as category browsing.

**Business Rules:**
- Menu data is fetched from the API and cached locally with a configurable TTL (e.g., 5 minutes).
- Unavailable items are shown at the bottom of the list with an "Unavailable" badge (grayed out).
- Search indexes item names (AR and EN), descriptions, and tags.
- Auto-suggest shows a maximum of 5 suggestions.
- Filters are cumulative (AND logic): selecting "Vegetarian" + "Under 30 SAR" shows only items matching both.
- Popular items are calculated by order count in the last 7 days (configurable).

**Edge Cases:**
- Category with zero items: Show empty state "No items in this category."
- Search with special characters: Sanitize input, treat as literal search.
- Menu loaded during restaurant closed hours: Show menu with an informational banner "Restaurant is currently closed. You can browse the menu."
- Slow network: Show skeleton loading state for menu items.

**UI/UX Requirements:**

**SCR-C-006: Home Screen**
- Layout: Top section: Restaurant logo/name, location selector (if multi-branch), search bar. Promotional banner carousel (auto-scroll, tappable). "Popular Items" horizontal scrollable section. Category grid/list. Bottom navigation bar (Home, Offers, Cart with badge, Orders, Profile).
- States: Loading (skeleton), Loaded, Error (retry button), Restaurant Closed (banner).
- Interactions: Pull-to-refresh to reload menu. Scroll down to see full category list.

**SCR-C-007: Menu Category Screen**
- Layout: Category name as header with back button. Subcategory chips (horizontal scroll, if applicable). Item list (vertical scroll). Each item card: image (left), name + short description (center), price (right), "Add" button.
- States: Loading, Loaded, Empty ("No items in this category"), Error.
- Interactions: Tap item card to go to detail. Tap "Add" for quick add (default options). Long-press for quick-view modal.

**SCR-C-008: Search Screen**
- Layout: Search bar (auto-focused). Auto-suggest dropdown (max 5 items). Search results list (same card format as category screen). Filter button. Sort button. Results count indicator.
- States: Empty (recent searches shown), Typing (auto-suggest appears), Results loaded, No results ("No items found. Try a different search."), Error.
- Filter modal: Price range slider, Availability toggle, Dietary checkboxes (Vegetarian, Vegan, Gluten-free, Spicy, Halal-certified). Apply/Clear buttons.
- Sort options: Relevance (default), Price Low-High, Price High-Low, Popularity, Rating, Newest.

**Data Requirements:**
- READ: Categories (id, name_ar, name_en, image, parent_id, display_order), MenuItems (id, name_ar, name_en, description_ar, description_en, price, images, category_id, is_available, nutrition_info, allergy_tags, popularity_score)
- READ: Search index (item names, descriptions, tags)

**Integration Points:**
- Backend API: GET /categories, GET /categories/:id/items, GET /menu/search?q=, GET /menu/popular
- Local cache: Menu data cached on device for offline browsing capability

**Permissions/Roles:**
- Guest and Registered Customer: Full access to browse and search
- Favorites: Registered Customer only

---

### 6.3 Product Details & Customization

**Description:** Displays complete item information and enables customization (variants, toppings, special instructions) before adding to cart. Shows nutrition and allergy information for informed decisions.

**User Stories Covered:** US-CUST-MENU-006, US-CUST-MENU-007, US-CUST-MENU-008

**Detailed Requirements:**

**Product Detail Flow:**
1. User taps a menu item from any list (category, search, popular, favorites).
2. Product detail screen loads with full-screen hero image, name, description, price.
3. If the item has customization options (variants), they are displayed below the description.
4. User selects required variants (e.g., size) and optional ones (e.g., toppings).
5. Price updates in real time based on selections.
6. User can add special instructions in a text field.
7. User adjusts quantity using +/- controls.
8. User taps "Add to Cart" to add with all customizations.
9. Confirmation toast/animation appears and cart badge updates.

**Business Rules:**
- Required variant groups must be selected before "Add to Cart" is enabled.
- Maximum special instructions length: 200 characters.
- If item is unavailable, "Add to Cart" is replaced with "Unavailable" (disabled).
- Favorite toggle is visible on the detail screen for logged-in users.
- Price display format: SAR with 2 decimal places (e.g., 25.00 SAR).
- Image carousel supports up to 5 images per item.

**Edge Cases:**
- Item becomes unavailable while user is on detail page: Show a real-time banner "This item is no longer available" and disable the add button.
- Item has no customization options: Hide the variants section entirely.
- Item has no images: Show a placeholder image with the restaurant logo.
- User adds same item with different customizations: Both appear as separate cart items.

**UI/UX Requirements:**

**SCR-C-009: Product Detail Screen**
- Layout: Hero image carousel (swipeable, full-width). Back button overlay on image. Favorite (heart) icon overlay on image. Item name (large text). Price (large, bold). Description text. Nutrition info (collapsible section with calories, protein, carbs, fat). Allergy warnings (icon badges: nuts, dairy, gluten, etc.). Variant groups (each with label and options as chips/toggles). Special Instructions text field. Quantity selector (+/- with number). "Add to Cart" button with live total price. Sticky bottom bar with quantity and add button.
- States: Loading (skeleton), Loaded, Unavailable (grayed, disabled add button), Added to cart (brief success animation).
- Form fields: Special Instructions (textarea, optional, max 200 chars). Variant selections (radio for single-select groups, checkbox for multi-select groups). Quantity (number, min 1, max 99).

**Data Requirements:**
- READ: MenuItem full details (id, name_ar, name_en, description_ar, description_en, price, images[], nutrition_info{}, allergy_tags[], is_available, variants[])
- READ: Variant groups and options (group_id, group_name, is_required, options[{id, name, price_modifier}])
- CREATE: Favorite (user_id, menu_item_id)
- DELETE: Unfavorite

**Integration Points:**
- Backend API: GET /menu/:id (full item detail), POST /favorites, DELETE /favorites/:id
- Image CDN: AWS S3/CloudFront for item images

**Permissions/Roles:**
- Guest: View details, add to local cart
- Registered Customer: All above + favorite/unfavorite

---

### 6.4 Shopping Cart & Checkout

**Description:** Manages the shopping cart with inline editing, promo code application, VAT calculation, delivery/pickup selection, address management, order scheduling, and a streamlined one-page checkout experience. Includes upsell prompts and comprehensive fee transparency.

**User Stories Covered:** US-CUST-CART-001 through US-CUST-CART-011

**Detailed Requirements:**

**Cart Management Flow:**
1. User adds items from menu/product detail (items appear in cart with badge count on tab).
2. User taps cart icon/tab to view cart.
3. Cart displays all items with: name, customizations, quantity (+/-), line total, and remove button.
4. User can modify quantity inline (+ and - buttons update total instantly).
5. Upsell suggestions appear based on cart contents (rule-based).
6. Promo code entry field is available.
7. Cart summary shows: Subtotal, Discount, VAT (15%), Delivery Fee, Total.

**Checkout Flow:**
1. User taps "Proceed to Checkout" from cart.
2. If guest, registration/login is required first.
3. One-page checkout loads with all sections visible on scroll.
4. Section 1 - Order Type: Delivery / Pickup toggle.
5. Section 2 - Address (if delivery): Saved addresses or add new. Branch selection (if pickup).
6. Section 3 - Delivery Time: ASAP or Schedule for Later.
7. Section 4 - Payment Method: List of available methods.
8. Section 5 - Order Summary: Full itemized breakdown.
9. User taps "Place Order" to submit.
10. Order confirmation screen appears with order number and ETA.

**Business Rules:**
- Cart persists across app sessions for logged-in users (server-side). Guest cart is local storage only.
- Promo codes: Only one promo code per order. Validation includes: expiry, minimum order, usage limits, target audience.
- VAT is always 15% (configurable by restaurant). Applied to subtotal after discounts.
- Delivery fee is zone-based: determined by the customer's delivery address zone.
- Minimum order validation: Cart must meet minimum before checkout is enabled.
- Order scheduling: Only available within restaurant operating hours. Slots in 15-minute increments.
- ETA calculation: Preparation time (restaurant default or per-order) + estimated delivery time (Google Maps).
- Upsell rules: Configured by restaurant (e.g., "If cart contains Burger, suggest Fries and Drink").

**Edge Cases:**
- Cart item becomes unavailable during checkout: Show alert, remove item, recalculate totals.
- Promo code removed when items change and total drops below minimum: Auto-remove promo with notification.
- Delivery address changes to different zone: Delivery fee updates automatically.
- Restaurant closes during checkout: Show "Restaurant is now closed" modal, offer to schedule for next available time.
- Double-tap on "Place Order": Disable button after first tap to prevent duplicate orders.

**UI/UX Requirements:**

**SCR-C-010: Cart Screen**
- Layout: Cart header with item count. Item list (each row: image thumbnail, name, customization summary, quantity +/-, line total, swipe-to-delete or X button). Upsell section ("You might also like..." horizontal scroll of item cards). Promo code field with "Apply" button. Order summary (Subtotal, Discount, VAT, Delivery Fee, Total). "Proceed to Checkout" button (disabled if below minimum order).
- States: Items in cart (default), Empty cart ("Your cart is empty. Browse the menu!" with CTA button), Loading, Promo applied (green badge showing discount), Promo error (red text below field).
- Interactions: Swipe left on item to reveal delete. Tap +/- for quantity. Tap item name to go back to product detail for editing.

**SCR-C-011: Checkout Screen**
- Layout: Single scrollable page. Progress indicator at top (Address > Time > Payment > Review). Order Type toggle (Delivery/Pickup). Address section (saved address cards, "Add New" button, or branch selector for pickup). Delivery Time section (ASAP radio, Schedule radio with date/time picker). Payment Method section (saved cards, Mada, Google Pay, STC Pay, COD as selectable cards with icons). Order Summary section (itemized list, all fees, grand total). "Place Order" button (fixed at bottom). Terms text ("By placing this order, you agree to our Terms").
- States: Default, Validation errors (highlighted sections), Processing payment (full-screen loader with "Processing your order..."), Error (payment failed modal with retry option).
- Form fields: Delivery/Pickup (radio toggle). Address (selection or map pin-drop). Schedule date (date picker, only future dates during operating hours). Schedule time (time picker, 15-min slots). Payment method (radio selection). Promo code (text input).

**SCR-C-012: Order Confirmation Screen**
- Layout: Success checkmark animation. "Order Confirmed!" heading. Order number (large, prominent). ETA display. Order summary (collapsed, expandable). "Track Order" button (primary). "Continue Shopping" button (secondary). Confetti animation (brief).
- States: Default (success). This screen is a terminal state; back button goes to home.

**Data Requirements:**
- CREATE: Cart (user_id, items[]), Order (user_id, items[], address_id, payment_method, promo_code, delivery_fee, vat, total, status, scheduled_at)
- READ: Cart contents, addresses, promo code validation, delivery fee by zone
- UPDATE: Cart item quantities, applied promo
- DELETE: Cart items

**Integration Points:**
- Backend API: POST /cart, PUT /cart/items/:id, DELETE /cart/items/:id, POST /cart/promo, POST /orders, GET /delivery-fee?zone_id=
- Stripe API: Payment intent creation (Section 6.5)
- Google Maps API: ETA calculation, address validation, zone determination

**Permissions/Roles:**
- Guest: Cart management (local only). Checkout requires registration.
- Registered Customer: Full cart and checkout access.

---

### 6.5 Payment Processing

**Description:** Handles all payment methods for order completion: credit/debit cards, Mada, Google Pay, STC Pay, and Cash on Delivery. Includes saved card management for repeat customers and a quick selection UI for fast checkout.

**User Stories Covered:** US-CUST-PAY-001 through US-CUST-PAY-007

**Detailed Requirements:**

**Payment Flow (Card/Mada):**
1. User selects "Credit/Debit Card" or "Mada" at checkout.
2. If saved card exists, user selects it. Otherwise, card input form appears.
3. User enters card number, expiry, CVV (Stripe Elements handles PCI-compliant input).
4. Optional: "Save this card for future orders" checkbox.
5. User taps "Place Order."
6. Payment intent is created on the backend via Stripe API.
7. Stripe processes the payment (3D Secure if required).
8. On success: Order is created, confirmation shown.
9. On failure: Error displayed, user can retry or choose different method.

**Payment Flow (Google Pay):**
1. User selects "Google Pay" at checkout.
2. Google Pay sheet appears with order total.
3. User authenticates (fingerprint/PIN) and confirms.
4. Payment token is sent to Stripe for processing.
5. On success/failure: Same as card flow.

**Payment Flow (STC Pay):**
1. User selects "STC Pay" at checkout.
2. STC Pay flow is initiated (redirect or in-app SDK).
3. User authenticates within STC Pay.
4. Payment confirmation is sent back.
5. On success/failure: Same as card flow.

**Payment Flow (COD):**
1. User selects "Cash on Delivery."
2. User taps "Place Order."
3. Order is created with payment_status = "pending_cod."
4. Upon delivery, driver confirms cash collection.
5. Payment status updates to "collected."

**Business Rules:**
- All card data is handled via Stripe Elements/SDK. No raw card data touches our servers (PCI compliance).
- Saved cards are stored as Stripe customer payment methods (tokenized). Only last 4 digits and brand are stored locally.
- Google Pay availability is checked at runtime; hidden if not available on device.
- STC Pay integration: If Stripe supports STC Pay natively in Saudi, use Stripe. Otherwise, separate STC Pay SDK integration.
- COD orders may have a maximum order amount limit (restaurant-configurable).
- Currency: SAR (Saudi Riyal). All amounts in SAR with 2 decimal precision.
- Failed payments: Allow up to 3 retry attempts before suggesting a different method.
- Double-charge prevention: Idempotency keys on payment intents.

**Edge Cases:**
- 3D Secure challenge during card payment: Stripe handles the redirect/modal; app waits for result.
- Payment succeeds but order creation fails: Refund the payment automatically, show error, log incident.
- Network loss during payment: Show "Checking payment status..." on reconnect, verify with backend.
- Google Pay not available (older device, not set up): Option is hidden from payment methods.
- STC Pay timeout: Show timeout error, allow retry.

**UI/UX Requirements:**

**SCR-C-013: Payment Method Selection (within Checkout)**
- Layout: Payment section within checkout screen. Each method as a tappable card: icon (Visa/MC/Mada/Google Pay/STC Pay/Cash), name, last 4 digits (for saved cards). Radio button for selection. "Add New Card" option. Selected method highlighted with checkmark.
- States: Default (methods listed), Card input (Stripe Elements form), Processing (spinner on button), Error (red text below method), Success (redirect to confirmation).

**Data Requirements:**
- CREATE: Payment (order_id, method, amount, currency, status, stripe_payment_intent_id, transaction_id)
- READ: Saved payment methods (via Stripe Customer API), Payment status
- UPDATE: Payment status (pending > completed/failed/refunded), COD status (pending > collected)
- DELETE: Saved card (via Stripe API)

**Integration Points:**
- Stripe API: Payment Intents, Customer API (saved cards), Payment Methods, Mada support, Google Pay
- STC Pay API: Payment initiation, confirmation webhook
- Backend: POST /payments/intent, POST /payments/confirm, GET /payments/:id, DELETE /payment-methods/:id

**Permissions/Roles:**
- Registered Customer: Make payments, save cards, view payment history

---

### 6.6 Real-Time Order Tracking

**Description:** Provides customers with live visibility into their order status through every stage (confirmed, preparing, ready, picked up, on the way, delivered) with real-time GPS tracking of the delivery driver on a map. Includes driver contact options and push notification updates.

**User Stories Covered:** US-CUST-TRACK-001 through US-CUST-TRACK-004

**Detailed Requirements:**

**Tracking Flow:**
1. After order confirmation, user is directed to the tracking screen (or can access from order detail).
2. Status timeline at top shows all stages with the current stage highlighted.
3. Status updates are received in real time via Socket.io connection.
4. When order is "On the Way," a map section appears showing driver's live location.
5. Driver location pin updates every 10-15 seconds with smooth animation.
6. Driver contact buttons (Call, Message) appear when driver is assigned.
7. ETA updates dynamically based on driver's real-time location and traffic.
8. On delivery confirmation, status changes to "Delivered" with a rating prompt.

**Business Rules:**
- Socket.io connection is established when tracking screen opens and closed when user navigates away.
- GPS updates frequency: Every 10-15 seconds from driver app to server, relayed to customer.
- Status stages: Order Placed > Confirmed > Preparing > Ready for Pickup > Driver Picked Up > On the Way > Delivered.
- ETA recalculation: Triggered whenever driver location updates significantly (>200m movement).
- Driver contact: Available only after driver is assigned and until delivery is confirmed.
- Push notifications sent at each stage transition (even if app is closed).

**Edge Cases:**
- Driver GPS loses signal: Show last known position with "Updating location..." indicator. Resume when signal returns.
- Order cancelled after tracking starts: Show "Order Cancelled" status with reason.
- Driver changed mid-delivery: Update driver info on tracking screen with new driver's details and location.
- User closes and reopens app during delivery: Reconnect Socket.io, fetch latest status and driver location from API as fallback.
- Very long delivery (> 1 hour): Periodic "Still on the way" notifications.

**UI/UX Requirements:**

**SCR-C-014: Order Tracking Screen**
- Layout: Status timeline (horizontal or vertical) at top with stage icons and labels. Current stage highlighted/animated. ETA display prominently below timeline. Map section (Google Maps) showing: restaurant pin, customer pin, driver pin (moving), route line. Driver info card: driver name, photo, vehicle info, rating. "Call Driver" and "Message Driver" buttons. Order summary (collapsible). "Help" button for support.
- States: Waiting for confirmation (pulsing "Waiting for restaurant..."), Confirmed (checkmark animation), Preparing (kitchen icon), Ready (bag icon), On the Way (map visible, driver moving), Delivered (success animation, rating prompt). Error (Socket.io disconnected: "Reconnecting...").
- Interactions: Tap driver card to see more details. Tap Call/Message for direct contact. Pinch/zoom on map. Tap "View Order" to expand summary. Pull down for manual refresh as backup.

**Data Requirements:**
- READ: Order status (real-time via Socket.io), Driver location (real-time via Socket.io), Order details
- READ (fallback): GET /orders/:id/status, GET /orders/:id/driver-location

**Integration Points:**
- Socket.io: Real-time order status updates (channel: order:{order_id}), Driver location updates (channel: driver:{driver_id}:location)
- Google Maps SDK: Map rendering, driver pin animation, route display, ETA calculation
- Firebase Cloud Messaging: Push notifications for status changes
- Backend API: GET /orders/:id (full order + current status + driver info)

**Permissions/Roles:**
- Registered Customer: Track their own orders only

---

### 6.7 Order History & Ratings

**Description:** Provides customers access to their complete order history with detailed receipt views, one-click reorder functionality, and the ability to rate and review individual menu items after delivery. Receipts are VAT-compliant per Saudi regulations.

**User Stories Covered:** US-CUST-TRACK-005 through US-CUST-TRACK-008

**Detailed Requirements:**

**Order History Flow:**
1. User taps "Orders" in the bottom navigation.
2. Order history list loads showing all past orders in reverse chronological order.
3. Each order row shows: date, order number, items summary (first 2-3 item names), total, and status badge.
4. Tapping an order opens the full order detail.
5. Order detail shows: all items with customizations, pricing breakdown, delivery address, payment method, driver info, timestamps for each status change.
6. "Reorder" button adds all items to cart. "View Receipt" opens the VAT-compliant receipt.

**Rating Flow:**
1. After order delivery, a rating prompt appears (in-app or push notification).
2. User can rate each item individually (1-5 stars).
3. User can write an optional text review per item.
4. User can rate the overall delivery experience.
5. Submitted ratings are visible to the restaurant dashboard.

**Business Rules:**
- Order history is paginated (20 orders per page, infinite scroll).
- Reorder: If items are unavailable, available items are added and a message lists unavailable ones.
- Reorder: Current prices are used, not historical prices. User is notified of price changes.
- Receipts: Must include restaurant name, VAT registration number, order date/time, itemized list with individual prices, subtotal, discount, VAT amount, delivery fee, total, payment method, and unique receipt number.
- Ratings: 1-5 star scale. Review text optional, max 500 characters. One rating per item per order (can be updated).
- Rating window: Users can rate within 7 days of delivery.

**Edge Cases:**
- Reorder with all items unavailable: Show message "None of the items from this order are currently available."
- Receipt for COD order: Payment method shows "Cash on Delivery."
- Rating after 7-day window: "Rating period has ended for this order."

**UI/UX Requirements:**

**SCR-C-015: Order History Screen**
- Layout: "My Orders" heading. Tab filters: Active / Completed / Cancelled. Order list (each card: date, order #, items preview, total, status badge, reorder button). Infinite scroll pagination.
- States: Loading (skeleton), Orders loaded, Empty ("No orders yet. Start ordering!" with browse CTA), Error.

**SCR-C-016: Order Detail Screen**
- Layout: Order # and date at top. Status timeline (completed). Items list with customizations and individual prices. Price breakdown (subtotal, discount, VAT, delivery fee, total). Delivery address. Payment method. Driver info (name, rating). Timestamps (placed, confirmed, picked up, delivered). "Reorder" button. "View Receipt" button. "Rate Items" button (if within rating window).
- States: Loaded, Reorder processing, Receipt loading.

**SCR-C-017: Receipt Screen**
- Layout: Restaurant name and logo. "TAX INVOICE" heading. Receipt number. Date and time. VAT Registration Number. Itemized list (name, qty, unit price, line total). Subtotal. Discount (if any). VAT (15%). Delivery Fee. Grand Total. Payment method. "Download PDF" button. "Share" button.
- States: Loaded, Downloading PDF, Share sheet.

**SCR-C-018: Rating Screen**
- Layout: "Rate Your Order" heading. Order summary. For each item: item name, star rating (1-5, tappable), optional text review field. Overall delivery rating (1-5 stars). "Submit" button.
- States: Default, Partially filled, Submitted (thank you message), Already rated (shows existing ratings, editable).

**Data Requirements:**
- READ: Orders list (paginated), Order detail, Receipt data
- CREATE: Rating (user_id, order_id, menu_item_id, stars, review_text), Receipt PDF generation
- UPDATE: Rating (edit existing)

**Integration Points:**
- Backend API: GET /orders (paginated), GET /orders/:id, GET /orders/:id/receipt, POST /ratings, PUT /ratings/:id
- PDF generation: Server-side receipt PDF generation (or client-side with jsPDF)
- AWS S3: Receipt PDF storage

**Permissions/Roles:**
- Registered Customer: View own order history, rate items, download receipts

---

### 6.8 Offers & Promotions (Customer)

**Description:** Dedicated offers experience for customers showing all available promotions, introductory offers for new users, and easy promo code application. Drives conversion and repeat ordering through discounts.

**User Stories Covered:** US-CUST-MISC-001, US-CUST-MISC-002

**Detailed Requirements:**

**Offers Tab Flow:**
1. User taps "Offers" in the bottom navigation.
2. All active promotions are displayed as cards.
3. Each offer shows: title, description, discount amount, minimum order requirement, expiry date, and applicable items/categories.
4. User taps "Apply" to automatically apply the code and navigate to menu or cart.
5. Introductory offers for new users are shown at the top with special styling.

**Business Rules:**
- Offers are sorted: introductory first, then by expiry (soonest first).
- One-tap apply: Automatically copies the promo code to the cart.
- Expired offers are hidden.
- Offers respect usage limits (per-user and global).
- New customer offers: Shown only to users with zero completed orders.

**Edge Cases:**
- All offers expired: Empty state "No offers right now. Check back soon!"
- Offer applied but cart is empty: Navigate to menu with the code pre-applied.
- User already used a one-time offer: Show it grayed out with "Already used."

**UI/UX Requirements:**

**SCR-C-019: Offers Screen**
- Layout: "Offers" heading. Introductory offer banner (for new users, prominent styling). Offer cards list (each: image/illustration, title, description, discount badge, "Apply" button, expiry countdown). Categories filter (if offers are category-specific).
- States: Loading, Offers available, No offers (empty state), Error.

**Data Requirements:**
- READ: Active promotions list (id, title_ar, title_en, description_ar, description_en, discount_type, discount_amount, min_order, max_uses, uses_count, start_date, end_date, target_audience, applicable_items[])

**Integration Points:**
- Backend API: GET /promotions/active, POST /cart/promo

**Permissions/Roles:**
- Registered Customer: View and apply offers (guest can view but applying requires registration)

---

### 6.9 Address Management

**Description:** Full address management for customers including adding addresses via map pin-drop with reverse geocoding, saving multiple addresses with labels, setting defaults, and postal system integration for Saudi address accuracy.

**User Stories Covered:** US-CUST-MISC-003 through US-CUST-MISC-006

**Detailed Requirements:**

**Add Address Flow:**
1. User navigates to "My Addresses" from profile or initiates "Add Address" during checkout.
2. Map loads centered on user's current location (if GPS permission granted) or city default.
3. Draggable pin is placed on the map.
4. User moves the pin to their exact location.
5. On pin release, reverse geocoding fills address fields (street, city, district, postal code).
6. User reviews/edits auto-filled fields and adds: apartment/floor, building name, delivery instructions.
7. User assigns a label (Home, Work, Other with custom name).
8. User saves the address.

**Business Rules:**
- Maximum 10 saved addresses per user.
- One address must be set as default.
- Labels: Home, Work, and up to 8 custom labels.
- GPS permission: Requested on first use. If denied, manual entry is the fallback.
- Reverse geocoding: Uses Google Maps Geocoding API.
- Postal system integration: Auto-suggest from Saudi Post (SPL) API if available; fallback to manual entry.
- Delivery zone validation: On save, check if address falls within any delivery zone.

**Edge Cases:**
- GPS permission denied: Map centers on a default location (city center); user can search for address.
- Reverse geocoding returns incomplete data: Fields are partially filled; user completes manually.
- Address outside all delivery zones: Warning shown but address can still be saved (for future zones).
- Saudi Post API unavailable: Graceful fallback to manual entry with no error shown.

**UI/UX Requirements:**

**SCR-C-020: Address List Screen**
- Layout: "My Addresses" heading. Address cards (each: label icon, label name, address text, "Default" badge if default, edit/delete buttons). "Add New Address" button. Swipe to delete with confirmation.
- States: Loading, Addresses listed, Empty ("No saved addresses. Add one!"), Error.

**SCR-C-021: Address Add/Edit Screen**
- Layout: Google Map (top half of screen, draggable pin). Address fields below map: Street (text, auto-filled), District (text, auto-filled), City (text, auto-filled), Postal Code (text, auto-filled), Apartment/Floor (text, optional), Building Name (text, optional), Delivery Instructions (textarea, optional, max 200 chars). Label selector (Home/Work/Other chips, custom text input for Other). "Set as Default" toggle. "Save Address" button.
- States: Loading map, Map loaded with pin, Geocoding in progress (spinner on fields), Fields filled, Validation errors, Saving.
- Form validations: Street (required), City (required), Label (required).

**Data Requirements:**
- CREATE: Address (user_id, label, latitude, longitude, street, district, city, postal_code, apartment, building_name, delivery_instructions, is_default)
- READ: User addresses list
- UPDATE: Address fields, default toggle
- DELETE: Address (soft delete)

**Integration Points:**
- Google Maps API: Map display, pin-drop, reverse geocoding
- Saudi Post API (SPL): Address auto-suggest (if available, P2)
- Backend API: GET /addresses, POST /addresses, PUT /addresses/:id, DELETE /addresses/:id

**Permissions/Roles:**
- Registered Customer: Manage own addresses

---

### 6.10 Notifications & Settings

**Description:** Customer notification management including push notification preferences, language toggle between Arabic and English, and general app settings. Ensures users have control over their notification experience.

**User Stories Covered:** US-CUST-MISC-007, US-CUST-MISC-008

**Detailed Requirements:**

**Settings Flow:**
1. User navigates to "Profile" > "Settings."
2. Settings screen shows: Language, Notifications, Account, About.
3. Language section: Toggle between Arabic and English. Change takes effect immediately.
4. Notification section: Toggles for Order Updates, Promotions, General Announcements.
5. Account section: Change password, manage payment methods, delete account.

**Business Rules:**
- Language change: Entire UI switches immediately. Persisted to user profile.
- Notification preferences: Synced with FCM topic subscriptions.
- Order update notifications cannot be fully disabled (critical for order flow); they remain as in-app notifications even if push is disabled.
- Language default: Arabic (based on Saudi market).

**Edge Cases:**
- Language change mid-order: App reloads in new language; active order data preserved.
- Push notification permission denied at OS level: Show guidance to enable in device settings.

**UI/UX Requirements:**

**SCR-C-022: Profile Screen**
- Layout: User avatar/initials. Name. Phone/Email. "Edit Profile" button. Quick links: My Orders, My Addresses, Payment Methods, Favorites, Loyalty Points. Settings link. Logout button.
- States: Loaded, Loading.

**SCR-C-023: Settings Screen**
- Layout: Language section (Arabic/English toggle or radio). Notifications section (toggles: Order Updates, Promotions, Announcements). Account section (Change Password, Payment Methods, Delete Account). About section (Version, Terms, Privacy Policy, Contact Us).
- States: Loaded, Saving (when toggling), Error.

**SCR-C-024: Notifications Screen**
- Layout: "Notifications" heading. List of notifications (each: icon, title, body, timestamp, read/unread indicator). Tap to open related screen (order detail, offer, etc.).
- States: Loading, Notifications listed, Empty ("No notifications yet"), Error.

**Data Requirements:**
- READ: Notification list (user_id, type, title, body, data, read, created_at)
- UPDATE: Notification read status, User preferences (language, notification toggles)

**Integration Points:**
- Firebase Cloud Messaging: Topic subscriptions (promotions, announcements)
- Backend API: GET /notifications, PUT /notifications/:id/read, PUT /users/preferences

**Permissions/Roles:**
- Registered Customer: Manage own settings and preferences

---

### 6.11 Loyalty Program

**Description:** Basic loyalty framework allowing customers to earn and redeem points or cashback on orders. The program rules (points per SAR, redemption rates) are configurable by the restaurant via the dashboard. Phase 1 includes the earning/redemption foundation without complex tiers.

**User Stories Covered:** US-CUST-MISC-009

**Detailed Requirements:**

**Loyalty Earning Flow:**
1. Customer places an order and it is successfully delivered.
2. System calculates loyalty points based on restaurant-configured rules (e.g., 1 point per 10 SAR spent).
3. Points are credited to the customer's loyalty account.
4. Customer receives a notification: "You earned X points on your order!"

**Loyalty Redemption Flow:**
1. At checkout, customer sees their points balance.
2. Customer can choose to redeem points (e.g., 100 points = 10 SAR discount).
3. Redemption reduces the order total.
4. Points are deducted from the loyalty account.

**Business Rules:**
- Points earning: Calculated on order subtotal (before VAT and delivery fees).
- Points are credited only after successful delivery (not on cancelled orders).
- Redemption rate: Configurable by restaurant (e.g., 1 point = 0.10 SAR).
- Minimum redemption: Configurable (e.g., minimum 50 points to redeem).
- Maximum redemption per order: Configurable (e.g., max 50% of order value).
- Points expiry: Configurable (e.g., expire after 12 months of inactivity).
- COD orders earn points only after delivery confirmation.
- If restaurant has not configured loyalty rules, the feature is hidden from customers.

**Edge Cases:**
- Order cancelled after points credited: Points are reversed.
- Partial redemption: Remaining points stay in account.
- Points expire: Notification sent 30 days before expiry.
- Restaurant disables loyalty program: Customer balances are frozen (not lost), feature hidden.

**UI/UX Requirements:**

**SCR-C-025: Loyalty Screen**
- Layout: Current balance (large number with "Points" label). Equivalent value in SAR. "Redeem at Checkout" CTA. Earning history (list: date, order #, points earned/redeemed, balance). Program rules summary (how to earn, how to redeem, expiry policy).
- States: Loading, Loaded, No points yet ("Start earning! Place your first order."), Program not configured (hidden or "Coming soon").

**Data Requirements:**
- READ: LoyaltyAccount (user_id, balance, lifetime_earned, lifetime_redeemed), LoyaltyTransactions (type, points, order_id, created_at)
- CREATE: LoyaltyTransaction (earn)
- UPDATE: LoyaltyAccount balance (earn/redeem)

**Integration Points:**
- Backend API: GET /loyalty/balance, GET /loyalty/transactions, POST /loyalty/redeem
- Order service: Trigger point earning on delivery confirmation

**Permissions/Roles:**
- Registered Customer: View balance, earn and redeem points

---

### 6.12 Driver Authentication & Profile

**Description:** Provides driver login using restaurant-issued credentials and profile management including personal info, vehicle details, and document uploads. Drivers do not self-register; accounts are created by the restaurant admin.

**User Stories Covered:** US-DRV-001, US-DRV-002

**Detailed Requirements:**

**Driver Login Flow:**
1. Driver opens the Driver app.
2. Login screen appears with restaurant branding.
3. Driver enters username/ID and password (provided by restaurant).
4. On success, driver is directed to the dashboard.
5. On failure, error message is shown.

**Profile Management Flow:**
1. Driver navigates to "Profile" from the dashboard.
2. Profile displays: name, phone, email, vehicle type, license plate, uploaded documents.
3. Driver can edit contact info and vehicle details.
4. Driver can upload required documents (driver's license, national ID, vehicle registration).

**Business Rules:**
- Driver accounts are created exclusively by the restaurant admin via the dashboard.
- Password reset: Drivers contact the restaurant to reset their password.
- Document uploads: Stored on AWS S3 with secure URLs.
- Deactivated accounts cannot log in.
- Session: JWT token with configurable expiry (e.g., 7 days).

**Edge Cases:**
- Driver tries to log in with deactivated account: "Your account is inactive. Contact the restaurant."
- Password expired: Force password change on next login (if policy configured).
- Document upload fails: Show retry option, preserve entered data.
- Slow upload (large file): Progress indicator with cancel option.

**UI/UX Requirements:**

**SCR-D-001: Driver Login Screen**
- Layout: Restaurant logo and name. "Driver Login" heading. Username/ID field (text, required). Password field (password, required, show/hide toggle). "Login" button (primary). "Forgot Password? Contact Restaurant" text link.
- States: Default, Loading, Error (invalid credentials), Account inactive error.

**SCR-D-008: Driver Profile Screen**
- Layout: Driver photo/avatar. Name. Phone. Email. Vehicle section (type, license plate). Documents section (list of uploaded docs with status badges: Approved, Pending, Expired). "Edit Profile" button. "Upload Document" button. "Change Password" section.
- States: Loaded, Editing (form mode), Uploading document (progress bar), Error.
- Form fields: Name (text, required). Phone (tel, required). Email (email, optional). Vehicle Type (dropdown: motorcycle, car, bicycle). License Plate (text, required). Document upload (file picker: camera, gallery, files; accepted: JPG, PNG, PDF; max 5MB).

**Data Requirements:**
- READ: Driver profile (id, name, phone, email, vehicle_type, license_plate, documents[], status)
- UPDATE: Driver profile fields, password
- CREATE: Document upload (driver_id, document_type, file_url, upload_date, status)

**Integration Points:**
- Backend API: POST /drivers/login, GET /drivers/profile, PUT /drivers/profile, POST /drivers/documents
- AWS S3: Document file storage
- JWT: Session token management

**Permissions/Roles:**
- Driver: Manage own profile, upload documents

---

### 6.13 Driver Availability & Orders

**Description:** Manages driver availability toggling, shift scheduling, order assignment viewing, and the accept/decline workflow. Enables drivers to control when they receive deliveries and manage their delivery queue efficiently.

**User Stories Covered:** US-DRV-003 through US-DRV-006

**Detailed Requirements:**

**Availability Flow:**
1. Driver logs in and sees their dashboard with availability toggle prominently displayed.
2. Driver toggles "Online" to start receiving delivery assignments.
3. GPS location sharing begins when online.
4. Shift schedule is visible showing upcoming scheduled shifts.
5. Driver can submit leave requests for future dates.

**Order Assignment Flow:**
1. Restaurant assigns an order to the driver.
2. Driver receives a push notification with order summary.
3. App shows order detail: items, customer name, delivery address, distance, estimated time.
4. Driver taps "Accept" or "Decline."
5. If accepted, order moves to active queue with navigation option.
6. If declined (with optional reason), order returns to restaurant for reassignment.
7. If no response within timeout (configurable, default 2 minutes), order auto-returns.

**Business Rules:**
- Online status persists until driver toggles off or logs out.
- Auto-offline: If driver is inactive (no GPS movement) for 30 minutes, prompt to confirm online status.
- Shift management: Restaurant defines shift schedules visible to drivers.
- Leave requests require 24-hour advance notice (configurable).
- Accept/decline timeout: Default 2 minutes, configurable by restaurant.
- Multiple concurrent orders: Configurable maximum (e.g., max 2 concurrent deliveries).

**Edge Cases:**
- Driver accepts but restaurant cancels: Notification sent, order removed from queue.
- Driver goes offline with active delivery: Warning "You have active deliveries. Complete before going offline."
- Network interruption during accept: Retry on reconnection; if timeout passed, order may have been reassigned.
- Driver receives assignment while on active delivery: Shows as queued with priority ordering.

**UI/UX Requirements:**

**SCR-D-002: Driver Home/Dashboard**
- Layout: Availability toggle (large, prominent: green=Online, gray=Offline). Current status indicator. Active delivery card (if any: order #, customer name, address, status, navigate button). Stats summary (today's deliveries, earnings if applicable). New assignment notification card (slides in from top). Queue of upcoming assignments.
- States: Offline (toggle off, no orders), Online waiting (toggle on, no current orders, "Waiting for orders..." message), Active delivery (current order card visible), New assignment (notification card with Accept/Decline), Multiple queued (list of assigned orders).
- Interactions: Toggle availability. Tap assignment for details. Accept/Decline buttons on new assignments. Tap active order for navigation.

**SCR-D-003: Order Detail (Driver)**
- Layout: Order # and time placed. Items list with quantities and customizations. Customer info (name, phone -- masked until accepted). Delivery address with map preview. Special delivery instructions. Distance and estimated time. Accept/Decline buttons (for new assignments). "Navigate" button (for accepted orders). "Call Customer" and "Message Customer" buttons.
- States: New assignment (accept/decline visible), Accepted (navigate and contact visible), Picked up (navigation to customer active), Completed.

**Data Requirements:**
- READ: Driver availability status, shift schedule, assigned orders, order details
- CREATE: Leave request (driver_id, date, reason)
- UPDATE: Availability status (online/offline), Order response (accepted/declined)

**Integration Points:**
- Socket.io: Real-time order assignment notifications, status updates
- Firebase Cloud Messaging: Push notifications for new assignments
- Google Maps API: Distance and time estimation for order preview
- Backend API: PUT /drivers/availability, GET /drivers/shifts, POST /drivers/leave-requests, PUT /orders/:id/respond

**Permissions/Roles:**
- Driver: Manage own availability, view and respond to assigned orders

---

### 6.14 Driver Navigation & Delivery

**Description:** Provides turn-by-turn GPS navigation to customer locations, real-time location sharing with restaurant and customers, and delivery confirmation workflow. Core to the delivery execution experience.

**User Stories Covered:** US-DRV-007 through US-DRV-009

**Detailed Requirements:**

**Navigation Flow:**
1. Driver accepts an order and taps "Navigate."
2. First navigation leg: Restaurant to customer (for picked-up orders). If driver needs to go to restaurant first: restaurant location shown.
3. Turn-by-turn navigation activates via Google Maps integration.
4. Driver's location is shared in real time (every 10-15 seconds) to the server.
5. Customer and restaurant see the driver's location on their respective maps.
6. On arrival, navigation ends and delivery confirmation screen appears.

**Delivery Confirmation Flow:**
1. Driver arrives at customer location.
2. Driver hands over the order.
3. Driver taps "Confirm Delivery."
4. If COD: Driver enters collected amount and confirms.
5. Order status updates to "Delivered."
6. Customer and restaurant receive delivery confirmation notifications.
7. Driver is returned to the dashboard, ready for next assignment.

**Business Rules:**
- Location sharing uses high-accuracy GPS mode (battery-intensive; warn driver).
- Location updates: Every 10-15 seconds via Socket.io.
- Navigation: Uses Google Maps Directions API for routes.
- Delivery confirmation is a single irreversible action.
- COD collection: Driver must confirm the exact amount collected.
- After delivery confirmation, the driver's location stops sharing for that order.

**Edge Cases:**
- GPS signal lost: Use last known location, show "Reconnecting GPS..." to driver.
- Customer unreachable at delivery: Driver uses "Report Issue" flow (Section 6.15).
- Wrong address: Driver contacts customer or reports issue.
- App crashes during delivery: On reopen, active delivery state is restored from server.
- Battery low: Warning to driver to connect charger for GPS accuracy.

**UI/UX Requirements:**

**SCR-D-004: Navigation Screen**
- Layout: Full-screen Google Maps with turn-by-turn navigation overlay. Route highlighted in blue. Current location (blue dot). Destination pin. Bottom card: ETA, distance remaining, customer name and address. "Call Customer" quick action. "End Navigation" button.
- States: Navigating (active turn-by-turn), Arrived (destination reached, prompt to confirm), GPS lost ("Reconnecting...").
- Interactions: Tap bottom card to expand for full address/instructions. Tap call button for customer contact.

**SCR-D-005: Delivery Confirmation Screen**
- Layout: "Confirm Delivery" heading. Order summary (order #, items count). Customer name. "Did you collect cash?" (COD only, with amount field). "Confirm Delivery" button (large, primary). "Report Issue" button (secondary, if there's a problem).
- States: Default, COD input, Confirming (loading), Confirmed (success animation, redirect to dashboard), Error.
- Form fields (COD): Amount collected (number, required for COD, pre-filled with order total).

**Data Requirements:**
- CREATE: Delivery confirmation (order_id, driver_id, timestamp, cod_amount)
- UPDATE: Order status (to "Delivered"), Driver location (real-time)
- READ: Active delivery details, customer location

**Integration Points:**
- Google Maps SDK: Navigation, directions, real-time routing
- Socket.io: Location sharing (emit: driver:{driver_id}:location, payload: {lat, lng, timestamp})
- Backend API: PUT /orders/:id/deliver, PUT /orders/:id/cod-confirm
- Firebase Cloud Messaging: Delivery confirmation notification to customer

**Permissions/Roles:**
- Driver: Navigate, share location, confirm delivery for assigned orders only

---

### 6.15 Driver Communication & Reporting

**Description:** Enables direct communication between drivers and customers (call/message) for delivery coordination, issue reporting for delivery problems, performance tracking dashboard, and a support channel to the restaurant.

**User Stories Covered:** US-DRV-010 through US-DRV-013

**Detailed Requirements:**

**Customer Communication Flow:**
1. Driver taps "Call Customer" on the active delivery screen.
2. Phone dialer opens with customer's number.
3. Alternatively, driver taps "Message Customer" to send an SMS or in-app message.

**Issue Reporting Flow:**
1. Driver encounters a problem during delivery.
2. Driver taps "Report Issue" from the delivery screen.
3. Issue categories presented: Customer Unavailable, Wrong Address, Order Damaged, Cannot Access Location, Vehicle Problem, Other.
4. Driver selects a category.
5. Driver adds optional notes (text field, max 500 chars).
6. Driver can optionally attach a photo (e.g., photo of wrong address, damaged order).
7. Report is submitted and restaurant is notified immediately.
8. Restaurant responds with instructions (wait, return to restaurant, leave at door, cancel).

**Performance Tracking:**
1. Driver navigates to "Performance" from the dashboard.
2. Dashboard shows: deliveries today/this week/this month, completion rate (%), average delivery time, average customer rating, on-time delivery rate.

**Restaurant Support:**
1. Driver taps "Support" from the menu.
2. A simple messaging interface opens.
3. Driver types and sends a message.
4. Messages appear in the restaurant dashboard's support queue.
5. Restaurant responds; driver receives a notification.

**Business Rules:**
- Customer phone numbers are visible to drivers only for active deliveries.
- Issue reports include: driver_id, order_id, category, notes, photo_url, timestamp, GPS location at time of report.
- Performance metrics reset: Daily stats reset at midnight, weekly on Sunday, monthly on 1st.
- Support messages are associated with the driver's restaurant.

**Edge Cases:**
- Customer phone unreachable: Driver uses "Report Issue" with "Customer Unavailable."
- Photo upload fails: Allow submission without photo, retry upload in background.
- Performance data not available (new driver): Show "Start delivering to see your stats."

**UI/UX Requirements:**

**SCR-D-006: Issue Report Screen**
- Layout: "Report an Issue" heading. Order # reference. Issue category selector (radio buttons or list). Notes field (textarea, optional, max 500 chars). Photo attachment button (camera or gallery). "Submit Report" button. "Cancel" link.
- States: Default, Uploading photo (progress), Submitting (loading), Submitted (confirmation message with "The restaurant has been notified"), Error.

**SCR-D-007: Performance Screen**
- Layout: Summary cards at top: Total Deliveries, Completion Rate, Average Rating. Period selector (Today / This Week / This Month). Detailed stats: deliveries per day chart, average delivery time, on-time rate, customer ratings breakdown (5-star distribution).
- States: Loading, Loaded, No data ("Complete your first delivery to see stats").

**SCR-D-009: Support Screen**
- Layout: Simple chat-like interface. Message bubbles (driver on right, restaurant on left). Text input field at bottom. "Send" button.
- States: Loading messages, Messages loaded, Empty ("Need help? Send a message to the restaurant."), Error.

**SCR-D-010: Driver Settings Screen**
- Layout: Language toggle (Arabic/English). Notification preferences. GPS accuracy mode (High/Standard). About (app version). Logout button.
- States: Loaded, Saving.

**Data Requirements:**
- CREATE: IssueReport (driver_id, order_id, category, notes, photo_url, location, created_at), SupportMessage (driver_id, restaurant_id, message, created_at)
- READ: Performance metrics, support message history
- UPDATE: Issue report status (acknowledged, resolved)

**Integration Points:**
- Phone dialer: Native phone call intent
- SMS: Native SMS intent or in-app messaging
- AWS S3: Photo uploads for issue reports
- Backend API: POST /drivers/issues, GET /drivers/performance, POST /drivers/support-messages, GET /drivers/support-messages
- Socket.io: Real-time support message updates

**Permissions/Roles:**
- Driver: Report issues, view own performance, contact customers for active orders, message restaurant support

---

### 6.16 Restaurant Dashboard & Auth

**Description:** Secure web-based dashboard authentication and main overview panel for restaurant administrators. Provides at-a-glance business health metrics, real-time order counts, and operational status.

**User Stories Covered:** US-REST-001, US-REST-002

**Detailed Requirements:**

**Admin Login Flow:**
1. Admin navigates to the dashboard URL (e.g., dashboard.restaurantbrand.com).
2. Login page displays with restaurant branding.
3. Admin enters email and password.
4. On success, redirected to the main dashboard.
5. Session persists with JWT token (httpOnly cookie, configurable expiry).

**Dashboard Overview:**
1. Main dashboard loads with real-time widgets.
2. Top metrics row: Today's Orders, Today's Revenue (SAR), Active Orders, Available Drivers, Pending Issues.
3. Charts section: Revenue trend (hourly/daily), Order volume (hourly/daily), Top-selling items (bar chart).
4. Quick actions: View Order Board, Manage Menu, Send Notification.
5. Recent activity feed: Latest orders, driver assignments, support tickets.
6. Data refreshes automatically via Socket.io for order and driver counts.

**Business Rules:**
- Session timeout: Configurable (default 8 hours).
- Password requirements: Minimum 8 characters, at least one number and one special character.
- Failed login attempts: Lock account after 5 consecutive failures for 30 minutes.
- Dashboard data refreshes: Real-time for order counts and driver status; charts refresh every 5 minutes.
- Multi-admin support: Multiple admin accounts per restaurant with role-based permissions (future consideration).

**Edge Cases:**
- Session expired during use: Modal "Session expired. Please log in again." with login redirect.
- Dashboard loads with no data (new restaurant): Show empty states with setup guidance.
- Browser tab left open overnight: Auto-refresh on focus.

**UI/UX Requirements:**

**SCR-R-001: Dashboard Login**
- Layout: Centered login card. Restaurant logo above. Email field (email, required). Password field (password, required, show/hide). "Login" button (primary). "Forgot Password?" link.
- States: Default, Loading, Error (invalid credentials), Locked (too many attempts).

**SCR-R-002: Main Dashboard**
- Layout: Left sidebar navigation (persistent). Top bar with restaurant name, admin name, notifications bell, language toggle. Main content area with: KPI cards row (4-5 cards with numbers and trend arrows). Charts row (2 charts: revenue trend, order volume). Top items list. Recent activity feed. Quick action buttons.
- States: Loading (skeleton), Loaded, Error (connection lost banner with retry).
- Sidebar items: Dashboard, Orders, Menu, Drivers, Customers, Promotions, Reports, Support, Settings.

**Data Requirements:**
- READ: Dashboard metrics (orders count, revenue, active orders, available drivers, pending issues), Chart data (revenue by period, orders by period, top items), Recent activity log

**Integration Points:**
- Backend API: POST /admin/login, GET /admin/dashboard/metrics, GET /admin/dashboard/charts
- Socket.io: Real-time order count and driver status updates
- JWT: Session management (httpOnly cookie)

**Permissions/Roles:**
- Restaurant Admin: Full dashboard access

---

### 6.17 Menu Management

**Description:** Complete menu catalog management including CRUD operations for items, hierarchical category management, variant configuration, pricing control, image management, and real-time availability toggling. The restaurant's primary tool for maintaining their menu.

**User Stories Covered:** US-REST-003 through US-REST-007

**Detailed Requirements:**

**Menu Item CRUD Flow:**
1. Admin navigates to "Menu" in the sidebar.
2. Menu list shows all items grouped by category with search and filters.
3. Admin clicks "Add New Item."
4. Form opens with tabs: Basic Info, Variants, Nutrition, Images.
5. Basic Info: Name (AR), Name (EN), Description (AR), Description (EN), Category (dropdown), Price (SAR), Availability toggle.
6. Variants tab: Add variant groups (e.g., "Size" with Small/Medium/Large and price modifiers).
7. Nutrition tab: Calories, protein, carbs, fat, allergy tags (checkboxes).
8. Images tab: Upload up to 5 images (drag-and-drop or file picker).
9. Admin saves the item; it appears in the customer app.

**Category Management Flow:**
1. Admin navigates to "Menu" > "Categories."
2. Category tree is displayed with drag-and-drop reordering.
3. Admin can add a category (name AR/EN, parent category, icon/image, display order).
4. Admin can edit or delete categories.
5. Deleting a category with items requires reassignment.

**Availability Control:**
1. Menu list shows availability toggle per item.
2. Admin toggles to instantly show/hide items in the customer app.
3. Bulk actions: Select multiple items and toggle availability.
4. Stock tracking (optional): Set stock count; auto-unavailable at zero.

**Business Rules:**
- Item names required in both Arabic and English.
- Category hierarchy: Maximum 2 levels (category > subcategory).
- Images: Max 5 per item, max 5MB each, accepted formats: JPG, PNG, WebP.
- Images are resized server-side to standard dimensions and optimized.
- Soft delete: Deleted items are hidden, not removed (referenced in existing orders).
- Variant pricing: Base price + variant modifier. Displayed as total on customer app.
- Availability changes are instant (no caching delay) via Socket.io push to connected clients.

**Edge Cases:**
- Uploading an image that exceeds 5MB: Error message with size limit guidance.
- Creating a category that already exists: Duplicate name warning.
- Deleting the last item in a category: Category becomes empty (hidden from customer unless admin prefers visible).
- Bulk availability toggle on 50+ items: Progress indicator, async processing.

**UI/UX Requirements:**

**SCR-R-003: Menu List Screen**
- Layout: "Menu Management" heading. Search bar. Category filter dropdown. Availability filter (All/Available/Unavailable). Add New Item button. Items table: Image thumbnail, Name (AR/EN), Category, Price, Availability toggle, Actions (Edit, Delete). Bulk action toolbar (on selection). Pagination.
- States: Loading, Items listed, Empty ("No menu items yet. Add your first item!"), Search no results.

**SCR-R-004: Menu Item Form**
- Layout: Tabbed form (Basic Info | Variants | Nutrition | Images). Basic Info tab: Name AR (text, required), Name EN (text, required), Description AR (textarea), Description EN (textarea), Category (dropdown, required), Price (number, required, min 0.01), Availability toggle. Variants tab: Variant groups list with "Add Group" button. Each group: Group Name (AR/EN), Required toggle, Options list (name, price modifier, each with add/remove). Nutrition tab: Calories (number), Protein (number), Carbs (number), Fat (number), Allergy tags (multi-select checkboxes: Nuts, Dairy, Gluten, Eggs, Soy, Shellfish, Sesame). Images tab: Drag-and-drop upload area, Image thumbnails with reorder and delete. "Save" and "Cancel" buttons.
- States: New item (empty form), Edit item (pre-filled), Saving (loading), Validation errors, Image uploading.

**SCR-R-005: Category Manager**
- Layout: Category tree (drag-and-drop sortable). Each row: Icon/image, Name (AR/EN), Item count, Actions (Edit, Delete). "Add Category" button. Add/edit modal: Name AR (text, required), Name EN (text, required), Parent Category (dropdown, optional), Icon/Image upload, Display Order (number).
- States: Loading, Loaded, Empty, Drag in progress, Delete confirmation modal.

**Data Requirements:**
- CREATE: MenuItem, MenuCategory, MenuItemVariant
- READ: All menu items (filtered, paginated), categories tree, item with variants
- UPDATE: MenuItem fields, category fields, variant options, display order, availability
- DELETE: Soft delete items, categories (with reassignment check)

**Integration Points:**
- AWS S3: Image upload (presigned URLs for direct upload from browser)
- Backend API: GET /admin/menu, POST /admin/menu, PUT /admin/menu/:id, DELETE /admin/menu/:id, GET /admin/categories, POST /admin/categories, PUT /admin/categories/:id, DELETE /admin/categories/:id
- Socket.io: Push availability changes to connected customer apps

**Permissions/Roles:**
- Restaurant Admin: Full CRUD on menu and categories

---

### 6.18 Order Processing

**Description:** Real-time order management system for receiving, accepting/rejecting, tracking preparation, coordinating with kitchen staff, assigning drivers, and monitoring the full order lifecycle. The operational core of the restaurant dashboard.

**User Stories Covered:** US-REST-008 through US-REST-012

**Detailed Requirements:**

**Order Reception Flow:**
1. New order arrives via Socket.io.
2. Audible alert plays (configurable sound).
3. Visual notification appears on the order board and notification badge increments.
4. Order board shows the new order in the "New" column.

**Order Processing Flow:**
1. Admin clicks on a new order to view details.
2. Order detail shows: items with customizations, customer info, delivery address, payment method, special instructions.
3. Admin clicks "Accept" with an optional preparation time override.
4. Order moves to "Preparing" column. Customer is notified.
5. When food is ready, admin moves order to "Ready for Pickup."
6. Admin assigns a driver (or auto-assignment if configured).
7. Driver picks up order, status moves to "Out for Delivery."
8. Driver confirms delivery, status moves to "Delivered."

**Order Rejection Flow:**
1. Admin clicks "Reject" on a new order.
2. Reason selection: Out of Stock, Too Busy, Closing Soon, Other (with text).
3. Customer is notified with the reason.
4. If payment was made (not COD), refund is initiated.

**Business Rules:**
- Order board is a Kanban-style view with columns: New, Preparing, Ready, Out for Delivery, Delivered, Cancelled.
- New orders have a visual timer showing time since placement.
- Auto-reject: If no action within configurable timeout (e.g., 10 minutes), order is auto-rejected.
- Preparation time: Default from restaurant settings, overridable per order.
- Order history is searchable by order #, customer name, date range.
- Real-time updates: All order status changes reflected instantly across dashboard and customer/driver apps.

**Edge Cases:**
- Multiple orders arrive simultaneously: All appear in "New" column; admin processes sequentially.
- Internet drops while processing: Queue actions locally, sync on reconnection.
- Order for unavailable item: System should prevent (availability check at checkout), but admin can still reject.
- Customer cancellation request (before preparation): Admin can cancel and initiate refund.

**UI/UX Requirements:**

**SCR-R-006: Order Board**
- Layout: Kanban board with drag-and-drop columns: New (red highlight for urgency), Preparing (yellow), Ready (green), Out for Delivery (blue), Delivered (gray). Each order card: Order #, customer name, items count, total, time since placed, payment method badge (COD/Card). Sound toggle for alerts. Filter by status, date, payment method. Real-time badge count on sidebar "Orders" item.
- States: Loading, Active orders displayed, No orders ("No active orders right now"), Connection lost ("Reconnecting...").
- Interactions: Click card to open detail. Drag card between columns (with validation). Double-click for quick accept.

**SCR-R-007: Order Detail (Restaurant)**
- Layout: Order # and timestamp. Status badge. Customer section (name, phone, email, address with map, delivery instructions). Items table (name, customizations, quantity, unit price, line total). Price breakdown (subtotal, discount, VAT, delivery fee, total). Payment method and status. Driver assignment section (assigned driver or "Assign Driver" button). Status action buttons (Accept, Reject, Mark Ready, Cancel). Preparation time input. Order timeline (all status changes with timestamps).
- States: New order (accept/reject buttons), Accepted (preparation timer), Ready (assign driver), Out for delivery (driver tracking), Delivered (completed), Cancelled.

**Data Requirements:**
- READ: Orders list (real-time), order detail, available drivers for assignment
- UPDATE: Order status, preparation time, driver assignment
- CREATE: Order rejection (order_id, reason, refund_initiated)

**Integration Points:**
- Socket.io: Real-time order updates (new orders, status changes)
- Backend API: GET /admin/orders, GET /admin/orders/:id, PUT /admin/orders/:id/accept, PUT /admin/orders/:id/reject, PUT /admin/orders/:id/status, PUT /admin/orders/:id/assign-driver
- Firebase Cloud Messaging: Customer and driver notifications on status changes
- Stripe API: Refund initiation for rejected paid orders

**Permissions/Roles:**
- Restaurant Admin: Full order management

---

### 6.19 Driver Management

**Description:** Complete driver lifecycle management from the restaurant dashboard: creating driver accounts, assigning deliveries, real-time GPS tracking of all drivers on a map, and performance monitoring. Enables the restaurant to manage its own delivery fleet.

**User Stories Covered:** US-REST-013 through US-REST-016

**Detailed Requirements:**

**Driver Account Management Flow:**
1. Admin navigates to "Drivers" in the sidebar.
2. Driver list shows all drivers with status (Online/Offline), current assignment, and key metrics.
3. Admin clicks "Add Driver."
4. Form: Name, Phone, Email, Vehicle Type, License Plate, Initial Password.
5. On save, driver account is created and credentials can be shared with the driver.
6. Admin can edit driver details, reset password, or deactivate/activate accounts.

**Driver Assignment Flow:**
1. From the order detail, admin clicks "Assign Driver."
2. A modal shows available (online) drivers with: name, current location, active deliveries count, distance from restaurant.
3. Admin selects a driver and confirms.
4. Driver receives push notification.

**Real-Time Driver Map:**
1. Admin navigates to "Driver Map."
2. Google Maps displays all online drivers as pins.
3. Pins move in real time as drivers share location.
4. Clicking a pin shows driver details and current assignment.

**Business Rules:**
- Driver accounts are managed exclusively by the restaurant admin.
- Initial password is set by admin; driver can change it after first login.
- Deactivated drivers cannot log in and are hidden from assignment list.
- Driver map refreshes every 10-15 seconds via Socket.io.
- Performance data is aggregated daily and available for all time ranges.

**Edge Cases:**
- Creating a driver with duplicate phone number: Error "A driver with this phone number already exists."
- Assigning to a driver who just went offline: Refresh driver list, show updated status.
- Driver map with zero online drivers: "No drivers are currently online."
- Admin deletes a driver with active deliveries: Warning "This driver has active deliveries. Reassign before deactivating."

**UI/UX Requirements:**

**SCR-R-008: Driver List**
- Layout: "Driver Management" heading. "Add Driver" button. Search bar. Drivers table: Name, Phone, Vehicle, Status (Online/Offline badge), Active Deliveries, Avg Rating, Actions (Edit, Deactivate/Activate). Filters: Status (All/Online/Offline). Pagination.
- States: Loading, Drivers listed, Empty ("No drivers registered. Add your first driver!"), Search no results.

**SCR-R-009: Driver Form**
- Layout: "Add/Edit Driver" heading. Form fields: Name (text, required), Phone (tel, required), Email (email, optional), Vehicle Type (dropdown: Motorcycle, Car, Bicycle, required), License Plate (text, required), Password (password, required for new, optional for edit). "Save" and "Cancel" buttons.
- States: New (empty form), Edit (pre-filled), Saving, Validation errors.

**SCR-R-010: Driver Map**
- Layout: Full-width Google Map showing all online drivers. Driver pins with name tooltips. Filter: Show All Drivers / Busy Drivers / Available Drivers. Click pin for driver detail popup: name, phone, current order (if any), status. Side panel option: list of drivers with live status.
- States: Loading map, Map loaded with drivers, No online drivers, Connection lost.

**SCR-R-011: Delivery Zones Screen**
- Layout: Google Map with polygon drawing tools. List of defined zones (name, fee, color on map). Edit zone: name, delivery fee (SAR), polygon coordinates. Delete zone with confirmation.
- States: Loading, Zones displayed, No zones ("Define your first delivery zone"), Drawing mode.

**Data Requirements:**
- CREATE: Driver account (name, phone, email, vehicle_type, license_plate, password_hash)
- READ: Drivers list (paginated, filtered), driver detail, driver locations (real-time), driver performance metrics
- UPDATE: Driver profile, driver status, password reset
- DELETE: Driver deactivation (soft delete)

**Integration Points:**
- Google Maps SDK: Driver map rendering, polygon zone drawing
- Socket.io: Real-time driver location updates
- Backend API: GET /admin/drivers, POST /admin/drivers, PUT /admin/drivers/:id, DELETE /admin/drivers/:id, GET /admin/drivers/locations, GET /admin/drivers/:id/performance
- Firebase Cloud Messaging: Assignment notifications to drivers

**Permissions/Roles:**
- Restaurant Admin: Full driver management

---

### 6.20 Business Settings & Configuration

**Description:** Restaurant operational configuration including operating hours, delivery zones with zone-based fees, minimum order amounts, delivery fee structures, and tax/VAT settings. Central configuration hub for all business parameters.

**User Stories Covered:** US-REST-017 through US-REST-021

**Detailed Requirements:**

**Operating Hours Configuration:**
1. Admin navigates to "Settings" > "Operating Hours."
2. A weekly schedule grid is displayed.
3. For each day, admin sets: open time, close time, or "Closed" toggle.
4. Support for split hours (e.g., 9AM-2PM and 5PM-11PM).
5. Holiday/special date overrides available.

**Delivery Zone & Fee Configuration:**
1. Admin navigates to "Settings" > "Delivery Zones."
2. Google Map loads with existing zones (colored polygons).
3. Admin draws new zones using polygon tool.
4. For each zone: name, delivery fee (SAR), color, active/inactive toggle.
5. Zones can overlap; the most specific (smallest) zone takes priority.

**Minimum Order & Tax Configuration:**
1. Admin navigates to "Settings" > "Order Settings."
2. Fields: Minimum Order Amount (SAR), Default Preparation Time (minutes).
3. Admin navigates to "Settings" > "Tax Settings."
4. Fields: VAT Rate (%, default 15), VAT Registration Number.

**Business Rules:**
- Operating hours determine when customers can place orders.
- Delivery zones: Polygon-based, defined on Google Maps.
- Zone fee: Each zone has its own fee. If address falls in multiple zones, smallest area zone applies.
- Minimum order: Applied to subtotal before VAT and delivery fees.
- VAT rate: Default 15% (Saudi standard). Configurable for future regulation changes.
- All settings changes take effect immediately.

**Edge Cases:**
- Setting operating hours with invalid times (close before open): Validation error.
- Delivery zone that doesn't close (polygon not complete): Require closed polygon.
- VAT rate set to 0: Warning "Are you sure? VAT is typically 15% in Saudi Arabia."
- Minimum order set to very high amount: Warning that it may affect order volume.

**UI/UX Requirements:**

**SCR-R-012: Business Settings**
- Layout: Settings navigation tabs: General, Operating Hours, Order Settings, Tax, Payment. General: Restaurant name, description, contact info. Operating Hours: Weekly grid with time pickers per day, closed toggle, split-hours support. Order Settings: Minimum order amount (number, SAR), default preparation time (number, minutes). Tax: VAT rate (number, %), VAT registration number (text). "Save" button per section.
- States: Loading, Loaded, Saving, Saved (success toast), Validation errors.

**SCR-R-013: Payment Records**
- Layout: "Payment Records" heading. Date range filter. Payment method filter. Status filter (Completed, Pending, Failed, Refunded). Transactions table: Date, Order #, Amount, Method, Status, Actions (View, Refund for eligible). Export button (CSV/Excel). Summary cards: Total Revenue, Total Refunds, Net Revenue.
- States: Loading, Transactions listed, Empty, Filtered no results, Exporting.

**Data Requirements:**
- READ: Business settings (hours, zones, minimums, tax), payment transactions
- UPDATE: Operating hours, delivery zones, minimum order, VAT settings, general info
- CREATE: Delivery zone
- DELETE: Delivery zone

**Integration Points:**
- Google Maps SDK: Polygon zone drawing and display
- Backend API: GET /admin/settings, PUT /admin/settings, GET /admin/zones, POST /admin/zones, PUT /admin/zones/:id, DELETE /admin/zones/:id, GET /admin/payments, POST /admin/refunds
- Stripe API: Transaction records, refund processing

**Permissions/Roles:**
- Restaurant Admin: Full settings management

---

### 6.21 Marketing & Promotions (Restaurant)

**Description:** Marketing toolkit for the restaurant including promo code creation, push notification campaigns, and email marketing. Enables the restaurant to directly engage customers, drive orders, and build brand loyalty.

**User Stories Covered:** US-REST-025 through US-REST-027

**Detailed Requirements:**

**Promo Code Creation Flow:**
1. Admin navigates to "Promotions" > "Promo Codes."
2. Clicks "Create Promo Code."
3. Form: Code (text, auto-generate option), Discount Type (Percentage/Fixed Amount), Discount Value, Minimum Order Amount, Maximum Discount (for percentage), Usage Limit (total), Per-User Limit, Start Date, End Date, Target Audience (All/New Customers/Specific Segment), Applicable Items or Categories (optional).
4. Admin saves; code becomes active on start date.

**Push Notification Campaign Flow:**
1. Admin navigates to "Promotions" > "Push Notifications."
2. Clicks "New Notification."
3. Form: Title (AR/EN), Body (AR/EN), Image (optional), Target (All Customers/Segment/Specific Customers), Schedule (Now/Later with date-time picker).
4. Preview shown before sending.
5. Admin confirms and sends.

**Email Campaign Flow:**
1. Admin navigates to "Promotions" > "Email Campaigns."
2. Clicks "New Campaign."
3. Form: Subject (AR/EN), Body (rich text editor, AR/EN), Target Audience, Schedule.
4. Admin previews and sends.

**Business Rules:**
- Promo codes are case-insensitive.
- Auto-generated codes: 8-character alphanumeric (e.g., "SAVE20AB").
- Usage tracking: Each use is logged with user_id, order_id, discount_applied.
- Push notifications: Sent via FCM. Respect user notification preferences.
- Email campaigns: Sent via configured email service provider. Respect unsubscribe preferences.
- Campaign analytics: Open rate (email), delivery rate (push), usage rate (promos).

**Edge Cases:**
- Duplicate promo code: Error "This code already exists."
- Push notification to segment with zero users: Warning "No customers match this segment."
- Email campaign with no email addresses: Warning "Selected customers have no email on file."
- Promo code with conflicting dates (end before start): Validation error.

**UI/UX Requirements:**

**SCR-R-014: Promo Manager**
- Layout: "Promotions" heading. Tabs: Promo Codes / Push Notifications / Email Campaigns. Promo codes list: Code, Type, Value, Usage (used/limit), Status (Active/Expired/Scheduled), Date range, Actions (Edit, Deactivate, Delete). "Create Promo" button. Filters: Status, Date range.
- States: Loading, Codes listed, Empty, Filtered no results.

**SCR-R-015: Promo Form**
- Layout: "Create/Edit Promotion" heading. Code field (text, required, with "Auto-generate" button). Discount Type (radio: Percentage, Fixed Amount). Discount Value (number, required). Minimum Order (number, optional). Maximum Discount for percentage type (number, optional). Usage Limit (number, optional, 0=unlimited). Per-User Limit (number, default 1). Start Date (date picker, required). End Date (date picker, required). Target Audience (radio: All, New Customers, Segment). Applicable Items/Categories (multi-select, optional). "Save" and "Cancel" buttons.
- States: New, Edit, Saving, Validation errors.

**SCR-R-016: Push Notification Manager**
- Layout: "Push Notifications" heading. History list: Title, Audience size, Sent date, Delivery rate. "New Notification" button. Form: Title AR (text, required), Title EN (text, required), Body AR (textarea, required), Body EN (textarea, required), Image (upload, optional), Target (radio: All, Segment, Specific). Schedule (radio: Now, Later with datetime picker). Preview pane (mobile mockup). "Send" button with confirmation dialog.
- States: History loaded, Empty, Form open, Previewing, Sending, Sent confirmation.

**SCR-R-017: Email Campaign Manager**
- Layout: "Email Campaigns" heading. History list: Subject, Audience, Sent date, Open rate. "New Campaign" button. Form: Subject AR (text, required), Subject EN (text, required), Body AR (rich text editor), Body EN (rich text editor), Target Audience, Schedule. "Preview" and "Send" buttons.
- States: History loaded, Empty, Form open, Previewing, Sending, Sent.

**Data Requirements:**
- CREATE: PromoCode, PushNotification, EmailCampaign
- READ: Promo codes (list, filtered), notifications history, campaigns history
- UPDATE: PromoCode (edit, deactivate)
- DELETE: PromoCode (soft delete)

**Integration Points:**
- Firebase Cloud Messaging: Push notification delivery
- Email Service Provider: Email campaign delivery (provider TBD)
- Backend API: GET /admin/promos, POST /admin/promos, PUT /admin/promos/:id, DELETE /admin/promos/:id, POST /admin/push-notifications, GET /admin/push-notifications, POST /admin/email-campaigns, GET /admin/email-campaigns

**Permissions/Roles:**
- Restaurant Admin: Full marketing management

---

### 6.22 Reporting & Analytics

**Description:** Comprehensive reporting and analytics suite providing sales reports, customer analytics, and popular item analysis. Enables data-driven decision making for restaurant operations and marketing.

**User Stories Covered:** US-REST-028 through US-REST-030

**Detailed Requirements:**

**Sales Reports:**
1. Admin navigates to "Reports" > "Sales."
2. Date range selector (Today, This Week, This Month, Custom Range).
3. Report displays: Total Revenue, Order Count, Average Order Value, Revenue by Payment Method (pie chart), Revenue Over Time (line chart), Orders Over Time (bar chart).
4. Detailed transaction table below charts.
5. Export options: CSV, PDF.

**Customer Analytics:**
1. Admin navigates to "Reports" > "Customers."
2. Metrics: Total Registered Customers, New Customers (period), Returning Customer Rate, Average Customer Lifetime Value, Order Frequency Distribution.
3. Customer segments: By order frequency (1-time, 2-5, 6-10, 10+), by total spend, by registration date.
4. Top customers list (by spend and order count).

**Popular Items Analysis:**
1. Admin navigates to "Reports" > "Popular Items."
2. Ranked list of items by order count and revenue.
3. Trend indicators (rising/falling compared to previous period).
4. Filter by category and date range.

**Business Rules:**
- Report data is aggregated nightly for performance (not real-time for historical data).
- Current day data may use real-time queries.
- Export includes all visible data plus additional detail columns.
- Revenue figures include VAT unless "Excluding VAT" toggle is used.
- Customer analytics respect privacy: No PII in exports beyond what is already visible.

**Edge Cases:**
- Date range with no data: Show "No data for the selected period" with empty charts.
- Very large date range (> 1 year): Warning about report generation time; async processing with notification.
- Export of large dataset: Generate asynchronously, send download link via notification.

**UI/UX Requirements:**

**SCR-R-018: Sales Reports**
- Layout: "Sales Reports" heading. Date range selector (preset buttons + custom range picker). KPI cards: Total Revenue (SAR), Order Count, Avg Order Value, Top Payment Method. Charts: Revenue trend (line), Order volume (bar), Revenue by payment (pie). Transactions table (sortable, filterable). Export buttons (CSV, PDF). VAT toggle (Include/Exclude VAT).
- States: Loading, Report loaded, No data, Exporting, Export ready.

**SCR-R-019: Customer Analytics**
- Layout: "Customer Analytics" heading. Date range selector. KPI cards: Total Customers, New (period), Returning Rate (%), Avg Lifetime Value. Charts: New vs returning (stacked bar), Order frequency distribution (histogram), Top customers (table). Segment filters.
- States: Loading, Loaded, No data.

**SCR-R-020: Popular Items**
- Layout: "Popular Items" heading. Date range selector. Category filter. Items ranking table: Rank, Item Name, Orders Count, Revenue, Trend arrow (up/down/stable). Chart: Top 10 items bar chart. Period comparison toggle.
- States: Loading, Loaded, No data.

**Data Requirements:**
- READ: Aggregated sales data (by period, by payment method), customer analytics (segments, lifetime value), item popularity rankings

**Integration Points:**
- Backend API: GET /admin/reports/sales?from=&to=, GET /admin/reports/customers?from=&to=, GET /admin/reports/popular-items?from=&to=, GET /admin/reports/export?type=&format=

**Permissions/Roles:**
- Restaurant Admin: View all reports, export data

---

### 6.23 Customer Support Management

**Description:** Customer support ticketing system for managing inquiries, complaints, and issue resolution. Provides the restaurant with tools to maintain customer satisfaction and resolve problems efficiently.

**User Stories Covered:** US-REST-031, US-REST-024

**Detailed Requirements:**

**Support Ticket Flow:**
1. Customer submits a support request (from app or via order issue).
2. Ticket appears in the dashboard support queue.
3. Admin views the ticket: customer info, order reference (if applicable), issue description, conversation history.
4. Admin responds to the customer.
5. Customer receives notification of the response.
6. Admin resolves the ticket when the issue is addressed.

**Customer Database Flow:**
1. Admin navigates to "Customers."
2. Customer list with search and filters.
3. Clicking a customer shows: profile, order history, loyalty balance, support tickets, total spend.

**Business Rules:**
- Ticket statuses: Open, In Progress, Resolved, Closed.
- Tickets auto-close after 7 days of no response from customer.
- Support responses are sent as push notifications and in-app notifications.
- Customer database is searchable by name, phone, email.
- Customer data includes: registration date, total orders, total spend, last order date, loyalty balance.

**Edge Cases:**
- Customer submits multiple tickets for the same order: Link tickets to the same order, show warning to admin.
- High volume of tickets: Pagination, sorting by date/priority.
- Ticket for a deleted/deactivated customer: Show ticket with "Customer account deactivated" label.

**UI/UX Requirements:**

**SCR-R-021: Customer List**
- Layout: "Customers" heading. Search bar (name, phone, email). Customer table: Name, Phone, Email, Registered Date, Total Orders, Total Spent, Last Order, Actions (View). Filters: Registration date range, order count range. Pagination. Export button.
- States: Loading, Customers listed, Empty, Search no results.

**SCR-R-022: Customer Detail**
- Layout: Customer profile card (name, phone, email, registration date, avatar). Tabs: Orders | Loyalty | Support | Addresses. Orders tab: Order history table. Loyalty tab: Points balance, transaction history. Support tab: Related tickets. Addresses tab: Saved addresses.
- States: Loading, Loaded.

**SCR-R-023: Support Tickets**
- Layout: "Support" heading. Ticket list: Ticket #, Customer Name, Subject, Status badge, Date, Priority. Status filters (All/Open/In Progress/Resolved/Closed). Sort by date or priority. "View" button per ticket.
- States: Loading, Tickets listed, Empty ("No support tickets"), Filtered no results.

**SCR-R-024: Ticket Detail**
- Layout: Ticket # and status badge. Customer info card (name, phone, email). Order reference (if linked, clickable to order detail). Conversation thread (messages with timestamps, sender labels). Reply text area. Status update dropdown (Open > In Progress > Resolved > Closed). "Send Reply" button. "Close Ticket" button.
- States: Loading, Loaded, Replying (sending), Reply sent, Closing.

**Data Requirements:**
- CREATE: Support ticket (customer_id, subject, message, order_id), Support response (ticket_id, admin_id, message)
- READ: Tickets list (filtered, paginated), ticket detail with conversation, customer list, customer detail
- UPDATE: Ticket status, add response

**Integration Points:**
- Backend API: GET /admin/support, GET /admin/support/:id, POST /admin/support/:id/reply, PUT /admin/support/:id/status, GET /admin/customers, GET /admin/customers/:id
- Firebase Cloud Messaging: Notification to customer on response

**Permissions/Roles:**
- Restaurant Admin: Full support and customer management

---

### 6.24 Platform Configuration & Branding

**Description:** White-label branding configuration and system-level settings for the platform. Allows the restaurant to customize the platform's appearance and behavior to match their brand identity. Includes notification configuration, loyalty program settings, and system preferences.

**User Stories Covered:** US-REST-032, US-REST-033, and loyalty configuration (related to US-CUST-MISC-009)

**Detailed Requirements:**

**Branding Configuration Flow:**
1. Admin navigates to "Settings" > "Branding."
2. Upload/change: Logo (displayed in app and dashboard), Favicon (browser tab), Splash screen image.
3. Set colors: Primary color (buttons, headers), Secondary color (accents), Background color.
4. Set: App name, Tagline.
5. Preview: Live preview of how the app will look with the new branding.
6. Save: Changes deploy to customer and driver apps.

**Notification Configuration Flow:**
1. Admin navigates to "Settings" > "Notifications."
2. Configure alert channels for each event type:
   - New Order: Dashboard sound (on/off, sound selection), Email (on/off), SMS (on/off).
   - Driver Assignment: Push (on/off).
   - Low Stock: Email (on/off).
   - Support Ticket: Dashboard sound (on/off), Email (on/off).
3. Set custom notification templates (future enhancement).

**Loyalty Configuration Flow:**
1. Admin navigates to "Settings" > "Loyalty Program."
2. Toggle: Enable/Disable loyalty program.
3. Configure: Points per SAR spent (e.g., 1 point per 10 SAR), Redemption rate (e.g., 100 points = 10 SAR), Minimum redemption points, Maximum redemption per order (% of total), Points expiry period (months).
4. Save: Changes apply to all future transactions.

**Business Rules:**
- Logo: Max 2MB, accepted formats: PNG, SVG. Recommended dimensions provided.
- Colors: Hex color picker with preview.
- App name: Max 30 characters.
- Branding changes may require app restart for full effect on mobile.
- Notification sounds: Selectable from a preset library.
- Loyalty configuration: Changes apply to future transactions only; existing balances are not affected.

**Edge Cases:**
- Uploading a non-transparent logo: Warning "Consider using a PNG with transparent background."
- Setting the same primary and secondary color: Warning "These colors are the same. Consider different colors for better contrast."
- Disabling loyalty after customers have balances: Freeze balances, hide the feature, show admin warning.
- Invalid color hex code: Validation error.

**UI/UX Requirements:**

**SCR-R-025: Branding Configuration**
- Layout: "Branding" heading. Logo upload (preview, drag-and-drop). Favicon upload. Splash image upload. Color picker section: Primary (hex input + picker), Secondary (hex input + picker), Background (hex input + picker). App Name (text, max 30 chars). Tagline (text, max 60 chars). Live preview panel (shows a mockup of the app with current settings). "Save" button.
- States: Loading, Loaded, Saving, Saved (success), Validation errors.

**SCR-R-026: System Settings**
- Layout: "System Settings" heading. Sections: General (time zone, currency, date format), Integrations (API keys display -- masked, connection status badges for Google Maps, Stripe, Firebase), Maintenance Mode toggle (shows "Under maintenance" to customers). "Save" button per section.
- States: Loading, Loaded, Saving, Saved.

**SCR-R-027: Notification Settings**
- Layout: "Notification Preferences" heading. Event types table: Event Name, Dashboard Alert (toggle), Email (toggle), SMS (toggle). Rows: New Order, Order Cancellation, Low Stock Alert, New Support Ticket, New Customer Registration, Driver Issue Report. Sound selection dropdown for dashboard alerts. "Save" button.
- States: Loading, Loaded, Saving, Saved.

**SCR-R-028: Loyalty Configuration**
- Layout: "Loyalty Program" heading. Enable/Disable toggle (prominent). If enabled: Points per SAR (number, e.g., "1 point per X SAR spent"). Redemption rate (number, e.g., "X points = 1 SAR discount"). Minimum points to redeem (number). Maximum redemption per order (% slider). Points expiry (months, or "Never"). Program summary text (auto-generated from settings). "Save" button.
- States: Loading, Loaded, Saving, Saved, Disabled (grayed out fields).

**Data Requirements:**
- READ: Branding settings, notification settings, loyalty configuration, system settings
- UPDATE: Branding (logo, colors, name), notification preferences, loyalty rules, system settings
- CREATE: Branding asset uploads

**Integration Points:**
- AWS S3: Logo, favicon, splash image uploads
- Backend API: GET /admin/settings/branding, PUT /admin/settings/branding, GET /admin/settings/notifications, PUT /admin/settings/notifications, GET /admin/settings/loyalty, PUT /admin/settings/loyalty, GET /admin/settings/system, PUT /admin/settings/system

**Permissions/Roles:**
- Restaurant Admin: Full platform configuration

---

## 7. Information Architecture & Screen Inventory

### 7.1 Sitemap / Navigation Structure

#### Customer App (Android + Web)

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

#### Driver App (Android)

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

#### Restaurant Dashboard (Web)

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

### 7.2 Screen Inventory

#### Customer App Screens

| Screen ID | Screen Name | Module | Purpose | Key Components | Accessible By |
|---|---|---|---|---|---|
| SCR-C-001 | Splash Screen | Auth | App entry point with branding | Restaurant logo, loading indicator, brand colors | All users |
| SCR-C-002 | Onboarding | Auth | Introduce app features on first launch | Swipeable carousel (2-3 slides), illustrations, Skip/Next buttons | New users (first launch) |
| SCR-C-003 | Login | Auth | User authentication | Phone/email input, password input, social login buttons, register link | Unauthenticated users |
| SCR-C-004 | OTP Verification | Auth | Verify phone/email via OTP | 6-digit input fields, countdown timer, resend button | Users during registration/login |
| SCR-C-005 | Register | Auth | New account creation | Name, phone, email, password fields, terms checkbox, social login | Unauthenticated users |
| SCR-C-006 | Home | Menu | Main landing page with menu discovery | Search bar, promo banner carousel, popular items, category grid, bottom nav | All users (guest + registered) |
| SCR-C-007 | Menu Category | Menu | Browse items within a category | Category header, subcategory chips, item cards list, add buttons | All users |
| SCR-C-008 | Search | Menu | Search and filter menu items | Search bar, auto-suggest dropdown, filter modal, sort options, results list | All users |
| SCR-C-009 | Product Detail | Menu | View full item info and customize | Hero image carousel, description, price, variants, special instructions, quantity, add to cart | All users |
| SCR-C-010 | Cart | Cart | Review and manage cart items | Item list with +/- controls, promo code field, upsell section, order summary, checkout button | All users (checkout requires auth) |
| SCR-C-011 | Checkout | Cart | Complete order placement | Order type toggle, address selection, time selection, payment method, order summary, place order button | Registered users |
| SCR-C-012 | Order Confirmation | Cart | Confirm successful order placement | Success animation, order number, ETA, track order button | Registered users |
| SCR-C-013 | Payment | Payment | Select and process payment | Payment method cards (Visa, Mada, Google Pay, STC Pay, COD), saved cards, add new card | Registered users |
| SCR-C-014 | Order Tracking | Tracking | Track active order in real-time | Status timeline, map with driver pin, ETA, driver info, call/message buttons | Registered users |
| SCR-C-015 | Order History | Orders | View past orders | Tab filters (Active/Completed/Cancelled), order cards list, reorder buttons | Registered users |
| SCR-C-016 | Order Detail | Orders | View full order details | Items list, price breakdown, address, payment, driver info, timestamps, reorder, view receipt | Registered users |
| SCR-C-017 | Receipt | Orders | View VAT-compliant receipt | Restaurant info, VAT number, itemized list, totals, payment method, download/share | Registered users |
| SCR-C-018 | Ratings | Orders | Rate delivered items | Star ratings per item, text review fields, delivery rating, submit button | Registered users |
| SCR-C-019 | Offers | Offers | View available promotions | Introductory offers banner, offer cards with apply buttons, expiry info | All users (apply requires auth) |
| SCR-C-020 | Address List | Address | Manage saved addresses | Address cards with labels, default badge, edit/delete, add new button | Registered users |
| SCR-C-021 | Address Add/Edit | Address | Add or edit a delivery address | Google Map with pin-drop, address fields, label selector, default toggle, save button | Registered users |
| SCR-C-022 | Profile | Settings | View and manage user profile | Avatar, name, contact info, quick links (orders, addresses, payments, favorites, loyalty) | Registered users |
| SCR-C-023 | Settings | Settings | App preferences and account settings | Language toggle, notification toggles, change password, payment methods, delete account, about | Registered users |
| SCR-C-024 | Notifications | Settings | View notification history | Notification list with read/unread indicators, tap to navigate | Registered users |
| SCR-C-025 | Loyalty | Loyalty | View loyalty points and history | Points balance, SAR equivalent, earning history, redemption history, program rules | Registered users |
| SCR-C-026 | Branch Map | Menu | View restaurant branches | Google Map with branch pins, branch detail cards, curbside pickup toggle | All users |
| SCR-C-027 | Favorites | Menu | View saved favorite items | Favorited item cards, remove button, availability badges | Registered users |
| SCR-C-028 | Language | Settings | Switch app language | Arabic/English selection (within settings screen) | All users |

#### Driver App Screens

| Screen ID | Screen Name | Module | Purpose | Key Components | Accessible By |
|---|---|---|---|---|---|
| SCR-D-001 | Login | Auth | Driver authentication | Username/ID field, password field, login button, contact restaurant link | Unauthenticated drivers |
| SCR-D-002 | Home/Dashboard | Dashboard | Main driver hub with availability | Availability toggle, active delivery card, stats summary, new assignment notification | Authenticated drivers |
| SCR-D-003 | Order Detail | Orders | View assigned delivery details | Items list, customer info, address with map preview, accept/decline buttons, navigate button | Authenticated drivers |
| SCR-D-004 | Navigation | Delivery | Turn-by-turn GPS navigation | Full-screen map, route overlay, ETA, distance, call customer button | Authenticated drivers (active delivery) |
| SCR-D-005 | Delivery Confirmation | Delivery | Confirm order delivered | Order summary, COD amount field (if applicable), confirm delivery button, report issue button | Authenticated drivers (active delivery) |
| SCR-D-006 | Issue Report | Support | Report delivery problems | Issue category selector, notes field, photo attachment, submit button | Authenticated drivers |
| SCR-D-007 | Performance | Analytics | View delivery statistics | Deliveries count, completion rate, avg rating, avg delivery time, period selector | Authenticated drivers |
| SCR-D-008 | Profile | Profile | Manage driver profile | Name, phone, vehicle details, documents list with upload, edit button | Authenticated drivers |
| SCR-D-009 | Support | Support | Contact restaurant support | Chat-like message interface, message history | Authenticated drivers |
| SCR-D-010 | Settings | Settings | App preferences | Language toggle, notification preferences, GPS mode, logout | Authenticated drivers |

#### Restaurant Dashboard Screens

| Screen ID | Screen Name | Module | Purpose | Key Components | Accessible By |
|---|---|---|---|---|---|
| SCR-R-001 | Login | Auth | Admin authentication | Email/password fields, login button, forgot password link | Unauthenticated admins |
| SCR-R-002 | Dashboard | Overview | Business overview and KPIs | KPI cards, revenue/order charts, top items, recent activity, quick actions | Authenticated admins |
| SCR-R-003 | Menu List | Menu | Manage all menu items | Items table with search/filter, availability toggles, bulk actions, add button | Authenticated admins |
| SCR-R-004 | Menu Item Form | Menu | Add/edit a menu item | Tabbed form (Basic Info, Variants, Nutrition, Images), save/cancel | Authenticated admins |
| SCR-R-005 | Category Manager | Menu | Manage menu categories | Category tree with drag-and-drop, add/edit/delete, item counts | Authenticated admins |
| SCR-R-006 | Order Board | Orders | Kanban board for order management | Drag-and-drop columns (New, Preparing, Ready, Out for Delivery, Delivered), order cards, sound alerts | Authenticated admins |
| SCR-R-007 | Order Detail | Orders | Full order view with actions | Customer info, items table, price breakdown, status actions, driver assignment, timeline | Authenticated admins |
| SCR-R-008 | Driver List | Drivers | Manage driver accounts | Drivers table with status, metrics, search/filter, add/edit/deactivate | Authenticated admins |
| SCR-R-009 | Driver Form | Drivers | Add/edit driver account | Name, phone, email, vehicle details, password fields | Authenticated admins |
| SCR-R-010 | Driver Map | Drivers | Real-time driver location tracking | Google Map with driver pins, status indicators, click for detail | Authenticated admins |
| SCR-R-011 | Delivery Zones | Drivers | Define delivery coverage areas | Google Map with polygon drawing, zone list with fees, add/edit/delete | Authenticated admins |
| SCR-R-012 | Business Settings | Settings | Configure operating parameters | Operating hours grid, minimum order, preparation time, general info | Authenticated admins |
| SCR-R-013 | Payment Records | Settings | View financial transactions | Transactions table, filters, summary cards, export, refund actions | Authenticated admins |
| SCR-R-014 | Promo Manager | Marketing | Manage promotional codes | Promo codes table, status badges, usage tracking, create/edit/delete | Authenticated admins |
| SCR-R-015 | Promo Form | Marketing | Create/edit promo code | Code, discount type/value, conditions, dates, audience, save | Authenticated admins |
| SCR-R-016 | Push Notification Manager | Marketing | Send push notifications | Notification form, target audience, schedule, preview, send history | Authenticated admins |
| SCR-R-017 | Email Campaign Manager | Marketing | Send email campaigns | Subject, body editor, audience, schedule, preview, send history | Authenticated admins |
| SCR-R-018 | Sales Reports | Reports | Sales and revenue analytics | Date range, KPI cards, charts (revenue, orders, payment methods), export | Authenticated admins |
| SCR-R-019 | Customer Analytics | Reports | Customer behavior insights | Date range, customer KPIs, segment charts, top customers | Authenticated admins |
| SCR-R-020 | Popular Items | Reports | Menu item performance | Date range, ranking table, trend indicators, category filter | Authenticated admins |
| SCR-R-021 | Customer List | Customers | View all registered customers | Customer table with search, order stats, registration date, export | Authenticated admins |
| SCR-R-022 | Customer Detail | Customers | Individual customer view | Profile card, order history tab, loyalty tab, support tab, addresses tab | Authenticated admins |
| SCR-R-023 | Support Tickets | Support | Manage support requests | Ticket list with status filters, priority, customer info | Authenticated admins |
| SCR-R-024 | Ticket Detail | Support | View and respond to a ticket | Conversation thread, customer info, order reference, status actions, reply | Authenticated admins |
| SCR-R-025 | Branding Config | Settings | Customize white-label branding | Logo upload, color pickers, app name, live preview | Authenticated admins |
| SCR-R-026 | System Settings | Settings | System-level configuration | Time zone, currency, API integration status, maintenance mode | Authenticated admins |
| SCR-R-027 | Notification Settings | Settings | Configure admin alert preferences | Event types table with channel toggles (dashboard, email, SMS), sound selection | Authenticated admins |
| SCR-R-028 | Loyalty Config | Settings | Configure loyalty program rules | Enable toggle, points/SAR rate, redemption rate, limits, expiry | Authenticated admins |

---

### 7.3 User Flows

#### Flow 1: Guest Browse to First Order

```
1. User installs app and opens it
2. Splash screen (SCR-C-001) displays with branding -> auto-advance
3. Onboarding carousel (SCR-C-002) appears (first launch) -> user skips or completes
4. Home screen (SCR-C-006) loads with full menu in guest mode
5. User browses categories (SCR-C-007) or searches (SCR-C-008)
6. User taps an item -> Product Detail (SCR-C-009)
7. User customizes and taps "Add to Cart" -> item added, cart badge updates
8. User repeats steps 5-7 for additional items
9. User taps Cart tab (SCR-C-010) -> reviews items
10. User taps "Proceed to Checkout"
11. Registration/Login modal appears (guest cannot checkout)
12. User selects registration method -> Register (SCR-C-005)
13. User enters minimal info (name, phone) -> OTP sent
14. OTP Verification (SCR-C-004) -> user enters code -> account created
15. User returned to Checkout (SCR-C-011) with cart preserved
16. User selects Delivery, chooses address (SCR-C-021 for new address via pin-drop)
17. User selects payment method (SCR-C-013 section within checkout)
18. User reviews order summary and taps "Place Order"
19. Payment processes -> Order Confirmation (SCR-C-012) displayed
20. User taps "Track Order" -> Order Tracking (SCR-C-014)
```

#### Flow 2: Returning Customer Reorder

```
1. User opens app -> Splash (SCR-C-001) -> auto-login via saved JWT
2. Home screen (SCR-C-006) loads
3. User taps Orders tab -> Order History (SCR-C-015)
4. User finds a previous order and taps "Reorder"
5. All available items from that order are added to cart with same customizations
6. System checks for unavailable items or price changes -> notifies user if any
7. Cart (SCR-C-010) opens with pre-populated items
8. User reviews, adjusts quantities if needed
9. User taps "Proceed to Checkout" -> Checkout (SCR-C-011)
10. Default address is pre-selected
11. Default/last-used payment method is pre-selected
12. User taps "Place Order"
13. Payment processes -> Order Confirmation (SCR-C-012)
14. User tracks order (SCR-C-014) until delivery
```

#### Flow 3: Driver Accepts and Completes Delivery

```
1. Driver opens app -> Login (SCR-D-001) with restaurant credentials
2. Dashboard (SCR-D-002) loads -> driver toggles Online
3. GPS location sharing starts
4. Restaurant assigns an order to this driver
5. Push notification arrives -> New assignment card appears on dashboard
6. Driver taps to view Order Detail (SCR-D-003)
7. Driver reviews: items, customer name, address, distance, estimated time
8. Driver taps "Accept"
9. Order status updates to assigned; restaurant and customer notified
10. Driver goes to restaurant to pick up food (if not already there)
11. When food is ready (restaurant marks "Ready") -> driver gets notification
12. Driver taps "Navigate" -> Navigation screen (SCR-D-004) with turn-by-turn
13. Driver follows route to customer -> location shared in real-time
14. Driver arrives at customer location
15. Driver hands over the order
16. If COD: Delivery Confirmation (SCR-D-005) -> driver enters collected amount
17. If paid online: Delivery Confirmation (SCR-D-005) -> driver taps "Confirm Delivery"
18. Order status updates to "Delivered" -> customer and restaurant notified
19. Driver returns to Dashboard (SCR-D-002) ready for next order
```

#### Flow 4: Restaurant Receives and Processes Order

```
1. Admin logs into dashboard (SCR-R-001) -> Dashboard (SCR-R-002) loads
2. New order arrives -> audible alert plays -> Order Board (SCR-R-006) badge updates
3. Admin navigates to Order Board -> new order appears in "New" column
4. Admin clicks order card -> Order Detail (SCR-R-007)
5. Admin reviews items, customer info, payment method, delivery address
6. Admin clicks "Accept" and optionally sets preparation time
7. Order moves to "Preparing" column -> customer notified "Order confirmed"
8. Kitchen prepares the food
9. Admin moves order to "Ready for Pickup" -> driver notified
10. Admin clicks "Assign Driver" -> available drivers list appears
11. Admin selects a driver -> driver receives push notification
12. Driver accepts and picks up the order
13. Order moves to "Out for Delivery" column
14. Admin monitors driver on Driver Map (SCR-R-010) if needed
15. Driver confirms delivery -> order moves to "Delivered" column
16. Order completed -> data flows to Sales Reports (SCR-R-018)
```

#### Flow 5: Restaurant Creates Menu Item

```
1. Admin navigates to Menu > Menu List (SCR-R-003)
2. Admin clicks "Add New Item" -> Menu Item Form (SCR-R-004) opens
3. Basic Info tab: Admin enters Name (AR), Name (EN), Description (AR), Description (EN)
4. Admin selects Category from dropdown
5. Admin enters base Price (SAR)
6. Admin toggles Availability to "Available"
7. Variants tab: Admin clicks "Add Variant Group"
8. Admin creates "Size" group with options: Small (0 SAR), Medium (+5 SAR), Large (+10 SAR)
9. Admin marks Size as "Required"
10. Admin creates "Extras" group with options: Extra Cheese (+3 SAR), Jalapenos (+2 SAR)
11. Admin marks Extras as "Optional"
12. Nutrition tab: Admin enters calories, protein, carbs, fat
13. Admin selects allergy tags: Dairy, Gluten
14. Images tab: Admin uploads 3 product photos (drag-and-drop)
15. Admin clicks "Save" -> item is created
16. Item immediately appears in customer app menu under the selected category
```

#### Flow 6: Customer Registration (OTP)

```
1. User taps "Register" on Login screen (SCR-C-003)
2. Registration screen (SCR-C-005) loads
3. User enters Full Name
4. User enters phone number (+966XXXXXXXXX format)
5. User enters password (min 8 characters)
6. User checks "I agree to Terms & Privacy Policy"
7. User taps "Register"
8. System validates input -> sends OTP via Firebase Auth
9. OTP Verification screen (SCR-C-004) appears
10. Display shows "OTP sent to +966XXXX...XXX"
11. 6 individual digit fields are shown with 5-minute countdown timer
12. User receives SMS with 6-digit code
13. User enters code (auto-advances between fields)
14. User taps "Verify" (or auto-verifies on last digit entry)
15. System verifies OTP with Firebase
16. If correct: Account created -> user logged in -> redirected to previous context
17. If incorrect: Error "Invalid code" -> shake animation -> user can retry (max 3 attempts)
18. If expired: Timer shows "Code expired" -> "Resend OTP" button becomes active
19. If max attempts exceeded: 60-second cooldown before retry
```

#### Flow 7: Order Tracking Flow

```
1. User places order -> Order Confirmation (SCR-C-012) shown
2. User taps "Track Order" -> Order Tracking (SCR-C-014)
3. Status timeline shows: [Order Placed] -> Confirmed (waiting)
4. Push notification: "Your order has been confirmed by the restaurant"
5. Status updates to [Confirmed] -> Preparing
6. Push notification: "Your order is being prepared"
7. Status updates to [Preparing] -> Ready for Pickup
8. Driver is assigned -> driver info card appears (name, photo, vehicle)
9. Driver picks up order -> status updates to [Picked Up]
10. Push notification: "Your order is on the way!"
11. Map section activates showing:
    - Restaurant pin (origin)
    - Customer pin (destination)
    - Driver pin (moving, updates every 10-15 seconds)
    - Route line
12. ETA displays and updates dynamically
13. "Call Driver" and "Message Driver" buttons are now active
14. As driver approaches, push notification: "Driver is arriving!"
15. Driver confirms delivery -> status updates to [Delivered]
16. Push notification: "Your order has been delivered! Enjoy your meal."
17. Success animation plays on tracking screen
18. Rating prompt appears: "How was your order?" -> Rate Items (SCR-C-018)
```

---

### 7.4 Global UI Elements

#### Customer App (Android + Web)

**Bottom Navigation Bar:**
- 5 tabs: Home (house icon), Offers (tag icon), Cart (bag icon with badge count), Orders (receipt icon), Profile (person icon)
- Active tab: Primary brand color. Inactive: Gray.
- Badge on Cart: Shows item count (red circle with white number).
- Badge on Orders: Shows active order count during delivery.
- Always visible except on full-screen flows (navigation, payment processing).

**Top App Bar:**
- Left: Back button (or hamburger for web). Right: Notifications bell (with badge count).
- Center: Screen title or restaurant logo (on home).
- Home screen: Location/branch selector, search bar.

**Toast/Snackbar Notifications:**
- Position: Bottom of screen, above bottom nav.
- Types: Success (green), Error (red), Info (blue), Warning (yellow).
- Duration: 3 seconds auto-dismiss (errors: 5 seconds or manual dismiss).

**Loading States:**
- Skeleton screens for content loading (matching layout shape).
- Full-screen spinner for processing actions (payment, order placement).
- Pull-to-refresh on scrollable content.

**Empty States:**
- Consistent pattern: Illustration, heading, description, CTA button.
- Examples: Empty cart, no orders, no addresses, no favorites.

**Modal/Bottom Sheet:**
- Used for: filter selection, confirmations, registration prompt, error details.
- Dismissible: Tap outside or swipe down.

#### Driver App (Android)

**Top Bar:**
- Left: Drawer menu icon (hamburger). Right: Notifications bell.
- Center: "Driver" app name or restaurant name.

**Drawer Navigation:**
- Items: Dashboard, Performance, Profile, Support, Settings, Logout.
- Driver name and status (Online/Offline) at top of drawer.

**Availability Toggle:**
- Large, prominent toggle on dashboard.
- Green = Online, Gray = Offline.
- Confirmation dialog when going offline with active deliveries.

**Order Notification Card:**
- Slides in from top or appears as overlay.
- Contains: Order summary, distance, "Accept" and "Decline" buttons.
- Auto-dismiss after timeout (returns to restaurant).

**Full-Screen Navigation Overlay:**
- Turn-by-turn directions overlay on Google Maps.
- Bottom card: ETA, distance, customer info, quick actions.

#### Restaurant Dashboard (Web)

**Left Sidebar Navigation:**
- Persistent, collapsible.
- Sections: Dashboard, Orders (with active count badge), Menu, Drivers, Customers, Promotions, Reports, Support (with open count badge), Settings.
- Restaurant logo at top. Admin name and avatar at bottom with logout.
- Active item: Highlighted background. Hover: Subtle highlight.

**Top Bar:**
- Left: Page title / breadcrumbs.
- Right: Notifications bell (with badge), language toggle (AR/EN), admin avatar dropdown (profile, logout).

**Data Tables:**
- Consistent table component with: search, filters, column sorting, pagination (25/50/100 per page), row actions, bulk selection, export.
- Responsive: Horizontal scroll on smaller screens.

**Modals:**
- Used for: confirmations, forms (add driver, add promo), detail views.
- Centered, dimmed backdrop, close button (X), cancel/confirm buttons.

**Notification System:**
- Sound alerts for new orders (configurable).
- Toast notifications for system events (top-right).
- Badge counts on sidebar items.

**Forms:**
- Consistent styling: Labels above fields, validation messages below fields in red, required fields marked with asterisk.
- Auto-save: Draft indicator for long forms (menu items).
- Cancel: Confirmation if unsaved changes exist.

**Charts & Visualizations:**
- Consistent chart library usage throughout.
- Responsive sizing. Color-coded with brand palette.
- Tooltips on hover for data points.

---

## 8. API & Integration Requirements

### 8.1 External Integrations

#### Stripe (Payment Processing)
- **Purpose:** Process credit/debit card payments, Mada, Google Pay; manage saved cards; handle refunds.
- **Integration Type:** Server-side SDK (Node.js) + Client-side SDK (React Native, React.js).
- **Key APIs:**
  - Payment Intents API: Create and confirm payments.
  - Customer API: Create customers, manage payment methods (saved cards).
  - Refunds API: Process refunds for technical failures.
  - Webhooks: Payment success/failure events, dispute notifications.
- **PCI Compliance:** Stripe Elements/SDK handles card input. No raw card data on our servers.
- **Mada Support:** Stripe natively supports Mada in Saudi Arabia. No additional integration needed.
- **Google Pay:** Via Stripe's Google Pay integration (Payment Request API).
- **Configuration:** Stripe API keys stored in environment variables. Webhook signing secret for verification.

#### STC Pay
- **Purpose:** Process payments via Saudi Arabia's STC Pay digital wallet.
- **Integration Type:** Server-side API or SDK.
- **Key APIs:**
  - Payment initiation: Create payment request with amount.
  - Payment confirmation: Receive callback/webhook on success.
  - Payment status: Check payment status.
- **Note:** If Stripe supports STC Pay natively in Saudi, use Stripe. Otherwise, direct STC Pay API integration required. Verification needed early in development (Risk R-003).

#### Google Maps Platform
- **Purpose:** Maps display, geocoding, directions, distance matrix, real-time tracking visualization.
- **Integration Type:** Client-side SDKs (Maps SDK for Android via React Native, Maps JavaScript API for web) + Server-side APIs.
- **Key APIs:**
  - Maps SDK: Map rendering in all apps (customer tracking, driver navigation, restaurant driver map, delivery zones, branch map, address pin-drop).
  - Geocoding API: Reverse geocoding for address pin-drop (lat/lng to address).
  - Directions API: Route calculation for driver navigation and ETA.
  - Distance Matrix API: ETA estimation, delivery time calculation.
  - Places API: Address auto-suggest (supplementary to postal system).
- **Quota Management:** Implement caching and rate limiting to manage API costs. Cache geocoding results. Batch distance matrix requests.

#### Firebase Authentication
- **Purpose:** OTP/phone authentication for customer registration and login.
- **Integration Type:** Client-side SDK (React Native, React.js) + Server-side Admin SDK (Node.js).
- **Key Features:**
  - Phone authentication: Send/verify OTP via SMS.
  - Custom tokens: Generate custom JWT tokens after Firebase auth for our session management.
  - User management: Create, update, disable users.
- **Free Tier:** Firebase Auth free tier covers up to 10,000 SMS verifications/month. Beyond that, costs apply.

#### Firebase Cloud Messaging (FCM)
- **Purpose:** Push notifications to Android devices (customer and driver apps).
- **Integration Type:** Server-side Admin SDK (Node.js) + Client-side SDK (React Native).
- **Key Features:**
  - Individual notifications: Order status updates, driver assignments.
  - Topic messaging: Promotional notifications to customer segments.
  - Data messages: Custom data payloads for in-app handling.
- **Channels:** Order updates, promotional, driver assignments, support responses.

#### Google OAuth
- **Purpose:** Social login for customers via Google account.
- **Integration Type:** Client-side SDK (Google Sign-In for React Native/Web).
- **Key Flow:** OAuth 2.0 authorization code flow. Token exchanged on server for user info. Account creation or linking.

#### Facebook OAuth
- **Purpose:** Social login for customers via Facebook account.
- **Integration Type:** Client-side SDK (Facebook Login for React Native/Web).
- **Key Flow:** OAuth 2.0 authorization code flow. Token exchanged on server for user info. Account creation or linking.

#### AWS S3
- **Purpose:** File storage for menu item images, driver documents, branding assets, receipt PDFs.
- **Integration Type:** Server-side AWS SDK (Node.js).
- **Key Features:**
  - Presigned URLs for direct client uploads (menu images, driver documents).
  - CDN integration via CloudFront for fast image delivery.
  - Bucket policies for security (private by default, signed URLs for access).
  - Image processing: Resize and optimize on upload (Lambda trigger or server-side).

#### Saudi Post (SPL) API
- **Purpose:** Address auto-suggest and validation for Saudi postal system.
- **Integration Type:** Server-side API proxy.
- **Priority:** P2 (may not be available; fallback to manual entry).
- **Status:** Requires early investigation of API availability and documentation (Risk R-004).

#### Email Service Provider (TBD)
- **Purpose:** Transactional emails (order confirmations, receipts) and marketing campaigns.
- **Integration Type:** Server-side API.
- **Candidates:** SendGrid, Amazon SES, Mailchimp.
- **Key Features:** Template management, audience segmentation, delivery tracking, unsubscribe management.
- **Decision:** Provider to be selected during development (OQ-008).

### 8.2 Internal API Architecture

The backend follows a microservices architecture with these primary services communicating via internal APIs:

| Service | Responsibility | Key Endpoints |
|---|---|---|
| Auth Service | User authentication, registration, session management | POST /auth/register, POST /auth/login, POST /auth/verify-otp, POST /auth/refresh, POST /auth/social |
| User Service | User profiles, addresses, preferences | GET/PUT /users/profile, CRUD /users/addresses, PUT /users/preferences |
| Menu Service | Menu items, categories, variants, search | CRUD /menu, CRUD /categories, GET /menu/search, GET /menu/popular |
| Cart Service | Shopping cart management, promo validation | CRUD /cart, POST /cart/promo, GET /cart/validate |
| Order Service | Order lifecycle, status management | POST /orders, GET /orders, PUT /orders/:id/status, GET /orders/:id/tracking |
| Payment Service | Payment processing, refunds, transaction records | POST /payments/intent, POST /payments/confirm, GET /payments, POST /refunds |
| Delivery Service | Driver management, assignment, tracking | CRUD /drivers, PUT /drivers/availability, POST /orders/:id/assign, GET /drivers/locations |
| Notification Service | Push, email, in-app notifications | POST /notifications/push, POST /notifications/email, GET /notifications |
| Analytics Service | Reporting, metrics, dashboards | GET /reports/sales, GET /reports/customers, GET /reports/items |
| Loyalty Service | Points earning, redemption, balance | GET /loyalty/balance, POST /loyalty/earn, POST /loyalty/redeem |
| Support Service | Tickets, messaging | CRUD /support/tickets, POST /support/messages |
| Config Service | Branding, settings, zones | GET/PUT /config/branding, GET/PUT /config/settings, CRUD /config/zones |

### 8.3 Real-Time Communication (Socket.io)

| Channel | Direction | Purpose | Payload |
|---|---|---|---|
| `order:{order_id}` | Server to Customer | Order status updates | `{ status, timestamp, eta }` |
| `order:{order_id}:driver` | Server to Customer | Driver location for tracking | `{ lat, lng, heading, speed, timestamp }` |
| `restaurant:orders` | Server to Restaurant | New order notifications | `{ order_id, items_count, total, customer_name }` |
| `restaurant:drivers` | Server to Restaurant | Driver status changes | `{ driver_id, status, location }` |
| `driver:{driver_id}:assign` | Server to Driver | New order assignment | `{ order_id, items, customer, address }` |
| `driver:{driver_id}:location` | Driver to Server | Driver location broadcast | `{ lat, lng, heading, speed, timestamp }` |
| `support:{ticket_id}` | Bidirectional | Support chat messages | `{ sender, message, timestamp }` |

---

## 9. Data Model (High Level)

### 9.1 Entity Relationship Overview

The following entities represent the core data model. All entities include standard audit fields (created_at, updated_at) unless noted.

#### User & Authentication

**User**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| name | VARCHAR(100) | Full name |
| email | VARCHAR(255) | Email address (unique, nullable) |
| phone | VARCHAR(20) | Phone number (unique, nullable) |
| password_hash | VARCHAR(255) | Hashed password |
| role | ENUM | 'customer', 'driver', 'admin' |
| auth_provider | ENUM | 'local', 'google', 'facebook' |
| firebase_uid | VARCHAR(128) | Firebase Auth UID |
| language | ENUM | 'ar', 'en' |
| status | ENUM | 'active', 'inactive', 'suspended' |
| avatar_url | VARCHAR(500) | Profile image URL |
| created_at | TIMESTAMP | Account creation date |
| updated_at | TIMESTAMP | Last update |

**Customer** (extends User where role='customer')
| Field | Type | Description |
|---|---|---|
| id | UUID (PK, FK -> User) | User reference |
| dietary_restrictions | JSONB | Array of dietary preferences |
| default_address_id | UUID (FK -> Address) | Default delivery address |
| default_payment_method | VARCHAR(50) | Stripe payment method ID |
| notification_prefs | JSONB | Notification toggle preferences |
| is_guest_converted | BOOLEAN | Whether converted from guest |
| first_order_date | TIMESTAMP | Date of first order |

**Driver** (extends User where role='driver')
| Field | Type | Description |
|---|---|---|
| id | UUID (PK, FK -> User) | User reference |
| restaurant_id | UUID (FK -> Restaurant) | Assigned restaurant |
| vehicle_type | ENUM | 'motorcycle', 'car', 'bicycle' |
| license_plate | VARCHAR(20) | Vehicle registration |
| is_available | BOOLEAN | Current availability status |
| current_lat | DECIMAL(10,8) | Current GPS latitude |
| current_lng | DECIMAL(11,8) | Current GPS longitude |
| last_location_update | TIMESTAMP | Last GPS update time |
| avg_rating | DECIMAL(3,2) | Average customer rating |
| total_deliveries | INTEGER | Lifetime delivery count |

#### Restaurant & Branches

**Restaurant**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| name_ar | VARCHAR(100) | Arabic name |
| name_en | VARCHAR(100) | English name |
| description_ar | TEXT | Arabic description |
| description_en | TEXT | English description |
| logo_url | VARCHAR(500) | Logo image URL |
| primary_color | VARCHAR(7) | Brand primary color (hex) |
| secondary_color | VARCHAR(7) | Brand secondary color (hex) |
| vat_registration_no | VARCHAR(50) | VAT registration number |
| vat_rate | DECIMAL(5,2) | VAT rate (default 15.00) |
| min_order_amount | DECIMAL(10,2) | Minimum order in SAR |
| default_prep_time | INTEGER | Default preparation time (minutes) |
| is_active | BOOLEAN | Restaurant active status |
| currency | VARCHAR(3) | Currency code (SAR) |
| timezone | VARCHAR(50) | Time zone |

**Branch**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| restaurant_id | UUID (FK -> Restaurant) | Parent restaurant |
| name_ar | VARCHAR(100) | Arabic branch name |
| name_en | VARCHAR(100) | English branch name |
| address | TEXT | Physical address |
| latitude | DECIMAL(10,8) | GPS latitude |
| longitude | DECIMAL(11,8) | GPS longitude |
| phone | VARCHAR(20) | Branch phone |
| operating_hours | JSONB | Weekly schedule |
| supports_curbside | BOOLEAN | Curbside pickup available |
| is_active | BOOLEAN | Branch active status |

#### Menu

**MenuCategory**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| parent_id | UUID (FK -> MenuCategory, nullable) | Parent category for subcategories |
| name_ar | VARCHAR(100) | Arabic name |
| name_en | VARCHAR(100) | English name |
| image_url | VARCHAR(500) | Category image |
| display_order | INTEGER | Sort order |
| is_active | BOOLEAN | Visibility status |

**MenuItem**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| category_id | UUID (FK -> MenuCategory) | Category reference |
| name_ar | VARCHAR(100) | Arabic name |
| name_en | VARCHAR(100) | English name |
| description_ar | TEXT | Arabic description |
| description_en | TEXT | English description |
| price | DECIMAL(10,2) | Base price (SAR) |
| images | JSONB | Array of image URLs |
| nutrition_info | JSONB | Nutritional data |
| allergy_tags | JSONB | Array of allergen identifiers |
| is_available | BOOLEAN | Current availability |
| stock_count | INTEGER (nullable) | Stock level (null = unlimited) |
| popularity_score | INTEGER | Calculated popularity |
| is_deleted | BOOLEAN | Soft delete flag |

**MenuItemVariant**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| menu_item_id | UUID (FK -> MenuItem) | Parent item |
| group_name_ar | VARCHAR(100) | Group name Arabic (e.g., "Size") |
| group_name_en | VARCHAR(100) | Group name English |
| is_required | BOOLEAN | Must select from this group |
| is_multi_select | BOOLEAN | Can select multiple options |
| display_order | INTEGER | Sort order |
| options | JSONB | Array of {name_ar, name_en, price_modifier} |

#### Cart & Orders

**Cart**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| user_id | UUID (FK -> User) | Customer reference |
| promo_code_id | UUID (FK -> PromoCode, nullable) | Applied promo |
| updated_at | TIMESTAMP | Last cart modification |

**CartItem**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| cart_id | UUID (FK -> Cart) | Cart reference |
| menu_item_id | UUID (FK -> MenuItem) | Item reference |
| quantity | INTEGER | Item quantity |
| selected_variants | JSONB | Selected variant options with prices |
| special_instructions | VARCHAR(200) | Custom instructions |
| line_total | DECIMAL(10,2) | Calculated line total |

**Order**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| order_number | VARCHAR(20) | Human-readable order number |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| branch_id | UUID (FK -> Branch, nullable) | Branch reference |
| customer_id | UUID (FK -> User) | Customer reference |
| driver_id | UUID (FK -> User, nullable) | Assigned driver |
| order_type | ENUM | 'delivery', 'pickup' |
| status | ENUM | 'placed', 'confirmed', 'preparing', 'ready', 'picked_up', 'on_the_way', 'delivered', 'cancelled' |
| subtotal | DECIMAL(10,2) | Items subtotal |
| discount_amount | DECIMAL(10,2) | Discount applied |
| vat_amount | DECIMAL(10,2) | VAT amount |
| delivery_fee | DECIMAL(10,2) | Delivery fee |
| total | DECIMAL(10,2) | Grand total |
| delivery_address_id | UUID (FK -> Address, nullable) | Delivery address |
| scheduled_at | TIMESTAMP (nullable) | Scheduled delivery time |
| estimated_delivery | TIMESTAMP | ETA |
| preparation_time | INTEGER | Estimated prep minutes |
| special_instructions | TEXT | Order-level instructions |
| cancellation_reason | TEXT (nullable) | If cancelled, reason |
| promo_code_id | UUID (FK -> PromoCode, nullable) | Applied promo |
| created_at | TIMESTAMP | Order placement time |
| delivered_at | TIMESTAMP (nullable) | Actual delivery time |

**OrderItem**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| order_id | UUID (FK -> Order) | Order reference |
| menu_item_id | UUID (FK -> MenuItem) | Item reference |
| name_ar | VARCHAR(100) | Item name at time of order (snapshot) |
| name_en | VARCHAR(100) | Item name at time of order (snapshot) |
| quantity | INTEGER | Quantity ordered |
| unit_price | DECIMAL(10,2) | Price at time of order |
| selected_variants | JSONB | Selected variants with prices |
| special_instructions | VARCHAR(200) | Item-level instructions |
| line_total | DECIMAL(10,2) | Line total |

**OrderStatus** (status change log)
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| order_id | UUID (FK -> Order) | Order reference |
| status | ENUM | Status value |
| changed_by | UUID (FK -> User) | Who changed the status |
| notes | TEXT (nullable) | Optional notes |
| created_at | TIMESTAMP | When status changed |

#### Delivery & Location

**Delivery**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| order_id | UUID (FK -> Order) | Order reference |
| driver_id | UUID (FK -> User) | Driver reference |
| status | ENUM | 'assigned', 'picked_up', 'in_transit', 'delivered', 'failed' |
| pickup_time | TIMESTAMP (nullable) | When driver picked up |
| delivery_time | TIMESTAMP (nullable) | When delivered |
| cod_collected | DECIMAL(10,2) (nullable) | COD amount collected |
| distance_km | DECIMAL(6,2) | Delivery distance |

**Address**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| user_id | UUID (FK -> User) | Customer reference |
| label | VARCHAR(50) | Address label (Home, Work, etc.) |
| latitude | DECIMAL(10,8) | GPS latitude |
| longitude | DECIMAL(11,8) | GPS longitude |
| street | VARCHAR(255) | Street name |
| district | VARCHAR(100) | District/neighborhood |
| city | VARCHAR(100) | City |
| postal_code | VARCHAR(10) | Postal code |
| apartment | VARCHAR(50) | Apartment/floor |
| building_name | VARCHAR(100) | Building name |
| delivery_instructions | VARCHAR(200) | Special instructions |
| is_default | BOOLEAN | Default address flag |
| is_deleted | BOOLEAN | Soft delete |

**DeliveryZone**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| branch_id | UUID (FK -> Branch, nullable) | Optional branch scope |
| name | VARCHAR(100) | Zone name |
| polygon | JSONB | Array of {lat, lng} coordinates |
| delivery_fee | DECIMAL(10,2) | Fee for this zone (SAR) |
| is_active | BOOLEAN | Zone active status |

#### Payments & Transactions

**Payment**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| order_id | UUID (FK -> Order) | Order reference |
| method | ENUM | 'card', 'mada', 'google_pay', 'stc_pay', 'cod' |
| amount | DECIMAL(10,2) | Payment amount (SAR) |
| currency | VARCHAR(3) | Currency code (SAR) |
| status | ENUM | 'pending', 'completed', 'failed', 'refunded', 'pending_cod', 'collected' |
| stripe_payment_intent_id | VARCHAR(100) (nullable) | Stripe reference |
| stripe_charge_id | VARCHAR(100) (nullable) | Stripe charge reference |
| stc_transaction_id | VARCHAR(100) (nullable) | STC Pay reference |
| refund_amount | DECIMAL(10,2) (nullable) | Refund amount if refunded |
| refund_reason | TEXT (nullable) | Refund reason |
| created_at | TIMESTAMP | Payment initiation |
| completed_at | TIMESTAMP (nullable) | Payment completion |

**Transaction** (financial ledger)
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| order_id | UUID (FK -> Order) | Order reference |
| payment_id | UUID (FK -> Payment) | Payment reference |
| type | ENUM | 'order_payment', 'refund' |
| amount | DECIMAL(10,2) | Transaction amount |
| description | TEXT | Transaction description |
| created_at | TIMESTAMP | Transaction date |

#### Promotions & Loyalty

**PromoCode**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| code | VARCHAR(20) | Promo code (unique per restaurant) |
| discount_type | ENUM | 'percentage', 'fixed' |
| discount_value | DECIMAL(10,2) | Discount amount or percentage |
| min_order_amount | DECIMAL(10,2) (nullable) | Minimum order requirement |
| max_discount_amount | DECIMAL(10,2) (nullable) | Cap for percentage discounts |
| usage_limit | INTEGER (nullable) | Total usage limit (null = unlimited) |
| per_user_limit | INTEGER | Per-user usage limit (default 1) |
| usage_count | INTEGER | Current usage count |
| target_audience | ENUM | 'all', 'new_customers', 'segment' |
| applicable_items | JSONB (nullable) | Specific item/category IDs |
| start_date | TIMESTAMP | Activation date |
| end_date | TIMESTAMP | Expiry date |
| is_active | BOOLEAN | Active status |

**Review**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| customer_id | UUID (FK -> User) | Customer reference |
| order_id | UUID (FK -> Order) | Order reference |
| menu_item_id | UUID (FK -> MenuItem) | Rated item |
| rating | INTEGER | 1-5 stars |
| review_text | TEXT (nullable) | Review content |
| created_at | TIMESTAMP | Review date |
| updated_at | TIMESTAMP | Last edit date |

**Rating** (delivery/overall rating)
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| customer_id | UUID (FK -> User) | Customer reference |
| order_id | UUID (FK -> Order) | Order reference |
| driver_id | UUID (FK -> User, nullable) | Driver rated |
| rating | INTEGER | 1-5 stars |
| created_at | TIMESTAMP | Rating date |

**Notification**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| user_id | UUID (FK -> User) | Recipient |
| type | ENUM | 'order_update', 'promotion', 'system', 'support' |
| title_ar | VARCHAR(200) | Arabic title |
| title_en | VARCHAR(200) | English title |
| body_ar | TEXT | Arabic body |
| body_en | TEXT | English body |
| data | JSONB | Additional data (order_id, promo_id, etc.) |
| is_read | BOOLEAN | Read status |
| created_at | TIMESTAMP | Sent date |

**LoyaltyAccount**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| customer_id | UUID (FK -> User) | Customer reference |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| balance | INTEGER | Current points balance |
| lifetime_earned | INTEGER | Total points ever earned |
| lifetime_redeemed | INTEGER | Total points ever redeemed |
| last_activity_date | TIMESTAMP | Last earn/redeem date |

**LoyaltyTransaction**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| loyalty_account_id | UUID (FK -> LoyaltyAccount) | Account reference |
| order_id | UUID (FK -> Order, nullable) | Related order |
| type | ENUM | 'earn', 'redeem', 'expire', 'adjustment' |
| points | INTEGER | Points amount (positive for earn, negative for redeem) |
| description | TEXT | Transaction description |
| created_at | TIMESTAMP | Transaction date |

**SupportTicket**
| Field | Type | Description |
|---|---|---|
| id | UUID (PK) | Unique identifier |
| restaurant_id | UUID (FK -> Restaurant) | Restaurant reference |
| customer_id | UUID (FK -> User, nullable) | Customer reference |
| driver_id | UUID (FK -> User, nullable) | Driver reference (for driver issues) |
| order_id | UUID (FK -> Order, nullable) | Related order |
| subject | VARCHAR(200) | Ticket subject |
| status | ENUM | 'open', 'in_progress', 'resolved', 'closed' |
| priority | ENUM | 'low', 'medium', 'high' |
| created_at | TIMESTAMP | Creation date |
| resolved_at | TIMESTAMP (nullable) | Resolution date |

---

## 10. Non-Functional Requirements

### 10.1 Performance

| Metric | Target | Notes |
|---|---|---|
| API response time (general) | < 500ms (p95) | For standard CRUD operations |
| Menu search response time | < 2 seconds | Including auto-suggest |
| Order placement to confirmation | < 3 seconds | End-to-end including payment |
| Real-time GPS updates | Every 10-15 seconds | Driver to server to customer |
| Socket.io message delivery | < 1 second | Order status updates |
| Dashboard page load | < 3 seconds | Initial load with data |
| Image load time | < 2 seconds | With CDN caching |
| Concurrent users (MVP) | 500 simultaneous | Scalable beyond with horizontal scaling |
| Concurrent WebSocket connections | 1000 | Socket.io connections for real-time features |
| Database query performance | < 100ms (p95) | Indexed queries |
| OTP delivery | < 60 seconds | SMS/email OTP |
| Push notification delivery | < 5 seconds | FCM to device |

### 10.2 Security

| Requirement | Details |
|---|---|
| Authentication | JWT-based tokens (access token: 15 min, refresh token: 7 days). httpOnly cookies for web dashboard. |
| Password Storage | Bcrypt hashing with salt rounds >= 12 |
| Data Encryption at Rest | AES-256 encryption for sensitive data in PostgreSQL. AWS RDS encryption enabled. |
| Data Encryption in Transit | TLS 1.2+ for all API communications. HTTPS enforced. |
| PCI DSS Compliance | Stripe Elements/SDK for card input. No raw card data on our servers. SAQ A compliance level. |
| PDPL Compliance | Saudi Personal Data Protection Law. User consent for data collection. Right to data access and deletion. Data minimization. |
| Input Validation | Server-side validation on all inputs. SQL injection prevention (parameterized queries). XSS prevention (output encoding). |
| Rate Limiting | API rate limiting: 100 requests/minute per user. Login: 5 attempts per 15 minutes. OTP: 3 attempts per 5 minutes. |
| CORS | Restrictive CORS policies. Whitelist specific origins only. |
| File Upload Security | File type validation (whitelist), size limits, virus scanning, secure storage on S3 with signed URLs. |
| Session Management | Token rotation on refresh. Forced logout on password change. Device tracking for suspicious activity. |
| Admin Security | Strong password policy. Session timeout (8 hours). Account lockout after 5 failed attempts. |
| API Security | API key management for third-party services. Secrets in environment variables, not code. |
| Logging & Audit | Security event logging (login, failed attempts, permission changes). Audit trail for order and payment operations. |

### 10.3 Scalability

| Aspect | Approach |
|---|---|
| Architecture | Microservices with independent scaling per service |
| API Layer | Horizontal scaling behind load balancer (AWS ALB) |
| Database | PostgreSQL with read replicas for reporting queries. Connection pooling. |
| Caching | Redis for session management, menu caching, rate limiting |
| File Storage | AWS S3 with CloudFront CDN for static assets |
| WebSocket | Socket.io with Redis adapter for multi-server broadcasting |
| Background Jobs | Message queue (SQS or Redis) for async tasks (email, reports, notifications) |
| Container Orchestration | Docker containers orchestrated with AWS ECS or EKS |
| Auto-Scaling | Auto-scaling groups based on CPU/memory/request metrics |

### 10.4 Accessibility

| Requirement | Details |
|---|---|
| WCAG Level | Target WCAG 2.1 Level AA |
| Touch Targets | Minimum 44x44dp touch targets on mobile apps |
| Screen Reader | Semantic HTML on web; accessibility labels on React Native components |
| Color Contrast | Minimum 4.5:1 contrast ratio for text |
| Font Sizing | Support dynamic type / system font scaling |
| Keyboard Navigation | Full keyboard navigation support on web dashboard |
| Error Indication | Errors indicated by color AND text/icon (not color alone) |
| Focus Management | Visible focus indicators on interactive elements |

### 10.5 Browser & Device Support

| Platform | Support |
|---|---|
| Android (Customer & Driver) | Android 8.0 (Oreo) and above |
| Web Browser (Customer) | Chrome 90+, Firefox 88+, Safari 14+, Edge 90+ |
| Web Browser (Dashboard) | Chrome 90+, Firefox 88+, Safari 14+, Edge 90+ |
| Responsive Breakpoints | Mobile: 320-767px, Tablet: 768-1023px, Desktop: 1024px+ |
| Dashboard Minimum Resolution | 1024 x 768 |
| Network | 3G (graceful degradation), 4G/5G (optimal), WiFi |

### 10.6 Localization

| Requirement | Details |
|---|---|
| Languages | Arabic (primary), English (secondary) |
| RTL Support | Full right-to-left layout for Arabic across all interfaces |
| Date Format | DD/MM/YYYY (Saudi standard) |
| Time Format | 12-hour with AM/PM (Arabic/English) |
| Currency | SAR (Saudi Riyal) with 2 decimal places. Symbol: SAR or ر.س |
| Phone Format | +966 prefix for Saudi numbers |
| Number Format | Arabic-Indic numerals supported (0123456789 / ٠١٢٣٤٥٦٧٨٩) |
| Calendar | Gregorian (primary). Hijri date display optional (future). |
| Translation Management | String externalization via i18n library. All user-facing strings in translation files. |
| Content Direction | Text direction, layout mirroring, icon mirroring for directional icons |

---

## 11. Technical Considerations

### 11.1 Technology Stack Details

| Component | Technology | Version/Notes |
|---|---|---|
| Customer/Driver Mobile | React Native | Latest stable. Single codebase for Android. |
| Customer Web | React.js | Latest stable. Lightweight SPA for menu browsing and ordering. |
| Restaurant Dashboard | React.js | Latest stable. Full-featured SPA with data tables, charts, real-time updates. |
| State Management | Redux Toolkit or Zustand | For React Native and React.js state management |
| UI Component Library | Custom + NativeBase (RN) / Ant Design or MUI (Web) | Consistent design system |
| Backend API | Node.js + Express.js | Latest LTS Node.js. RESTful API. |
| ORM | Prisma or TypeORM | PostgreSQL ORM for type-safe queries |
| Database | PostgreSQL 15+ | Hosted on AWS RDS (Bahrain region) |
| Cache | Redis | For sessions, caching, Socket.io adapter, rate limiting |
| Real-Time | Socket.io | For order tracking, driver location, dashboard updates |
| Authentication | Firebase Auth + JWT | Firebase for OTP/phone; JWT for session management |
| Push Notifications | Firebase Cloud Messaging | For Android push notifications |
| File Storage | AWS S3 + CloudFront | Images, documents, receipts |
| Maps | Google Maps Platform | Maps SDK, Geocoding, Directions, Distance Matrix |
| Payments | Stripe SDK + STC Pay | Payment processing |
| Email | TBD (SendGrid/SES) | Transactional and marketing emails |
| Internationalization | i18next | For Arabic/English translations and RTL support |
| Charts | Chart.js or Recharts | Dashboard analytics visualizations |

### 11.2 Microservices Architecture

```
                    +------------------+
                    |   Load Balancer  |
                    |    (AWS ALB)     |
                    +--------+---------+
                             |
              +--------------+--------------+
              |                             |
      +-------+-------+           +--------+--------+
      |  API Gateway   |           |  WebSocket Server|
      |  (Express.js)  |           |   (Socket.io)    |
      +-------+-------+           +--------+---------+
              |                             |
    +---------+---------+          +--------+---------+
    |                   |          |                  |
+---+---+  +---+---+  +---+---+  +---+---+    +----+----+
| Auth  |  | Menu  |  | Order |  |Delivery|    |Notific- |
|Service|  |Service|  |Service|  |Service |    |ation Svc|
+---+---+  +---+---+  +---+---+  +---+---+    +----+----+
    |          |          |          |               |
    +----------+----------+----------+---------------+
                          |
                  +-------+-------+
                  |   PostgreSQL   |
                  |   (AWS RDS)    |
                  +-------+-------+
                          |
                  +-------+-------+
                  |     Redis      |
                  | (ElastiCache)  |
                  +---------------+
```

### 11.3 Deployment

| Aspect | Details |
|---|---|
| Containerization | Docker containers for each microservice |
| Orchestration | AWS ECS (Fargate) or EKS (Kubernetes) |
| Registry | AWS ECR for Docker images |
| CI/CD Pipeline | GitHub Actions or AWS CodePipeline: Build > Test > Lint > Deploy |
| Environments | Development, Staging, Production |
| Infrastructure as Code | AWS CloudFormation or Terraform |
| Database Migrations | Managed via ORM migration tools (Prisma Migrate or TypeORM migrations) |
| Secrets Management | AWS Secrets Manager for API keys, credentials |
| Monitoring | AWS CloudWatch for logs and metrics. Sentry for error tracking. |
| Uptime Monitoring | AWS CloudWatch Alarms or external service (e.g., Uptime Robot) |

### 11.4 Environments

| Environment | Purpose | Infrastructure |
|---|---|---|
| Development | Active development, feature branches | Shared dev instance, local databases |
| Staging | Pre-production testing, QA | Mirror of production at smaller scale |
| Production | Live deployment | Full-scale AWS infrastructure (Bahrain region) |

### 11.5 CI/CD Pipeline

```
Code Push -> Lint (ESLint) -> Unit Tests (Jest) -> Build (Docker) -> Integration Tests -> Deploy to Staging -> QA -> Deploy to Production
```

- Branch strategy: Feature branches -> develop -> staging -> main (production)
- Automated testing gate: All tests must pass before merge
- Docker image tagging: Git commit SHA + semantic version
- Zero-downtime deployments: Rolling updates via ECS/EKS
- Rollback: Automatic rollback on health check failure

---

## 12. Release Strategy & Phasing

### 12.1 Phase 1: MVP

**Scope:** All core features as defined in Section 3.1 of the Scope Document. This includes every functional requirement FR-001 through FR-096.

**Customer App Screens (Phase 1):**
SCR-C-001 (Splash), SCR-C-002 (Onboarding), SCR-C-003 (Login), SCR-C-004 (OTP), SCR-C-005 (Register), SCR-C-006 (Home), SCR-C-007 (Menu Category), SCR-C-008 (Search), SCR-C-009 (Product Detail), SCR-C-010 (Cart), SCR-C-011 (Checkout), SCR-C-012 (Order Confirmation), SCR-C-013 (Payment), SCR-C-014 (Order Tracking), SCR-C-015 (Order History), SCR-C-016 (Order Detail), SCR-C-017 (Receipt), SCR-C-018 (Ratings), SCR-C-019 (Offers), SCR-C-020 (Address List), SCR-C-021 (Address Add/Edit), SCR-C-022 (Profile), SCR-C-023 (Settings), SCR-C-024 (Notifications), SCR-C-025 (Loyalty), SCR-C-026 (Branch Map), SCR-C-027 (Favorites), SCR-C-028 (Language)

**Driver App Screens (Phase 1):**
SCR-D-001 (Login), SCR-D-002 (Dashboard), SCR-D-003 (Order Detail), SCR-D-004 (Navigation), SCR-D-005 (Delivery Confirmation), SCR-D-006 (Issue Report), SCR-D-007 (Performance), SCR-D-008 (Profile), SCR-D-009 (Support), SCR-D-010 (Settings)

**Restaurant Dashboard Screens (Phase 1):**
SCR-R-001 (Login), SCR-R-002 (Dashboard), SCR-R-003 (Menu List), SCR-R-004 (Menu Item Form), SCR-R-005 (Category Manager), SCR-R-006 (Order Board), SCR-R-007 (Order Detail), SCR-R-008 (Driver List), SCR-R-009 (Driver Form), SCR-R-010 (Driver Map), SCR-R-011 (Delivery Zones), SCR-R-012 (Business Settings), SCR-R-013 (Payment Records), SCR-R-014 (Promo Manager), SCR-R-015 (Promo Form), SCR-R-016 (Push Notification Manager), SCR-R-017 (Email Campaign Manager), SCR-R-018 (Sales Reports), SCR-R-019 (Customer Analytics), SCR-R-020 (Popular Items), SCR-R-021 (Customer List), SCR-R-022 (Customer Detail), SCR-R-023 (Support Tickets), SCR-R-024 (Ticket Detail), SCR-R-025 (Branding Config), SCR-R-026 (System Settings), SCR-R-027 (Notification Settings), SCR-R-028 (Loyalty Config)

**Phase 1 Key Deliverables:**
1. Customer Android App + Lightweight Web App
2. Driver Android App
3. Restaurant Web Dashboard
4. Backend API (microservices)
5. PostgreSQL database
6. Payment integration (Stripe + Mada, Google Pay, STC Pay, COD)
7. Real-time communication (Socket.io)
8. Push notifications (FCM)
9. Google Maps integration
10. Arabic/RTL localization
11. White-label branding system
12. Basic loyalty (cashback/points)
13. Google Play Store deployment

**Phase 1 Constraints:**
- Rule-based upsell prompts only (no AI)
- Basic loyalty (points earn/redeem, no tiers)
- Refunds limited to technical/payment failures
- No in-app driver payments (handled offline)
- Android only (no iOS)

### 12.2 Phase 2: Advanced Features

**Scope:** Enhancements beyond MVP, adding intelligence and expanded platform capabilities.

**Features:**
1. **Advanced Tiered Loyalty Program:** Multiple tiers (Bronze, Silver, Gold, Platinum) with increasing benefits (multiplied points, exclusive offers, free delivery). Tier qualification based on spend or order frequency. Tier dashboard UI enhancements.
2. **AI-Driven Personalization:** Machine learning-based upsell recommendations (replacing rule-based). Personalized menu ordering based on past behavior. Smart search with typo tolerance and semantic matching. Predictive ETA improvements.
3. **iOS Apps:** Customer iOS app (React Native build for iOS). Driver iOS app. Apple App Store submission. Apple Pay integration (via Stripe). Apple Sign-In social login.
4. **Advanced Analytics:** AI-powered demand forecasting. Customer churn prediction. Menu optimization recommendations. Revenue prediction models.
5. **Kitchen Display System (KDS):** Dedicated kitchen screen for order preparation management. Separate from dashboard for kitchen staff use.

### 12.3 Phase 3: Marketplace Potential

**Scope:** Future exploration beyond white-label single-restaurant to multi-restaurant marketplace.

**Features (Exploratory):**
1. **Multi-Restaurant Marketplace:** Single app listing multiple restaurants. Customer chooses restaurant, then orders. Shared delivery fleet option.
2. **Admin Super-Panel:** Central management for white-label deployments. Multi-tenant administration. Deployment automation.
3. **Advanced Delivery Optimization:** Route optimization for multi-order deliveries. Auto-assignment algorithms based on driver proximity and load. Delivery batching.
4. **Subscription Model:** Monthly subscription for unlimited free delivery. Meal plan subscriptions.

---

## 13. Dependencies & Blockers

### 13.1 External Dependencies

| ID | Dependency | Type | Impact | Status | Mitigation |
|---|---|---|---|---|---|
| DEP-001 | Google Maps API | Third-party service | GPS tracking, navigation, geocoding, zones, branch map | Available | Monitor quota; implement caching |
| DEP-002 | Stripe Payment Gateway | Third-party service | Payment processing for cards, Mada, Google Pay | Available | Test all payment methods in Saudi sandbox |
| DEP-003 | Mada (via Stripe) | Third-party service | Saudi debit card payments | Available (Stripe supports) | Test with Saudi Mada cards in sandbox |
| DEP-004 | Google Pay (via Stripe) | Third-party service | Mobile wallet payments | Available | Test on Android devices |
| DEP-005 | STC Pay API | Third-party service | Saudi digital wallet payments | Uncertain (may need separate integration) | Verify Stripe support early; plan separate integration if needed |
| DEP-006 | Firebase Auth | Third-party service | OTP/phone verification | Available | Monitor free tier limits |
| DEP-007 | Firebase Cloud Messaging | Third-party service | Push notifications | Available | Standard FCM integration |
| DEP-008 | Google Play Store | Distribution | App publication | Requires submission | Account setup and compliance review |
| DEP-009 | SMS/OTP Provider | Third-party service | OTP delivery | Via Firebase Auth | Monitor delivery rates in Saudi |
| DEP-010 | Email Service Provider | Third-party service | Email campaigns, transactional emails | TBD | Select provider during development |
| DEP-011 | AWS (Bahrain Region) | Infrastructure | Cloud hosting | Available | Standard AWS setup |
| DEP-012 | Saudi Post (SPL) API | Government/third-party | Address auto-suggest | Uncertain | Research early; fallback to manual entry |
| DEP-013 | Google OAuth | Third-party service | Social login | Available | Standard Google OAuth |
| DEP-014 | Facebook OAuth | Third-party service | Social login | Available | Standard Facebook Login |

### 13.2 Client-Provided Dependencies

| ID | Dependency | Description | Status | Blocker? |
|---|---|---|---|---|
| DEP-C-001 | Restaurant Branding Assets | Logos, colors, content for white-label | Pending | Yes -- needed for branding configuration |
| DEP-C-002 | Menu Content | Menu items, descriptions, images, pricing, nutrition data | Pending | Yes -- needed for menu seeding |
| DEP-C-003 | Stripe Merchant Account | Stripe account setup for Saudi Arabia | Pending | Yes -- needed for payment testing |
| DEP-C-004 | STC Pay Merchant Setup | STC Pay merchant credentials | Pending | Yes -- needed for STC Pay integration |
| DEP-C-005 | Business Rules | Delivery zones, operating hours, fee structures, tax rates | Pending | Partially -- can use defaults |
| DEP-C-006 | Domain & SSL | For dashboard and API hosting | Pending | Yes -- needed for production deployment |
| DEP-C-007 | Google Play Developer Account | For app publication | Pending | Yes -- needed for launch |

### 13.3 Identified Blockers

| ID | Blocker | Impact | Resolution Needed |
|---|---|---|---|
| BLK-001 | No timeline or milestones defined | Cannot plan sprints or resource allocation | Client and vendor must agree on timeline (OQ-002) |
| BLK-002 | No project budget defined | Cannot prioritize features if cuts needed | Client must define budget structure (OQ-003) |
| BLK-003 | STC Pay integration uncertainty | May require significant additional development | Verify Stripe STC Pay support immediately (R-003) |
| BLK-004 | Saudi Post API availability | May not be available or documented | Research early; accept manual entry fallback |

---

## 14. Risks & Mitigations

| ID | Risk | Severity | Likelihood | Impact | Mitigation |
|---|---|---|---|---|---|
| R-001 | STC Pay may require separate integration outside Stripe | Medium | Medium | Additional development time and complexity | Verify Stripe STC Pay support in Saudi early. Budget time for separate integration. Have STC Pay SDK documentation ready. |
| R-002 | Saudi Post (SPL) API limited availability or documentation | Medium | Medium | Address auto-suggest feature may not work | Research SPL API early. Prepare fallback to Google Places + manual entry. Mark feature as P2. |
| R-003 | Arabic translation quality impacts UX | Medium | Low | Poor user experience for Arabic-speaking customers | Engage professional Arabic translators with domain expertise. Conduct user testing with native speakers. Iterative review. |
| R-004 | Real-time GPS tracking at scale (Socket.io) | Medium | Medium | Performance issues with many concurrent drivers | Load test Socket.io infrastructure. Plan for Redis adapter and horizontal scaling. Set connection limits. Implement efficient location broadcasting (not fan-out). |
| R-005 | No timeline or budget defined -- scope creep risk | High | High | Uncontrolled scope, missed deadlines | Establish timeline and budget before development. Strict change request process. Prioritize P0/P1 features. |
| R-006 | White-label deployment complexity | Medium | Medium | Each restaurant needs separate branding, config, app store listing | Define white-label architecture early. Template-based deployment. Environment variable-driven branding. |
| R-007 | PCI compliance requirements may extend timeline | Medium | Low | Security audit delays, additional security development | Use Stripe Elements (SAQ A). Engage PCI consultant early. Security-first development practices. |
| R-008 | Guest browsing to registration conversion UX friction | Low | Medium | Low conversion rate from browsing to first order | A/B test registration prompts. Minimize signup fields. Preserve cart across registration. Track conversion funnel analytics. |
| R-009 | Google Maps API cost management | Medium | Medium | Unexpected API costs at scale | Implement aggressive caching (geocoding results, distance calculations). Batch API requests. Monitor quotas. Set billing alerts. |
| R-010 | Multi-branch menu complexity | Medium | Low | Managing different menus per branch adds complexity | Design branch-aware data model from start. Clear UI for branch-specific menu management. |
| R-011 | Firebase Auth free tier limits | Low | Medium | OTP costs increase with user growth | Monitor usage. Budget for paid tier. Implement OTP rate limiting to prevent abuse. |
| R-012 | Socket.io connection management across mobile networks | Medium | Medium | Dropped connections on 3G/4G transitions | Implement reconnection logic. Fallback to HTTP polling. Use heartbeat checks. Restore state on reconnect. |
| R-013 | React Native performance for maps and real-time features | Medium | Low | Janky UI during map rendering and real-time updates | Use native map modules. Optimize re-renders. Profile and optimize JavaScript bridge usage. |
| R-014 | Saudi regulatory compliance gaps (PDPL, CITC, NCA) | High | Medium | Potential legal issues or launch delays | Engage local legal counsel for compliance review (OQ-015). Implement data privacy by design. |
| R-015 | Email service provider selection delays | Low | Low | Email campaigns feature delayed | Select from established providers (SendGrid, SES). Standard integration. Decision early in sprint planning. |

---

## 15. Open Questions & Assumptions

### 15.1 Open Questions

| ID | Question | Priority | Tag | Status |
|---|---|---|---|---|
| OQ-002 | What is the target timeline for Phase 1 (MVP) delivery? Are there hard launch dates? | High | [BLOCKING] | Open |
| OQ-003 | What is the project budget, and how is it structured (fixed price, T&M, milestones)? | High | [BLOCKING] | Open |
| OQ-009 | Which specific "official postal system" should be integrated for address management? Saudi Post (SPL)? | Medium | [NON-BLOCKING] | Open |
| OQ-011 | Should the vendor (Space-O) handle Google Play Store submission, or will the client manage this? | Medium | [NON-BLOCKING] | Open |
| OQ-012 | How many initial restaurant deployments are planned? This impacts infrastructure sizing. | Medium | [NON-BLOCKING] | Open |
| OQ-014 | What is the expected order volume at launch? This impacts architecture decisions (server sizing, database capacity). | Medium | [NON-BLOCKING] | Open |
| OQ-015 | Are there specific Saudi regulatory requirements beyond PCI and VAT that must be addressed? (CITC, NCA, PDPL) | High | [BLOCKING] | Open |
| OQ-017 | Should drivers be able to self-register, or is restaurant-provisioned accounts the only model? | Low | [NON-BLOCKING] | Open |
| OQ-020 | Will the platform need to handle restaurants operating in multiple time zones, or is it Saudi Arabia only? | Low | [NON-BLOCKING] | Open |
| OQ-PRD-001 | What is the maximum number of concurrent deliveries per driver? | Medium | [DESIGN] | Open |
| OQ-PRD-002 | Should there be an auto-assignment algorithm for drivers, or only manual assignment by restaurant admin? | Medium | [DESIGN] | Open |
| OQ-PRD-003 | What is the timeout for a driver to accept/decline an order before it auto-returns to restaurant? | Medium | [DESIGN] | Open |
| OQ-PRD-004 | Should customers be able to cancel orders after placement? If so, at which stages? | Medium | [DESIGN] | Open |
| OQ-PRD-005 | What is the refund policy for cancelled orders (refund to original payment method, store credit, etc.)? | Medium | [DESIGN] | Open |
| OQ-PRD-006 | Should the web customer interface support the full ordering flow or just menu browsing? | Medium | [DESIGN] | Open |
| OQ-PRD-007 | What is the maximum delivery radius or zone size? | Low | [DESIGN] | Open |
| OQ-PRD-008 | Should there be a driver rating threshold below which they are flagged for review? | Low | [DESIGN] | Open |
| OQ-PRD-009 | What email service provider should be used for transactional and marketing emails? | Medium | [NON-BLOCKING] | Open |
| OQ-PRD-010 | Should the platform support promotional banners/images on the home screen managed from the dashboard? | Low | [DESIGN] | Open |

### 15.2 Assumptions

| ID | Assumption | Risk Level | Notes |
|---|---|---|---|
| A-001 | Mobile framework: React Native (confirmed) | Resolved | Android only in Phase 1 |
| A-002 | Database: PostgreSQL (confirmed) | Resolved | AWS RDS hosting |
| A-003 | Cloud provider: AWS Bahrain region (confirmed) | Resolved | Low latency for Saudi users |
| A-004 | Google Maps API will be the maps/navigation provider | Low | Standard integration |
| A-005 | Firebase Cloud Messaging will handle all push notifications | Low | Android FCM standard |
| A-006 | Socket.io is sufficient for real-time communication at expected scale | Low | Redis adapter for scaling |
| A-007 | Platform targets Saudi Arabian market primarily | Low | Based on Mada, STC Pay, Arabic localization |
| A-008 | Driver payments are entirely offline (no in-app wallet or payouts) | Medium | Simplifies financial architecture |
| A-009 | Each white-label deployment serves a single restaurant brand (not marketplace) | High | Core architectural assumption |
| A-010 | Client will provide restaurant branding assets | Medium | Needed for white-label configuration |
| A-011 | Arabic translations provided by vendor (Space-O) | Medium | Professional translations required |
| A-012 | OTP SMS costs borne by client/restaurant operator | Low | Firebase Auth billing |
| A-013 | Google Maps API usage costs borne by client/restaurant operator | Low | Usage-based billing |
| A-014 | Payment gateway merchant accounts set up by client | Medium | Required for live payments |
| A-015 | Competitive parity targets: Maestro, Herfy, Albaik apps | Low | UX benchmark reference |
| A-016 | Agile development methodology with iterative releases | Low | Standard process |
| A-017 | User flow diagrams from SOW have been finalized | Medium | May need revision |
| A-018 | SOW represents agreed scope | Low | Scope change log documents changes |
| A-PRD-001 | Default order acceptance timeout for restaurants is 10 minutes | Medium | Configurable in settings |
| A-PRD-002 | Default driver response timeout is 2 minutes | Medium | Configurable in settings |
| A-PRD-003 | Maximum 10 saved addresses per customer | Low | Reasonable limit |
| A-PRD-004 | Menu item images limited to 5 per item, 5MB each | Low | Storage management |
| A-PRD-005 | Category hierarchy limited to 2 levels (category > subcategory) | Low | Sufficient for food menus |
| A-PRD-006 | Customer web interface is "lightweight" -- menu browsing and ordering but not all native app features | Medium | Need confirmation (OQ-PRD-006) |

---

## 16. Glossary

| Term | Definition |
|---|---|
| **White-Label** | A product made by one company that is rebranded by another company to appear as their own |
| **OTP** | One-Time Password -- a temporary code sent via SMS or email for identity verification |
| **RTL** | Right-to-Left -- text direction used in Arabic language interfaces |
| **Mada** | Saudi Arabia's national payment network for debit card transactions |
| **STC Pay** | A digital wallet and payment service by Saudi Telecom Company |
| **VAT** | Value Added Tax -- currently 15% in Saudi Arabia |
| **COD** | Cash on Delivery -- payment method where customer pays upon receiving the order |
| **ETA** | Estimated Time of Arrival -- predicted delivery time |
| **JWT** | JSON Web Token -- a standard for securely transmitting information between parties |
| **PCI DSS** | Payment Card Industry Data Security Standard -- security standard for card payment handling |
| **CI/CD** | Continuous Integration / Continuous Deployment -- automated build, test, and deployment pipeline |
| **Socket.io** | JavaScript library enabling real-time, bidirectional communication between web clients and servers |
| **KDS** | Kitchen Display System -- screen-based system for kitchen order management (not in Phase 1 scope) |
| **MVP** | Minimum Viable Product -- the first production-ready version with core features |
| **Promo Engine** | A system for creating, managing, and applying promotional discounts and offers |
| **PDPL** | Saudi Personal Data Protection Law -- governs collection, processing, and storage of personal data |
| **NCA** | National Cybersecurity Authority -- Saudi Arabia's cybersecurity regulatory body |
| **CITC** | Communications, Information Technology and Communications Commission -- Saudi telecoms regulator |
| **SPL** | Saudi Post Logistics -- the national postal service of Saudi Arabia |
| **FCM** | Firebase Cloud Messaging -- Google's push notification service for mobile and web |
| **SAR** | Saudi Riyal -- the official currency of Saudi Arabia |
| **SAQ A** | Self-Assessment Questionnaire A -- PCI DSS compliance level for merchants using fully hosted payment forms |
| **ALB** | Application Load Balancer -- AWS load balancing service |
| **ECS** | Elastic Container Service -- AWS container orchestration service |
| **EKS** | Elastic Kubernetes Service -- AWS managed Kubernetes service |
| **ECR** | Elastic Container Registry -- AWS Docker image registry |
| **RDS** | Relational Database Service -- AWS managed database service |
| **S3** | Simple Storage Service -- AWS object storage service |
| **CDN** | Content Delivery Network -- distributed network for fast content delivery |
| **CRUD** | Create, Read, Update, Delete -- basic data operations |
| **REST** | Representational State Transfer -- API architectural style |
| **OAuth** | Open Authorization -- protocol for token-based authentication and authorization |
| **UUID** | Universally Unique Identifier -- 128-bit identifier for database records |
| **JSONB** | JSON Binary -- PostgreSQL data type for efficient JSON storage and querying |
| **Webhook** | HTTP callback triggered by an event in a source system |
| **Kanban** | Visual project management method using columns to represent workflow stages |
| **Idempotency Key** | Unique key ensuring a request can be safely retried without duplicate effects |
| **Reverse Geocoding** | Converting GPS coordinates (latitude/longitude) to a human-readable address |
| **Polygon Zone** | A geographic area defined by a series of coordinates forming a closed shape |

---

## 17. Appendix

### 17.1 Traceability Matrix

This matrix maps each Scope Document requirement to its corresponding User Story, Feature Specification section, and associated screens.

| Scope Req ID | Requirement | User Story | Feature Section | Screen(s) |
|---|---|---|---|---|
| FR-001 | Guest Browsing | US-CUST-AUTH-001 | 6.1 Customer Auth | SCR-C-006, SCR-C-007, SCR-C-008, SCR-C-009 |
| FR-002 | OTP Registration | US-CUST-AUTH-002 | 6.1 Customer Auth | SCR-C-004, SCR-C-005 |
| FR-003 | Social Login | US-CUST-AUTH-003 | 6.1 Customer Auth | SCR-C-003 |
| FR-004 | Phone/Email Registration | US-CUST-AUTH-004 | 6.1 Customer Auth | SCR-C-005 |
| FR-005 | Minimized Signup | US-CUST-AUTH-005 | 6.1 Customer Auth | SCR-C-005 |
| FR-006 | Arabic-Friendly Interface | US-CUST-AUTH-006 | 6.1 Customer Auth | All customer screens |
| FR-007 | Profile Completion | US-CUST-AUTH-007 | 6.1 Customer Auth | SCR-C-022, SCR-C-021 |
| FR-008 | Category Browsing | US-CUST-MENU-001 | 6.2 Menu Browse | SCR-C-006, SCR-C-007 |
| FR-009 | Advanced Search | US-CUST-MENU-002 | 6.2 Menu Browse | SCR-C-008 |
| FR-010 | Filtering | US-CUST-MENU-003 | 6.2 Menu Browse | SCR-C-008 |
| FR-011 | Sorting | US-CUST-MENU-004 | 6.2 Menu Browse | SCR-C-008 |
| FR-012 | Popular Items Section | US-CUST-MENU-005 | 6.2 Menu Browse | SCR-C-006 |
| FR-013 | Product Detail View | US-CUST-MENU-006 | 6.3 Product Details | SCR-C-009 |
| FR-014 | Item Customization | US-CUST-MENU-007 | 6.3 Product Details | SCR-C-009 |
| FR-015 | Save Favorites | US-CUST-MENU-008 | 6.3 Product Details | SCR-C-009, SCR-C-027 |
| FR-016 | Cart Management | US-CUST-CART-001 | 6.4 Cart & Checkout | SCR-C-010 |
| FR-017 | Promo Code Application | US-CUST-CART-002 | 6.4 Cart & Checkout | SCR-C-010, SCR-C-011 |
| FR-018 | VAT Display | US-CUST-CART-003 | 6.4 Cart & Checkout | SCR-C-010, SCR-C-011 |
| FR-019 | Upsell Prompts | US-CUST-CART-004 | 6.4 Cart & Checkout | SCR-C-010 |
| FR-020 | Delivery/Pickup Toggle | US-CUST-CART-005 | 6.4 Cart & Checkout | SCR-C-011 |
| FR-021 | Order Scheduling | US-CUST-CART-006 | 6.4 Cart & Checkout | SCR-C-011 |
| FR-022 | ETA Display | US-CUST-CART-007 | 6.4 Cart & Checkout | SCR-C-011, SCR-C-014 |
| FR-023 | Branch Map | US-CUST-CART-008 | 6.4 Cart & Checkout | SCR-C-026 |
| FR-024 | Address Selection | US-CUST-CART-009 | 6.4 Cart & Checkout | SCR-C-011, SCR-C-020, SCR-C-021 |
| FR-025 | One-Page Checkout | US-CUST-CART-010 | 6.4 Cart & Checkout | SCR-C-011 |
| FR-026 | Fee Transparency | US-CUST-CART-011 | 6.4 Cart & Checkout | SCR-C-010, SCR-C-011 |
| FR-027 | Credit/Debit Card Payment | US-CUST-PAY-001 | 6.5 Payment Processing | SCR-C-013 |
| FR-028 | Mada Payment | US-CUST-PAY-002 | 6.5 Payment Processing | SCR-C-013 |
| FR-029 | Google Pay | US-CUST-PAY-003 | 6.5 Payment Processing | SCR-C-013 |
| FR-030 | STC Pay | US-CUST-PAY-004 | 6.5 Payment Processing | SCR-C-013 |
| FR-031 | Cash on Delivery | US-CUST-PAY-005 | 6.5 Payment Processing | SCR-C-013 |
| FR-032 | Saved Cards | US-CUST-PAY-006 | 6.5 Payment Processing | SCR-C-013, SCR-C-023 |
| FR-033 | Quick Payment Selection | US-CUST-PAY-007 | 6.5 Payment Processing | SCR-C-013 |
| FR-034 | Order Status Tracking | US-CUST-TRACK-001 | 6.6 Real-Time Tracking | SCR-C-014 |
| FR-035 | Live GPS Tracking | US-CUST-TRACK-002 | 6.6 Real-Time Tracking | SCR-C-014 |
| FR-036 | Driver Contact | US-CUST-TRACK-003 | 6.6 Real-Time Tracking | SCR-C-014 |
| FR-037 | Push Notifications | US-CUST-TRACK-004 | 6.6 Real-Time Tracking | SCR-C-024 |
| FR-038 | Order History | US-CUST-TRACK-005 | 6.7 Order History | SCR-C-015 |
| FR-039 | Reorder Function | US-CUST-TRACK-006 | 6.7 Order History | SCR-C-015, SCR-C-016 |
| FR-040 | VAT-Compliant Receipts | US-CUST-TRACK-007 | 6.7 Order History | SCR-C-017 |
| FR-041 | Item Ratings & Reviews | US-CUST-TRACK-008 | 6.7 Order History | SCR-C-018 |
| FR-042 | Offers Tab | US-CUST-MISC-001 | 6.8 Offers & Promotions | SCR-C-019 |
| FR-043 | Introductory Offers | US-CUST-MISC-002 | 6.8 Offers & Promotions | SCR-C-019 |
| FR-044 | Multiple Addresses | US-CUST-MISC-003 | 6.9 Address Management | SCR-C-020 |
| FR-045 | Map Pin-Drop | US-CUST-MISC-004 | 6.9 Address Management | SCR-C-021 |
| FR-046 | Default Address | US-CUST-MISC-005 | 6.9 Address Management | SCR-C-020 |
| FR-047 | Postal System Integration | US-CUST-MISC-006 | 6.9 Address Management | SCR-C-021 |
| FR-048 | Notification Preferences | US-CUST-MISC-007 | 6.10 Notifications & Settings | SCR-C-023 |
| FR-049 | Language Toggle | US-CUST-MISC-008 | 6.10 Notifications & Settings | SCR-C-023, SCR-C-028 |
| FR-050 | Basic Loyalty Program | US-CUST-MISC-009 | 6.11 Loyalty Program | SCR-C-025 |
| FR-051 | Driver Login | US-DRV-001 | 6.12 Driver Auth | SCR-D-001 |
| FR-052 | Driver Profile | US-DRV-002 | 6.12 Driver Auth | SCR-D-008 |
| FR-053 | Availability Toggle | US-DRV-003 | 6.13 Driver Availability | SCR-D-002 |
| FR-054 | Shift Management | US-DRV-004 | 6.13 Driver Availability | SCR-D-002 |
| FR-055 | Order Assignment View | US-DRV-005 | 6.13 Driver Availability | SCR-D-002, SCR-D-003 |
| FR-056 | Accept/Decline Orders | US-DRV-006 | 6.13 Driver Availability | SCR-D-002, SCR-D-003 |
| FR-057 | GPS Navigation | US-DRV-007 | 6.14 Driver Navigation | SCR-D-004 |
| FR-058 | Real-Time Location Sharing | US-DRV-008 | 6.14 Driver Navigation | SCR-D-004 |
| FR-059 | Delivery Confirmation | US-DRV-009 | 6.14 Driver Navigation | SCR-D-005 |
| FR-060 | Customer Communication | US-DRV-010 | 6.15 Driver Communication | SCR-D-003, SCR-D-004 |
| FR-061 | Issue Reporting | US-DRV-011 | 6.15 Driver Communication | SCR-D-006 |
| FR-062 | Performance Dashboard | US-DRV-012 | 6.15 Driver Communication | SCR-D-007 |
| FR-063 | Restaurant Support Channel | US-DRV-013 | 6.15 Driver Communication | SCR-D-009 |
| FR-064 | Admin Login | US-REST-001 | 6.16 Dashboard Auth | SCR-R-001 |
| FR-065 | Dashboard Overview | US-REST-002 | 6.16 Dashboard Auth | SCR-R-002 |
| FR-066 | Menu CRUD | US-REST-003 | 6.17 Menu Management | SCR-R-003, SCR-R-004 |
| FR-067 | Category Management | US-REST-004 | 6.17 Menu Management | SCR-R-005 |
| FR-068 | Item Variants | US-REST-005 | 6.17 Menu Management | SCR-R-004 |
| FR-069 | Pricing Management | US-REST-006 | 6.17 Menu Management | SCR-R-004 |
| FR-070 | Availability Control | US-REST-007 | 6.17 Menu Management | SCR-R-003 |
| FR-071 | Order Reception | US-REST-008 | 6.18 Order Processing | SCR-R-006 |
| FR-072 | Order Accept/Reject | US-REST-009 | 6.18 Order Processing | SCR-R-006, SCR-R-007 |
| FR-073 | Preparation Time Setting | US-REST-010 | 6.18 Order Processing | SCR-R-007 |
| FR-074 | Kitchen Coordination | US-REST-011 | 6.18 Order Processing | SCR-R-006 |
| FR-075 | Order Lifecycle Tracking | US-REST-012 | 6.18 Order Processing | SCR-R-006, SCR-R-007 |
| FR-076 | Driver Account Management | US-REST-013 | 6.19 Driver Management | SCR-R-008, SCR-R-009 |
| FR-077 | Driver Assignment | US-REST-014 | 6.19 Driver Management | SCR-R-007, SCR-R-008 |
| FR-078 | Driver GPS Tracking | US-REST-015 | 6.19 Driver Management | SCR-R-010 |
| FR-079 | Driver Performance Monitoring | US-REST-016 | 6.19 Driver Management | SCR-R-008 |
| FR-080 | Operating Hours Config | US-REST-017 | 6.20 Business Settings | SCR-R-012 |
| FR-081 | Delivery Zone Config | US-REST-018 | 6.20 Business Settings | SCR-R-011 |
| FR-082 | Minimum Order Config | US-REST-019 | 6.20 Business Settings | SCR-R-012 |
| FR-083 | Delivery Fee Config | US-REST-020 | 6.20 Business Settings | SCR-R-011 |
| FR-084 | Tax Settings | US-REST-021 | 6.20 Business Settings | SCR-R-012 |
| FR-085 | Payment Processing | US-REST-022 | 6.20 Business Settings | SCR-R-013 |
| FR-086 | Refund Management | US-REST-023 | 6.20 Business Settings | SCR-R-013 |
| FR-087 | Customer Database | US-REST-024 | 6.23 Customer Support | SCR-R-021, SCR-R-022 |
| FR-088 | Promo Engine | US-REST-025 | 6.21 Marketing & Promos | SCR-R-014, SCR-R-015 |
| FR-089 | Push Notification Management | US-REST-026 | 6.21 Marketing & Promos | SCR-R-016 |
| FR-090 | Email Marketing | US-REST-027 | 6.21 Marketing & Promos | SCR-R-017 |
| FR-091 | Sales Reports | US-REST-028 | 6.22 Reporting & Analytics | SCR-R-018 |
| FR-092 | Customer Analytics | US-REST-029 | 6.22 Reporting & Analytics | SCR-R-019 |
| FR-093 | Popular Items Analysis | US-REST-030 | 6.22 Reporting & Analytics | SCR-R-020 |
| FR-094 | Support Management | US-REST-031 | 6.23 Customer Support | SCR-R-023, SCR-R-024 |
| FR-095 | Branding Configuration | US-REST-032 | 6.24 Platform Config | SCR-R-025 |
| FR-096 | Notification Configuration | US-REST-033 | 6.24 Platform Config | SCR-R-027 |

### 17.2 Screen-to-Feature Mapping (Reverse Lookup)

This provides a reverse lookup: for each screen, which features and requirements does it serve?

#### Customer App

| Screen ID | Screen Name | Features Served | Requirements |
|---|---|---|---|
| SCR-C-001 | Splash Screen | Branding, App Launch | FR-095 |
| SCR-C-002 | Onboarding | Customer Acquisition | FR-005 |
| SCR-C-003 | Login | Authentication | FR-003, FR-004 |
| SCR-C-004 | OTP Verification | Authentication | FR-002 |
| SCR-C-005 | Register | Authentication | FR-002, FR-004, FR-005 |
| SCR-C-006 | Home | Menu Browse, Guest Access, Popular Items | FR-001, FR-008, FR-012 |
| SCR-C-007 | Menu Category | Menu Browse | FR-001, FR-008 |
| SCR-C-008 | Search | Menu Search, Filter, Sort | FR-009, FR-010, FR-011 |
| SCR-C-009 | Product Detail | Item Detail, Customization, Favorites | FR-013, FR-014, FR-015 |
| SCR-C-010 | Cart | Cart Management, Promo, VAT, Upsell, Fee Transparency | FR-016, FR-017, FR-018, FR-019, FR-026 |
| SCR-C-011 | Checkout | Checkout, Delivery/Pickup, Scheduling, Address, Payment, Fees | FR-020, FR-021, FR-022, FR-024, FR-025, FR-026 |
| SCR-C-012 | Order Confirmation | Order Confirmation | FR-034 |
| SCR-C-013 | Payment | All Payment Methods, Saved Cards | FR-027, FR-028, FR-029, FR-030, FR-031, FR-032, FR-033 |
| SCR-C-014 | Order Tracking | Status Tracking, GPS, Driver Contact, Notifications | FR-034, FR-035, FR-036, FR-037 |
| SCR-C-015 | Order History | Order History, Reorder | FR-038, FR-039 |
| SCR-C-016 | Order Detail | Order Detail, Reorder, Receipt | FR-038, FR-039, FR-040 |
| SCR-C-017 | Receipt | VAT-Compliant Receipt | FR-040 |
| SCR-C-018 | Ratings | Item Ratings & Reviews | FR-041 |
| SCR-C-019 | Offers | Offers Tab, Introductory Offers | FR-042, FR-043 |
| SCR-C-020 | Address List | Multiple Addresses, Default Address | FR-044, FR-046 |
| SCR-C-021 | Address Add/Edit | Map Pin-Drop, Postal Integration, Address Management | FR-044, FR-045, FR-047 |
| SCR-C-022 | Profile | Profile Completion | FR-007 |
| SCR-C-023 | Settings | Notifications, Language, Account | FR-048, FR-049 |
| SCR-C-024 | Notifications | Push Notifications, Notification History | FR-037, FR-048 |
| SCR-C-025 | Loyalty | Basic Loyalty Program | FR-050 |
| SCR-C-026 | Branch Map | Branch Map, Curbside Pickup | FR-023 |
| SCR-C-027 | Favorites | Save Favorites | FR-015 |
| SCR-C-028 | Language | Language Toggle | FR-049 |

#### Driver App

| Screen ID | Screen Name | Features Served | Requirements |
|---|---|---|---|
| SCR-D-001 | Login | Driver Authentication | FR-051 |
| SCR-D-002 | Home/Dashboard | Availability, Order View, Accept/Decline | FR-053, FR-054, FR-055, FR-056 |
| SCR-D-003 | Order Detail | Order Details, Accept/Decline, Customer Contact | FR-055, FR-056, FR-060 |
| SCR-D-004 | Navigation | GPS Navigation, Location Sharing, Customer Contact | FR-057, FR-058, FR-060 |
| SCR-D-005 | Delivery Confirmation | Delivery Confirm, COD Collection | FR-059 |
| SCR-D-006 | Issue Report | Issue Reporting | FR-061 |
| SCR-D-007 | Performance | Performance Dashboard | FR-062 |
| SCR-D-008 | Profile | Driver Profile, Documents | FR-052 |
| SCR-D-009 | Support | Restaurant Support Channel | FR-063 |
| SCR-D-010 | Settings | Language, Notifications, GPS Settings | FR-006 (RTL), FR-049 (language) |

#### Restaurant Dashboard

| Screen ID | Screen Name | Features Served | Requirements |
|---|---|---|---|
| SCR-R-001 | Login | Admin Authentication | FR-064 |
| SCR-R-002 | Dashboard | Dashboard Overview | FR-065 |
| SCR-R-003 | Menu List | Menu CRUD, Availability Control | FR-066, FR-070 |
| SCR-R-004 | Menu Item Form | Menu CRUD, Variants, Pricing | FR-066, FR-068, FR-069 |
| SCR-R-005 | Category Manager | Category Management | FR-067 |
| SCR-R-006 | Order Board | Order Reception, Accept/Reject, Kitchen Coordination, Lifecycle | FR-071, FR-072, FR-074, FR-075 |
| SCR-R-007 | Order Detail | Order Detail, Prep Time, Driver Assignment, Lifecycle | FR-072, FR-073, FR-075, FR-077 |
| SCR-R-008 | Driver List | Driver Account Management, Performance | FR-076, FR-079 |
| SCR-R-009 | Driver Form | Driver Account Creation/Edit | FR-076 |
| SCR-R-010 | Driver Map | Driver GPS Tracking | FR-078 |
| SCR-R-011 | Delivery Zones | Delivery Zone Config, Delivery Fee Config | FR-081, FR-083 |
| SCR-R-012 | Business Settings | Operating Hours, Minimum Order, Tax Settings | FR-080, FR-082, FR-084 |
| SCR-R-013 | Payment Records | Payment Processing, Refund Management | FR-085, FR-086 |
| SCR-R-014 | Promo Manager | Promo Engine | FR-088 |
| SCR-R-015 | Promo Form | Promo Engine (Create/Edit) | FR-088 |
| SCR-R-016 | Push Notification Manager | Push Notification Management | FR-089 |
| SCR-R-017 | Email Campaign Manager | Email Marketing | FR-090 |
| SCR-R-018 | Sales Reports | Sales Reports | FR-091 |
| SCR-R-019 | Customer Analytics | Customer Analytics | FR-092 |
| SCR-R-020 | Popular Items | Popular Items Analysis | FR-093 |
| SCR-R-021 | Customer List | Customer Database | FR-087 |
| SCR-R-022 | Customer Detail | Customer Database (Detail) | FR-087 |
| SCR-R-023 | Support Tickets | Support Management | FR-094 |
| SCR-R-024 | Ticket Detail | Support Management (Detail) | FR-094 |
| SCR-R-025 | Branding Config | Branding Configuration | FR-095 |
| SCR-R-026 | System Settings | Platform Configuration | FR-095 |
| SCR-R-027 | Notification Settings | Notification Configuration | FR-096 |
| SCR-R-028 | Loyalty Config | Loyalty Program Configuration | FR-050 |

---

*End of Product Requirements Document*

*Document Version: v1.0 Draft*
*Last Updated: March 16, 2026*
*Total Screens: 28 (Customer) + 10 (Driver) + 28 (Restaurant) = 66 screens*
*Total User Stories: 96 (mapped from FR-001 through FR-096)*
*Total Feature Modules: 24*
