# Project Scope Document

## Food Delivery Platform - White-Label Solution

| Field | Detail |
|---|---|
| **Client Name** | Nael Mattar |
| **Vendor** | Space-O Technologies |
| **Project Name** | Food Delivery Platform |
| **Platform Type** | Mobile & Web-Based Food Delivery Platform |
| **Document Version** | v1.1 (based on SOW dated 28th August 2025) |
| **Scope Document Date** | March 2026 |

---

## 1. Executive Summary

This project is a comprehensive **white-label food delivery platform** designed for individual restaurants to manage their own branded food delivery operations. The platform enables restaurants to sell menu items directly to customers through a dedicated mobile application, eliminating third-party commission structures (such as Talabat, HungerStation, etc.) and giving restaurants complete control over their delivery operations, pricing, and customer relationships.

The platform follows a **three-role architecture**: **Customers** place orders through an Android mobile app and a lightweight web interface, **Drivers** handle deliveries using an Android mobile app, and **Restaurants** manage the entire operation through a web-based dashboard. The solution targets the **Saudi Arabian market** with full Arabic language support, RTL interface design, and integration with local payment methods (Mada, Google Pay, STC Pay).

The development is phased, with the **MVP (Phase 1)** covering all core ordering, delivery, and management features including a basic loyalty program (cashback/points). **Phase 2** is planned for advanced features such as tiered loyalty rewards and AI-driven personalization. Driver payments and settlements are handled offline between restaurants and drivers, simplifying the initial platform financial architecture.

---

## 2. Project Objectives & Goals

### Primary Objectives

- Build a white-label food delivery platform deployable for individual restaurant brands
- Deliver Android mobile apps for Customers and Drivers
- Deliver a responsive web dashboard for Restaurant management
- Support the Saudi Arabian market with full Arabic localization and RTL design
- Integrate local payment gateways (Mada, Google Pay, STC Pay) alongside international options
- Enable direct restaurant-to-customer ordering without third-party commission

### Business Goals

- Eliminate dependency on third-party delivery platforms and their commission structures
- Provide restaurants with full ownership of customer relationships and data
- Achieve competitive feature parity with market leaders (Maestro, Herfy, Albaik apps)
- Optimize customer conversion and retention through UX improvements (guest browsing, one-page checkout, upsells)
- Enable scalable white-label deployment across multiple restaurant brands

### Success Criteria / KPIs

- Successful deployment on Google Play Store
- All payment methods (Mada, Google Pay, STC Pay, credit/debit, COD) processing correctly
- Real-time GPS tracking functional for all deliveries
- Arabic/RTL interface passing comprehensive localization testing
- Guest browsing-to-registration conversion flow operational
- VAT-compliant receipt generation
- PCI compliance and local Saudi regulatory compliance achieved

---

## 3. Scope of Work

### 3.1 In-Scope

#### A. Customer Mobile Application (Android)

| # | Module | Description |
|---|---|---|
| 1 | User Registration & Authentication | OTP verification, social login (Google, Facebook), guest browsing, minimized signup, Arabic-friendly interface |
| 2 | Menu Browse & Search | Category browsing, advanced search, filters (price, availability, dietary), sorting, auto-suggest, popular items |
| 3 | Product Details & Customization | Images, descriptions, pricing, nutrition/allergy info, customization with icons/toggles, save favorites |
| 4 | Shopping Cart Management | Add/remove/edit items inline, promo codes, VAT display upfront, upsell prompts (rule-based) |
| 5 | Delivery & Pickup Options | Toggle delivery/pickup, scheduling, ETA, address management, branch map, curbside pickup |
| 6 | Streamlined Checkout | One-page checkout, progress indicator, comprehensive fee summary |
| 7 | Payment Processing | Credit/debit cards, Mada, Google Pay, STC Pay, COD, saved cards, quick selection |
| 8 | Real-Time Order Tracking | Order status tracking, live GPS, driver location on map, driver contact, push notifications |
| 9 | Order History & Ratings | Order history, reorder button, VAT-compliant receipts, favorite items, item-level ratings & reviews |
| 10 | Exclusive Offers & Discounts | Offers tab, one-tap apply, promo codes, introductory offers, push integration |
| 11 | Address Management | Multiple addresses, map pin-drop, labels, default locations, postal system integration |
| 12 | Notification System | Push notifications (orders, promos, delivery), preference controls, segmented/localized, rich notifications |
| 13 | Multi-Language Support | Arabic translations, RTL support, language toggle |
| 14 | Loyalty Features (Basic) | Introductory cashback/points system in MVP |

