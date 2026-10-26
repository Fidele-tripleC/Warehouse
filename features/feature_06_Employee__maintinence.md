# Feature: Employee

**Feature ID:**        N06  
**Branch pattern:**    `feature/6-employee`  
**Status:**            Draft  
**Created:**           2026-09-21  
**Input:**             Creating, viewing, editing, and maintaining employee records  
**Depends on:**        [Company](feature_01_Company_maintinence.md)  
**Related:**           [Authentication](feature_20_authentication.md), [Warehouse](feature_02_Warehouse__maintinence.md), [Customer Order](feature_09_Customer_Order_Management.md), [Supplier Order](feature_08_Supplier_order_Management.md)

---

## User Stories

### US-N06.1: View Employees
**As a**        Employee Manager  
**I want to**   View all employees  
**So that**     I can see employee information maintained by the company  
**Priority:**               P1  
**Independent test:** Select View Employees and verify that the System displays all employees and their information  
**Acceptance scenarios:**   See AC-N06.1

### US-N06.2: Add Employee
**As a**       Employee Manager  
**I want to**  add an employee  
**So that**    employee information can be maintained by the company  
**Priority:**               P1  
**Independent test:** Enter valid employee information and save it. Verify that the new employee appears in the employee list  
**Acceptance scenarios:**   See AC-N06.2

### US-N06.3: Edit Employee
**As a**       Employee information  
**I want to**  edit employee information  
**So that**    employee records remain accurate  
**Priority:**               P1  
**Independent test:**  Modify employee information and verify that the update information is displayed  
**Acceptance scenarios:**   See AC-N06.3

### US-N06.4: delete Employee
**As a**       Employee Manager  
**I want to**  delete an employee  
**So that**    the employee who no longer works for the company get deleted  
**Priority:**               P1  
**Independent test:** create an employee and delete him, see if he disappears from the list  
**Acceptance scenarios:**   See AC-N06.4

---

## Functional Requirements

- **FR-001**: System Must assign every employee a unique identifier
- **FR-002**: System Must allow an authorized Employee Manager to view employee information.
- **FR-003**: System Must allow an authorized Employee Manager to add an employee
- **FR-004**: System Must allow an authorized employee Manager to edit employee information
- **FR-005**: System Must allow an authorized Employee Manager to delete an employee
- **FR-006**: System associate each employee with a company
- **FR-007**: System Must prevent unauthorized users from modifying employee information

---

## Key Entities

- **Employee**:     Represent a person employed by the company
- **Company**:      Represents the company employing the employee

**Relationships**
- one **Company** can have multiple **Employees**

---

## Data Model Requirements

### `Employee` table

 `first_name`   : this is the name of the employee  
 `last_name`    : this is the last name  
 `email`        : this is working personal email  
 `phone_number` : this is the personal phone number  
 `position`     : this is the position one have in the company

---

## Acceptance Criteria

### AC-N06.1 â€” View Employees

#### Scenario: View Existing Employees
*   **Given** Employee exist in the system
*   **When**  the Employee Manager selects view Employees
*   **Then**  The system displays employees
*   **And**   displays their current information.

#### Scenario: No employees
*   **Given**  No employees exist in the system
*   **When**   The employee Manager selects View employees
*   **Then**   the employee list is empty
*   **And**    The system displays "No employees are available"

### AC-N06.2 â€” Add Employee

#### Scenario: Add Employee
*   **Given** The employee Manager is authorized
*   **When**  the manager enters valid employee information
*   **Then**  the system saves the employee
*   **And**   associates the employee with the company
*   **And**   the new employee appears in the employee list

### AC-N06.3 â€” edit Employee

#### Scenario: Edit Employee
*   **Given** the Manager wants to edit an employee
*   **When**  the updates are entered
*   **Then**  the information for the employee changes
*   **And**   the system displays the updated employee information

### AC-N06.4 â€” delete an employee

#### Scenario: delete an employee
*   **Given**  an employee no longer works for the company
*   **When**   the manager deletes him
*   **Then**   then he disappears from the list of the employees
*   **And**    the system displays "Employee deleted"

#### Scenario: Unauthorized update
*   **Given** the user is not authorized to modify employee information
*   **When**  the user attempts to add, edit, or delete an employee
*   **Then**  the employee is not changed
*   **And**   the system displays "You are not authorized to manage employees"
