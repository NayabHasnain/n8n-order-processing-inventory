# Setup Guide

## 1. Import the Workflow

Import `workflow/order-processing-inventory.sanitised.json` into n8n. Keep it inactive during setup.

## 2. Create the Inventory Table

Create an n8n Data Table called `inventory_products` with these columns:

- `sku` — String
- `product_name` — String
- `unit_price` — Number
- `stock_quantity` — Number
- `reorder_level` — Number
- `active` — Boolean

Add fictional products whose SKUs match the test data.

## 3. Create the Processed-Orders Table

Create an n8n Data Table called `processed_orders` with these columns:

- `order_reference` — String
- `customer_email` — String
- `status` — String
- `received_at` — String

## 4. Reconnect the Data Table Nodes

Open and configure these nodes:

- `New Order Only` → `processed_orders`
- `Look Up Inventory Product` → `inventory_products`
- `Update Inventory Stock` → `inventory_products`
- `Record Processed Order` → `processed_orders`

## 5. Configure Notifications

The exported public workflow contains no Gmail credentials. Connect your own Gmail account only if notification testing is required.

Replace `inventory-alerts@example.com` and `test-customer@example.com` with approved test recipients. Do not use real customer information.

## 6. Test Safely

Use `sample-data/test-orders.json` to test:

1. A successful order
2. A successful order that leaves low stock
3. An insufficient-stock order
4. A repeated order reference
5. Invalid order-items JSON

Verify the execution path, inventory quantity and processed-order record after every test.

## 7. Activate Only After Review

Confirm all table mappings, recipient addresses and form settings before activating the workflow.

