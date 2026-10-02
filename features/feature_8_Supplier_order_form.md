# Feature: <Supplier Order Form>

**Feature ID:**        N04 
**Branch pattern:**   `Supplier Order Form`  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**       Creating, Viewing, editing submitting , and tracking purchase orders sent suppliers  
**Depends on:**       Supplier, Inventory
**Related:**           Warehouse
---

## User Stories

### US-N.4.1:  Create Supplier Order
**As a**        A purchase Agent
**I want to**   create an order for ssupplier 
**So that**     Needed inventory can be ordered.
**Priority:**               P1  
**Independent test:**   Create an order for 50 units of item and verify that the order is saved with the correct supplier, item, and quantiy.
**Acceptance scenarios:**   US-2.1: under th acceptance criteria

### US-N.4.2: View Supplier Orders
**As a**       a purchase Agent
**I want to**  View suppliers orders
**So that**   Ican see what inventory has been ordered
**Priority:**               P1  
**Independent test:**  Create a supplier order and verify that it appears in the supplier order list
**Acceptance scenarios:**   US-2.2: under th acceptance criteria


### US-N.4.3:  Edit Supplier Order
**As a**       Apurchasing Agent
**I want to**  Edit an order before it is submitted
**So that**    Incorrect order information can be corrected

**Priority:**               P1  
**Independent test:**  Change an order quantity from 50 to 60 and verify that the updated quantity is saved
**Acceptance scenarios:**   US-2.2: under th acceptance criteria

### US-N.4.4:  Submit Supplier Order
**As a**       apurchase Agent 
**I want to**  submit a completed supplier order
**So that**    the order can be tracked as an active order

**Priority:**               P1  
**Independent test:**  Submit a draft order and verify that its status changes to submitted
**Acceptance scenarios:**   US-2.2: under th acceptance criteria



### Functional Requirements

- **FR-001**:  System MUST assign every supplier order a unique identifier
- **FR-002**:  System MUST associate each order with an active supplier.
- **FR-003**:  System MUST allow authorized users to create and view supplier orders.
- **FR-004**:  System MUST allow a Draft order to be edited.
- **FR-005**:  System MUST record the items and quantities being ordered.
- **FR-006**:  System MUST maintain the order status.
- **FR-006**: System MUST prevent unauthorized users from modifying supplier orders.

## Key Entities

- **Supplier ordeer**: An order placed with a supplier.
- **Supplier**:        The supplier receiving the order.
- **Order Item**       The supplier receiving the order
- **Inventory Item**    An item and quantity inncluded in an order 


- one **Supplier** can have multiple **Orders**
- one **Supplier** cab contain Multiple **Items**


---

## Data Model Requirements

### `Supplier Order` table
---------------------------------------------------------------
| Field              | Type         | Rules                   |
|-------             |------        |-------                  |
| `order_id`         | INTEGER PK   |Auto-increment, unique   |
| `order_name`       | INTEGER PK   |Required                 |
| `order_code`       |   INTEGER FK |Required                 |
| `status`           |VARCHAR(20)   |required                 |
| `created_at`       | DATETIME     |required                 |
| `status`           |VARCHAR(20)   |Draft,Submitted, Received|
| `created_at`       |DATETIME      |Required                 | 

### `Supplier_Order_item ` table
---------------------------------------------------------------
| Field              | Type         | Rules                   |
|-------             |------        |-------                  |
| `order_item_id`    | INTEGER PK   |Auto-increment, unique   |
| `order_id`         | INTEGER PK   |Required                 |
| `item_id`          |   INTEGER FK |Required                 |
| `Quantity_ordered` |Integer       |required                 |

### Associations (if known)
- …

---

## Acceptance Criteria

### US-N.4.1 — Create Supplier Order

#### Scenario: Create order
*   **Given** an active supplier exists
*   **When**  the Purchasing Agent creates an order with valid items and quantities
*   **Then**  the system saves the order
*   **And**  assigns it a unique identifier.

#### Scenario: Invalid Quantity
*   **Given** the Purchasing Agent is creating an order
*   **When** the quantity is zero or less …
*   **Then**  the system rejects the order item.


### US-N.4.2 — View Supplier Orders

#### Scenario: View Orders
*   **Given** supplier orders exist
*   **When** the Purchasing Agent selects View Supplier Orders
*   **Then** the system displays the supplier orders and their current statuses.

### US-N.4.3 —Edit Supplier Order

#### Scenario: Edit Draft Order
*   **Given** a supplier order has Draft status
*   **When**  the Purchasing Agent changes the order
*   **Then**  the system saves the updated information.


### US-N.2.3 — Edit Warehouse code

#### Scenario: Edit warehouse
*   **Given**  A warehouse exists
*   **When**  The Warehouse manager edits its information
*   **Then**  the system saves the updated informmation  …
*   **And**   displays the updated warehouse

### US-N.2.3 —Submit Supplier Order
#### Scenario: Submit Order
*   **Given** a valid Draft supplier order exists
*   **When**  the Purchasing Agent submits the order
*   **Then**  the status changes to Submitted.






