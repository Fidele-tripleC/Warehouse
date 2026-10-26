# Feature: Supplier_Order

**Feature ID:**        N08
**Branch pattern:**    `supplier-order/<short-description>`
**Status:**            Draft
**Created:**           2026-09-21
**Input:**             Create, view, edit, submit, and track purchase orders sent to suppliers.
**Depends on:**        [Supplier](features/feature_supplier.md), [Inventory](features/feature_5_Inventory.md) 
**Related:**           Warehouse

---

## User Stories

### US-N08.1: Create supplier order
**As a**       Purchasing Agent
**I want to**  create an order for a supplier
**So that**    needed inventory can be ordered

**Priority:**             P1
**Independent test:**     Create an order for 50 units of an item; the order is saved with the correct supplier, item, and quantity.
**Acceptance scenarios:** See AC-N04.1

### US-N08.2: View supplier orders
**As a**       Purchasing Agent
**I want to**  view supplier orders
**So that**    I can see what inventory has been ordered

**Priority:**             P1
**Independent test:**     Create a supplier order; it appears in the supplier order list with its status.
**Acceptance scenarios:** See AC-N04.2

### US-N08.3: Edit supplier order
**As a**       Purchasing Agent
**I want to**  edit an order before it is submitted
**So that**    incorrect order information can be corrected

**Priority:**             P1
**Independent test:**     Change an order quantity from 50 to 60; the updated quantity is saved.
**Acceptance scenarios:** See AC-N04.3

### US-N08.4: Submit supplier order
**As a**       Purchasing Agent
**I want to**  submit a completed supplier order
**So that**    the order can be tracked as an active order

**Priority:**             P1
**Independent test:**     Submit a Draft order; its status changes to Submitted.
**Acceptance scenarios:** See AC-N04.4

---

## Requirements

### Functional Requirements

- **FR-001**: The system MUST assign every supplier order a unique identifier.
- **FR-002**: The system MUST associate each order with an active supplier.
- **FR-003**: The system MUST allow authorized users to create and view supplier orders.
- **FR-004**: The system MUST allow a Draft order to be edited, and MUST NOT allow Submitted or Received orders to be edited.
- **FR-005**: The system MUST record the items and quantities being ordered.
- **FR-006**: The system MUST maintain the order status (Draft, Submitted, Received).
- **FR-007**: The system MUST prevent unauthorized users from creating, editing, or submitting supplier orders.
- **FR-008**: The system MUST reject order items with a quantity of zero or less.
- **FR-009**: The system MUST NOT allow an order with no items to be submitted.

---

## Key Entities

- **Supplier Order**: a purchase order placed with one Supplier. Contains one or more Order Items.
- **Supplier**: the company receiving the order. One Supplier can have many Supplier Orders.
- **Order Item**: one line of an order: an Inventory Item and the quantity ordered. Belongs to one Supplier Order.
- **Inventory Item**: a stocked item (see N05) that can be ordered.
- **Purchasing Agent**: the authorized user who manages supplier orders.
---

## Data Model Requirements

### `supplier_order` table
 Field                                                            

 `order_id`          : this the unique  id important for the database
 `order_code`        : this the unique code for the order       
 `created_at`        : this is the time when the order was created
 `updated_at`        : this is the time it was updated 
 `submitted_at`      : this it the time it was submitted

## Acceptance Criteria

### AC-N08.1 — Create Supplier Order

#### Scenario: Create order
* **Given** an active supplier exists
* **When**  the Purchasing Agent creates an order with valid items and quantities
* **Then**  the system saves the order with status Draft
* **And**   assigns it a unique identifier

#### Scenario: Invalid quantity
* **Given** the Purchasing Agent is creating an order
* **When**  the quantity is zero or less
* **Then**  the system rejects the order item and shows a validation error

#### Scenario: Inactive supplier
* **Given** a supplier has status Inactive
* **When**  the Purchasing Agent tries to create an order for that supplier
* **Then**  the system rejects the order

### AC-N08.2 — View Supplier Orders

#### Scenario: View orders
* **Given** supplier orders exist
* **When**  the Purchasing Agent selects "View Supplier Orders"
* **Then**  the system displays the supplier orders and their current statuses

#### Scenario: No orders
* **Given** no supplier orders exist
* **When**  the Purchasing Agent selects "View Supplier Orders"
* **Then**  the system displays a message that no orders are available

### AC-N08.3 — Edit Supplier Order

#### Scenario: Edit Draft order
* **Given** a supplier order has Draft status
* **When**  the Purchasing Agent changes the order
* **Then**  the system saves the updated information

#### Scenario: Edit non-Draft order
* **Given** a supplier order has status Submitted or Received
* **When**  the Purchasing Agent tries to edit it
* **Then**  the system rejects the change

### AC-N08.4 — Submit Supplier Order

#### Scenario: Submit order
* **Given** a valid Draft supplier order with at least one item exists
* **When**  the Purchasing Agent submits the order
* **Then**  the status changes to Submitted

#### Scenario: Submit empty order
* **Given** a Draft supplier order has no items
* **When**  the Purchasing Agent tries to submit it
* **Then**  the system rejects the submission and shows an error

#### Scenario: Unauthorized change
* **Given** the user is not authorized to manage supplier orders
* **When**  they try to create, edit, or submit an order
* **Then**  the system rejects the change