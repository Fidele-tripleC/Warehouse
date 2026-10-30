# Feature: Supplier Order

**Feature ID:**        N08  
**Branch pattern:**    `feature/8-supplier-order`  
**Status:**            Draft  
**Created:**           2026-09-21  
**Input:**             Create, view, edit, submit, and track purchase orders sent to suppliers.  
**Depends on:**        [Supplier](feature_03_Supplier__maintinence.md), [Inventory](feature_05_Inventory__maintinence.md), [Items](feature_04_Items__maintinence.md)  
**Related:**           [Warehouse](feature_02_Warehouse__maintinence.md), [Receiving](feature_11_receiving.md), [Put Away](feature_12_put_away.md), [Supplier Did Not Ship](feature_17_supplier_did_not_ship.md)

---

## User Stories

### US-N08.1: Create supplier order
**As a**       Purchasing Agent  
**I want to**  create an order for a supplier  
**So that**    needed inventory can be ordered  
**Priority:**             P1  
**Independent test:**     Create an order for 50 units of an item; the order is saved with the correct supplier, item, and quantity.  
**Acceptance scenarios:** See AC-N08.1

### US-N08.2: View supplier orders
**As a**       Purchasing Agent  
**I want to**  view supplier orders  
**So that**    I can see what inventory has been ordered  
**Priority:**             P1  
**Independent test:**     Create a supplier order; it appears in the supplier order list with its status.  
**Acceptance scenarios:** See AC-N08.2

### US-N08.3: Edit supplier order
**As a**       Purchasing Agent  
**I want to**  edit an order before it is submitted  
**So that**    incorrect order information can be corrected  
**Priority:**             P1  
**Independent test:**     Change an order quantity from 50 to 60; the updated quantity is saved.  
**Acceptance scenarios:** See AC-N08.3

### US-N08.4: Submit supplier order
**As a**       Purchasing Agent  
**I want to**  submit a completed supplier order  
**So that**    the order can be tracked as an active order  
**Priority:**             P1  
**Independent test:**     Submit a Draft order; its status changes to Submitted.  
**Acceptance scenarios:** See AC-N08.4

---

## Functional Requirements

- **FR-001**: The system MUST assign every supplier order a unique identifier.
- **FR-002**: The system MUST associate each order with an active supplier.
- **FR-003**: The system MUST allow authorized users to create and view supplier orders.
- **FR-004**: The system MUST allow a Draft order to be edited, and MUST NOT allow Submitted or Received orders to be edited.
- **FR-005**: The system MUST record the items and quantities being ordered.
- **FR-006**: The system MUST maintain the order status (Draft, Submitted, Received).
- **FR-007**: The system MUST prevent unauthorized users from creating, editing, or submitting supplier orders.
- **FR-008**: The system MUST reject order items with a quantity of zero or less.
- **FR-009**: The system MUST NOT allow an order with no items to be submitted.

### Status transitions
- Draft → Submitted (when the order is submitted)
- Submitted → Received (when receiving is saved in N11)
- Draft may be edited. Submitted and Received may not be edited.

---

## Key Entities

- **Supplier Order**: a purchase order placed with one Supplier. Contains one or more Order Items.
- **Supplier**: the company receiving the order. One Supplier can have many Supplier Orders.
- **Order Item**: one line of an order: an Inventory Item and the quantity ordered. Belongs to one Supplier Order.
- **Inventory Item**: a stocked item (see N04) that can be ordered.
- **Purchasing Agent**: the authorized user who manages supplier orders.

---

## Data Model Requirements

### `supplier_order` table

 `order_id`          : this is the unique id important for the database  
 `order_code`        : this is the unique code for the order  
 `created_at`        : this is the time when the order was created  
 `updated_at`        : this is the time it was updated  
 `submitted_at`      : this is the time it was submitted

---

## Acceptance Criteria

### AC-N08.1 â€” Create Supplier Order

#### Scenario: Create order
* **Given** an active supplier exists
* **When**  the Purchasing Agent creates an order with valid items and quantities
* **Then**  the system saves the order with status Draft
* **And**   assigns it a unique identifier

#### Scenario: Invalid quantity
* **Given** the Purchasing Agent is creating an order
* **When**  the quantity is zero or less
* **Then**  the order item is not saved
* **And**   the system displays "Quantity must be greater than zero"

#### Scenario: Inactive supplier
* **Given** a supplier has status Inactive
* **When**  the Purchasing Agent tries to create an order for that supplier
* **Then**  the order is not created
* **And**   the system displays "Supplier is not active"

### AC-N08.2 â€” View Supplier Orders

#### Scenario: View orders
* **Given** supplier orders exist
* **When**  the Purchasing Agent selects "View Supplier Orders"
* **Then**  the system displays the supplier orders and their current statuses

#### Scenario: No orders
* **Given** no supplier orders exist
* **When**  the Purchasing Agent selects "View Supplier Orders"
* **Then**  the supplier order list is empty
* **And**   the system displays "No orders are available"

### AC-N08.3 â€” Edit Supplier Order

#### Scenario: Edit Draft order
* **Given** a supplier order has Draft status
* **When**  the Purchasing Agent changes the order
* **Then**  the system saves the updated information

#### Scenario: Edit non-Draft order
* **Given** a supplier order has status Submitted or Received
* **When**  the Purchasing Agent tries to edit it
* **Then**  the order is not changed
* **And**   the system displays "Only a Draft supplier order can be edited"

### AC-N08.4 â€” Submit Supplier Order

#### Scenario: Submit order
* **Given** a valid Draft supplier order with at least one item exists
* **When**  the Purchasing Agent submits the order
* **Then**  the status changes to Submitted

#### Scenario: Submit empty order
* **Given** a Draft supplier order has no items
* **When**  the Purchasing Agent tries to submit it
* **Then**  the status stays Draft
* **And**   the system displays "Order has no items"

#### Scenario: Unauthorized change
* **Given** the user is not authorized to manage supplier orders
* **When**  they try to create, edit, or submit an order
* **Then**  the supplier order is not changed
* **And**   the system displays "You are not authorized to manage supplier orders"