#### B. Driver Mobile Application (Android)

| # | Module | Description |
|---|---|---|
| 1 | Authentication & Profile | Restaurant-provided credentials login, profile management, document storage |
| 2 | Availability Management | Online/offline toggle, shift management, leave requests |
| 3 | Order Assignment | View assigned deliveries with full order and customer details |
| 4 | Order Management Workflow | Accept/decline requests, view order contents, customer contact info |
| 5 | GPS Navigation & Tracking | Built-in navigation, real-time location sharing to restaurant and customers |
| 6 | Delivery Confirmation | Confirm successful deliveries |
| 7 | Customer Communication | Direct call/message for delivery coordination |
| 8 | Issue Reporting | Report problems, customer unavailability, order issues with detailed reporting |
| 9 | Performance Tracking | Delivery statistics, completion rates, customer ratings |
| 10 | Support Communication | Direct channel with restaurant support |

#### C. Restaurant Web Dashboard

| # | Module | Description |
|---|---|---|
| 1 | Admin Authentication & Dashboard | Secure login, control panel with orders overview, sales metrics, operational status |
| 2 | Menu Catalog Management | CRUD for menu items with images, descriptions, pricing, availability, nutrition/allergy info |
| 3 | Category & Organization | Hierarchical categories, subcategories, menu structure |
| 4 | Real-Time Order Processing | Incoming orders, accept/reject, preparation times, kitchen coordination |
| 5 | Order Management System | Full order lifecycle from placement to delivery, status tracking |
| 6 | Driver Management | Create driver accounts, assign deliveries, live GPS tracking, performance monitoring |
| 7 | Business Settings | Operating hours, delivery zones (zone-based fee model), minimum orders, delivery fees, tax settings |
| 8 | Payment Management | Transaction processing, payment tracking, financial records |
| 9 | Customer Account Management | Customer database, registration monitoring |
| 10 | Marketing & Promotions | Discount codes, promo engine, push notifications, email campaigns |
| 11 | Sales Reporting & Analytics | Sales reports, customer analytics, popular items, driver performance metrics |
| 12 | Customer Support Management | Inquiries, support requests, issue resolution |
| 13 | Platform Configuration | System settings, branding, notification preferences, operational parameters |
| 14 | Menu Availability Control | Real-time availability, stock management, menu item toggling |

#### D. Backend Infrastructure & Integrations

- RESTful API backend (Node.js / Express.js)
- Real-time communication layer (Socket.io)
- Payment gateway integration (Stripe + Mada, Google Pay, STC Pay)
- Google Maps API integration
- Firebase Authentication (OTP/phone auth) + Firebase Cloud Messaging (push notifications)
- Cloud file storage (AWS S3)
- JWT-based authentication system
- PostgreSQL database
- AWS hosting (Bahrain region)
- CI/CD pipeline and containerized deployment

### 3.2 Out of Scope

**Explicitly excluded or deferred to Phase 2:**

| Item | Status |
|---|---|
| iOS mobile apps (Customer & Driver) | Excluded -- Android and Web only (scope change from original SOW) |
| Apple Pay integration | Excluded -- replaced by Google Pay (consequence of dropping iOS) |
| Apple Sign-In (social login) | Excluded -- not required without iOS. Google + Facebook login retained |
| Apple App Store submission | Excluded -- no iOS apps |
| Advanced tiered loyalty/rewards program | Deferred to Phase 2 |
| AI-driven personalization for upsell prompts | Deferred to Phase 2 (rule-based in Phase 1) |
| In-app driver payment/settlement processing | Explicitly excluded -- handled offline between restaurants and drivers |

**Items requiring clarification (ambiguous):**

| Item | Notes |
|---|---|
| Full customer web ordering app | SOW mentions "access via web browser" once, but all features are mobile-focused. Scope includes lightweight customer web interface alongside Android app. |
| General order refund workflow | No refund policy for order-related issues. Refunds limited to technical/payment failures only (stuck payments, double charges). |
| Multi-restaurant marketplace | NOT in scope -- platform is white-label per individual restaurant |
| Admin super-panel for white-label management | NOT in scope -- not mentioned in SOW |
| Detailed refund/cancellation workflow | NOT in scope as a standalone feature -- SOW mentions "refunds" once in passing under financial reconciliation. Basic refund handling via dashboard only. |
| Kitchen Display System (KDS) | NOT in scope -- "kitchen coordination" in SOW refers to dashboard order management, not a separate KDS screen |
| Email service provider | Email marketing mentioned in SOW but provider not specified -- to be decided during development |
| Google Play Store submission | Not mentioned in SOW -- to be confirmed who handles (iOS removed from scope) |

