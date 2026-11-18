# Feature: Route

**Feature ID:**        N10 
**Branch pattern:**    `route/<short-description>`
**Status:**            Draft
**Created:**           2026-10-02
**Input:**             Plan, view, edit, start, track, and cancel delivery routes that carry fulfilled customer orders to customers.
**Depends on:**        [Customer Order](features/feature_6_customer_order.md), [Customer](features/feature_7_customer.md)   
**Related:**           Warehouse, Inventory

---

## User Stories

### US-N10.1: Create route
**As a**       Warehouse Manager
**I want to**  create a delivery route with a planned date and a list of orders to deliver
**So that**    fulfilled orders are organized into a delivery trip

**Priority:**             P1
**Independent test:**     Create a route for a future date with two Fulfilled orders; the route is saved as Planned with two stops in sequence.
**Acceptance scenarios:** See AC-N10.1

### US-N10.2: View routes
**As a**       Warehouse Manager
**I want to**  view all routes and their stops
**So that**    I can see what is planned, in progress, and completed

**Priority:**             P1
**Independent test:**     Create a route; it appears in the route list with its date, status, and stops.
**Acceptance scenarios:** See AC-N10.2

### US-N010.3: Edit route
**As a**       Warehouse Manager
**I want to**  edit a planned route (date, stops, and stop order)
**So that**    the plan can be corrected before the trip starts

**Priority:**             P1
**Independent test:**     Move the second stop to first position on a Planned route; the new order is saved and displayed.
**Acceptance scenarios:** See AC-N08.3

### US-N10.4: Start route
**As a**       Warehouse Manager
**I want to**  start a planned route
**So that**    the route is tracked as an active delivery trip

**Priority:**             P1
**Independent test:**     Start a Planned route that has at least one stop; its status changes to In Progress.
**Acceptance scenarios:** See AC-N10.4

### US-N10.5: Record stop result
**As a**       Warehouse Manager
**I want to**  mark each stop as delivered or failed
**So that**    I know which customers have received their orders

**Priority:**             P1
**Independent test:**     Mark the only remaining Pending stop as Delivered; the stop is Delivered and the route becomes Completed.
**Acceptance scenarios:** See AC-N08.5

### US-N10.6: Cancel route
**As a**       Warehouse Manager
**I want to**  cancel a route that will not run
**So that**    its orders can be placed on another route

**Priority:**             P2
**Independent test:**     Cancel a Planned route; its status changes to Cancelled and its orders can be added to a new route.
**Acceptance scenarios:** See AC-N10.6

---

## Requirements

### Functional Requirements

- **FR-001**: The system MUST assign every route a unique identifier.
- **FR-002**: The system MUST allow an authorized user to create a route with a planned date and one or more stops.
- **FR-003**: The system MUST only allow Fulfilled customer orders to be added to a route.
- **FR-004**: The system MUST NOT allow a customer order to be on more than one active (Planned or In Progress) route.
- **FR-005**: The system MUST keep each stop's sequence number unique and ordered within a route.
- **FR-006**: The system MUST allow only Planned routes to be edited.
- **FR-007**: The system MUST NOT allow a route with no stops to be started.
- **FR-008**: The system MUST allow stops to be marked Delivered or Failed only while the route is In Progress.
- **FR-009**: The system MUST set a route to Completed when all of its stops are Delivered or Failed.
- **FR-010**: The system MUST allow Planned and In Progress routes to be cancelled, and MUST NOT allow Completed routes to be cancelled.
- **FR-011**: The system MUST maintain the route status (Planned, In Progress, Completed, Cancelled).
- **FR-012**: The system MUST reject a planned date in the past when a route is created.
- **FR-013**: The system MUST prevent unauthorized users from creating, editing, starting, updating, or cancelling routes.

### Out of Scope
- Assigning drivers or vehicles.
- GPS tracking, distance calculation, and route optimization.
- Re-delivery of failed stops (a failed order must be added to a new route manually).
- Customer notifications.

---

## Key Entities

