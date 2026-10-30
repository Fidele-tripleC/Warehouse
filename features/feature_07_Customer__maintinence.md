# Feature: Customer

**Feature ID:**        N07  
**Branch pattern:**    `feature/7-customer`  
**Status:**            Draft  
**Created:**           2026-09-21  
**Input:**             Create, view, edit, and maintain retailer (store) information. The company's customers are retailers. Retailers do not log in.  
**Depends on:**        [Company](feature_01_Company_maintinence.md)  
**Related:**           [Customer Order](feature_09_Customer_Order_Management.md), [Inventory](feature_05_Inventory__maintinence.md), [Warehouse](feature_02_Warehouse__maintinence.md), [Ship Customer Order](feature_14_ship_customer_order.md), [Route](feature_10_route_maintenence.md)

---

## User Stories

### US-N07.1: View customers
**As a**       Warehouse Manager  
**I want to**  view all customers  
**So that**    I can see the retailer stores that send orders to the warehouse  
**Priority:**             P1  
**Independent test:**     Select "View Customers"; the system displays all existing customers and their information.  
**Acceptance scenarios:** See AC-N07.1

### US-N07.2: Add customer
**As a**       Warehouse Manager  
**I want to**  add a customer  
**So that**    the warehouse can record orders that the retailer sends  
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
**So that**    retailer stores that no longer order are not treated as active  
**Priority:**             P1  
**Independent test:**     Archive an active customer; the customer's status changes to Inactive.  
**Acceptance scenarios:** See AC-N07.4

---

## Functional Requirements

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
- A retailer logging into the warehouse system.

---

## Key Entities

- **Customer**: a retailer store that buys from this warehouse. Can have many Customer Orders. The retailer does not log in.
- **Customer Order**: an order the retailer sent, then the warehouse recorded. Belongs to one Customer.
- **Warehouse Manager**: the authorized user who manages retailer records.

---

## Data Model Requirements

### `customer` table

 `customer_code`   : this is the unique code for the retailer store  
 `customer_name`   : this is the name of the retailer store  
 `customer_email`  : this is the working email of the store  
 `customer_phone`  : this is the working phone of the store  
 `address`         : this is the store location  
 `status`          : this is Active or Inactive

---

## Acceptance Criteria

### AC-N07.1 â€” View Customers

#### Scenario: View existing customers
* **Given** customers exist in the system
* **When**  the Warehouse Manager selects "View Customers"
* **Then**  the system displays all Active customers
* **And**   each customer shows its current information

#### Scenario: No customers
* **Given** no customers exist
* **When**  the Warehouse Manager selects "View Customers"
* **Then**  the customer list is empty
* **And**   the system displays "No customers are available"

### AC-N07.2 â€” Add Customer

#### Scenario: Add customer
* **Given** the Warehouse Manager is authorized
* **When**  valid customer information is entered
* **Then**  the system assigns the customer a unique identifier
* **And**   saves the customer with status Active
* **And**   the customer appears in the customer list

#### Scenario: Duplicate customer code
* **Given** a customer with code `CUS001` already exists
* **When**  another customer is added using `CUS001`
* **Then**  the new customer is not saved
* **And**   the system displays "Duplicate customer code"

#### Scenario: Invalid customer data
* **Given** the Warehouse Manager is authorized
* **When**  they submit a customer with an empty name or malformed email
* **Then**  the customer is not saved
* **And**   the system displays "Invalid customer data"

### AC-N07.3 â€” Edit Customer

#### Scenario: Edit customer
* **Given** a customer exists
* **When**  the Warehouse Manager edits the customer's information
* **Then**  the system saves the updated information
* **And**   displays the updated customer information

### AC-N07.4 â€” Archive Customer

#### Scenario: Archive customer
* **Given** an Active customer exists
* **When**  the Warehouse Manager archives the customer
* **Then**  the customer's status changes to Inactive
* **And**   the customer no longer appears in the default (Active) list
* **And**   the system displays "Customer archived"

#### Scenario: Unauthorized change
* **Given** the user is not authorized to manage customers
* **When**  they attempt to add, edit, or archive a customer
* **Then**  the customer is not changed
* **And**   the system displays "You are not authorized to manage customers"
