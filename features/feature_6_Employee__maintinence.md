# Feature: <Employee>

**Feature ID:**        N06 
**Branch pattern:**   `Employee`  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**       Creating, viewing, editing, and maintaining employee records
**Depends on:**       Company
**Related:**           Warehouse, Customer orders, supplier Orders
---

## User Stories

### US-N.6.1:  View Employees
**As a**        Employee Manager
**I want to**   View all employees
**So that**     Ican see employee information maintained by the company 
**Priority:**               P1  
**Independent test:** Select View Employees and verify that the System displays all employees and their information
**Acceptance scenarios:**   US-6.1: under th acceptance criteria

### US-N.6.2: Add Employee 
**As a**       Employee Manager 
**I want to**  add an employee
**So that**    employee information can be maintained by the company
**Priority:**               P1  
**Independent test:** Enter valid employee information and save it. Verfy that the new employee appears in the employee list
**Acceptance scenarios:**   US-6.2: under th acceptance criteria


### US-N.6.3:  Edit Employee
**As a**       Employee information
**I want to**  edit employee information
**So that**    employee records reamin accurate

**Priority:**               P1  
**Independent test:**  Modify employee information and verify that the update information is displayed
**Acceptance scenarios:**   US-6.3: under th acceptance criteria

### US-N.6.4:  delete Employee 
**As a**       Employee Manager 
**I want to**  delete an employee
**So that**    the eemployee who nolonger works for the company get deleted

**Priority:**               P1  
**Independent test:** create an employee and delete him, see if he desappears from the list
**Acceptance scenarios:**   US-6.4: under th acceptance criteria



### Functional Requirements

- **FR-001**: System Must assign every employee a unique identifier
- **FR-002**: System Must allow an outhorized Employee Manager to view employee information.
- **FR-003**: System Must allow an authorized Employee Manager to add an employee
- **FR-004**: System Must allow an authorized employee Manager to edit employee information
- **FR-005**:  System Must allow an authorized Employee Manager to delete an employee
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

 Field             
-------                 
 `first_name`  : this is the nam of the employee   
 `last_name`   : this is the last name     
`email`        : this is working personal email   
 `phone_number`: this is the personal phone number   
 `position`    : this is tge position one have in the company     
     
---

## Acceptance Criteria

### US-N.6.1 — View Employees

#### Scenario: View Existimg Employees
*   **Given** Employee exist in the system
*   **When**  the Employee Manager selects view Employees
*   **Then**  The system displays employees
*   **And**   displays their currebt information.

#### Scenario:  No employees 
*   **Given**  No employees exist in the system
*   **When**   The employee Manager slects View mployees 
*   **Then**   The system displays a message indicating that no employees are available.


### US-N.6.2 — Add Employee 

#### Scenario: Add Employee
*   **Given** The employee Mnager is authorized 
*   **When**  the manager enters valid employee information
*   **Then**  the system saves the employee
*   **And**   associate the employee with the company

### US-N.6.3 — edit Employee 

#### Scenario: 
*   **Given** the Manager wants to edit an employee
*   **When**  the update are entered
*   **Then**  the information for the employee changes


### US-N.6.4 — delete an employee

#### Scenario: delete an employee
*   **Given**  an employee no longer works for the company
*   **When**   When the manager deletes him
*   **Then**   then he disappears from the list of the employees








