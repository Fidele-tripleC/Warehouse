# Feature: Supplier Did Not Ship

**Feature ID:**        N17  
**Branch pattern:**    `feature/17-supplier-did-not-ship`  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Showing suppliers that did not ship what was ordered.
**Depends on:**        [Supplier](feature_03_Supplier__maintinence.md), [Supplier Order](feature_08_Supplier_order_Management.md), [Receiving](feature_11_receiving.md)
**Related:**           [Items](feature_04_Items__maintinence.md), [Inventory](feature_05_Inventory__maintinence.md)
---

## User Stories

### US-N.17.1: View suppliers that did not ship what we ordered
**As a**        Warehouse Manager
**I want to**   View suppliers that did not ship what we ordered
**So that**     I can see when the received quantity is not the same as the ordered quantity.
**Priority:**               P1  
**Independent test:**    Order 50 and receive 40. Select View Supplier Did Not Ship. The supplier and the missing quantity are displayed.
**Acceptance scenarios:**   US-17.1: under the acceptance criteria

### US-N.17.2: View missing items from a supplier order
**As a**       Warehouse Manager
**I want to**  View the items a supplier did not ship
**So that**    I know which items and quantities are missing.

**Priority:**               P1  
**Independent test:**   Open a supplier did not ship record and verify the item, ordered quantity, and received quantity.
**Acceptance scenarios:**   US-17.2: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must compare ordered quantity and received quantity for each supplier order item.
- **FR-002**: System Must display a supplier when received quantity is less than ordered quantity.
- **FR-003**: System Must display the item, ordered quantity, received quantity, and missing quantity.
- **FR-004**: System Must allow the warehouse Manager to view this list.
- **FR-005**: System Must display a message when every supplier shipped what was ordered.

---

## Key Entities

- **Supplier Short Ship**: a record that a supplier sent less than the supplier order.
- **Supplier**: the company that did not ship the full quantity.
- **Supplier Order**: the order that was placed.
- **Receive**: the quantity that arrived.

- **relationships**
- one **Supplier** can have multiple **Supplier Short Ships**
- one **Supplier Order** can have multiple missing items

---

## Data Model Requirements

### `Supplier Short Ship` table

 Field             
-------            
 `short_ship_id`        : this is the unique id
 `supplier_code`        : this is the supplier
 `supplier_order_code`  : this is the supplier order
 `item_id`              : this is the item
 `ordered_quantity`     : this is the quantity ordered
 `received_quantity`    : this is the quantity received
 `missing_quantity`     : this is ordered quantity minus received quantity
 `created_at`           : this is the time it was recorded

---

## Acceptance Criteria

### US-N.17.1 â€” View suppliers that did not ship what we ordered

#### Scenario: Received less than ordered
*   **Given** a supplier order ordered 50 units
*   **And**   the receive quantity is 40
*   **When**  the warehouse Manager selects View Supplier Did Not Ship
*   **Then**  the system displays the supplier
*   **And**   displays the missing quantity 10

#### Scenario: All quantities received
*   **Given** every supplier order was received with the ordered quantity
*   **When**  the warehouse Manager selects View Supplier Did Not Ship
*   **Then**  the list is empty
*   **And**   the system displays "No suppliers are on the list"

### US-N.17.2 â€” View missing items from a supplier order

#### Scenario: View missing item details
*   **Given** a supplier did not ship the full quantity for an item
*   **When**  the warehouse Manager views that record
*   **Then**  the system displays the item
*   **And**   displays the ordered quantity and the received quantity
