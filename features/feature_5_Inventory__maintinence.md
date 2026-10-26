# Feature: <Inventory>

**Feature ID:**        N05  
**Branch pattern:**   `inventory/ `  
**Status:**            Draft  
**Created:**           2026-21-09  
**Input:**             Tracking, inspecting, and maintaining the inventory.
**Depends on:**        [Feature X — …](features\feature_5_Inventory.md)  
**Related:**           optional links to ADRs or reference docs  

---

## User Stories

### US-N.5.1: View Live Stock level
**As a**       a Warehouse Manager 
**I want to**  View the current quantity of each Item in the stock
**So that**    I know what items are available in the stock

**Priority:**               P1  
**Independent test:**       select view the items, the system must display each item and the current quantity in the stock
**Acceptance scenarios:**   US-1.1: under th acceptance criteria ##5.1

### US-N.5.2: Add an imventory    
**As a**       As a warehouse Manager 
**I want to**  To add an inventory 
**So that**    Ican have the inventory information

**Priority:**              P1  
**Independent test:**      if inventory is added it will appear on the list of the inventories
**Acceptance scenarios:**  see ### US-N.1.2 under the acceptance criteria

### US-N.5.3: Update an inventory    
**As a**       As a warehouse Manager 
**I want to**  To update the inventory information 
**So that**    i can have the updted information of the inventory
**Priority:**              P1  
**Independent test:**      if an inventory name is eddited the new name appears on the list of the informations
**Acceptance scenarios:**  see ### US-N.1.2 under the acceptance criteria

### US-N.5.4:   update the inventory  
**As a**       As a warehouse Manager 
**I want to**  To update the inventory information 
**So that**    i can have the updted information of the inventory
**Priority:**              P1  
**Independent test:**      if an inventory name is eddited the new name appears on the list of the informations
**Acceptance scenarios:**  see ### US-N.1.2 under the acceptance criteria

### US-N.5.5:Automated warning
**As a**        Application
**I want to**   Display the warning message 
**When**        The item is bellow the minimum.
**So that**     They can order the items needed to be to the maximum level.

**Priority:**             P1  
**Independent test:**     when the item is below the minimum , the system gives the warning messsage.       
**Acceptance scenarios:** see ### US-N.1.3 under the acceptance criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System shall display the currents Stock quantity of each item in a warehouse.
- **FR-002**: System  MUST allow the authorised inventory manager to adda an inventory
- **FR-002**: System  MUST allow the authorised inventory manager to eddit the inventory information
- **FR-002**: System  MUST allow the authorised inventory manager to delete 
- **FR-003**: the system Must give the warning to the inventory manager when given type of the item goes below the minimum quantity… 

---
## Key Entities

- **Inventory**: a named stock collection (e.g., a warehouse). Contains many Items.
- **Item**: a stocked product with a quantity and min/max thresholds. Belongs to one Inventory.
- **Warehouse Manager**: the authorized user who manages Items.

---

## Data Model Requirements

### `Inventory` table
 Field                        
 `inventory_id`     : this is the  unique id for the inventory       
 `inventory_name`   : this is the name of th inventory        
 `Description`      : this is the short description for the inventory    


## Acceptance Criteria

### US-N.5.1 — View Live Stock Level

#### Scenario: View Current Stock
*   **Given** the warehuse manager is using the warehouse System 
*   **When**  the warehouse manager selects View Items
*   **Then**  the system displys all items in the inventory
*   **And**   the displys the inventory with the 

#### Scenario: No Items in the stock
*   **Given** There is no items in the inventory …
*   **When**  The warehouse manager selects View Items …
*   **Then**  The system displays a nessage indicating that no items are available…

### US-N.2 — Update the Stock

#### Scenario: Add an Item
*   **Given** Given the ware house manager is authorized…
*   **When**  The manager adds a new item and its quantity…
*   **Then**  The System Saves the item    …
*   **And**   The updated item appears in the inventory …

#### Scenario: Edit an Item
*   **Given** An item already exist in the inventory …
*   **When**  The warehouse manager edits the item or uits quantity…
*   **Then**  The System saves and displays the uupdated information  …

#### Scenario: Delete an Item
*   **Given** An item already exist in the inventory …
*   **When**  The warehouse manager delete the item …
*   **Then**  The item is removed from the inventory …

#### Scenario: Unathorized update
*   **Given** The user is not authorized to update inventory  …
*   **When**  The user tries to add ,edit, or delete an item …
*   **Then**  The system does not allow the change …

### US-N.2 — Automated Warning

#### Scenario: Item is below minimum quantity
*   **Given**  An item has a defined minimum quantity…
*   **When**  The Item's current quantity goes below the minimum quantity…
*   **Then**  The System displays a warning to the warehouse Manager  …
*   **And**   The warning identifies the item that needs to be restocked …

#### Scenario: Item is not below minimum quantity
*   **Given** An item a defined minimum quantity …
*   **When**  The item's current qauntity is eqaual to or above the    minimum quantity…
*   **Then**  The System does not display a low-stock warning  …


