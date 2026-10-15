# ABHA — Fashion & Accessories

A responsive fashion storefront featuring the ABHA brand, built with HTML, CSS, and JavaScript and backed by an Express API and SQLite database. The checkout records demo orders locally; it does not collect payment information or connect to a payment gateway.

## Features

- Browse 35 ABHA products, including 17 Summer Deals, with backend-sourced names, prices, categories, size choices, descriptions, and images.
- Explore women's clothing, co-ord sets and footwear; men's fashion; bags; kids' fashion; and jewellery.
- Search products and filter by category.
- View product details, select a product-specific size (including shoe sizes and accessory sizing), and choose a quantity.
- Keep the same product in different sizes as separate cart items.
- Update quantities, remove cart items, apply supported demo coupons, and review totals.
- Submit validated delivery details and save order records and line items to SQLite.
- View an order confirmation with its saved order ID, products, quantities, and totals.
- Responsive layout for desktop and mobile.

## Requirements

- Node.js 18 or newer
- npm
- VS Code Live Server (or another static server on `localhost:5500` or `127.0.0.1:5500`)

## Run locally

1. Open a terminal in the `backend` folder and install dependencies:

   ```powershell
   cd backend
   npm install
   ```

2. Seed or update the catalog, then start the API:

   ```powershell
   npm run seed
   npm start
   ```

   The API listens on `http://localhost:4000`. SQLite data is stored in `backend/store.db`.

3. In VS Code, open the project folder and start Live Server from `index.html`. The API allows the default Live Server origins on ports 5500 and 5501.

4. Browse from Home to Shop, open a product, choose a size and quantity, then continue through Cart, Checkout, and Order Confirmation.

## API

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `GET` | `/api/products` | List catalog products |
| `GET` | `/api/products/:id` | Load product details |
| `POST` | `/api/orders` | Validate and save a demo order |
| `GET` | `/api/orders/:id` | Load a saved order for confirmation |

The server calculates order prices from the database instead of trusting prices supplied by the browser. It validates the product IDs, product-specific sizes, quantities, customer information, and coupon before saving the order and its items in a database transaction. Quantities are limited to 99 per product and size.

Supported demo coupons are `WELCOME10` (10% off) and `FREESHIP` (shipping is already free). The database creates the required tables at server startup and adds the order discount, size, category, and product-size columns to existing databases when necessary.

## Project structure

```text
index.html, shop.html, sproduct.html    Storefront pages
cart.html, checkout.html                Cart and checkout
order-confirmation.html                 Order confirmation
script.js, checkout.js                  Frontend behavior
style.css                               Shared responsive styles
backend/server.js                       Express API
backend/db.js, backend/seed.js           SQLite schema and catalog seed
```

## Demo and production notes

This project does not charge customers. Do not enter or store card numbers, CVVs, or other payment credentials. A production store needs a payment provider and server-side payment verification before an order can be marked as paid. Authentication, inventory management, and live shipping calculations are not implemented.
