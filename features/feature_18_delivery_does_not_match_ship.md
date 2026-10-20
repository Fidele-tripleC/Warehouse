# Feature: <Delivery Does Not Match Ship>

**Feature ID:**        N18  
**Branch pattern:**   `delivery-does-not-match-ship `  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Showing deliveries that do not match what was shipped.
**Depends on:**        [Ship Customer Order](feature_14_ship_customer_order.md), [Deliver Customer Order](feature_15_deliver_customer_order.md), [Route](feature_10_route_maintenence.md), [Customer Order](feature_09_Customer_Order_Management.md)
**Related:**           [Customer](feature_07_Customer__maintinence.md), [Warehouse](feature_02_Warehouse__maintinence.md)
---

## User Stories

### US-N.18.1: View deliveries that do not match what we ship
**As a**        Warehouse Manager
**I want to**   View deliveries that do not match what we shipped
**So that**     I can see when a customer did not receive the shipped items.
**Priority:**               P1  
**Independent test:**    Ship an order then mark the route stop Failed. Select View Delivery Does Not Match. The order is displayed.
**Acceptance scenarios:**   US-18.1: under the acceptance criteria

### US-N.18.2: View the ship and delivery difference
**As a**       Warehouse Manager
**I want to**  View the shipped quantity and the delivered result
**So that**    I know what did not match.

**Priority:**               P1  
**Independent test:**   Open a mismatch record and verify the shipped quantity and the delivery status.
**Acceptance scenarios:**   US-18.2: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must compare each ship to the delivery result on the route.
- **FR-002**: System Must display a mismatch when a shipped order stop is Failed.
- **FR-003**: System Must display a mismatch when delivered quantity is not the same as shipped quantity.
- **FR-004**: System Must display the customer order, shipped quantity, and delivery result.
- **FR-005**: System Must display a message when every delivery matches what was shipped.

---

## Key Entities

- **Delivery Mismatch**: a record that delivery did not match the ship.
- **Ship**: what left the warehouse.
- **Route Stop**: the delivery result for the customer order.
- **Customer Order**: the order that was shipped and delivered.

- **relationships**
- one **Ship** can have one **Delivery Mismatch**
- one **Customer Order** can have one **Delivery Mismatch**

---

## Data Model Requirements

### `Delivery Mismatch` table

 Field             
-------            
 `mismatch_id`          : this is the unique id
 `customer_order_code`  : this is the customer order
 `ship_code`            : this is the ship record
 `shipped_quantity`     : this is the quantity that was shipped
 `delivery_status`      : this is Delivered or Failed
 `created_at`           : this is the time it was recorded

---

## Acceptance Criteria

### US-N.18.1 â€” View deliveries that do not match what we ship

#### Scenario: Delivery failed after ship
*   **Given** a customer order is shipped
*   **And**   the route stop is marked Failed
*   **When**  the warehouse Manager selects View Delivery Does Not Match
*   **Then**  the system displays the customer order
*   **And**   displays that the delivery does not match the ship

#### Scenario: All deliveries match
*   **Given** every shipped order stop is Delivered
*   **When**  the warehouse Manager selects View Delivery Does Not Match
*   **Then**  the mismatch list is empty
*   **And**   the system displays "No mismatches are available"

### US-N.18.2 â€” View the ship and delivery difference

#### Scenario: View mismatch details
*   **Given** a delivery does not match a ship
*   **When**  the warehouse Manager views that record
*   **Then**  the system displays the shipped quantity
*   **And**   displays the delivery status