- **Route**: a planned delivery trip on a given date. Contains one or more Route Stops.
- **Route Stop**: one delivery on a route. References one Customer Order and has a position in the route's sequence.
- **Customer Order**: a Fulfilled order (see N06) to be delivered. Can be on at most one active route.
- **Customer**: the recipient of the order (see N07); the delivery address comes from the customer record.
- **Warehouse Manager**: the authorized user who manages routes.

---

## Data Model Requirements

### `route` table
| Field         
|----------------

| `route_code`   : this is the code for the route                                        
| `route_name`    : thi is the unique name given to the route                                                             
| `planned_date`  : this is the date that it will alivw at the destinatio                                                     
| `status`        : thi is the checks if the good alived, transit or declined
| `created_at`    : this is the time that the good left the warehouse                                             


## Acceptance Criteria

### AC-N08.1 — Create Route

#### Scenario: Create route
* **Given** Fulfilled customer orders exist that are not on an active route
* **When**  the Warehouse Manager creates a route with a future planned date and selects those orders
* **Then**  the system saves the route with status Planned
* **And**   assigns it a unique identifier
* **And**   creates a stop for each order with sequence numbers starting at 1

#### Scenario: Order not fulfilled
* **Given** a customer order has status Draft, Submitted, or Cancelled
* **When**  the Warehouse Manager tries to add it to a route
* **Then**  the system rejects it and shows an error

#### Scenario: Order already on an active route
* **Given** a Fulfilled order is on a Planned or In Progress route
* **When**  the Warehouse Manager tries to add it to another route
* **Then**  the system rejects it and shows an error

#### Scenario: Planned date in the past
* **Given** the Warehouse Manager is creating a route
* **When**  they enter a planned date in the past
* **Then**  the system rejects the route and shows a validation error

### AC-N08.2 — View Routes

#### Scenario: View routes
* **Given** routes exist
* **When**  the Warehouse Manager selects "View Routes"
* **Then**  the system displays each route with its date, status, and stops in sequence order

#### Scenario: No routes
* **Given** no routes exist
* **When**  the Warehouse Manager selects "View Routes"
* **Then**  the system displays a message that no routes are available

### AC-N08.3 — Edit Route

#### Scenario: Edit Planned route
* **Given** a route has status Planned
* **When**  the Warehouse Manager changes its date, adds or removes a stop, or reorders stops
* **Then**  the system saves the changes
* **And**   stop sequence numbers remain unique and consecutive

#### Scenario: Edit non-Planned route
* **Given** a route has status In Progress, Completed, or Cancelled
* **When**  the Warehouse Manager tries to edit it
* **Then**  the system rejects the change

### AC-N08.4 — Start Route

#### Scenario: Start route
* **Given** a route has status Planned and at least one stop
* **When**  the Warehouse Manager starts the route
* **Then**  the status changes to In Progress
* **And**   all stops have status Pending

#### Scenario: Start empty route
* **Given** a Planned route has no stops
* **When**  the Warehouse Manager tries to start it
* **Then**  the system rejects the action and shows an error

### AC-N08.5 — Record Stop Result

#### Scenario: Mark stop delivered or failed
* **Given** a route is In Progress and a stop is Pending
* **When**  the Warehouse Manager marks the stop Delivered or Failed
* **Then**  the system saves the stop status

#### Scenario: Route completes automatically
* **Given** a route is In Progress and only one stop is still Pending
* **When**  the Warehouse Manager marks that stop Delivered or Failed
* **Then**  the route status changes to Completed
* **And**   the completion time is recorded

#### Scenario: Update stop on a route that is not In Progress
* **Given** a route has status Planned, Completed, or Cancelled
* **When**  the Warehouse Manager tries to change a stop's status
* **Then**  the system rejects the change

### AC-N08.6 — Cancel Route

#### Scenario: Cancel route
* **Given** a route has status Planned or In Progress
* **When**  the Warehouse Manager cancels it
* **Then**  the status changes to Cancelled
* **And**   its orders are no longer considered on an active route

#### Scenario: Cancel Completed route
* **Given** a route has status Completed
* **When**  the Warehouse Manager tries to cancel it
* **Then**  the system rejects the action

#### Scenario: Unauthorized change
* **Given** the user is not authorized to manage routes
* **When**  they try to create, edit, start, update, or cancel a route
* **Then**  the system rejects the change
