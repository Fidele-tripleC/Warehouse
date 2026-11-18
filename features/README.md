# Feature catalog

Read and build **first to last**. Feature IDs stay N01–N20 (do not renumber). Authentication is first even though its file is N20.

Retailers do **not** log in. The warehouse records store orders (N09). Receiving (N11) is supplier goods, not store orders.

**Company:** one operating company (Fidele Warehouse Co). `company_id` is on company, warehouse, and user — not on every table. Orders use `warehouse_id`. See [ADR-0002](../docs/adr/0002-warehouse-ownership.md).

**Roles that log in:** System Administrator, Warehouse Manager, Employee Manager. If a spec says Purchasing Agent or Procurement Manager, that person is the Warehouse Manager.

## First to last

| Order | ID | What it is | Why this place |
|------:|----|------------|----------------|
| 1 | [N20 Authentication](feature_20_authentication.md) | Log in, log out, forgot password, add user | Nothing else opens until login |
| 2 | [N01 Company](feature_01_Company_maintinence.md) | The company that owns the warehouses | Need a company before warehouses and people |
| 3 | [N02 Warehouse](feature_02_Warehouse__maintinence.md) | Buildings / locations | Stock lives in a warehouse |
| 4 | [N06 Employee](feature_06_Employee__maintinence.md) | People who work here | Logins can link to an employee |
| 5 | [N03 Supplier](feature_03_Supplier__maintinence.md) | Who we buy from | Need a supplier before a supplier order |
| 6 | [N04 Items](feature_04_Items__maintinence.md) | Product list (SKU, name) | Need items before stock and orders |
| 7 | [N05 Inventory](feature_05_Inventory__maintinence.md) | How many of each item in a warehouse | Stock after items exist |
| 8 | [N07 Customer](feature_07_Customer__maintinence.md) | Retailer stores (no login) | Need the store before recording its order |
| 9 | [N08 Supplier order](feature_08_Supplier_order_Management.md) | We order goods from a supplier | Inbound starts here |
| 10 | [N11 Receiving](feature_11_receiving.md) | Goods arrive from the supplier | After the supplier order |
| 11 | [N12 Put away](feature_12_put_away.md) | Put received goods on a shelf | After receive; stock goes up |
| 12 | [N09 Customer order](feature_09_Customer_Order_Management.md) | Warehouse records a store order | Outbound starts here |
| 13 | [N13 Picking](feature_13_picking.md) | Take items off the shelf for that order | After the store order; stock goes down |
| 14 | [N10 Route](feature_10_route_maintenence.md) | Truck stops for deliveries | After we know which orders go out |
| 15 | [N14 Ship](feature_14_ship_customer_order.md) | Order leaves the warehouse | After pick |
| 16 | [N15 Deliver](feature_15_deliver_customer_order.md) | Confirm the store got it | After ship |
| 17 | [N16 Out of stock](feature_16_out_of_stock.md) | Items at quantity 0 | Report after stock moves |
| 18 | [N17 Supplier did not ship](feature_17_supplier_did_not_ship.md) | Ordered more than we received | Report after receive |
| 19 | [N18 Delivery does not match ship](feature_18_delivery_does_not_match_ship.md) | Shipped but stop failed | Report after ship and deliver |
| 20 | [N19 Monthly shipping](feature_19_monthly_shipping_quantities.md) | Totals shipped in a month | Report after ship |

## Flow (short)

1. Log in  
2. Set up company, warehouse, employees, suppliers, items, inventory, retailers  
3. Inbound: supplier order → receive → put away  
4. Outbound: record store order → pick → route → ship → deliver  
5. Reports: out of stock, supplier short, delivery mismatch, monthly totals  

## ID list (file names)

| ID | File | Branch |
|----|------|--------|
| N20 | [feature_20_authentication.md](feature_20_authentication.md) | `feature/20-authentication` |
| N01 | [feature_01_Company_maintinence.md](feature_01_Company_maintinence.md) | `feature/1-company` |
| N02 | [feature_02_Warehouse__maintinence.md](feature_02_Warehouse__maintinence.md) | `feature/2-warehouse` |
| N03 | [feature_03_Supplier__maintinence.md](feature_03_Supplier__maintinence.md) | `feature/3-supplier` |
| N04 | [feature_04_Items__maintinence.md](feature_04_Items__maintinence.md) | `feature/4-items` |
| N05 | [feature_05_Inventory__maintinence.md](feature_05_Inventory__maintinence.md) | `feature/5-inventory` |
| N06 | [feature_06_Employee__maintinence.md](feature_06_Employee__maintinence.md) | `feature/6-employee` |
| N07 | [feature_07_Customer__maintinence.md](feature_07_Customer__maintinence.md) | `feature/7-customer` |
| N08 | [feature_08_Supplier_order_Management.md](feature_08_Supplier_order_Management.md) | `feature/8-supplier-order` |
| N09 | [feature_09_Customer_Order_Management.md](feature_09_Customer_Order_Management.md) | `feature/9-customer-order` |
| N10 | [feature_10_route_maintenence.md](feature_10_route_maintenence.md) | `feature/10-route` |
| N11 | [feature_11_receiving.md](feature_11_receiving.md) | `feature/11-receiving` |
| N12 | [feature_12_put_away.md](feature_12_put_away.md) | `feature/12-put-away` |
| N13 | [feature_13_picking.md](feature_13_picking.md) | `feature/13-picking` |
| N14 | [feature_14_ship_customer_order.md](feature_14_ship_customer_order.md) | `feature/14-ship-customer-order` |
| N15 | [feature_15_deliver_customer_order.md](feature_15_deliver_customer_order.md) | `feature/15-deliver-customer-order` |
| N16 | [feature_16_out_of_stock.md](feature_16_out_of_stock.md) | `feature/16-out-of-stock` |
| N17 | [feature_17_supplier_did_not_ship.md](feature_17_supplier_did_not_ship.md) | `feature/17-supplier-did-not-ship` |
| N18 | [feature_18_delivery_does_not_match_ship.md](feature_18_delivery_does_not_match_ship.md) | `feature/18-delivery-does-not-match-ship` |
| N19 | [feature_19_monthly_shipping_quantities.md](feature_19_monthly_shipping_quantities.md) | `feature/19-monthly-shipping-quantities` |
