# Feature: Supplier

**Feature ID:**        N03  
**Branch pattern:**    `feature/3-supplier`  
**Status:**            Draft  
**Created:**           2026-09-21  
**Input:**             Supplier registration, supplier management, purchase ordering, and supplier performance tracking.  
**Depends on:**        [Company](feature_1_Company_maintinence .md)  
**Related:**           [Supplier Order](feature_8_Supplier_order_Management.md), [Inventory](feature_5_Inventory__maintinence.md), [Receive Supplier Order](feature_13_receive_supplier_order.md), [Supplier Did Not Ship](feature_17_supplier_did_not_ship.md)

---

## User Stories

### US-N03.1: View Suppliers
**As a**        Procurement Manager  
**I want to**  View Supplier information  
**So that**    I can access supplier details when needed.  
**Priority:**               P1  
**Independent test:**   Select View Suppliers and verify that all suppliers are displayed  
**Acceptance scenarios:**   See AC-N03.1

### US-N03.2: Add Supplier
**As a**      Procurement Manager  
**I want to** add a supplier  
**So that**   the company can purchase inventory from that supplier.  
**Priority:**              P1  
**Independent test:**    Enter valid supplier information and verify the supplier is saved.  
**Acceptance scenarios:**  See AC-N03.2

### US-N03.3: Edit Supplier
**As a**         Procurement Manager  
**I want to**    edit supplier information  
**So that**     supplier records remain accurate.  
**Priority:**             P1  
**Independent test:**  Update supplier information and verify the changes are saved.  
**Acceptance scenarios:** See AC-N03.3

### US-N03.4: Delete Supplier
**As a**        Procurement Manager  
**I want to**   Delete a supplier  
**So that**     The list of the suppliers must be updated  
**Priority:**             P1  
**Independent test:** Deleted supplier must not appear to the list of suppliers  
**Acceptance scenarios:** See AC-N03.4

### US-N03.5: Track Supplier Performance
**As a**       Procurement Manager  
**I want to**   track supplier delivery performance  
**So that**     I can evaluate supplier reliability.  
**Priority:**             P1  
**Independent test:** View supplier history and verify delivery information is displayed.  
**Acceptance scenarios:** See AC-N03.5

---

## Functional Requirements

- **FR-001**: System MUST assign every supplier a unique identifier.
- **FR-002**: System MUST allow authorized users to create, edit, view, and archive suppliers.
- **FR-003**: System MUST allow authorized users to view supplier information.
- **FR-004**: System MUST allow authorized users to edit supplier information.
- **FR-005**: System MUST allow authorized users to archive suppliers.
- **FR-006**: System MUST prevent duplicate supplier codes.
- **FR-007**: System MUST store supplier contact information.
- **FR-008**: System MUST store supplier lead time information.
- **FR-009**: System MUST prevent unauthorized users from creating, editing, or archiving a supplier.

---

## Key Entities

- **Supplier**:        A company that provides inventory items.
- **Company**:         The company purchasing inventory from suppliers.
- **Supplier Order**:  Orders placed with suppliers.
- **Inventory Item**:  Items supplied by suppliers.

---

## Data Model Requirements

### `Suppliers` table

 `supplier_code`   : unique code for the Supplier  
 `supplier_email`  : Work email for the supplier  
 `supplier_phone`  : Phone number for the supplier  
 `lead_time_days`  : the days the supplier is available  
 `created_at`      : this is the time that it was created

---

## Acceptance Criteria

### AC-N03.1 â€” View Suppliers

#### Scenario: View Existing Suppliers
*   **Given** suppliers exist in the system
*   **When**  the Procurement Manager selects View Suppliers
*   **Then**  the system displays all suppliers
*   **And**   Displays their Supplier information

### AC-N03.2 â€” Add Supplier

#### Scenario: Add Supplier
*   **Given** the Procurement Manager is authorized
*   **When** valid supplier information is entered
*   **Then** the system saves the supplier
*   **And** assigns a unique supplier identifier
*   **And** the supplier appears in the supplier list

#### Scenario: Duplicate Supplier Code
*   **Given** a supplier already has supplier code SUP001
*   **When**  The manager creates another supplier with SUP001
*   **Then**  the new supplier is not saved
*   **And**   the system displays "Duplicate supplier code"

### AC-N03.3 â€” Edit Supplier

#### Scenario: Edit Supplier
*   **Given** an active supplier exists
*   **When**  the Procurement Manager updates the supplier information
*   **Then** the system saves the updated information
*   **And** displays the updated supplier information

### AC-N03.4 â€” Delete Supplier

#### Scenario: Delete Supplier
*   **Given** a supplier no longer supplies the Company
*   **When**  the Procurement Manager deletes the supplier
*   **Then** the supplier disappears from the list
*   **And** the system displays "Supplier deleted"

### AC-N03.5 â€” Track Supplier Performance

#### Scenario: View Supplier Performance
*   **Given** supplier performance records exist
*   **When** the Procurement Manager views supplier performance
*   **Then** the system displays delivery history
*   **And** supplier performance information

#### Scenario: Unauthorized Update
*   **Given** the user is not authorized
*   **When** the user attempts to create, edit, or archive a supplier
*   **Then** the supplier is not changed
*   **And** the system displays "You are not authorized to manage suppliers"
