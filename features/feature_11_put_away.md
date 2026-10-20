# Feature: <Put Away>

**Feature ID:**        N11  
**Branch pattern:**   `put-away `  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Putting received items into a warehouse location and updating inventory.
**Depends on:**        [Warehouse](feature_02_Warehouse__maintinence.md), [Items](feature_04_Items__maintinence.md), [Inventory](feature_05_Inventory__maintinence.md), [Supplier Order](feature_08_Supplier_order_Management.md), [Receive Supplier Order](feature_13_receive_supplier_order.md)
**Related:**           [Customer Order](feature_09_Customer_Order_Management.md), [Picking](feature_12_picking.md)
---

## User Stories

### US-N.11.1: View items to put away
**As a**        Warehouse Manager
**I want to**   View items that are ready to put away
**So that**     I can see what arrived from a supplier order and still needs a location.
**Priority:**               P1  
**Independent test:**    Receive a supplier order and select View Put Away. The items from that order are displayed.
**Acceptance scenarios:**   US-11.1: under the acceptance criteria

### US-N.11.2: Put away items
**As a**       Warehouse Manager
**I want to**  put items into a warehouse location
**So that**    the inventory in that warehouse is updated and the items are stored.

**Priority:**               P1  
**Independent test:**    Put away 20 units of an item from a Received supplier order into a warehouse. The put away is saved and the inventory quantity increases by 20.
**Acceptance scenarios:**   US-11.2: under the acceptance criteria

### US-N.11.3: View put away records
**As a**       Warehouse Manager
**I want to**  View put away records
**So that**    I can see where items were stored.

**Priority:**               P1  
**Independent test:**   Complete a put away and select View Put Away records. The warehouse, item, quantity, and location are displayed.
**Acceptance scenarios:**   US-11.3: under the acceptance criteria

### US-N.11.4: Put away from a customer return
**As a**       Warehouse Manager
**I want to**  put returned customer order items back into a warehouse location
**So that**    the inventory is updated after the items come back.

**Priority:**               P2  
**Independent test:**   Put away a returned item from a customer order. The inventory quantity increases.
**Acceptance scenarios:**   US-11.4: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must allow the warehouse Manager to view items that are ready to put away.
- **FR-002**: System Must allow an authorised Warehouse Manager to put away items from a Received supplier order into a warehouse location.
- **FR-003**: System Must update the inventory quantity when a put away is saved.
- **FR-004**: System Must associate each put away with a warehouse and an item.
- **FR-005**: System Must reject a put away when the supplier order is not Received.
- **FR-006**: System Must reject a put away quantity of zero or less.
- **FR-007**: System Must reject a put away quantity that is more than the quantity still not put away for that order item.
- **FR-008**: System Must allow an authorised Warehouse Manager to view put away records.
- **FR-009**: System Must prevent unauthorized users from creating a put away.

---

## Key Entities

- **Put Away**: moving items into a warehouse location so they are stored in inventory.
- **Supplier Order**: the order the items came from. A Received supplier order can have one or more put aways.
- **Customer Order**: a customer order can send items back to the warehouse to be put away.
- **Warehouse**: the location where the items are stored.
- **Item**: the inventory item being put away.
- **Inventory**: the stock quantity in the warehouse. Put away increases the quantity.

- **relationships**
- one **Supplier Order** can have multiple **Put Aways**
- one **Warehouse** can have multiple **Put Aways**
- one **Item** can be in multiple **Put Aways**

---

## Data Model Requirements

### `Put Away` table

 Field             
-------            
 `put_away_id`      : this is the unique id
 `put_away_code`    : this is the unique code for the put away
 `warehouse_code`   : this is the warehouse where the items are stored
 `item_id`          : this is the item being put away
 `quantity`         : this is the quantity put into the location
 `location`         : this is the place in the warehouse
 `supplier_order_code` : this is the supplier order the items came from when it is a supplier put away
 `customer_order_code` : this is the customer order the items came from when it is a return
 `created_at`       : this is the time when the put away was saved

---

## Acceptance Criteria

### US-N.11.1 â€” View items to put away

#### Scenario: View items ready to put away
*   **Given** a Received supplier order has items that are not all put away
*   **When**  the warehouse Manager selects View Put Away
*   **Then**  the system displays the items that still need to be put away
*   **And**   displays the remaining quantity for each item

#### Scenario: No items to put away
*   **Given** there are no items ready to put away
*   **When**  the warehouse Manager selects View Put Away
*   **Then**  the system displays a message indicating that no items are available to put away

### US-N.11.2 â€” Put away items

#### Scenario: Put away from a supplier order
*   **Given** the Warehouse Manager is authorized
*   **And**   a supplier order has status Received
*   **When**  the manager enters a valid warehouse location and quantity for an order item
*   **Then**  the system saves the put away
*   **And**   associates it with the warehouse and the supplier order
*   **And**   the inventory quantity of that item increases by the put away quantity

#### Scenario: Supplier order is not Received
*   **Given** a supplier order has status Draft or Submitted
*   **When**  the Warehouse Manager tries to put away items from that order
*   **Then**  the system rejects the put away
*   **And**   displays a message that the supplier order is not Received

#### Scenario: Invalid put away quantity
*   **Given** the Warehouse Manager is putting away items
*   **When**  the quantity is zero or less
*   **Then**  the system rejects the put away
*   **And**   displays a validation error

#### Scenario: Quantity more than remaining
*   **Given** a Received supplier order still has 10 units not put away
*   **When**  the Warehouse Manager tries to put away 15 units of that item
*   **Then**  the system rejects the put away
*   **And**   displays a message that the quantity is more than remaining

### US-N.11.3 â€” View put away records

#### Scenario: View existing put aways
*   **Given** put away records exist in the system
*   **When**  the warehouse Manager selects View Put Away records
*   **Then**  the system displays the put aways
*   **And**   displays the warehouse, item, quantity, and location

#### Scenario: No put away records
*   **Given** no put away records exist
*   **When**  the warehouse Manager selects View Put Away records
*   **Then**  the system displays a message indicating that no put aways are available

### US-N.11.4 â€” Put away from a customer return

#### Scenario: Put away returned items
*   **Given** items from a customer order are returned to the warehouse
*   **When**  the Warehouse Manager puts the items into a warehouse location
*   **Then**  the system saves the put away
*   **And**   associates it with the customer order
*   **And**   the inventory quantity of that item increases by the put away quantity

#### Scenario: Unauthorized update
*   **Given** the user is not authorized to manage put away
*   **When**  the user attempts to create a put away
*   **Then**  the put away is not saved
*   **And**   the system displays "You are not authorized to manage put away"