---

## 4. Functional Requirements

### 4.1 Customer App - Registration & Access

| ID | Requirement | Description |
|---|---|---|
| FR-001 | Guest Browsing | Users can browse full restaurant menu, view items and prices without registration |
| FR-002 | OTP Registration | Register via SMS/email OTP verification |
| FR-003 | Social Login | Login via Google and Facebook accounts (Apple Sign-In removed -- not required without iOS) |
| FR-004 | Phone/Email Registration | Alternative registration with phone or email |
| FR-005 | Minimized Signup | Reduced form fields to minimize registration friction |
| FR-006 | Arabic-Friendly Interface | Registration flow supports Arabic language and RTL layout |
| FR-007 | Profile Completion | Add delivery addresses (map pin-drop), payment preferences, dietary restrictions |

### 4.2 Customer App - Menu & Search

| ID | Requirement | Description |
|---|---|---|
| FR-008 | Category Browsing | Browse menu organized by categories and subcategories |
| FR-009 | Advanced Search | Search with auto-suggest functionality |
| FR-010 | Filtering | Filter by price, availability, dietary preferences |
| FR-011 | Sorting | Multiple sorting options for menu items |
| FR-012 | Popular Items Section | Display trending/popular menu items |
| FR-013 | Product Detail View | Images, descriptions, pricing, nutrition/allergy information |
| FR-014 | Item Customization | Size, toppings, spice level, special instructions via clear icons/toggles |
| FR-015 | Save Favorites | Save favorite menu items for quick access |

### 4.3 Customer App - Cart & Checkout

| ID | Requirement | Description |
|---|---|---|
| FR-016 | Cart Management | Add/remove items, inline quantity editing |
| FR-017 | Promo Code Application | Apply discount codes and promotional codes |
| FR-018 | VAT Display | Show VAT calculations upfront in cart totals |
| FR-019 | Upsell Prompts | Rule-based "Frequently ordered together" suggestions |
| FR-020 | Delivery/Pickup Toggle | Switch between home delivery and restaurant pickup |
| FR-021 | Order Scheduling | Schedule delivery/pickup for a future time |
| FR-022 | ETA Display | Show estimated delivery/pickup time |
| FR-023 | Branch Map | Map showing restaurant branches with curbside pickup option |
| FR-024 | Address Selection | Select from saved addresses or add new via map pin-drop |
| FR-025 | One-Page Checkout | Single-page checkout with progress indicator |
| FR-026 | Fee Transparency | Comprehensive order summary showing all fees (subtotal, VAT, delivery, discounts) |

### 4.4 Customer App - Payment

| ID | Requirement | Description |
|---|---|---|
| FR-027 | Credit/Debit Card Payment | Standard card payment processing |
| FR-028 | Mada Payment | Saudi local debit card payment integration |
| FR-029 | Google Pay | Google Pay payment integration via Stripe (replaces Apple Pay -- not applicable on Android) |
| FR-030 | STC Pay | STC Pay payment integration |
| FR-031 | Cash on Delivery | COD payment option |
| FR-032 | Saved Cards | Save payment cards for quick future checkout |
| FR-033 | Quick Payment Selection | Fast payment method selection UI |

### 4.5 Customer App - Order Tracking & History

| ID | Requirement | Description |
|---|---|---|
| FR-034 | Order Status Tracking | Track order through confirmation, preparation, pickup, delivery stages |
| FR-035 | Live GPS Tracking | Real-time driver location on map |
| FR-036 | Driver Contact | Call/message driver directly from tracking screen |
| FR-037 | Push Notifications | Notifications for order confirmation, status changes, delivery alerts |
| FR-038 | Order History | View complete past order history |
| FR-039 | Reorder Function | Dedicated reorder button for one-click repeat orders |
| FR-040 | VAT-Compliant Receipts | Generate and view receipts compliant with VAT regulations |
| FR-041 | Item Ratings & Reviews | Rate and review individual menu items with comments |

### 4.6 Customer App - Offers, Addresses & Settings

