# Feature: <Company>

**Feature ID:**        N01  
**Branch pattern:**   `Company `  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**             Company registration, company information management, and company status management.     
**Depends on:**        None
---

## User Stories

### US-N.1.1: Creating company
**As a**        System Administrator 
**I want to**   Create a company information
**So that**     the System maintains accurate information about the company using the warehouse system.
**Priority:**               P1  
**Independent test:**    Create a company with a unique code and valid company information
**Acceptance scenarios:**   US-1.1: under th acceptance criteria


### US-N.1.2: View Company Information
**As a**      System Administrator
**I want to** View company details
**So that**   Ican access company information when needed.
**Priority:**               P1  
**Independent test:**  Search for an existing company and verify its information is displayed.
**Acceptance scenarios:**   US-1.2: under th acceptance criteria


### US-N.1.3: Edit Company Information
**As a**      System Administrator
**I want to** Update Company information
**So that**   company records remain accurate and update
**Priority:**               P1  
**Independent test:** Update company information and verify the changes are saved and can be displayed.
**Acceptance scenarios:**   US-1.3: under th acceptance criteria

### US-N.1.4: Assigning a warehose to Acompany
**As a**      system Administrator
**I want to** assign the warehouse to acompany 
**So that**  so that the warehouse belong to the Company. 
status of the    Company.
**Priority:**  P1  
**Independent test:** When a company is given aware house, it belongs to it in the documentation.


### US-N.1.5: Delete a Company
**As a**      system Administrator
**I want to** Delete A company
**So that**   The company's status should coresopond to the actual status of the    Company.
**Priority:**               P1  
**Independent test:** When a company stops permantly, its information should not exist.

### Functional Requirements

- **FR-001**: System MUST assign each company a unique identifier.
-**FR-001**:   System Must allow the outhorised user to view the Company that exists.
- **FR-002**: System MUST allow the authorized users to create company information.
- **FR-003**: System MUST allow authorized users toedit company information.
- **FR-004**: System MUST allow warehouses to be associated with a company.
- **FR-005**: System Must allow the authorized user to delete a company.

---

## Key Entities

- **Company**: Represents the business using the inventory system.
- **Warehouse**: A storage facility belonging to a company. …


- **Relationship** One company can have one or more warehouses.

---

## Data Model Requirements

### `Company` table
              
 `company_code`  : unique code identification
 `company_name`  : Unique name for the reference
 `company_email` : Compan busness E-mail
 `company_phone` : This is the busness Phone for the busness
 `address`       : This is the Map address for the busness Location  
 `created_at`    : This is the Date date it was created
## Acceptance Criteria

### US-N.1.1 — Create Company 
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


### US-N.2 — View Acompany
#### Scenario: Edit Company
*   **Given** a company already exists
*   **When**  the authorized user clicks view the company
*   **Then**  the system the system displays companies

### US-N.2 — Edit Company Information
#### Scenario: Edit Company 
*   **Given** a company already exists
*   **When**  the authorized user updates the company information
*   **Then**  the system saves the changes
*   **And**   Displays the updated company information

### US-N.1.4 — Delete a company

#### Scenario: Delete company
*   **Given**  The company nolong works
*   **When**   When the authorized user press DELETE the company become deleted in the System.
*   **And**    the company become deleted in the System.

### US-N.1.4 — Delete a company

#### Scenario: Associate Warehouse
*   **Given**  a company exists
*   **When**   awarehouse exist
*   **then**   awarehouse is linked to the company
*   **And**    The association is saved

### Scenario : View Associated Warehouse
*   **Given**  acompany has one or more warehouses
*   **When**   the authorized user views the company details
*   **then**   the system displys associated warehouse


