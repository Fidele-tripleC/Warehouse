# Feature: <Supplier Order Form>

**Feature ID:**        N06 
**Branch pattern:**   `Employee`  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**       Creating, viewing, editing, and maintaining employee records
**Depends on:**       Company
**Related:**           Warehouse, Customer orders, supplier Orders
---

## User Stories

### US-N.4.1:  View Employees
**As a**        Employee Manager
**I want to**   View all employees
**So that**     Ican see employee information maintained by the company 
**Priority:**               P1  
**Independent test:** Select View Employees and verify that the System displays all employees and their information
**Acceptance scenarios:**   US-6.1: under th acceptance criteria

### US-N.4.2: Add Employee 
**As a**       Employee Manager 
**I want to**  add an employee
**So that**    employee information can be maintained by the company
**Priority:**               P1  
**Independent test:** Enter valid employee information and save it. Verfy that the new employee appears in the employee list
**Acceptance scenarios:**   US-6.2: under th acceptance criteria


### US-N.4.3:  Edit Employee
**As a**       Employee information
**I want to**  edit employee information
**So that**    employee records reamin accurate

**Priority:**               P1  
**Independent test:**  Modify employee information and verify that the update information is displayed
**Acceptance scenarios:**   US-6.3: under th acceptance criteria

### US-N.4.4:  Archive Employee 
**As a**       Employee Manager 
**I want to**  ARCHIVE AN EMPLOYEE
**So that**    Former employees are no longer treated as active employees

**Priority:**               P1  
**Independent test:** Archive an employee and verify that the employee status changes to inactive
**Acceptance scenarios:**   US-6.4: under th acceptance criteria



### Functional Requirements

- **FR-001**: System Must assign every employee a unique identifier
- **FR-002**: System Must allow an outhorized Employee Manager to view employee information.
- **FR-003**: System Must allow an authorized Employee Manager to add an employee
- **FR-004**: System Must allow an authorized employee Manager to edit employee information
- **FR-005**:  System Must allow an authorized Employee Manager to archive an employee
- **FR-006**: System associate each employee with a company
- **FR-007**: System Must prevent unauthorized users from modifying employee information
## Key Entities

- **Employee**:     Represent a person employed by the company
- **Company**:      Represents the company employing the employee

**Relationships**
- one **Company** can have multiple **Employees**



---

## Data Model Requirements

### `Supplier Order` table
---------------------------------------------------------------
| Field              | Type         | Rules                   |
|-------             |------        |-------                  |
| `employee_id`      | INTEGER PK   |Auto-increment, unique   |
| `first_name`       | VARCHAR(50)  |Required                 |
| `last_name`        | VARCHAR(50)  |Required                 |
| `email`            |VARCHAR(100)  |rEQUIRED, unique         |
| `phone_number`     |VARCHAR(20)   |required                 |
| `position`         | VARCHAR(50)  |required                 |
| `company_id`       |INTEGER FK    |required                 |
| `status`           |Varchar(20)   |Active, Inactive         | 
| `created_at`       |DATETIME      |Required                 | 
---------------------------------------------------------------


### Associations (if known)
- …

---

## Acceptance Criteria

### US-N.6.1 — View Employees

#### Scenario: View Existimg Employees
*   **Given** Employee exist in the system
*   **When**  the Employee Mnager selects view Employees
*   **Then**  The system displays employees
*   **And**   displays their currebt information.

#### Scenario:  No employees 
*   **Given** No employees exist in the system
*   **When**  The employee Manager slects View mployees 
*   **Then**  The system displays a message indicating that no employees are available.


### US-N.6.2 — Add Employee 

#### Scenario: Add Employee
*   **Given** The employee Mnager is authorized 
*   **When**  the manager enters valid employee information
*   **Then**  the system saves the employee
*   **And**   associate the employee with the company

///keep working from here


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