| ID | Requirement | Description |
|---|---|---|
| FR-042 | Offers Tab | Dedicated tab showing all available offers with one-tap apply |
| FR-043 | Introductory Offers | Strong introductory discount offers for new customers |
| FR-044 | Multiple Addresses | Save multiple delivery addresses with labels (Home, Work, etc.) |
| FR-045 | Map Pin-Drop | Add addresses using map pin-drop interface |
| FR-046 | Default Address | Set a default delivery address |
| FR-047 | Postal System Integration | Integration with official postal system for accurate addressing |
| FR-048 | Notification Preferences | User control over notification types and frequency |
| FR-049 | Language Toggle | Switch between Arabic and English |
| FR-050 | Basic Loyalty Program | Introductory cashback/points framework as mentioned in SOW. Detailed rules (points per SAR, redemption rates) to be defined by restaurant via dashboard. No complex tiered logic in Phase 1. |

### 4.7 Driver App

| ID | Requirement | Description |
|---|---|---|
| FR-051 | Driver Login | Login with restaurant-provided credentials (username/ID + password) |
| FR-052 | Driver Profile | Basic profile management with contact info, vehicle details, document storage |
| FR-053 | Availability Toggle | Set available/unavailable status |
| FR-054 | Shift Management | Manage work schedule and leave requests |
| FR-055 | Order Assignment View | View assigned deliveries with order details, customer info, delivery instructions |
| FR-056 | Accept/Decline Orders | Accept or decline delivery requests |
| FR-057 | GPS Navigation | Built-in navigation to customer locations |
| FR-058 | Real-Time Location Sharing | Share live location with restaurant and customers |
| FR-059 | Delivery Confirmation | Confirm successful delivery completion |
| FR-060 | Customer Communication | Direct call/message to customer |
| FR-061 | Issue Reporting | Report problems with detailed reporting system |
| FR-062 | Performance Dashboard | View delivery stats, completion rates, customer ratings |
| FR-063 | Restaurant Support Channel | Direct communication with restaurant support |

### 4.8 Restaurant Web Dashboard

| ID | Requirement | Description |
|---|---|---|
| FR-064 | Admin Login | Secure dashboard authentication |
| FR-065 | Dashboard Overview | Control panel with orders overview, sales metrics, operational status |
| FR-066 | Menu CRUD | Add, edit, delete menu items with images, descriptions, pricing, nutrition/allergy info |
| FR-067 | Category Management | Create/manage hierarchical categories and subcategories |
| FR-068 | Item Variants | Configure size, topping, modification variants with individual pricing |
| FR-069 | Pricing Management | Set prices, bulk discounts, promotional pricing |
| FR-070 | Availability Control | Real-time toggle item availability, stock level management |
| FR-071 | Order Reception | Receive incoming orders with real-time notifications |
| FR-072 | Order Accept/Reject | Accept or reject orders based on capacity |
| FR-073 | Preparation Time Setting | Set estimated preparation times per order |
| FR-074 | Kitchen Coordination | Tools for coordinating with kitchen staff |
| FR-075 | Order Lifecycle Tracking | Track orders from placement through delivery |
| FR-076 | Driver Account Management | Create and manage driver accounts |
| FR-077 | Driver Assignment | Assign deliveries to available drivers |
| FR-078 | Driver GPS Tracking | Monitor driver locations in real-time on map |
| FR-079 | Driver Performance Monitoring | Track driver metrics and performance |
| FR-080 | Operating Hours Config | Set business operating hours and days |
| FR-081 | Delivery Zone Config | Define delivery coverage areas |
| FR-082 | Minimum Order Config | Set minimum order amounts |
| FR-083 | Delivery Fee Config | Zone-based delivery fee configuration (restaurant defines delivery zones on map with different fee per zone) |
| FR-084 | Tax Settings | Configure VAT and tax rates |
| FR-085 | Payment Processing | Process and track transactions |
| FR-086 | Refund Management | Limited to technical/payment failure scenarios only (e.g., payment stuck, double charge). No general order refund workflow in Phase 1. |
| FR-087 | Customer Database | View customer registrations and information |
| FR-088 | Promo Engine | Create discount codes, promotional campaigns |
| FR-089 | Push Notification Management | Send targeted push notifications to customers |
| FR-090 | Email Marketing | Email campaign capabilities |
| FR-091 | Sales Reports | Generate detailed sales and revenue reports |
| FR-092 | Customer Analytics | Customer behavior and segment analytics |
| FR-093 | Popular Items Analysis | Track and analyze trending menu items |
| FR-094 | Support Management | Handle customer inquiries and complaints |
| FR-095 | Branding Configuration | Configure white-label branding elements |
| FR-096 | Notification Configuration | Set up system notification preferences |

