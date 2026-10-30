# QuickKart ⚡ Everyday essentials, delivered fast

> A realistic, modern **quick-commerce grocery delivery platform** inspired by Indian 10–20 minute delivery apps, built with an original brand identity, product catalog, and visual design.
> 
> **QuickKart** also serves as an automated **software QA and autonomous AI bug-detection benchmark**, seeded with **12 intentional, reproducible software defects** across business logic, cart math, search ranking, filters, delivery boundaries, and validation.

---

## 🚀 Key Features

- **Hyperlocal Quick-Commerce Homepage**:
  - Live "Delivery in 12–18 mins" indicator with dark-store proximity simulation.
  - Interactive category grid (Fruits & Vegetables, Dairy, Snacks, Staples, Household, Personal Care).
  - Deals of the day, bestsellers, and morning fresh arrivals.
- **Realistic 48+ Indian Product Catalog**:
  - Accurate ₹ INR pricing, MRP strikethroughs, discounts, and ratings.
  - Multi-pack variant selections (e.g. 500 ml / 1 L / 2 L milk; 250 g / 500 g / 1 kg coffee).
  - Ingredients, nutritional values, and real-time variant price updates.
- **Search & Auto-Suggestions**:
  - Instant product search with suggestion chips, recent searches, and zero-results fallback.
- **Filtering & Sorting**:
  - Category filters, brand pickers, rating filters, in-stock toggles, and price caps.
  - Sorters: Popularity, price low/high, rating, and biggest discount.
- **Cart & Multi-Step Checkout**:
  - Interactive slide-out cart drawer with quantity steppers and line subtotal breakdowns.
  - Transparent bill calculation: Item total, coupon discounts, tiered delivery charges, handling fee, and 5% GST.
  - Saved delivery address management (Home, College, Other) with new address creator.
  - Simulated payment methods: Instant UPI (QR / VPA), Credit/Debit Card, and Cash on Delivery (COD).
- **Live Order Tracking**:
  - Real-time order progression timeline: `Order Placed` ➔ `Packing` ➔ `Picked Up` ➔ `Out for Delivery` ➔ `Delivered`.
  - Order history with reorder capabilities.

---

## 🧪 Hidden QA Benchmark Console (`/#qa`)

The platform contains a dedicated internal QA suite at **`/#qa`** (or accessible via the discreet **QA Benchmark Console** link in the footer).

- **12 Deterministic Seeded Defects**: Real underlying logic errors (not UI text mocks).
- **One-Click Live Test Runner**: Executes assertion checks directly against the app's services and captures live evidence.
- **Automated AI Bug Report Generator**: Generates formatted, evidence-based bug reports matching production QA standards.
- **Export Reports**: Download or copy all reports in markdown format.

### Seeded Defect Summary

| Bug ID | Title | Severity | Priority | Affected Service |
| :--- | :--- | :---: | :---: | :--- |
| **BUG-01** | Line subtotal calculation multiplies by `(qty - 1)` for milk items | High | P1 | `cartService.calculateLineTotal` |
| **BUG-02** | Removing staples items leaves ₹100 residual balance in cart subtotal | High | P1 | `cartService.removeItem` |
| **BUG-03** | Percentage coupon (`SAVE10`) includes delivery fee in discount base | Medium | P2 | `couponService.calculateDiscount` |
| **BUG-04** | Description keyword matches weighted higher (50) than title matches (10) | Medium | P2 | `searchService.searchProducts` |
| **BUG-05** | Price filter evaluates `product.mrp <= maxPrice` instead of selling price | Medium | P2 | `filterService.filterAndSort` |
| **BUG-06** | Out-of-stock variant can be added because button checks base product stock | High | P1 | `ProductDetailModal.jsx` |
| **BUG-07** | Strict `>` operator charges incorrect delivery fee at ₹299 and ₹600 boundaries | Medium | P2 | `shippingService.calculateDeliveryFee` |
| **BUG-08** | Storage hydration resets selected pack size back to default variant | Medium | P2 | `cartService.loadCartFromStorage` |
| **BUG-09** | Selected variant price on product page reverts to base price in cart | High | P1 | `cartService.addItem` |
| **BUG-10** | Checkout tax calculated on undiscounted subtotal causing total mismatch | High | P1 | `checkoutService.calculateOrderSummary` |
| **BUG-11** | Inverted date check causes expired coupon `EXPIRED20` to be accepted | Medium | P2 | `couponService.validateCoupon` |
| **BUG-12** | Form validation passes empty pincode due to missing required presence check | Medium | P2 | `addressService.validateAddress` |

---

## 🤖 Autonomous AI Agent API (`window.__QUICKKART_QA__`)

Autonomous browser testing agents can test and inspect the application programmatically:

```javascript
// Run test case for any defect
const report = await window.__QUICKKART_QA__.runAutomatedTest('BUG-01');

// Inspect current cart state and totals
const cart = window.__QUICKKART_QA__.getCartState();

// Get defect specifications
const defects = window.__QUICKKART_QA__.getDefectsList();

// Reset all test data and localStorage
window.__QUICKKART_QA__.resetState();
```

---

## 🛠️ Tech Stack & Architecture

- **Frontend**: React 19 + Vite 6
- **Styling**: Vanilla CSS with modern custom properties, glassmorphism, and responsive grids
- **Icons**: Lucide React
- **Typography**: Plus Jakarta Sans & Inter (Google Fonts)

```text
src/
├── components/   # Header, Footer, ProductCard, CartDrawer, AddressModal, etc.
├── context/      # AppContext (Cart, Address, Location, QA Hooks)
├── data/         # Products (48+), Categories, Coupons, Addresses, QA Defect specs
├── pages/        # HomePage, CategoriesPage, SearchResultsPage, CheckoutPage, OrderSuccess, QA Console
├── services/     # cartService, couponService, shippingService, searchService, filterService, etc.
└── styles/       # Design tokens, global CSS, layout stylesheets
```

---

## 📦 Getting Started

### Prerequisites
- Node.js (v18+)
- npm (v9+)

### Installation & Run

```bash
# Clone the repository
git clone <YOUR_REPO_URL>
cd demo

# Install dependencies
npm install

# Start local dev server
npm run dev
```

Visit **`http://localhost:5173/`** to view QuickKart, and **`http://localhost:5173/#qa`** to view the QA Benchmark Suite.

### Production Build

```bash
npm run build
npm run preview
```
