# Scope Checklist

## Food Delivery Platform - Nael Mattar / Space-O Technologies

---

## 1. Deliverables Checklist

### Customer Mobile Application (Android) + Customer Web Interface

- [ ] Guest browsing (menu access without registration)
- [ ] OTP verification registration (SMS/email)
- [ ] Social login integration (Google, Facebook) -- Apple Sign-In removed (no iOS)
- [ ] Phone/email registration with minimized signup fields
- [ ] Arabic-friendly registration interface
- [ ] Profile setup (addresses, payment preferences, dietary restrictions)
- [ ] Menu category browsing
- [ ] Advanced search with auto-suggest
- [ ] Filtering (price, availability, dietary preferences)
- [ ] Sorting capabilities
- [ ] Popular items section
- [ ] Product detail view (images, descriptions, pricing, nutrition/allergy info)
- [ ] Item customization (size, toppings, spice level, special instructions) with icons/toggles
- [ ] Save favorites functionality
- [ ] Shopping cart (add/remove/edit inline)
- [ ] Promo code and discount code application
- [ ] VAT calculations displayed upfront
- [ ] Rule-based upsell prompts ("Frequently ordered together")
- [ ] Delivery/pickup toggle
- [ ] Order scheduling
- [ ] ETA display
- [ ] Branch map with curbside pickup option
- [ ] Address management (multiple, labels, default, map pin-drop)
- [ ] Official postal system integration
- [ ] One-page checkout with progress indicator
- [ ] Comprehensive fee summary display
- [ ] Credit/debit card payment
- [ ] Mada payment integration
- [ ] Google Pay integration (replaces Apple Pay -- Android only)
- [ ] STC Pay integration
- [ ] Cash on delivery option
- [ ] Saved cards functionality
- [ ] Quick payment selection UI
- [ ] Real-time order status tracking
- [ ] Live GPS driver tracking on map
- [ ] Driver contact options (call/message)
- [ ] Push notifications (orders, status, promotions, delivery)
- [ ] Notification preference controls
- [ ] Segmented and localized push notifications
- [ ] Rich push notifications
- [ ] Order history view
- [ ] Reorder button (one-click reorder)
- [ ] VAT-compliant receipts
- [ ] Favorite items highlighting
- [ ] Item-level ratings and reviews with comments
- [ ] Dedicated offers tab with one-tap apply
- [ ] Introductory offers for new customers
- [ ] Multi-language support (Arabic/English)
- [ ] RTL layout support
- [ ] Language toggle
- [ ] Basic loyalty program (cashback/points)

### Driver Mobile Application (Android)

- [ ] Login with restaurant-provided credentials
- [ ] Basic profile management
- [ ] Document storage
- [ ] Availability toggle (online/offline)
- [ ] Shift management and leave requests
- [ ] View assigned deliveries with full details
- [ ] Accept/decline delivery requests
- [ ] View order contents and customer contact info
- [ ] Built-in GPS navigation to customer location
- [ ] Real-time location sharing to restaurant and customers
- [ ] Delivery confirmation
- [ ] Direct call functionality to customers
- [ ] Direct message functionality to customers
- [ ] Issue reporting with detailed reporting system
- [ ] Performance dashboard (stats, completion rates, ratings)
- [ ] Restaurant support communication channel

### Restaurant Web Dashboard

- [ ] Secure admin login
- [ ] Dashboard overview (orders, sales metrics, operational status)
- [ ] Menu item CRUD (add, edit, delete) with full details
- [ ] Image upload for menu items
- [ ] Nutrition/allergy information management
- [ ] Category and subcategory management
- [ ] Item variant configuration (sizes, toppings, modifications)
- [ ] Pricing management (regular, bulk discount, promotional)
- [ ] Real-time item availability toggle
- [ ] Stock level management
- [ ] Incoming order reception with notifications
- [ ] Order accept/reject functionality
- [ ] Preparation time setting
- [ ] Kitchen coordination tools
- [ ] Full order lifecycle tracking
- [ ] Driver account creation and management
- [ ] Driver assignment to deliveries
- [ ] Live GPS driver tracking on map
- [ ] Driver performance monitoring
- [ ] Operating hours configuration
- [ ] Delivery zone configuration
- [ ] Minimum order amount setting
- [ ] Delivery fee configuration (zone-based: restaurant defines zones on map with per-zone fees)
- [ ] Tax/VAT settings
- [ ] Payment processing and tracking
- [ ] Financial records and reconciliation
- [ ] Customer database and registration monitoring
- [ ] Promo engine (discount codes, campaigns)
- [ ] Push notification management
- [ ] Email marketing campaign tools
- [ ] Sales reports generation
- [ ] Customer analytics
- [ ] Popular items analysis
- [ ] Driver performance metrics
- [ ] Customer support/inquiry management
- [ ] White-label branding configuration
- [ ] System notification preferences
- [ ] Operational parameter settings