---

## 5. Non-Functional Requirements

### 5.1 Performance

| ID | Requirement | Description |
|---|---|---|
| NFR-001 | Real-Time Updates | Order tracking and GPS location updates must be real-time via Socket.io |
| NFR-002 | Fast Query Performance | Database optimized for fast query performance (as stated in SOW) |
| NFR-003 | Scalable Architecture | Microservices architecture supporting horizontal scaling |

### 5.2 Security

| ID | Requirement | Description |
|---|---|---|
| NFR-004 | Data Encryption | Multi-layer security with data encryption at rest and in transit |
| NFR-005 | Secure Authentication | JWT-based token authentication with OTP verification |
| NFR-006 | PCI Compliance | Payment processing must meet PCI DSS requirements |
| NFR-007 | Local Regulation Compliance | Compliance with Saudi Arabian regulations (data privacy, commerce) |

### 5.3 Localization

| ID | Requirement | Description |
|---|---|---|
| NFR-008 | Arabic Language Support | Professional Arabic translations throughout the platform |
| NFR-009 | RTL Layout | Full right-to-left layout support with comprehensive RTL testing |
| NFR-010 | Regional Preferences | Culturally appropriate content, formats, and UX patterns |

### 5.4 Platform & Technology Constraints

| ID | Requirement | Description |
|---|---|---|
| NFR-011 | Android Mobile | Android support via **React Native** (iOS not in scope) |
| NFR-012 | Web Dashboard | React.js responsive web application |
| NFR-013 | Backend | Node.js with Express.js |
| NFR-014 | Database | **PostgreSQL** |
| NFR-015 | Cloud Hosting | **AWS** (Bahrain region for Saudi market proximity) |
| NFR-016 | API Architecture | RESTful API design |
| NFR-017 | Containerized Deployment | Docker containerization with CI/CD pipeline |
| NFR-018a | OTP/Auth Provider | **Firebase Authentication** (phone auth with free tier) |

### 5.5 Testing

| ID | Requirement | Description |
|---|---|---|
| NFR-018 | Unit Testing | Comprehensive unit test coverage |
| NFR-019 | Integration Testing | API and service integration testing |
| NFR-020 | End-to-End Testing | Full user flow E2E testing |
| NFR-021 | Arabic/RTL Testing | Dedicated testing for Arabic translations and RTL interface |

---

## 6. Deliverables & Milestones

### 6.1 Deliverables

| # | Deliverable | Format/Platform |
|---|---|---|
| 1 | Customer Mobile App (Android) | Google Play Store deployment |
| 2 | Customer Web Interface | Lightweight responsive web (menu browsing, ordering) |
| 3 | Driver Mobile App (Android) | Google Play Store deployment |
| 4 | Restaurant Web Dashboard | Web application (responsive) |
| 5 | Backend API Services | Node.js microservices |
| 6 | Database Schema & Setup | PostgreSQL |
| 7 | Payment Gateway Integration | Stripe + Mada, Google Pay, STC Pay |
| 8 | Real-Time Communication Layer | Socket.io implementation |
| 9 | Push Notification System | Firebase Cloud Messaging setup |
| 10 | Maps & Navigation Integration | Google Maps API integration |
| 11 | API Documentation | RESTful API documentation |
| 12 | White-Label Configuration System | Branding customization capability |
| 13 | Arabic/RTL Localization | Complete Arabic translations and RTL support |

### 6.2 Phase Breakdown

| Phase | Scope | Status |
|---|---|---|
| **Phase 1 (MVP)** | All features listed in Section 3.1 including basic loyalty (cashback/points), rule-based upsell prompts | Current scope |
| **Phase 2** | Advanced tiered loyalty/rewards program, AI-driven personalization for recommendations | Future scope |

### 6.3 Milestones & Timeline

> **NOTE:** The SOW document does **not** specify any timeline, milestones, sprint schedule, or delivery dates. These must be negotiated and agreed upon with the client.

---

## 7. Assumptions

### Technical Assumptions

