# Feature: Customer

**Feature ID:**        N07
**Branch pattern:**    `customer/<short-description>`
**Status:**            Draft
**Created:**           2026-09-21
**Input:**             Create, view, edit, and maintain customer information.
**Depends on:**        [Authentication & Roles](features/feature_1_auth.md) 
**Related:**           Customer Orders, Inventory, Warehouse

---

## User Stories

### US-N07.1: View customers
**As a**       Warehouse Manager
**I want to**  view all customers
**So that**    I can see the customers maintained by the company

**Priority:**             P1
**Independent test:**     Select "View Customers"; the system displays all existing customers and their information.
**Acceptance scenarios:** See AC-N07.1

### US-N07.2: Add customer
**As a**       Warehouse Manager
**I want to**  add a customer
**So that**    customer information is stored and can be used when creating customer orders

**Priority:**             P1
**Independent test:**     Enter valid customer information; the customer is saved and appears in the customer list.
**Acceptance scenarios:** See AC-N07.2

### US-N07.3: Edit customer
**As a**       Warehouse Manager
**I want to**  edit customer information
**So that**    customer records remain accurate

**Priority:**             P1
**Independent test:**     Change an existing customer's phone number; the updated number is saved and displayed.
**Acceptance scenarios:** See AC-N07.3

### US-N07.4: Archive customer
**As a**       Warehouse Manager
**I want to**  archive a customer
**So that**    customers who are no longer active are not treated as active

**Priority:**             P1
**Independent test:**     Archive an active customer; the customer's status changes to Inactive.
**Acceptance scenarios:** See AC-N07.4

---

## Requirements

### Functional Requirements

- **FR-001**: The system MUST assign every customer a unique identifier.
- **FR-002**: The system MUST allow an authorized user to add a customer.
- **FR-003**: The system MUST allow an authorized user to view customer information.
- **FR-004**: The system MUST allow an authorized user to edit customer information.
- **FR-005**: The system MUST allow an authorized user to archive a customer.
- **FR-006**: The system MUST prevent duplicate customer codes.
- **FR-007**: The system MUST prevent unauthorized users from modifying customer information.
- **FR-008**: The system MUST reject invalid input (empty name, malformed email).
- **FR-009**: The customer list MUST show Active customers by default; Inactive customers MUST be viewable via a filter.

### Out of Scope
- Reactivating an archived customer.
- Permanently deleting a customer.

---

## Key Entities

- **Customer**: a person or company that purchases items from the company. Can have many Customer Orders.
- **Customer Order**: an order placed by a customer. Belongs to one Customer.
- **Warehouse Manager**: the authorized user who manages customers.

---

## Data Model Requirements

### `customer` table

 `customer_code`   : this is the unique code for the customer
 `customer_name`   : this is the identification code for the customer
 `customer_email`  : this is the workin
 `customer_phone`  : this is the working email of the customer
 `address`         : this is the phone number of the customer  
 `status`        
    
---

## Acceptance Criteria

### AC-N07.1 — View Customers

#### Scenario: View existing customers
* **Given** customers exist in the system
* **When**  the Warehouse Manager selects "View Customers"
* **Then**  the system displays all Active customers
* **And**   each customer shows its current information

#### Scenario: No customers
* **Given** no customers exist
* **When**  the Warehouse Manager selects "View Customers"
* **Then**  the system displays a message that no customers are available

### AC-N07.2 — Add Customer

#### Scenario: Add customer
* **Given** the Warehouse Manager is authorized
* **When**  valid customer information is entered
* **Then**  the system assigns the customer a unique identifier
* **And**   saves the customer with status Active
* **And**   the customer appears in the customer list

#### Scenario: Duplicate customer code
* **Given** a customer with code `CUS001` already exists
* **When**  another customer is added using `CUS001`
* **Then**  the system rejects it and displays a duplicate customer code message

#### Scenario: Invalid customer data
* **Given** the Warehouse Manager is authorized
* **When**  they submit a customer with an empty name or malformed email
* **Then**  the system rejects it and displays a validation error

### AC-N07.3 — Edit Customer

#### Scenario: Edit customer
* **Given** a customer exists
* **When**  the Warehouse Manager edits the customer's information
* **Then**  the system saves the updated information
* **And**   displays the updated customer information

### AC-N07.4 — Archive Customer

#### Scenario: Archive customer
* **Given** an Active customer exists
* **When**  the Warehouse Manager archives the customer
* **Then**  the customer's status changes to Inactive
* **And**   the customer no longer appears in the default (Active) list

#### Scenario: Unauthorized change
* **Given** the user is not authorized to manage customers
* **When**  they attempt to add, edit, or archive a customer
* **Then**  the system rejects the change