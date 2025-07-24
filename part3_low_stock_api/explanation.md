# Part 3 – Low Stock Alert API

## 🎯 Goal

To return alerts for all products below the low-stock threshold for a given company. It must only consider products with recent sales and should return supplier info for quick reordering.

---

## 🔗 How It Works

1. I first fetched all **warehouses** for the given company.
2. Then I checked the **inventory** of each warehouse.
3. For each product:
   - I ensured it had **recent sales activity** (last 30 days).
   - I compared current stock with its **threshold** (assumed to be a column in Product).
   - If stock is below threshold, I looked up the **supplier** info.
4. The final alert includes product, warehouse, supplier, and estimated stockout time.

---

## 🧠 Assumptions Made

- Each product has a `low_stock_threshold` column.
- "Recent activity" means any sale in the past 30 days.
- A product has one primary supplier (for now).
- Function `estimate_days_until_stockout()` is stubbed (in reality, it would use sales rate).
- `Sale` model exists with `created_at`, `product_id`.

---

## ✅ Edge Cases Considered

- Missing supplier → nulls returned
- Product exists but has no recent sales → skipped
- Multiple warehouses under a company → handled
- Quantity = 0 → triggers alert

---

## 🔍 Improvements for Real-World

- Support multiple suppliers and pick based on priority or price
- Add pagination for large alert lists
- Support dynamic thresholds per warehouse
