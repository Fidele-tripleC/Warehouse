# Feature: Company

**Feature ID:**        N01  
**Branch pattern:**    `feature/1-company`  
**Status:**            Draft  
**Created:**           2026-09-21  
**Input:**             Company registration, company information management, and company status management.  
**Build order:**        2 of 20  
**Depends on:**        [Authentication](feature_20_authentication.md)  
**Related:**           [Warehouse](feature_02_Warehouse__maintinence.md) (next)

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
- **FR-007**: System Must prevent unauthorized users from creating, editing, assigning a warehouse, or deleting a company.

---

## Assumptions

- Only a System Administrator can add, edit, or delete a company.
- The user is logged in before this screen opens (see N20).
- Company code must be unique.
- One company can have more than one warehouse.
- A retailer does not log in and does not change company records.

---

## Edge Cases

- The company code is already used.
- There is no company yet.
- The warehouse is already linked to a company.
- The user is not a System Administrator.
- Name or code is empty.

---

## Success Criteria

- **SC-001**: A System Administrator can save a company with a unique code and see it in the list.
- **SC-002**: If the code is already used, the system displays "Duplicate company code".
- **SC-003**: A System Administrator can see the company and the warehouses linked to it.
- **SC-004**: A System Administrator can edit the company and see the new information.
- **SC-005**: If the user is not allowed, the system displays "You are not authorized to manage companies".
- **SC-006**: If there is no company, the system displays "No companies are available".

---

## Key Entities

- **Company**: the business that owns the warehouses.
- **Warehouse**: a place where stock is stored. It belongs to a company.
- **Relationship:** one company can have one or more warehouses.

---

## Initial Data Model

### `Company` table

 `company_id`    : this is the unique id  
 `company_code`  : unique code identification  
 `company_name`  : Unique name for the reference  
 `company_email` : Company business E-mail  
 `company_phone` : This is the business Phone for the business  
 `address`       : This is the Map address for the business Location  
 `created_at`    : This is the Date it was created

---

## Gherkin AC

### AC-N01.1 — Create Company

#### Scenario: Create Company

* **Given**  System Administrator is authorized
* **When**  the System Administrator enters valid company information
* **Then**  the system creates the company
* **And**   assigns the company a unique identifier
* **And**   the new company appears in the company list

#### Scenario: Duplicate Company Code

* **Given** a company with code COMP001 already exists
* **When**  another company is created using COMP001
* **Then**  the new company is not created
* **And**   the system displays "Duplicate company code"

#### Scenario: Invalid company data

* **Given** the System Administrator is authorized
* **When**  they submit a company with an empty name or empty code
* **Then**  the company is not created
* **And**   the system displays "Invalid company data"

### AC-N01.2 — View a company

#### Scenario: View Company

* **Given** a company already exists
* **When**  the authorized user clicks view the company
* **Then**  the system displays companies
* **And**   displays the company information

#### Scenario: No companies

* **Given** no company exists
* **When**  the authorized user selects View Company
* **Then**  the company list is empty
* **And**   the system displays "No companies are available"

### AC-N01.3 — Edit Company Information

#### Scenario: Edit Company

* **Given** a company already exists
* **When**  the authorized user updates the company information
* **Then**  the system saves the changes
* **And**   Displays the updated company information

### AC-N01.4 — Assigning a warehouse to a company

#### Scenario: Associate Warehouse

* **Given**  a company exists
* **And**    a warehouse exists
* **When**   the authorized user assigns the warehouse to the company
* **Then**   a warehouse is linked to the company
* **And**    The association is saved
* **And**    the company details show the associated warehouse

#### Scenario: View Associated Warehouse

* **Given**  a company has one or more warehouses
* **When**   the authorized user views the company details
* **Then**   the system displays associated warehouse

### AC-N01.5 — Delete a company

#### Scenario: Delete company

* **Given**  The company no longer works
* **When**   the authorized user presses DELETE
* **Then**   the company become deleted in the System
* **And**    the company does not appear in the company list
* **And**    the system displays "Company deleted"

