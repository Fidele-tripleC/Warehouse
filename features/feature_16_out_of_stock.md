# Feature: <Out of Stock>

**Feature ID:**        N16  
**Branch pattern:**   `out-of-stock `  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Showing which items have been out of stock.
**Depends on:**        [Items](feature_4_Items__maintinence.md), [Inventory](feature_5_Inventory__maintinence.md)
**Related:**           [Supplier Order](feature_8_Supplier_order_Management.md), [Picking](feature_12_picking.md), [Customer Order](feature_9_Customer_Order_Management)
---

## User Stories

### US-N.16.1: View items that are out of stock
**As a**        Warehouse Manager
**I want to**   View items that are out of stock
**So that**     I know what we cannot pick or ship right now.
**Priority:**               P1  
**Independent test:**    Set an item quantity to 0 and select View Out of Stock. The item is displayed.
**Acceptance scenarios:**   US-16.1: under the acceptance criteria

### US-N.16.2: View items that have been out of stock
**As a**       Warehouse Manager
**I want to**  View items that have been out of stock
**So that**    I can see which items had no quantity.

**Priority:**               P1  
**Independent test:**   An item goes to quantity 0 then is put away later. View Out of Stock history still shows that item was out of stock.
**Acceptance scenarios:**   US-16.2: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must allow the warehouse Manager to view items with quantity 0.
- **FR-002**: System Must display the item and the warehouse for each out of stock item.
- **FR-003**: System Must record when an item becomes out of stock.
- **FR-004**: System Must allow the warehouse Manager to view items that have been out of stock.
- **FR-005**: System Must display a message when no items are out of stock.

---

## Key Entities

- **Out of Stock Record**: a record that an item had quantity 0.
- **Item**: the product that is out of stock.
- **Inventory**: the quantity in the warehouse. Quantity 0 means out of stock.

- **relationships**
- one **Item** can have multiple **Out of Stock Records**
- one **Warehouse** can have multiple **Out of Stock Records**

---

## Data Model Requirements

### `Out of Stock` table

 Field             
-------            
 `out_of_stock_id`  : this is the unique id
 `item_id`          : this is the item that is out of stock
 `warehouse_code`   : this is the warehouse
 `quantity`         : this is the quantity, it is 0
 `started_at`       : this is the time the item became out of stock
 `ended_at`         : this is the time the item had quantity again

---

## Acceptance Criteria

### US-N.16.1 â€” View items that are out of stock

#### Scenario: View current out of stock items
*   **Given** an item has quantity 0 in a warehouse
*   **When**  the warehouse Manager selects View Out of Stock
*   **Then**  the system displays the item
*   **And**   displays the warehouse

#### Scenario: No items out of stock
*   **Given** no item has quantity 0
*   **When**  the warehouse Manager selects View Out of Stock
*   **Then**  the out of stock list is empty
*   **And**   the system displays "No items are out of stock"

### US-N.16.2 â€” View items that have been out of stock

#### Scenario: View out of stock history
*   **Given** an item was at quantity 0 and later the quantity increased
*   **When**  the warehouse Manager selects View Out of Stock history
*   **Then**  the system displays that the item has been out of stock
*   **And**   displays the time it started and ended
