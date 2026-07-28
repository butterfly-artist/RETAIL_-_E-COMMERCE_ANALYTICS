# Synthetic Data Assumptions

**Week:** 2  
**Purpose:** Document the assumptions and boundaries of the synthetic datasets used in the CartFlow project.

---

# 1. Synthetic Data Boundary

This project uses **synthetic fictional retail and e-commerce data** created exclusively for educational purposes.

The datasets do **not** contain any real customer, seller, payment, product, marketplace, or business information. They are designed only to help students build, validate, and demonstrate an end-to-end data engineering pipeline.

The data must **never** be presented as representing a real company, customer, payment system, or commercial marketplace.

---

# 2. Domain Assumptions

| Area | Assumption |
|---|---|
| Geography / Scope | Fictional retail and e-commerce marketplace using synthetic regional and state codes (for example: South, North, West, Central, KA, TS, MH, GJ). The project does not represent any real company or marketplace. |
| Time Period | Synthetic transaction data primarily spans the 2025 calendar year. The streaming simulation uses controlled event drops dated **20 December 2025**. |
| Source Systems | Five batch source systems (`orders`, `order_items`, `payments`, `reviews`, `sellers`) and two controlled incremental JSON event drops (`order_status_drop_01.json` and `order_status_drop_02.json`). |
| Event Types | Order lifecycle events including order creation, payments, product purchases, customer reviews, and incremental order status changes (`order_status_changed`). |
| Reference Data | Seller master information, customer regions, customer segments, product categories, seller types, service bands, currencies, order statuses, and location codes. |

---

# 3. Data Volume Assumptions

| File | Approximate Rows | Reason |
|---|---:|---|
| `orders.csv` | 100,000 | Represents one row per order lifecycle header. |
| `order_items.parquet` | 120,000 | Represents one row per product item within an order. Supports one-to-many relationships. |
| `payments.csv` | 110,000 | Represents one payment or installment transaction per row. Some orders contain multiple payments. |
| `reviews.csv` | 85,000 | Represents eligible customer reviews for fulfilled orders only. |
| `sellers.json` | 3,000 | Seller master reference dataset. |
| `order_status_drop_01.json` | 100 | First controlled streaming status-event batch. |
| `order_status_drop_02.json` | 100 | Second controlled incremental streaming status-event batch. |

---

# 4. Controlled Data Quality Issues

The project intentionally includes controlled data quality scenarios to validate engineering rules and quarantine processing.

| Issue Type | Why It Exists |
|---|---|
| Duplicate or invalid business keys | To validate uniqueness and primary key rules. |
| Missing mandatory values | To validate completeness checks. |
| Invalid foreign key references | To test referential integrity across related datasets. |
| Invalid monetary values | To validate payment, item price, and freight value rules. |
| Invalid order lifecycle chronology | To detect incorrect purchase, approval, delivery, and return timestamps. |
| Invalid payment reconciliation | To verify order totals reconcile with payment totals within the allowed tolerance. |
| Invalid seller information | To validate seller status, active dates, and seller master integrity. |
| Invalid review records | To validate review eligibility, chronology, and review score ranges. |
| Invalid delivery status logic | To verify consistency between order status and delivery timestamps. |

**Note:** The playbook intentionally defines the **types** of data quality failures but **does not specify percentages** (such as 1% duplicates or 0.5% missing values). Therefore, no percentages are documented here to avoid introducing unsupported information.

---

# 5. Manual Verification

Before beginning implementation, the project team should verify that:

- Source row counts match the approved dataset counts.
- All required key fields (such as `order_id`, `order_item_id`, `payment_id`, `review_id`, and `seller_id`) are present.
- Source grains match the documented business grain for each dataset.
- Date, timestamp, and numeric fields are stored in expected formats.
- Parent-child relationships between orders, order items, payments, reviews, and sellers are logically consistent.
- Streaming event files follow the documented event schema.
- Data quality rules can successfully identify invalid records without affecting valid records.
- Bronze layer preserves every physical source record without modification.
- Silver Candidate, Trusted Silver, and Quarantine tables satisfy the reconciliation rule:

```
Silver Candidate Records
=
Trusted Silver Records
+
Quarantine Records
```

- The source datasets maintain sufficient variation to demonstrate standardization, reconciliation, aggregation, and data quality processing throughout the Lakehouse pipeline.