### Backend & Infrastructure

- [ ] RESTful API services (Node.js / Express.js)
- [ ] JWT authentication system
- [ ] Real-time communication (Socket.io)
- [ ] Database setup and schema (PostgreSQL)
- [ ] Stripe payment gateway integration (primary processor)
- [ ] Mada payment integration (via Stripe)
- [ ] Google Pay integration (via Stripe)
- [ ] STC Pay integration (may need separate integration if Stripe doesn't support natively)
- [ ] Google Maps API integration
- [ ] Firebase Authentication setup (OTP/phone auth)
- [ ] Firebase Cloud Messaging setup (push notifications)
- [ ] Cloud file storage (AWS S3)
- [ ] CI/CD pipeline setup
- [ ] Containerized deployment (Docker)
- [ ] AWS hosting setup (Bahrain region)
- [ ] API documentation
- [ ] Arabic/RTL complete localization

### Testing

- [ ] Unit test coverage
- [ ] Integration testing
- [ ] End-to-end testing
- [ ] Arabic/RTL interface testing
- [ ] Payment gateway testing (all methods)
- [ ] Real-time GPS tracking testing
- [ ] Android mobile testing (multiple device sizes/OS versions)
- [ ] Customer web interface testing (cross-browser)
- [ ] Performance/load testing
- [ ] Security audit / PCI compliance verification

---

## 2. Open Questions to Discuss with Client

### Resolved

- [x] **OQ-001**: ~~Customer web interface~~ -- **Android + Web (no iOS)**
- [x] **OQ-004**: ~~Mobile framework~~ -- **React Native**
- [x] **OQ-005**: ~~Database~~ -- **PostgreSQL**
- [x] **OQ-006**: ~~Cloud provider~~ -- **AWS (Bahrain region)**
- [x] **OQ-007**: ~~SMS/OTP provider~~ -- **Firebase Authentication (phone auth)**

### Recently Resolved

- [x] **OQ-010**: ~~Refund/cancellation~~ -- **No general refund. Technical/payment failures only.**
- [x] **OQ-016**: ~~Loyalty rules~~ -- **Framework only. Restaurant configures via dashboard.**
- [x] **OQ-018**: ~~Multi-branch~~ -- **Yes, confirmed. SOW implies with "branch map".**
- [x] **OQ-019**: ~~Delivery fee model~~ -- **Zone-based. Restaurant defines zones on map.**
- [x] **OQ-021**: ~~Payment gateway~~ -- **Stripe (supports Mada + Google Pay natively).**
- [x] **OQ-008**: ~~Email provider~~ -- **Feature in scope per SOW. Provider deferred to dev-time decision.**

### Still Open

- [ ] **OQ-002**: What is the **target timeline** for Phase 1 (MVP) delivery? (No timeline set yet)
- [ ] **OQ-003**: What is the **project budget**, and how is it structured?
- [ ] **OQ-009**: Which specific "**official postal system**" should be integrated? (Saudi Post/SPL?)
- [ ] **OQ-011**: Should the vendor handle **Google Play Store submission**, or will the client?
- [ ] **OQ-012**: How many **initial restaurant deployments** are planned? (impacts infrastructure sizing)
- [ ] **OQ-013**: Is a **kitchen display system (KDS)** required, or is "kitchen coordination" limited to dashboard?
- [ ] **OQ-014**: What is the **expected order volume** at launch? (Not decided yet)
- [ ] **OQ-015**: Are there specific **Saudi regulatory requirements** beyond PCI and VAT? (CITC, NCA, PDPL)

### Low Priority (Still Open)

- [ ] **OQ-017**: Should drivers be able to **self-register**, or is restaurant-provisioned the only model?
- [ ] **OQ-020**: Will the platform need **multi-timezone support**, or Saudi Arabia only?

---

## 3. Assumptions to Validate

### Technical Assumptions

- [x] **A-001**: ~~Mobile framework~~ -- **Confirmed: React Native**
- [x] **A-002**: ~~Database~~ -- **Confirmed: PostgreSQL**
- [x] **A-003**: ~~Cloud provider~~ -- **Confirmed: AWS (Bahrain region)**
- [x] **A-003a**: ~~OTP provider~~ -- **Confirmed: Firebase Authentication**
- [ ] **A-004**: Google Maps API is confirmed as the maps/navigation provider
- [ ] **A-005**: Firebase Cloud Messaging is confirmed for push notifications
- [ ] **A-006**: Socket.io is sufficient for real-time communication at expected scale

### Business Assumptions

- [ ] **A-007**: Platform targets the **Saudi Arabian market** primarily
- [ ] **A-008**: Driver payments are **entirely offline** -- no in-app wallet, earnings tracking, or payout features needed
- [ ] **A-009**: Each white-label deployment serves a **single restaurant brand** (not multi-restaurant marketplace)
- [ ] **A-010**: Client will provide all **restaurant branding assets** (logos, colors, content)
- [ ] **A-011**: Arabic translations will be provided by **Space-O** (vendor) as professional translations
- [ ] **A-012**: OTP SMS costs will be borne by the **client/restaurant operator**
- [ ] **A-013**: Google Maps API usage costs will be borne by the **client/restaurant operator**
- [ ] **A-014**: Payment gateway **merchant accounts** will be set up by the client
- [ ] **A-015**: Competitive parity targets are **Maestro, Herfy, and Albaik apps**

### Process Assumptions

- [ ] **A-016**: **Agile development** methodology with iterative releases
- [ ] **A-017**: User flow diagrams (Customer, Driver, Restaurant) referenced in SOW are **finalized and approved**
- [ ] **A-018**: All **bold items** in the SOW represent incorporated client feedback and are confirmed requirements

---

## 4. Risk Tracking

| Risk ID | Risk | Severity | Status |
|---|---|---|---|
| R-001 | ~~Mobile framework not decided~~ | ~~High~~ | - [x] **Resolved: React Native** |
| R-002 | ~~Database not decided~~ | ~~High~~ | - [x] **Resolved: PostgreSQL** |
| R-003 | STC Pay may need separate integration outside Stripe | **Medium** | - [ ] Mitigated |
| R-004 | Postal system integration unclear | **Medium** | - [ ] Mitigated |
| R-005 | Arabic translation quality | **Medium** | - [ ] Mitigated |
| R-006 | Real-time GPS scaling | **Medium** | - [ ] Mitigated |
| R-007 | No timeline/budget defined | **High** | - [ ] Mitigated |
| R-008 | White-label deployment complexity | **Medium** | - [ ] Mitigated |
| R-009 | PCI compliance timeline impact | **Medium** | - [ ] Mitigated |
| R-010 | Guest-to-registration conversion UX | **Low** | - [ ] Mitigated |

---

## 5. Phase 2 Backlog (Deferred)

Items explicitly deferred to Phase 2 -- track but do not implement in MVP:

- [ ] iOS mobile apps (Customer + Driver) -- if market demand requires
- [ ] Apple Pay integration (requires iOS apps)
- [ ] Apple Sign-In (requires iOS apps)
- [ ] Advanced tiered loyalty/rewards program
- [ ] AI-driven personalization for upsell recommendations
- [ ] Any other features identified during development as Phase 2 candidates

---

*Last updated: March 2026*
*Source: Space-O Technologies SOW v1.1 (28 August 2025)*
*Scope change: iOS removed -- Android + Web only. Apple Pay replaced with Google Pay. Apple Sign-In removed.*
