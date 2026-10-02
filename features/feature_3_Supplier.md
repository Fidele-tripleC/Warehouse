# Feature: <Supplier>

**Feature ID:**        N03  
**Branch pattern:**   `Supplier `  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**         Supplier registration, supplier management,        purchase ordering, and supplier performance tracking.
**Depends on:** [Company Feature](features/feature_1_)
**Related**     Supplier Order, Inventory
---

## User Stories

### US-N.3.1: View Suppliers
**As a**        Procurement Manager
**I want to**  View Supplier information
**So that**    Sothet i can access supplier details when needed.

**Priority:**               P1  
**Independent test:**   Select View Suppliers and verify that all supplier are displayed
**Acceptance scenarios:**   US-3.1: under th acceptance criteria

### US-N.3.2: -Add Supplier
**As a**      Procurement Manager
**I want to** add a supplier
**So that**   the company can purchase inventory from that supplier.
**Priority:**              P1  

**Independent test:**    Enter valid supplier information and verify the supplier is saved.

**Acceptance scenarios:**  see ### US-N.3.2 under the acceptance criteria

### US-N.3.3:    Edit Supplier
**As a**         Procurement Manager
**I want to**    edit supplier information
**So that**     supplier records remain accurate.
**Priority:**             P1  
**Independent test:**  Update supplier information and verify the changes are saved.

**Acceptance scenarios:** see ### US-N.3.3 under the acceptance criteria

---

### US-N.3.4: Delete Supplier
**As a**        Procurement Manager
**I want to**   Delete a supplier
**So that**     The list of the supplers must be updated
**Priority:**             P1  
**Independent test:** Deleted supplier must not apperar to the list of suppliers

### US-N.3.5: Track Supplier Performance
**As a**       Procurement Manager
**I want to**   track supplier delivery performance
**So that**     I can evaluate supplier reliability.
**Priority:**             P1  
**Independent test:** View supplier history and verify delivery information is displayed.


### Functional Requirements

- **FR-001**:System MUST assign every supplier a unique identifier.
- **FR-002**:System MUST allow authorized users to create, edit, view, and archive suppliers.
- **FR-003**:System MUST allow authorized users to view supplier information.
- **FR-004**:System MUST allow authorized users to edit supplier information.
 **FR-005**:System MUST allow authorized users to archive suppliers.
 **FR-006**:System MUST prevent duplicate supplier codes.
 **FR-007**:System MUST store supplier contact information.
 **FR-008**:System MUST store supplier lead time information.
 
---

## Key Entities

**Supplier**:        A company that provides inventory items.
**Company**:         The company purchasing inventory from suppliers.
**Supplier Order**:  Orders placed with suppliers.
**Inventory Item**:  Items supplied by suppliers.

---

## Data Model Requirements

### `Sppliers` table
_
 Fields:           
           
 `supplier_code`   : unique code for the Supplier 
 `supplier_email`  : Work emaill for the supplier
 `supplier_phone`  : Phone number for the supplier   
 `lead_time_days`  : the days the supplier is available  
 `created_at`      : this is the time that it was created   

---

## Acceptance Criteria

### US-N.3.1 — View Suppliers
#### Scenario: View Existing Suppliers
*   **Given** suppliers exist in the system
*   **Then**  the Procurement Manager selects View Suppliers
*   **And**   the system displays all suppliers
*   ***And**  Displys their Supplier

### US-N.3.2 — Add Supplier
#### Scenario: Add Supplier
*   **Given** the Procurement Manager is authorized
*   **When** valid supplier information is entered
*   **Then** the system saves the supplier
*   **And*** assigns a unique supplier identifier


#### Scenario: Duplicate Supplier Code
*   **Given** a supplier already has supplier code SUP001 …
*   **When**  The manager creates another supplier with SUP001 …
*   **Then**  The system rejects the supplier …
*   **And**   Displays a duplicate supplier code message

### US-N.3.3 — Edit Supplier
#### Scenario: Edit Supplier
*   **Given** an active supplier exists …
*   **When**  the Procurement Manager updates the supplier information 
*   **Then** the system saves the updated information …

#### Scenario: ADelete Supplier
*   **Given** a suupplier no longer supply the Company …
*   **When**  the Procurement Manager deletes the supplier 
*   **Then** the supplier desappears from the list …

### US-N.3.5 — Track Supplier Performance

#### Scenario: View Supplier Performance
*   **Given** supplier performance records exist
*   **When** the Procurement Manager views supplier performance
*   **Then** the system displays delivery history
*   **And** supplier performance information

#### Scenario: Unauthorized Update
*   **Given** the user is not authorized
*   **When** the user attempts to create, edit, or archive a supplier
*   **Then** the system does not allow the change.