| # | Assumption | Risk Level |
|---|---|---|
| A-001 | Mobile framework: **React Native** (confirmed) | Resolved |
| A-002 | Database: **PostgreSQL** (confirmed) | Resolved |
| A-003 | Cloud provider: **AWS** (confirmed) | Resolved |
| A-004 | Google Maps API will be the maps/navigation provider | Low |
| A-005 | Firebase Cloud Messaging will handle all push notifications | Low |
| A-006 | Socket.io is sufficient for real-time communication at expected scale | Low |

### Business Assumptions

| # | Assumption | Risk Level |
|---|---|---|
| A-007 | The platform targets the Saudi Arabian market primarily (based on Mada, STC Pay, Arabic localization references) | Low |
| A-008 | Driver payments are entirely offline and do NOT require in-app wallet, earnings tracking, or payout features | Medium |
| A-009 | Each white-label deployment serves a single restaurant brand (not a multi-restaurant marketplace) | High |
| A-010 | The client (Nael Mattar) will provide all restaurant branding assets (logos, colors, content) | Medium |
| A-011 | Arabic translations will be provided by the vendor (Space-O) as "professional translations" are mentioned | Medium |
| A-012 | OTP SMS costs will be borne by the client/restaurant operator | Low |
| A-013 | Google Maps API usage costs will be borne by the client/restaurant operator | Low |
| A-014 | Payment gateway merchant accounts will be set up by the client | Medium |
| A-015 | Competitive parity targets are Maestro, Herfy, and Albaik apps (mentioned in document) | Low |

### Process Assumptions

| # | Assumption | Risk Level |
|---|---|---|
| A-016 | Agile development methodology with iterative releases (as stated in SOW) | Low |
| A-017 | User flow diagrams referenced in the SOW (Customer, Driver, Restaurant) have been finalized and approved | Medium |
| A-018 | The SOW represents the agreed-upon scope and all bold items reflect incorporated client feedback | Low |

---

## 8. Dependencies & Constraints

### External Dependencies

| # | Dependency | Type | Impact |
|---|---|---|---|
| D-001 | Google Maps API | Third-party service | GPS tracking, navigation, address pin-drop all depend on this |
| D-002 | Stripe Payment Gateway | Third-party service | Primary payment processing (credit/debit cards, Google Pay). Stripe supports Mada in Saudi Arabia. |
| D-003 | Mada (via Stripe) | Third-party service | Saudi local debit card payments. Supported natively by Stripe in Saudi Arabia. |
| D-004 | Google Pay (via Stripe) | Third-party service | Google Pay checkout via Stripe integration |
| D-005 | STC Pay API | Third-party service | STC Pay checkout. May require separate integration if Stripe does not support STC Pay natively. |
| D-006 | Firebase Cloud Messaging | Third-party service | Push notifications for Android |
| D-007 | Google Play Store | Distribution | Android app publishing and review process |
| D-009 | SMS/OTP Service Provider | Third-party service | Customer registration verification |
| D-010 | Email Service Provider | Third-party service | Email marketing campaigns, transactional emails |
| D-011 | Cloud Hosting Provider | Infrastructure | Application hosting and scaling |
| D-012 | Official Postal System API | Government/third-party | Address management integration (Saudi postal system) |
| D-013 | Social Login Providers | Third-party service | Google, Facebook OAuth |

### Client-Provided Dependencies

| # | Dependency | Description |
|---|---|---|
| D-014 | Restaurant Branding Assets | Logos, color schemes, content for white-label customization |
| D-015 | Menu Content | Initial menu items, descriptions, images, pricing, nutrition data |
| D-016 | Payment Merchant Accounts | Stripe merchant account, STC Pay merchant setup |
| D-017 | Business Rules | Delivery zones, operating hours, fee structures, tax rates |
| D-018 | Domain & SSL Certificates | For web dashboard hosting |

### Constraints

| # | Constraint | Description |
|---|---|---|
| C-001 | Saudi Regulations | Must comply with Saudi Arabian e-commerce, data privacy, and food delivery regulations |
| C-002 | PCI DSS | Payment processing must meet PCI compliance standards |
| C-003 | VAT Compliance | Receipts and pricing must be VAT-compliant per Saudi tax requirements |
| C-004 | RTL Design | All UI must fully support right-to-left Arabic layout |
| C-005 | Offline Driver Payments | Platform must NOT process driver payments -- handled outside the system |

---

## 9. Risks & Open Questions

### Identified Risks

