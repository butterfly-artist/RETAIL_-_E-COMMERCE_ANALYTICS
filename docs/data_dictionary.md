# Data Dictionary

**Week:** 2  
**Purpose:** Define the source datasets, field schemas, Silver layer mappings, and streaming event structure.

---

# 1. Source File Catalog

| File Name | Grain | Purpose | Approx. Rows | Notes |
|---|---|---|---:|---|
| `orders.csv` | One row per order | Stores order lifecycle information | 100,000 | Primary order header dataset |
| `order_items.parquet` | One row per order item | Stores purchased products and seller information | 120,000 | One order may contain multiple items |
| `payments.csv` | One row per payment/installment | Stores payment transactions | 110,000 | Orders may have multiple installments |
| `reviews.csv` | One row per review | Stores customer review information | 85,000 | Only eligible orders contain reviews |
| `sellers.json` | One row per seller | Seller master reference data | 3,000 | Seller dimension table |
| `order_status_drop_01.json` | One row per status event | First streaming event batch | 100 | Week 10 streaming simulation |
| `order_status_drop_02.json` | One row per status event | Second streaming event batch | 100 | Incremental streaming file |

---

# 2. Raw File Schema: `orders.csv`

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| source_record_id | string | Yes | ORDSRC0000001 | Physical source record identifier |
| order_id | string | Yes | ORD0000001 | Unique order identifier |
| customer_region | string | Yes | South | Customer region |
| customer_state | string | Yes | KA | Customer state |
| customer_city_code | string | Yes | KA-C24 | Customer city code |
| customer_segment | string | Yes | Business | Customer segment |
| order_status | string | Yes | delivered | Current order status |
| purchase_ts | timestamp | Yes | 2025-10-20T03:33:21 | Purchase timestamp |
| approval_ts | timestamp | No | 2025-10-21T02:33:21 | Approval time |
| carrier_handoff_ts | timestamp | No | 2025-10-23T18:33:21 | Courier handoff time |
| delivered_ts | timestamp | No | 2025-10-31T08:33:21 | Delivery time |
| estimated_delivery_ts | timestamp | Yes | 2025-10-27T03:33:21 | Expected delivery |
| return_ts | timestamp | No | 2025-11-05T10:00:00 | Return completion time |
| currency_code | string | Yes | INR | Currency |

---

# 3. Raw File Schema: `order_items.parquet`

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| source_record_id | string | Yes | ITMSRC0000001 | Physical source record ID |
| order_item_id | string | Yes | ITM00000001 | Unique order item ID |
| order_id | string | Yes | ORD0000001 | Parent order |
| order_item_seq | integer | No | 1 | Item sequence number |
| product_id | string | Yes | PRD02450 | Product ID |
| category_code | string | Yes | automotive | Product category |
| seller_id | string | Yes | SLR000867 | Seller ID |
| item_price | decimal | Yes | 964.04 | Product price |
| freight_value | decimal | Yes | 107.86 | Shipping cost |
| quantity | integer | No | 1 | Quantity ordered |
| item_created_ts | timestamp | Yes | 2025-10-20 03:33:21 | Item creation timestamp |

---

# 4. Reference File Schema: `sellers.json`

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| source_record_id | string | Yes | SLRSRC0000001 | Physical source record ID |
| seller_id | string | Yes | SLR000001 | Seller identifier |
| seller_region | string | Yes | West | Seller region |
| seller_state | string | Yes | MH | Seller state |
| seller_type | string | Yes | Individual | Seller type |
| service_band | string | Yes | Standard | Service category |
| active_from | date | Yes | 2023-12-25 | Active start date |
| active_to | date | Yes | 2027-10-13 | Active end date |
| seller_status | string | Yes | active | Seller status |

---

# 5. Canonical Silver Table Design

Final Silver Tables

```text
silver_candidate_orders
silver_candidate_order_items
silver_candidate_payments
silver_candidate_reviews
silver_candidate_sellers
```

| Silver Field | Data Type | Source Mapping | Business Meaning |
|---|---|---|---|
| order_id | string | orders.order_id | Business order identifier |
| purchase_date | date | purchase_ts | Analytics date |
| customer_region | string | customer_region | Customer geography |
| customer_state | string | customer_state | Customer state |
| customer_segment | string | customer_segment | Customer category |
| order_status | string | order_status | Current order lifecycle |
| total_item_value | decimal | item_price | Product value |
| freight_value | decimal | freight_value | Shipping cost |
| payment_value | decimal | payment_value | Amount paid |
| review_score | integer | review_score | Customer rating |
| seller_id | string | seller_id | Seller reference |
| category_code | string | category_code | Product category |

---

# 6. Streaming Event Schema

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| event_id | string | Yes | EVT100001 | Unique event ID |
| schema_version | integer | Yes | 1 | Event schema version |
| event_ts | timestamp | Yes | 2025-12-20T10:00:00 | Event timestamp |
| event_type | string | Yes | order_status_changed | Event type |
| order_id | string | Yes | ORD0020633 | Order identifier |
| seller_id | string | Yes | SLR001458 | Seller identifier |
| order_item_id | string | No | ITM00024672 | Related order item |
| previous_status | string | Yes | approved | Previous status |
| new_status | string | Yes | shipped | Updated status |
| status_reason | string | Yes | carrier_handoff | Reason for status change |
| promised_delivery_ts | timestamp | Yes | 2025-11-07T07:51:29 | Promised delivery time |
| location_code | string | Yes | HUB-01 | Event location |
| event_sequence_no | integer | Yes | 1 | Event sequence |
| producer_run_id | string | Yes | CARTFLOW-RUN-01 | Streaming batch identifier |
