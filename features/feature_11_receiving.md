# Feature: Receiving

**Feature ID:**        N11  
**Branch pattern:**    `feature/11-receiving`  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Receiving items that arrive from a supplier order.
**Depends on:**        [Supplier](feature_03_Supplier__maintinence.md), [Supplier Order](feature_08_Supplier_order_Management.md), [Items](feature_04_Items__maintinence.md)
**Related:**           [Put Away](feature_12_put_away.md), [Inventory](feature_05_Inventory__maintinence.md), [Warehouse](feature_02_Warehouse__maintinence.md)
---

## User Stories

### US-N.11.1: View orders to receive
**As a**        Warehouse Manager
**I want to**   View supplier orders that are ready to receive
**So that**     I can see what the supplier is sending to the warehouse.
**Priority:**               P1  
**Independent test:**    Submit a supplier order and select View Receive. The order is displayed.
**Acceptance scenarios:**   US-11.1: under the acceptance criteria

### US-N.11.2: Receive supplier order
**As a**       Warehouse Manager
**I want to**  receive items from a supplier order
**So that**    the system records what arrived and the order can be put away.

**Priority:**               P1  
**Independent test:**    Receive 50 units for a Submitted supplier order. The receive is saved and the order status becomes Received when all items are received.
**Acceptance scenarios:**   US-11.2: under the acceptance criteria

### US-N.11.3: View receive records
**As a**       Warehouse Manager
**I want to**  View receive records
**So that**    I can see what arrived from each supplier order.

**Priority:**               P1  
**Independent test:**   Complete a receive and select View Receive records. The supplier order, item, and quantity are displayed.
**Acceptance scenarios:**   US-11.3: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must allow the warehouse Manager to view supplier orders that are ready to receive.
- **FR-002**: System Must allow an authorised Warehouse Manager to receive items from a Submitted supplier order.
- **FR-003**: System Must associate each receive with a supplier order and an item.
- **FR-004**: System Must reject a receive when the supplier order is not Submitted.
- **FR-005**: System Must reject a receive quantity of zero or less.
- **FR-006**: System Must allow a receive quantity that is less than the ordered quantity.
- **FR-007**: System Must record when the received quantity is not the same as the ordered quantity.
- **FR-008**: System Must set the supplier order status to Received when the receive is saved.
- **FR-009**: System Must allow an authorised Warehouse Manager to view receive records.
- **FR-010**: System Must prevent unauthorized users from creating a receive.

### Status transitions
- A supplier order must be Submitted before it can be received
- Submitted → Received when the receive is saved
- Draft and Received orders cannot be received again

---

## Key Entities

- **Receive**: recording the items that arrived from a supplier order.
- **Supplier Order**: the order being received. A Submitted supplier order can be received.
- **Supplier**: the company that sent the items.
- **Item**: the inventory item that arrived.
- **Put Away**: after receive, items are put away into a warehouse location.

- **relationships**
- one **Supplier Order** can have multiple **Receives**
- one **Item** can be in multiple **Receives**

---

## Data Model Requirements

### `Receive` table

 Field             
-------            
 `receive_id`           : this is the unique id
 `receive_code`         : this is the unique code for the receive
 `supplier_order_code`  : this is the supplier order the items came from
 `item_id`              : this is the item that arrived
 `ordered_quantity`     : this is the quantity that was ordered
 `received_quantity`    : this is the quantity that arrived
 `created_at`           : this is the time when the receive was saved

---

## Acceptance Criteria

### US-N.11.1 — View orders to receive

#### Scenario: View orders ready to receive
*   **Given** a Submitted supplier order exists
*   **When**  the warehouse Manager selects View Receive
*   **Then**  the system displays the supplier orders that are ready to receive
*   **And**   displays the items and ordered quantity

#### Scenario: No orders to receive
*   **Given** there are no supplier orders ready to receive
*   **When**  the warehouse Manager selects View Receive
*   **Then**  the system displays "No orders are available to receive"

### US-N.11.2 — Receive supplier order

#### Scenario: Receive all ordered quantity
*   **Given** the Warehouse Manager is authorized
*   **And**   a supplier order has status Submitted
*   **When**  the manager enters the received quantity equal to the ordered quantity
*   **Then**  the system saves the receive
*   **And**   associates it with the supplier order
*   **And**   the supplier order status becomes Received

#### Scenario: Receive less than ordered
*   **Given** a supplier order has status Submitted
*   **And**   the ordered quantity is 50
*   **When**  the Warehouse Manager receives 40
*   **Then**  the system saves the receive
*   **And**   records that the received quantity is not the same as the ordered quantity
*   **And**   the supplier order status becomes Received

#### Scenario: Supplier order is not Submitted
*   **Given** a supplier order has status Draft or Received
*   **When**  the Warehouse Manager tries to receive that order
*   **Then**  the receive is not saved
*   **And**   the system displays "Supplier order is not Submitted"

#### Scenario: Invalid receive quantity
*   **Given** the Warehouse Manager is receiving a supplier order
*   **When**  the quantity is zero or less
*   **Then**  the receive is not saved
*   **And**   the system displays "Quantity must be greater than zero"

### US-N.11.3 — View receive records

#### Scenario: View existing receives
*   **Given** receive records exist in the system
*   **When**  the warehouse Manager selects View Receive records
*   **Then**  the system displays the receives
*   **And**   displays the supplier order, item, ordered quantity, and received quantity

#### Scenario: No receive records
*   **Given** no receive records exist
*   **When**  the warehouse Manager selects View Receive records
*   **Then**  the system displays "No receives are available"

#### Scenario: Unauthorized update
*   **Given** the user is not authorized to manage receive
*   **When**  the user attempts to create a receive
*   **Then**  the receive is not saved
*   **And**   the system displays "You are not authorized to manage receive"
