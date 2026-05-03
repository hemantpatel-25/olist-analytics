# Data Quality Issues & Fixes

## Summary

During the project audit, the following issues were identified and addressed:

---

## Issues Fixed

### 1. Payment Null Values (3 rows)
**Problem:** 3 orders had missing `payment_type`, `payment_total`, and `installments` values

**Fix:** Added code to `02_data_cleaning.ipynb` to fill missing payment values with 'unknown' and 0

---

### 2. Customer ID Naming Confusion
**Problem:** 
- `customer_id` in master.csv = per-order reference (98,666 unique)
- `customer_unique_id` = true customer identifier (95,420 unique)

**Fix:** Documented in notebooks and README. This is a known Olist dataset limitation.

---

### 3. Undelivered Orders (2,461 rows - 2.2%)
**Problem:** `delay_days`, `is_late`, `actual_delivery_days` have NULL values

**This is EXPECTED** - orders with status != 'delivered'

**Fix:** Added `is_delivered` flag to track which orders have delivery data

---

### 4. Missing Review Sentiment (942 rows - 0.8%)
**Problem:** `sentiment` column has NULL values

**This is EXPECTED** - not all customers leave text reviews

---

## Current Data Quality Status

| Metric | Status |
|--------|--------|
| Total Rows | 112,650 |
| Unique Orders | 98,666 |
| Unique Customers | 95,420 (true) |
| Unique Products | 32,951 |
| Unique Sellers | 3,095 |
| Total Revenue | R$ 15,843,553.24 |
| Exact Duplicates | 0 |
| Negative Prices | 0 |
| Invalid State Codes | 0 |

---

## Recommendations for Power BI

1. **Use `customer_unique_id`** for true customer counts
2. **Filter undelivered orders** when analyzing delivery metrics
3. **Handle NULL sentiment** - orders without text reviews are normal

---

*Last Updated: 2026-04-22*
