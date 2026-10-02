# Feature: <Supplier>

**Feature ID:**        N03 
**Branch pattern:**   `Customer`  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**         Creating, viewing, editing, and maintaining customer information.
**Related:**      Customer Orders, Inventory, Warehouse
---

## User Stories

### US-N.3.1: View Customers
**As a**       Warehouse Manager
**I want to** View all customers
**So that**   Ican see the customers maintained by the company

**Priority:**               P1  
**Independent test:**    Select View Customers and verfy that the system displays all  existing customers and their information  
**Acceptance scenarios:**   US-3.1: under th acceptance criteria

### US-N.3.2: Add Customer
**As a**     Warehouse manager
**I want to** add a customer
**So that**   Customer information can be stored and when creating customer orders
**Priority:**              P1  

**Independent test:**   Enter Valid customer information and verify that the customer is saved and appears in the customers lists

**Acceptance scenarios:**  see ### US-N.3.2 under the acceptance criteria

### US-N.2.3:    Edit Customer
**As a**         Warehouse Manager 
**I want to**    edit customer information
**So that**      customer records reamin accurate 

**Priority:**             P1  
**Independent test:**  Change an existing cuatomer's phone number and verfy that the updated information is saves and displayed

---

### US-N.2.4: Archive Customer
**As a**        Warehouse Manager
**I want to**   Archive a customer
**So that** Customers who are no longer active are not treated as active customers

**Priority:**             P1  
**Independent test:**Archive an active customer ans veryfy that the customer's status changes to **Inactive**

### Functional Requirements

- **FR-001**: System Mast assign every customer a nique identifier 
- **FR-002**: System Must allow an authorized user to add a customer
- **FR-003**: System Must allow an authorized user to view cuatomer information
- **FR-004**: System Must allow an authorized user to edit customer information
 **FR-005**:  Systemm Must allow an authorized user to archive a customer.
 **FR-006**:  System Must prevent duplicate customer codes
 **FR-007**:  System Must prevent unauthorized usera from modifying customer information.

---



## Key Entities

- **Customer**:  Represents a customer who purchases items from the company
- **Customer Order**: Represents an order placed by a customer …

---

## Data Model Requirements

### `Sppliers` table
_______________________________________________________________
| Field              | Type         | Rules                   |
|-------             |------        |-------                  |
| `Customer_id`      | INTEGER PK   | Auto-increment, unique  |
| `customer_name`   |VARCHAR(100)   | Required, unique        |
| `customer_email`   |VARCHAR       | ptional                 |  
| `customer_phone`   |INTGER        | optional                |
| `address`          |VARCHAR(20)   |  optional               | 
| `status`           |VARCHAR(20)   |  Active, Inacive,       | 
| `created_at`       |DATETIME      |Required                 | 
_______________________________________________________________


---

## Acceptance Criteria

### US-N.3.1 — View Customers

#### Scenario: View Existing Customers
*   **Given**  Customer exist in the System
*   **When**   The Warehouse manager selects View customers 
*   **Then**   the system dispays all customers
*   **And**    displayas their current information

#### Scenario: No Customers
*   **Given** No customers exist
*   **When**  The warehouse  Manager selects view customers 
*   **Then**  The system rejects the supplier …
*   **And**   Thes system displays a message indicating that customers are available

### US-N.3.2 — Add Customer

#### Scenario: Add Customer
*   **Given**  The warehouse Manager is authorized …
*   **When**   valid customer information is entered
*   **Then**   Assigns the customer a unique identifier…

#### Scenario: Duplicate custmer code
*   **Given**  a customer with code CUS001 already exists …
*   **When**  another customer is added using CUS001 
*   **Then**  Displays a duplicate customer code message …

### US-N.3.3:  Edit Customer

#### Scenario: Edit Customer 
*   **Given**  a customer exists…
*   **When**   the Warehouse Manager edits the customer's information…
*   **Then**   the syatem saves the updated information   …
*   **And**    display the updted customer information

### US-N.3.4:  Edit Customer

#### Scenario: Archive Customer
*   **Given** An acive customer exists …
*   **When**  The warehouse Manager archives the customer…
*   **Then**  The customer's status changes to Inactive  …

#### Scenario: Unauthorized Update
*   **Given**  the user is not autnorized to amnage customers  …
*   **When**   the user attempts to add, edit, orchive a cusatomer  …
*   **Then**   the System does not allow the change …





