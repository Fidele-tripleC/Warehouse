# Feature: <Warehouse>

**Feature ID:**        N02 
**Branch pattern:**   `Warehouse `  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**             Creating, Viewing, editing and maintaining warehouse locations  
**Depends on:** [Company Feature](features/feature_1_)
---

## User Stories

### US-N.2.1:   View Warehouses
**As a**        A warehouse Manager
**I want to**   View all warehouses
**So that**     I can see the Warehouse locations maintained by the company.
**Priority:**               P1  
**Independent test:**    Select View Warehouses and verify that the system displays all existing warehouses and their information.
**Acceptance scenarios:**   US-2.1: under th acceptance criteria

### US-N.2.2: Add Warehouse
**As a**       Warehouse Manager
**I want to**  add a warehouse
**So that**    The company can maintain inventory at that location

**Priority:**               P1  
**Independent test:**    Enter valid warehouse information and save it. Verify that the new warehouse appears in the warehouse list
**Acceptance scenarios:**   US-2.2: under th acceptance criteria

### US-N.2.3:  eddit Warehouse
**As a**       Warehouse Manager
**I want to**  Edit warehouse information
**So that**    Warehouse information remains accurates

**Priority:**               P1  
**Independent test:**   Change an existing warehouse address and identify that the updated address is saved and displayed
**Acceptance scenarios:**   US-2.3: under th acceptance criteria

### US-N.2.4:  Delete warehouse
**As a**       As a Warehouse Manager  
**I want to**  Delete a warehouse
**So that**   Warehouse that are no longer being desappers from the company 
**Priority:**               P1  
**Independent test:** Create a warehouse with WH001 and Delete it, view warehouse and see , it will no longer exists.
**Acceptance scenarios:**   US-2.4: under th acceptance criteria



### Functional Requirements

- **FR-001**: System Must allow the warehouse Manager to view the warehouses that the company have
- **FR-002**: System Must allow an authorised Aware house manager to create a warehouse with the unique Code.
- **FR-003**: System must allow an outhorised  Warehouse Manager to eddit the infromation of an existing Warehouse when needed
- **FR-004**: System MUST allow an authorized Warehouse Manager to delete the warehouse when no longer works.


## Key Entities

- **Warehouse**: Represents a physical location where inventory is stored.
- **Company**:   The company Associated with the warehouse 

- **relationships** Stock maintained at a warehouse .
- one **Company** can have multiple **Warehouses**
- one **Warehouse** cab contain Multiple **Items**


---

## Data Model Requirements

### `Warehouse` table

 Field              Description
-------            
 `warehouse_id`     : This is the unique id  
 `warehouse_name`   : This is the name  of the Warehouse
 `warehouse_code`   : This is the code that is unique
 `address`          : This is the Physical location           
 `created_at`       : This is the time when the warehouse were created 
---

## Acceptance Criteria

### US-N.2.1 — View Warehouses

#### Scenario: View existing Warehouses
*   **Given** warehouse exists int the system
*   **When**  the warehouse Manager selects View Warehouses
*   **Then**  The system displays the warehouses
*   **And**   Displays their current information

#### Scenario: No warehouse
*   **Given** No warehouse exits
*   **When**  the warehouse Manager selects View Warehouses …
*   **Then**  the system rejects the new company
*   **And**   the system displays a message indicating that no warehouses are availeble


### US-N.2.2 — Add warehouse

#### Scenario: Add warehouse
*   **Given** The Warehouse Manager us authorized
*   **When**  The amanager enters valid warehouse information
*   **Then**  the system saves the warehouse  …
*   **And**   associate it with the company


#### Scenario: Duplicate Warehouse code
*   **Given** a warehouse with a given code  already exists…
*   **When**  the manager tries to create another warehouse with the same code…
*   **Then**  The system rejects the warehouse …
*   **And**   display a duplicate warehouse code message

### US-N.2.3 — Edit Warehouse code

#### Scenario: Edit warehouse
*   **Given**  A warehouse exists
*   **When**  The Warehouse manager edits its information
*   **Then**  the system saves the updated informmation  …
*   **And**   displays the updated warehouse

### US-N.2.4 — Delete warehouse 

#### Scenario:  Delete warehouse
*   **Given**  an active warehouse exist and No longer works…
*   **When**   The Awarehouse deletes it
*   **Then**   the warehouse desappeas from the lists…

#### Scenario: Unauthorized update
*   **Given**  The user is not authorized to manage warehouses…
*   **When**   the user attempts to add, eddit , or archive a warehouse 
*   **Then**   The system does not allow the change …




