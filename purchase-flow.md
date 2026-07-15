# Purchase flow — Pharmappy (mobile)

Spec for engineering: end-to-end shop purchase path.

**Browse → Product detail → Detail info → Add to cart → Checkout → Order confirmation + order number**

Reference style: health ecom (Hims-like). Order number pattern: pharmacy retail (CVS-like) — always show a clear order # on confirmation.

---

## Journey overview

```
Shop / browse
    ↓ tap product
Product detail (PDP)
    ↓ scroll / read
Detail info (benefits, how it works, ingredients, etc.)
    ↓ CTA
Add to cart → Cart
    ↓ checkout
Checkout (shipping → payment → place order)
    ↓ success
Order confirmation + order number
```

---

## Screens to build

### 1. Product browsing

**Goal:** User discovers and selects a product.

- Shop / catalog entry
- Product grid or list (image, name, short label / price)
- Optional categories or filters
- Tap product → PDP

### 2. Product detail (PDP)

**Goal:** User opens one product and understands what it is.

- Hero image + product name
- Short summary (what it treats / who it’s for)
- Primary CTA visible (Add to cart / Continue) — sticky is fine
- Clear scroll path into more detail

### 3. Detail info

**Goal:** User can review full product info before buying.

- On the same PDP (or linked sections): benefits, how it works, ingredients / warnings, FAQs as needed
- Stay in product context — no forced detour
- CTA still available after reading

### 4. Add to cart

**Goal:** User adds the product and can review cart.

- Add to cart from PDP
- Feedback (badge, toast, or sheet)
- Cart: line items, qty, subtotal, proceed to checkout

### 5. Checkout

**Goal:** User completes purchase.

Minimum path:

1. Shipping / delivery details  
2. Payment method  
3. Order review (items + totals)  
4. Place order  

Validate each step before allowing place order.

### 6. Order confirmation + order number

**Goal:** User knows the order succeeded and can reference it later.

Must show:

- Success / confirmation state  
- **Order number** (human-readable, e.g. `Order #741610123`)  
- Short summary (what was ordered / next step)  
- Path back to home or order detail  

Confirmation without an order number is **incomplete**.

---

## Acceptance criteria

- [ ] Browse products and open PDP
- [ ] PDP includes scrollable detail info before buy
- [ ] Add to cart + open cart
- [ ] Checkout: shipping → payment → place order
- [ ] Confirmation screen includes a clear **order number**
- [ ] Order number findable again (order detail / history)

---

## Out of scope (for now)

- Prescription transfer / Rx refill
- Subscription / recurring billing
- Complex promo / multi-wallet stacks

---

## Implementation notes

- Ship happy path first; then empty cart, payment fail, out of stock
- Keep PDP → ATC → checkout low friction
- Don’t force clinical questionnaires on a normal shop purchase path