| ID | Risk | Severity | Mitigation |
|---|---|---|---|
| R-001 | ~~Mobile framework not decided~~ | ~~High~~ | **RESOLVED: React Native confirmed** |
| R-002 | ~~Database not decided~~ | ~~High~~ | **RESOLVED: PostgreSQL confirmed** |
| R-003 | STC Pay may require separate integration outside Stripe. Mada and Google Pay are supported via Stripe natively. | **Medium** | Verify Stripe STC Pay support in Saudi Arabia early. If unsupported, plan separate STC Pay integration. |
| R-004 | "Official postal system integration" is vague -- Saudi postal APIs may have limited availability or documentation | **Medium** | Research Saudi Post (SPL) API availability early; prepare fallback (manual address entry) |
| R-005 | Arabic translation quality could impact UX if not done by native speakers with domain expertise | **Medium** | Engage professional Arabic translators; conduct user testing with native Arabic speakers |
| R-006 | Real-time GPS tracking at scale requires careful Socket.io architecture and server capacity planning | **Medium** | Load test real-time features; plan for WebSocket connection scaling |
| R-007 | No timeline or budget defined -- scope creep risk is elevated without clear boundaries | **High** | Establish timeline, milestones, and budget before development begins |
| R-008 | White-label deployment complexity -- each restaurant instance needs its own branding, config, and potentially its own app store listing | **Medium** | Define white-label deployment architecture and process early |
| R-009 | PCI compliance requires specific security measures that may extend development timeline | **Medium** | Engage PCI compliance consultant; use PCI-compliant payment SDKs to reduce scope |
| R-010 | Guest browsing to registration conversion may have UX friction points | **Low** | A/B test registration prompts; minimize signup friction as specified |

### Open Questions for Client

| # | Question | Priority |
|---|---|---|
| OQ-001 | ~~Customer web interface~~ -- **RESOLVED: Android + Web (no iOS). Lightweight customer web interface is in scope alongside Android app** | Resolved |
| OQ-002 | What is the target timeline for Phase 1 (MVP) delivery? Are there hard launch dates? | **High** |
| OQ-003 | What is the project budget, and how is it structured (fixed price, T&M, milestones)? | **High** |
| OQ-004 | ~~Mobile framework~~ -- **RESOLVED: React Native** | Resolved |
| OQ-005 | ~~Database~~ -- **RESOLVED: PostgreSQL** | Resolved |
| OQ-006 | ~~Cloud provider~~ -- **RESOLVED: AWS (Bahrain region)** | Resolved |
| OQ-007 | ~~SMS/OTP provider~~ -- **RESOLVED: Firebase Authentication (phone auth)** | Resolved |
| OQ-008 | ~~Email service provider~~ -- **RESOLVED: SOW mentions email marketing as a feature (FR-090). Provider to be decided during development. Feature stays in scope, provider is a dev-time decision.** | Resolved |
| OQ-009 | Which specific "official postal system" should be integrated for address management? (Saudi Post/SPL?) | **Medium** |
| OQ-010 | ~~Refund/cancellation workflow~~ -- **RESOLVED: No general refund policy. Refunds only for technical/payment failures (stuck payments, double charges).** | Resolved |
| OQ-011 | Should the vendor handle Google Play Store submission, or will the client manage this? (iOS no longer applicable) | **Medium** |
| OQ-012 | How many initial restaurant deployments are planned? This impacts infrastructure sizing. | **Medium** |
| OQ-013 | Is there a kitchen display system (KDS) requirement, or is "kitchen coordination" limited to the dashboard order view? | **Medium** |
| OQ-014 | What is the expected order volume at launch? This impacts architecture decisions. | **Medium** |
| OQ-015 | Are there specific Saudi regulatory requirements beyond PCI and VAT that must be addressed? (e.g., CITC, NCA, PDPL) | **High** |
| OQ-016 | ~~Loyalty program rules~~ -- **RESOLVED: Build framework only per SOW. Restaurant configures rules (points per SAR, redemption rate) via dashboard. No hardcoded rules.** | Resolved |
| OQ-017 | Should drivers be able to self-register, or is restaurant-provisioned accounts the only model? | **Low** |
| OQ-018 | ~~Multi-branch support~~ -- **RESOLVED: Yes, multi-branch supported (SOW mentions "branch map"). Each restaurant brand can have multiple locations with separate menus, hours, delivery zones.** | Resolved |
| OQ-019 | ~~Delivery fee model~~ -- **RESOLVED: Zone-based. Restaurant defines delivery zones on map with different fees per zone.** | Resolved |
| OQ-020 | Will the platform need to handle restaurant operating in multiple time zones, or is it Saudi Arabia only? | **Low** |

