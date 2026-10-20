# Feature: Company

**Feature ID:**        N01  
**Branch pattern:**    `feature/1-company`  
**Status:**            Draft  
**Created:**           2026-09-21  
**Input:**             Company registration, company information management, and company status management.  
**Depends on:**        None  
**Related:**           [Warehouse](feature_2_Warehouse__maintinence.md)

---

## User Stories

### US-N01.1: Creating company
**As a**        System Administrator  
**I want to**   Create a company information  
**So that**     the System maintains accurate information about the company using the warehouse system.  
**Priority:**               P1  
**Independent test:**    Create a company with a unique code and valid company information  
**Acceptance scenarios:**   See AC-N01.1

### US-N01.2: View Company Information
**As a**      System Administrator  
**I want to** View company details  
**So that**   I can access company information when needed.  
**Priority:**               P1  
**Independent test:**  Search for an existing company and verify its information is displayed.  
**Acceptance scenarios:**   See AC-N01.2

### US-N01.3: Edit Company Information
**As a**      System Administrator  
**I want to** Update Company information  
**So that**   company records remain accurate and updated  
**Priority:**               P1  
**Independent test:** Update company information and verify the changes are saved and can be displayed.  
**Acceptance scenarios:**   See AC-N01.3

### US-N01.4: Assigning a warehouse to a company
**As a**      System Administrator  
**I want to** assign the warehouse to a company  
**So that**   the warehouse belongs to the Company.  
**Priority:**               P1  
**Independent test:** When a company is given a warehouse, it belongs to it in the documentation.  
**Acceptance scenarios:**   See AC-N01.4

### US-N01.5: Delete a Company
**As a**      System Administrator  
**I want to** Delete a company  
**So that**   The company's status should correspond to the actual status of the Company.  
**Priority:**               P1  
**Independent test:** When a company stops permanently, its information should not exist.  
**Acceptance scenarios:**   See AC-N01.5

---

## Functional Requirements

- **FR-001**: System MUST assign each company a unique identifier.
- **FR-002**: System Must allow the authorised user to view the Company that exists.
- **FR-003**: System MUST allow the authorized users to create company information.
- **FR-004**: System MUST allow authorized users to edit company information.
- **FR-005**: System MUST allow warehouses to be associated with a company.
- **FR-006**: System Must allow the authorized user to delete a company.

---

## Key Entities

- **Company**: Represents the business using the inventory system.
- **Warehouse**: A storage facility belonging to a company.

- **Relationship:** One company can have one or more warehouses.

---

## Data Model Requirements

### `Company` table

 `company_code`  : unique code identification  
 `company_name`  : Unique name for the reference  
 `company_email` : Company business E-mail  
 `company_phone` : This is the business Phone for the business  
 `address`       : This is the Map address for the business Location  
 `created_at`    : This is the Date it was created

---

## Acceptance Criteria

### AC-N01.1 â€” Create Company

#### Scenario: Create Company
*   **Given**  System Administrator is authorized
*   **When**  the System Administrator enters valid company information
*   **Then**  the system creates the company
*   **And**   assigns the company a unique identifier
*   **And**   the new company appears in the company list

#### Scenario: Duplicate Company Code
*   **Given** a company with code COMP001 already exists
*   **When**  another company is created using COMP001
*   **Then**  the new company is not created
*   **And**   the system displays "Duplicate company code"

### AC-N01.2 â€” View a company

#### Scenario: View Company
*   **Given** a company already exists
*   **When**  the authorized user clicks view the company
*   **Then**  the system displays companies
*   **And**   displays the company information

### AC-N01.3 â€” Edit Company Information

#### Scenario: Edit Company
*   **Given** a company already exists
*   **When**  the authorized user updates the company information
*   **Then**  the system saves the changes
*   **And**   Displays the updated company information

### AC-N01.4 â€” Assigning a warehouse to a company

#### Scenario: Associate Warehouse
*   **Given**  a company exists
*   **And**    a warehouse exists
*   **When**   the authorized user assigns the warehouse to the company
*   **Then**   a warehouse is linked to the company
*   **And**    The association is saved
*   **And**    the company details show the associated warehouse

#### Scenario: View Associated Warehouse
*   **Given**  a company has one or more warehouses
*   **When**   the authorized user views the company details
*   **Then**   the system displays associated warehouse

### AC-N01.5 â€” Delete a company

#### Scenario: Delete company
*   **Given**  The company no longer works
*   **When**   the authorized user presses DELETE
*   **Then**   the company become deleted in the System
*   **And**    the company does not appear in the company list
*   **And**    the system displays "Company deleted"
