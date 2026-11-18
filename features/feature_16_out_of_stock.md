# Feature: Out of Stock

**Feature ID:**        N16  
**Branch pattern:**    `feature/16-out-of-stock`  
**Status:**            Draft  
**Created:**           2026-19-10  
**Input:**             Showing which items have been out of stock.
**Build order:**        17 of 20  
**Depends on:**        [Inventory](feature_05_Inventory__maintinence.md)  
**Related:**           [Supplier Did Not Ship](feature_17_supplier_did_not_ship.md) (next)
---

## User Stories

### US-N.16.1: View items that are out of stock
**As a**        Warehouse Manager
**I want to**   View items that are out of stock
**So that**     I know what we cannot pick or ship right now.
**Priority:**               P1  
**Independent test:**    Set an item quantity to 0 and select View Out of Stock. The item is displayed.
**Acceptance scenarios:**   US-16.1: under the acceptance criteria

### US-N.16.2: View items that have been out of stock
**As a**       Warehouse Manager
**I want to**  View items that have been out of stock
**So that**    I can see which items had no quantity.

**Priority:**               P1  
**Independent test:**   An item goes to quantity 0 then is put away later. View Out of Stock history still shows that item was out of stock.
**Acceptance scenarios:**   US-16.2: under the acceptance criteria

---

## Functional Requirements

- **FR-001**: System Must allow the warehouse Manager to view items with quantity 0.
- **FR-002**: System Must display the item and the warehouse for each out of stock item.
- **FR-003**: System Must record when an item becomes out of stock.
- **FR-004**: System Must allow the warehouse Manager to view items that have been out of stock.
- **FR-005**: System Must display a message when no items are out of stock.

---

## Key Entities

- **Out of Stock Record**: a record that an item had quantity 0.
- **Item**: the product that is out of stock.
- **Inventory**: the quantity in the warehouse. Quantity 0 means out of stock.

- **relationships**
- one **Item** can have multiple **Out of Stock Records**
- one **Warehouse** can have multiple **Out of Stock Records**

---

## Data Model Requirements

### `Out of Stock` table

 Field             
-------            
 `out_of_stock_id`  : this is the unique id
 `item_id`          : this is the item that is out of stock
 `warehouse_code`   : this is the warehouse
 `quantity`         : this is the quantity, it is 0
 `started_at`       : this is the time the item became out of stock
 `ended_at`         : this is the time the item had quantity again

---

## Acceptance Criteria

### US-N.16.1 â€” View items that are out of stock

#### Scenario: View current out of stock items
*   **Given** an item has quantity 0 in a warehouse
*   **When**  the warehouse Manager selects View Out of Stock
*   **Then**  the system displays the item
*   **And**   displays the warehouse

#### Scenario: No items out of stock
*   **Given** no item has quantity 0
*   **When**  the warehouse Manager selects View Out of Stock
*   **Then**  the out of stock list is empty
*   **And**   the system displays "No items are out of stock"

### US-N.16.2 â€” View items that have been out of stock

#### Scenario: View out of stock history
*   **Given** an item was at quantity 0 and later the quantity increased
*   **When**  the warehouse Manager selects View Out of Stock history
*   **Then**  the system displays that the item has been out of stock
*   **And**   displays the time it started and ended

#### Scenario: Unauthorized view
*   **Given** the user is not authorized to view out of stock
*   **When**  the user selects View Out of Stock
*   **Then**  the out of stock list is not shown
*   **And**   the system displays "You are not authorized to manage out of stock"

---

## Assumptions

- The user is logged in as Warehouse Manager.
- Out of stock means quantity 0 in a warehouse.
- History is for items that were at 0 and later went up.

---

## Edge Cases

- No item is at quantity 0
- User is not authorized

---

## Success Criteria

- **SC-001**: Warehouse Manager can view current out of stock items and history.
- **SC-002**: Empty current list shows "No items are out of stock".
- **SC-003**: Unauthorized user sees "You are not authorized to manage out of stock".

---

## Data Ownership & Isolation

Out of stock views belong to the warehouse. Retailers cannot open this list.

| Rule | Requirement |
|------|-------------|
| **Read scope** | Warehouse Manager can view out of stock and history |
| **Write scope** | This feature is view only |
| **Create scope** | Rows come from inventory quantity 0 |
| **Cross-user access** | Forbidden → "You are not authorized to manage out of stock" |
| **UI scope** | Out of Stock menu after login |
| **Implementation** | Auth on `/api/out-of-stock` |

---

## API Requirements

Base path: `/api`. Errors: `{ "message": "..." }`. Auth: `Authorization: Bearer <token>`.

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `GET` | `/api/out-of-stock` | Yes | Current items at quantity 0 |
| `GET` | `/api/out-of-stock/history` | Yes | Items that were out of stock |

**Empty current list:** `{ "message": "No items are out of stock" }`  
**Unauthorized:** `401` `{ "message": "You are not authorized to manage out of stock" }`

---

## Screen Requirements

Menu after login: **Out of Stock**.

### Current out of stock
- Heading: Out of Stock
- List: item, warehouse
- Empty: "No items are out of stock"
- Button: **View History**

### Out of stock history
- List: item, start time, end time

---

## Definition of Done

- [ ] Current list and history match the Gherkin
- [ ] This screen is view only

---

## Out of Scope

- Auto-ordering a supplier when stock is 0
- Coding the app (that is later)