---

## 10. Acceptance Criteria

### High-Level Project Acceptance Criteria

| # | Criteria |
|---|---|
| AC-001 | All three applications (Customer App, Driver App, Restaurant Dashboard) are functional and deployed |
| AC-002 | Customer can complete full ordering flow: browse -> customize -> cart -> checkout -> payment -> track -> receive |
| AC-003 | Driver can complete full delivery flow: login -> set availability -> receive assignment -> navigate -> deliver -> confirm |
| AC-004 | Restaurant can complete full management flow: login -> manage menu -> process orders -> assign drivers -> track -> report |
| AC-005 | All payment methods (Mada, Google Pay, STC Pay, credit/debit, COD) process successfully |
| AC-006 | Real-time GPS tracking works for all active deliveries |
| AC-007 | Arabic language and RTL layout are complete and tested across all interfaces |
| AC-008 | Push notifications deliver for all critical events (order confirmation, status changes, promotions) |
| AC-009 | Guest browsing allows full menu access without registration |
| AC-010 | OTP and social login registration flows work correctly |
| AC-011 | VAT-compliant receipts are generated for all completed orders |
| AC-012 | Platform passes security audit for PCI compliance |
| AC-013 | White-label branding is configurable per restaurant deployment |
| AC-014 | Basic loyalty program (cashback/points) is functional |

### Per-Feature Acceptance Criteria (Key Features)

| Feature | Acceptance Criteria |
|---|---|
| Guest Browsing | User can view full menu, item details, and prices without creating an account. Cart and checkout require registration. |
| OTP Verification | User receives OTP within 60 seconds. OTP expires after reasonable timeout. Retry mechanism available. |
| Menu Search | Search returns relevant results within 2 seconds. Auto-suggest shows suggestions after 2+ characters. Filters correctly narrow results. |
| Cart Management | Items can be added, removed, and quantity modified inline. Promo codes apply correct discounts. VAT is calculated and displayed before checkout. |
| Real-Time Tracking | Driver location updates on map at minimum every 10-15 seconds. Order status changes reflect within seconds. |
| One-Page Checkout | Entire checkout (address, payment, summary) on single scrollable page. Progress indicator shows current step. |
| Driver Assignment | Restaurant can see available drivers, assign orders. Driver receives notification of new assignment. |
| Reporting | Sales reports can be filtered by date range, show totals for revenue, orders, average order value. Export capability. |

---

## 11. Glossary

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
| **KDS** | Kitchen Display System -- screen-based system for kitchen order management |
| **MVP** | Minimum Viable Product -- the first production-ready version with core features |
| **Promo Engine** | A system for creating, managing, and applying promotional discounts and offers |
| **PDPL** | Saudi Personal Data Protection Law |
| **NCA** | National Cybersecurity Authority (Saudi Arabia) |
| **CITC** | Communications, Information Technology and Communications Commission (Saudi Arabia) |
| **SPL** | Saudi Post Logistics -- the national postal service of Saudi Arabia |

---

---

### Scope Change Log

| Date | Change | Impact |
|---|---|---|
| March 2026 | **Removed iOS from scope** -- Android and Web only | Removed: iOS apps (Customer + Driver), Apple App Store, Apple Pay (replaced with Google Pay), Apple Sign-In. Reduced deliverables from 14 to 13. |
| March 2026 | **Technology stack finalized** | React Native, PostgreSQL, AWS (Bahrain), Firebase Auth for OTP, Stripe for payments |
| March 2026 | **Delivery fee model decided** | Zone-based delivery fees. Restaurant defines zones on map with different fees per zone. |
| March 2026 | **Multi-branch confirmed** | Each restaurant brand supports multiple branch locations with separate menus, hours, delivery zones. |
| March 2026 | **Refund policy defined** | No general refund workflow. Refunds limited to technical/payment failures only. |
| March 2026 | **Loyalty program scoped** | Build configurable framework only. Restaurant sets rules via dashboard. No hardcoded business logic. |

---

*Document prepared based on analysis of Space-O Technologies SOW v1.1 dated 28th August 2025.*
*Items marked with bold in the original SOW represent changes incorporated from client feedback.*
*Scope modifications (iOS removal) applied per project team decision, March 2026.*
