# Feature: <Ship Customer Order>

**Feature ID:**        N14  
**Branch pattern:**   `ship-customer-order `  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Shipping customer orders after the items are picked. Verify, package, and bill of lading.
**Depends on:**        [Customer Order](feature_09_Customer_Order_Management.md), [Picking](feature_12_picking.md), [Customer](feature_07_Customer__maintinence.md)
**Related:**           [Deliver Customer Order](feature_15_deliver_customer_order.md), [Route](feature_10_route_maintenence.md), [Inventory](feature_05_Inventory__maintinence.md), [Warehouse](feature_02_Warehouse__maintinence.md)
---

## User Stories

### US-N.14.1: View orders to ship
**As a**        Warehouse Manager
**I want to**   View customer orders that are ready to ship
**So that**     I can see which picked orders can leave the warehouse.
**Priority:**               P1  
**Independent test:**    Pick all items on a Submitted customer order and select View Ship. The order is displayed.
**Acceptance scenarios:**   US-14.1: under the acceptance criteria

### US-N.14.2: Verify and package then ship
**As a**       Warehouse Manager
**I want to**  verify the picked items, package the order, and ship it with a bill of lading
**So that**    the order is marked as shipped and can be delivered.

**Priority:**               P1  
**Independent test:**    Verify the pick, package the order, and save a bill of lading. The ship is saved and the order can be delivered.
**Acceptance scenarios:**   US-14.2: under the acceptance criteria

### US-N.14.3: View ship records
**As a**       Warehouse Manager
**I want to**  View ship records
**So that**    I can see what was shipped to customers.

**Priority:**               P1  
**Independent test:**   Complete a ship and select View Ship records. The customer order, items, quantities, and bill of lading are displayed.
**Acceptance scenarios:**   US-14.3: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must allow the warehouse Manager to view customer orders that are ready to ship.
- **FR-002**: System Must allow an authorised Warehouse Manager to verify the picked items before ship.
- **FR-003**: System Must allow an authorised Warehouse Manager to package a customer order that is fully picked.
- **FR-004**: System Must create a bill of lading when the order is shipped.
- **FR-005**: System Must associate each ship with a customer order.
- **FR-006**: System Must reject a ship when the customer order is not fully picked.
- **FR-007**: System Must reject a ship when the picked items do not match the customer order.
- **FR-008**: System Must reject a ship when the customer order is Draft, Cancelled, or already shipped.
- **FR-009**: System Must record the items and quantities that were shipped.
- **FR-010**: System Must allow an authorised Warehouse Manager to view ship records and the bill of lading.
- **FR-011**: System Must prevent unauthorized users from creating a ship.

---

## Key Entities

- **Ship**: recording that a picked customer order left the warehouse after verify and package.
- **Bill of Lading**: the shipping paper for the customer order. One ship has one bill of lading.
- **Customer Order**: the order being shipped. The order must be picked before it is shipped.
- **Pick**: the items taken from inventory for the order.
- **Deliver Order**: after ship, the order can be delivered and confirmed.
- **Customer**: the person or company receiving the shipment.

- **relationships**
- one **Customer Order** has one **Ship**
- one **Ship** has one **Bill of Lading**
- one **Ship** can have multiple shipped items

---

## Data Model Requirements

### `Ship` table

 Field             
-------            
 `ship_id`              : this is the unique id
 `ship_code`            : this is the unique code for the ship
 `customer_order_code`  : this is the customer order that was shipped
 `item_id`              : this is the item that was shipped
 `quantity`             : this is the quantity that was shipped
 `verified`             : this is yes when the pick was checked
 `packaged`             : this is yes when the order is packaged
 `bill_of_lading`       : this is the bill of lading code
 `created_at`           : this is the time when the ship was saved

---

## Acceptance Criteria

### US-N.14.1 â€” View orders to ship

#### Scenario: View orders ready to ship
*   **Given** a customer order has all items picked
*   **And**   the order is not shipped yet
*   **When**  the warehouse Manager selects View Ship
*   **Then**  the system displays the customer orders that are ready to ship
*   **And**   displays the items and quantities

#### Scenario: No orders to ship
*   **Given** there are no customer orders ready to ship
*   **When**  the warehouse Manager selects View Ship
*   **Then**  the system displays a message indicating that no orders are available to ship

### US-N.14.2 â€” Verify and package then ship

#### Scenario: Verify, package, and ship
*   **Given** the Warehouse Manager is authorized
*   **And**   a customer order has all items picked
*   **When**  the manager verifies the items, packages the order, and ships it
*   **Then**  the system saves the ship
*   **And**   records the items and quantities that were shipped
*   **And**   creates a bill of lading
*   **And**   the order can be delivered

#### Scenario: Picked items do not match
*   **Given** a customer order is ready to ship
*   **When**  the Warehouse Manager verifies and the picked items do not match the order
*   **Then**  the system rejects the ship
*   **And**   displays a message that the items do not match

#### Scenario: Order is not fully picked
*   **Given** a customer order still has items not picked
*   **When**  the Warehouse Manager tries to ship the order
*   **Then**  the system rejects the ship
*   **And**   displays a message that the order is not fully picked

#### Scenario: Order already shipped
*   **Given** a customer order is already shipped
*   **When**  the Warehouse Manager tries to ship it again
*   **Then**  the system rejects the ship

### US-N.14.3 â€” View ship records

#### Scenario: View existing ships
*   **Given** ship records exist in the system
*   **When**  the warehouse Manager selects View Ship records
*   **Then**  the system displays the ships
*   **And**   displays the customer order, item, quantity, and bill of lading

#### Scenario: No ship records
*   **Given** no ship records exist
*   **When**  the warehouse Manager selects View Ship records
*   **Then**  the system displays a message indicating that no ships are available

#### Scenario: Unauthorized update
*   **Given** the user is not authorized to manage ship
*   **When**  the user attempts to create a ship
*   **Then**  the ship is not saved
*   **And**   the system displays "You are not authorized to manage ship"
