# Feature: <Company>

**Feature ID:**        N01  
**Branch pattern:**   `Company `  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**             Company registration, company information management, and company status management.     
**Depends on:**        None
---

## User Stories

### US-N.1.1: Creating a company
**As a**        System Administrator
**I want to**   create, view, edit, and archive company information
**So that**     the system maintains accurate information about the company using the warehouse system.
**Priority:**               P1  
**Independent test:**     Create a company with a unique company code and valid company information. Verify that the company is saved and can be viewed. 
**Acceptance scenarios:**   US-1.1: under th acceptance criteria



### Functional Requirements

- **FR-001**: System MUST assign each company a unique identifier.
- **FR-002**: System MUST allow authorized users to create, view, and edit company information.
- **FR-003**: System MUST allow a company to be marked Active or Inactive.
- **FR-005**: System MUST record when the company was created.
- **FR-006**: System MUST allow warehouses to be associated with a company.
- **FR-007**: System MUST prevent duplicate company codes.

---

## Key Entities

- **Company**: Represents the business using the inventory system.
- **Warehouse**: A storage facility belonging to a company. …


- **Relationship** One company can have one or more warehouses.

---

## Data Model Requirements

### `Inventory` table
------------------------------------------------------------
| Field            | Type         | Rules                  |
|-------           |------        |-------                 |
| `company_id`     |INTEGER PK    |Auto-increment, unique  |
| `company_code`   |VARCHAR(100)  |Required , unique       |
| `company_name`   |VARCHAR       |Required                |
| `company_email`  |VARCHAR       |Optional                |
| `company_phone`  |VARCHAR(30)   |Optional                |
| `address`        |VARCHAR(255)  |Optional                |
| `status`         |VARCHAR(20)   |Active, Inactive        |
| `created_at`     |DATETIME      |Required                | 

### Associations (if known)
- …

---

## Acceptance Criteria

### US-N.1 — Manage company Creation

#### Scenario: Create Company
*   **Given**  System Administrator is authorized
*   **When**  the System Administrator enters valid company information
*   **Then**  the system creates the company
*   **And**   assigns the company a unique identifier.

#### Scenario: Duplicate Company Code
*   **Given** a company with code COMP001 already exists
*   **When**  another company is created using COMP001 …
*   **Then**  the system rejects the new company
*   **And**   displays a duplicate company code message


### US-N.1 — Maintain the company

#### Scenario: Edit Company
*   **Given** a company already exists
*   **When**  the authorized user updates the company information
*   **Then**  the system saves and displays the updated information …


#### Scenario: Archive Company
*   **Given** an active company exist…
*   **When**  The authorized user archives the company…
*   **Then**  The company's status channges to Inactive…

#### Scenario: Associate Warehouse
*   **Given** an authorized user creates a warehouse for the comapany…
*   **When**  The warehouse is associated with that company…
