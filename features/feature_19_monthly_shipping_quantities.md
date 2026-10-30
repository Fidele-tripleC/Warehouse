# Feature: Monthly Shipping Quantities

**Feature ID:**        N19  
**Branch pattern:**    `feature/19-monthly-shipping-quantities`  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Showing how many quantities of items have been shipping each month.
**Depends on:**        [Ship Customer Order](feature_14_ship_customer_order.md), [Items](feature_04_Items__maintinence.md)
**Related:**           [Customer Order](feature_09_Customer_Order_Management.md), [Inventory](feature_05_Inventory__maintinence.md)
---

## User Stories

### US-N.19.1: View quantities shipped each month
**As a**        Warehouse Manager
**I want to**   View how many quantities of items have been shipping each month
**So that**     I can see what left the warehouse in that month.
**Priority:**               P1  
**Independent test:**    Ship 10 units of an item in a month. Select View Monthly Shipping. The item shows quantity 10 for that month.
**Acceptance scenarios:**   US-19.1: under the acceptance criteria

### US-N.19.2: View monthly shipping for one item
**As a**       Warehouse Manager
**I want to**  View one item and the quantity shipped in a month
**So that**    I can see that item's shipping quantity.

**Priority:**               P1  
**Independent test:**   Select an item and a month and verify the shipped quantity.
**Acceptance scenarios:**   US-19.2: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must allow the warehouse Manager to view shipped quantities by month.
- **FR-002**: System Must group ship records by item and by month.
- **FR-003**: System Must display the item and the total quantity shipped in that month.
- **FR-004**: System Must allow the warehouse Manager to select a month.
- **FR-005**: System Must display a message when no items were shipped in that month.

---

## Key Entities

- **Monthly Shipping Total**: the total quantity of an item shipped in one month.
- **Ship**: the ship records used to calculate the total.
- **Item**: the product that was shipped.

- **relationships**
- one **Item** can have one **Monthly Shipping Total** for each month
- many **Ships** add up to one **Monthly Shipping Total**

---

## Data Model Requirements

### `Monthly Shipping` table

 Field             
-------            
 `monthly_shipping_id`  : this is the unique id
 `item_id`              : this is the item
 `month`                : this is the month
 `year`                 : this is the year
 `quantity_shipped`     : this is the total quantity shipped in that month

---

## Acceptance Criteria

### US-N.19.1 â€” View quantities shipped each month

#### Scenario: View monthly totals
*   **Given** 10 units of an item were shipped in a month
*   **When**  the warehouse Manager selects View Monthly Shipping for that month
*   **Then**  the system displays the item
*   **And**   displays quantity 10

#### Scenario: No ships in the month
*   **Given** no ship records exist for the selected month
*   **When**  the warehouse Manager selects View Monthly Shipping
*   **Then**  the monthly shipping list is empty
*   **And**   the system displays "No items were shipped in that month"

### US-N.19.2 â€” View monthly shipping for one item

#### Scenario: View one item
*   **Given** an item was shipped more than once in a month
*   **When**  the warehouse Manager views that item for the month
*   **Then**  the system displays the total quantity shipped