#### Scenario: Unauthorized change

* **Given** the user is not authorized to manage companies
* **When**  the user attempts to create, edit, or delete a company
* **Then**  the company is not changed
* **And**   the system displays "You are not authorized to manage companies"

---

## Data Ownership & Isolation

Only a logged in System Administrator can add, change, or delete a company.

| Rule | Requirement |
|------|-------------|
| **Read scope** | System Administrator can view companies |
| **Write scope** | Only System Administrator can add, edit, assign a warehouse, or delete |
| **Create scope** | The signed in System Administrator creates the new company |
| **Cross-user access** | If the company is not found or not allowed, return `404` and `{ "message": "..." }` |
| **UI scope** | Company screens open only after login |
| **Implementation** | Check the login token on `/api/companies` |

---

## API Requirements

Base path: `/api`. Error body: `{ "message": "..." }`. Send `Authorization: Bearer <token>`.

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `GET` | `/api/companies` | Yes | View the company list |
| `GET` | `/api/companies/:id` | Yes | View one company and its warehouses |
| `POST` | `/api/companies` | Yes | Add a company |
| `PUT` | `/api/companies/:id` | Yes | Edit a company |
| `DELETE` | `/api/companies/:id` | Yes | Delete a company |
| `PUT` | `/api/companies/:id/warehouses/:warehouseId` | Yes | Link a warehouse to the company |

**Add company body:**

```json
{
  "company_code": "COMP001",
  "company_name": "Fidele Warehouse Co",
  "company_email": "fidele@.example",
  "company_phone": "555-0100",
  "address": "100 Dock Road"
}
```

**Saved:** `201` and the company with `company_id`  
**Duplicate code:** `400` `{ "message": "Duplicate company code" }`  
**Empty name or code:** `400` `{ "message": "Invalid company data" }`  
**Not allowed:** `401` `{ "message": "You are not authorized to manage companies" }`  
**Not found:** `404`

---

## Screen Requirements

Menu after login: **Company** (System Administrator only). No Company menu on the login screen.

Pictures: [`docs/ui/feature-01/`](../docs/ui/feature-01/)

### Company list
- Heading: Company
- Button: **Add Company**
- List: code, name, email, phone
- On a row: View, Edit, Delete

![Company list](../docs/ui/feature-01/company-list.png)

Empty: "No companies are available"

![Empty company list](../docs/ui/feature-01/company-list-empty.png)

After delete: "Company deleted"

![Company deleted](../docs/ui/feature-01/company-deleted.png)

Not allowed: "You are not authorized to manage companies"

![Not authorized](../docs/ui/feature-01/company-not-authorized.png)

### Add Company
- Fields: code, name, email, phone, address
- Buttons: **Save**, **Cancel**

![Add Company](../docs/ui/feature-01/company-add.png)

Duplicate code: "Duplicate company code"

![Duplicate company code](../docs/ui/feature-01/company-add-duplicate.png)

Empty name or code: "Invalid company data"

![Invalid company data](../docs/ui/feature-01/company-add-invalid.png)

### Company details
- Shows company information and linked warehouses
- Buttons: **Assign Warehouse**, **Edit**, **Delete**

![Company details](../docs/ui/feature-01/company-details.png)

### Assign Warehouse
- Choose a warehouse
- Buttons: **Save**, **Cancel**

![Assign Warehouse](../docs/ui/feature-01/company-assign-warehouse.png)

### Edit Company
- Same fields as Add
- Buttons: **Save**, **Cancel**

![Edit Company](../docs/ui/feature-01/company-edit.png)

---

## Definition of Done

- [ ] Stories, FRs, Gherkin, API, and screens say the same thing
- [ ] Duplicate code shows "Duplicate company code"
- [ ] Empty list shows "No companies are available"
- [ ] Not allowed shows "You are not authorized to manage companies"
- [ ] Screen labels match the buttons and empty message above

---

## Out of Scope

- A retailer logging in
- Bringing a deleted company back
- Extra countries or extra languages
- Tests and coding this feature (that is later)

