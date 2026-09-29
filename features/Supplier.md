# Feature: <Supplier>

**Feature ID:**        N01  
**Branch pattern:**   `Supplier `  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**          Supplier registration, editing, purchase ordering, receiving, putaway, and supplier performance tracking.
**Related:**        Inventory Stocking Engine (Min-Max Algorithm), Bill of Lading (BOL) Tracking

---

## User Stories

### US-N.2.1: Manage Supplier Profiles
**As a**       Prcurement Manager
**I want to** Create, edit, inspect, and archive supplier profiles
**So that**   purchasing operations use accurate supplier information, contact details, and lead times.

**Priority:**               P1  
**Independent test:**    Create a supplier with a 5-day lead time. Verify that the supplier is saved and can be selected when creating a Purchase Order.
**Acceptance scenarios:**   US-1.1: under th acceptance criteria

### US-N.2.2:Generate Supplier Purchase Orders
**As a**      Apurchasing Agent / Automated Reorder Engine
**I want to** generate Purchase Orders manually or automatically using the Min-Max algorithm
**So that**   inventory can be replenished when stock falls below the minimum level.

**Priority:**              P1  

**Independent test:**     Set an item's minimum quantity to 20, maximum quantity to 100, and available quantity to 15. Trigger the reorder process and verify that a Purchase Order is generated.

**Reorder Formula:** Quantity to Order = Maximum Quantity - (Available Quantity + Quantity Already on Order)

**Acceptance scenarios:**  see ### US-N.1.2 under the acceptance criteria

### US-N.2.3:Dock Check-in and Reciving
**As a**         Warehouse Receiving cleck 
**I want to**    check incoming shipments against their Purchase Orders
**So that**      shortages, overages, and damaged goods are recorded correctly.

**Priority:**             P1  
**Independent test:**   Receive a PO expecting 100 units. Record 90 good units and 10 damaged units. Verify that 90 units move to Pending Putaway and 10 units are marked Quarantine/Discrepancy.


**Acceptance scenarios:** see ### US-N.1.3 under the acceptance criteria

---

### US-N.2.4: Putaway Processing 
**As a**        Warehouse floor Worker
**I want to**   Place checked-in stock into designated bin/rack locations 
**So that** received inventory becomes available in warehouse stock.

**Priority:**             P1  
**Independent test:** Select an item that has passed receiving check-in. Assign it to a valid bin and verify that its status changes from Pending Putaway to Available.

### US-N.2.5: Track Supplier Performance
**As a**       Procurement Manager
**I want to**   track supplier delivery performance and receiving discrepancies
**So that**I can evaluate supplier reliability.
**Priority:**             P1  
**Independent test:** Receive an order after its expected delivery date and record damaged products. Verify that the delivery and discrepancy information is recorded against the supplier.


### Functional Requirements

- **FR-001**:System MUST enforce a unique supplier identifier, such as supplier_code.
- **FR-002**:System MUST allow authorized users to create, edit, view, and archive suppliers.
- **FR-003**:System MUST store each supplier's lead time.
- **FR-004**:System MUST allow Purchase Orders to be assigned to an active supplier.
 **FR-005**:System MUST update quantity_in_order when a Purchase Order is submitted.
 **FR-006**:System MUST support partial receiving of Purchase Orders.
 **FR-007**:System MUST maintain PO status: Open, Partially Received, Fully Received.
 **FR-008**:System MUST record damaged, missing, or excess goods during receiving.
 **FR-009**:System MUST prevent putaway before dock check-in is completed.
 **FR-010**:System MUST record receiving timestamps and employee IDs.
 **FR-011**:System MUST maintain supplier delivery and discrepancy history.
---



## Key Entities

- **Entity**: short description; relationships in plain language
- **Entity**: …

---

## Data Model Requirements

### `Sppliers` table
_______________________________________________________________
| Field              | Type         | Rules                   |
|-------             |------        |-------                  |
| `Supplier_id`      | INTEGER PK   | Auto-increment, unique  |
| `supplier_code`    |VARCHAR(30)   |Required, unique, Indexed|
| `supplier_email`   |VARCHAR(100)  |Required, >= 1, Default:7|
| `supplier_phone`   |VARCHAR       |optional                 |  
| `lead_time_days`   |INTGER        | Required, >=0           | 
| `status`           |VARCHAR(20)   | Enum: Active, Inacive,  | 
| `created_at`       |DATETIME      |Required                 | 



---

## Acceptance Criteria

### US-N.1 — Manage Supplier Profiles

#### Scenario: Create Supplier
*   **Given** The producer Procurement Manager is authorized  
*   **When**  They enter valid supplier information
*   **Then**  The system creates the supplier 
*   **And**   Assigns the supplier a unique identifier

#### Scenario: Duplicate Supplier Code
*   **Given** a supplier already has supplier code SUP001 …
*   **When**  The manager creates another supplier with SUP001 …
*   **Then**  The system rejects the supplier …
*   **And**   Displays a duplicate supplier code message

#### Scenario: Edit Supplier
*   **Given** an active supplier exists …
*   **When**  the Procurement Manager updates the supplier information 
*   **Then** the system saves the updated information …

#### Scenario: Archive Supplier
*   **Given** an active supplier exists …
*   **When**  the Procurement Manager archives the supplier 
*   **Then** the supplier status changes to Inactive …

### US-N.1.2: Generate Purchase Orders

#### Scenario: Add an Item
*   **Given** Given the warehouse manager is authorized…
*   **When**  The manager adds a new item and its quantity…
*   **Then**  The System Saves the item    …
*   **And**   The updated item appears in the the quantity of that item in the inventory …

#### Scenario: Edit an Item
*   **Given** An item already exist in the inventory …
*   **When**  The warehouse manager edits the item or uits quantity…
*   **Then**  The System saves and displays the uupdated information  …

#### Scenario: Delete an Item
*   **Given** An item already exist in the inventory …
*   **When**  The warehouse manager delete the item …
*   **Then**  The item is removed from the inventory …

#### Scenario: Unathorized update
*   **Given** The user is not authorized to update inventory  …
*   **When**  The user tries to add ,edit, or delete an item …
*   **Then**  The system does not allow the change …

### US-N.2 — Automated Warning

#### Scenario: Item is below minimum quantity
*   **Given**  An item has a defined minimum quantity…
*   **When**   The Item's current quantity goes below the minimum quantity…
*   **Then**   The System displays a warning to the warehouse Manager  …
*   **And**    The warning identifies the item that needs to be restocked …



