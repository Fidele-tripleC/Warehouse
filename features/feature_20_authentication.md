# Feature: Authentication

**Feature ID:**        N20  
**Branch pattern:**    `feature/20-authentication`  
**Status:**            Draft  
**Created:**           2026-10-29  
**Input:**             Logging in with email and password, logging out, and adding users who can use the warehouse system  
**Depends on:**        None  
**Related:**           [Company](feature_01_Company_maintinence.md), [Warehouse](feature_02_Warehouse__maintinence.md), [Customer](feature_07_Customer__maintinence.md), [Customer Order](feature_09_Customer_Order_Management.md)

---

## User Stories

### US-N20.1: Log in
**As a**        System Administrator, Warehouse Manager, or Employee Manager  
**I want to**   Log in with my email and password  
**So that**     I can use the warehouse system as my role.  
**Priority:**               P1  
**Independent test:**    Enter a saved email and password and verify that the user gets into the system with that role.  
**Acceptance scenarios:**   See AC-N20.1

### US-N20.2: Log out
**As a**        A logged in user  
**I want to**   Log out  
**So that**     the next person on the computer is not still in my account.  
**Priority:**               P1  
**Independent test:**    Log in then select Log out and verify that the login screen is displayed.  
**Acceptance scenarios:**   See AC-N20.2

### US-N20.3: Add a user
**As a**        System Administrator  
**I want to**   Add a System Administrator, Warehouse Manager, or Employee Manager  
**So that**     those people can log in as their role.  
**Priority:**               P1  
**Independent test:**    Add a Warehouse Manager with a unique email and password. Verify that the manager can log in. Add the same email again and verify the system displays "Duplicate email".  
**Acceptance scenarios:**   See AC-N20.3

### US-N20.4: Block users who are not logged in
**As a**        The warehouse system  
**I want to**   Keep company and warehouse screens closed until a user logs in  
**So that**     a person who is not logged in cannot change company or warehouse information.  
**Priority:**               P1  
**Independent test:**    Open a warehouse screen without logging in. The login screen is displayed and no warehouse record is changed.  
**Acceptance scenarios:**   See AC-N20.4

---

## Functional Requirements

- **FR-001**: System Must allow a System Administrator, Warehouse Manager, or Employee Manager to log in with email and password.
- **FR-002**: System Must log the user in when the email and password match a saved user.
- **FR-003**: System Must prevent login when the email or password is wrong and display "Invalid email or password".
- **FR-004**: System Must keep the user role after login (System Administrator, Warehouse Manager, or Employee Manager).
- **FR-005**: System Must allow a logged in user to log out.
- **FR-006**: System Must allow an authorised System Administrator to add a user with a unique email, password, and role.
- **FR-007**: System Must prevent adding a user when that email already exists and display "Duplicate email".
- **FR-008**: System Must associate each user with an employee when the user is an employee of the company.
- **FR-009**: System Must prevent a person who is not logged in from viewing or changing company, warehouse, or employee information.
- **FR-010**: System Must prevent unauthorized users from adding a user.
- **FR-011**: System Must not give retailers a login. Retailers send orders outside the system. The warehouse records those orders.

### Out of Scope
- A retailer logging into the warehouse system.
- A retailer submitting an order from a store login.

---

## Key Entities

- **User**: a person who logs in. The role is System Administrator, Warehouse Manager, or Employee Manager.
- **Employee**: the company record for that person.
- **Company**: the company the user works for.

- **relationships**
- one **User** has one **Role**
- one **Employee** can have one **User** login
- one **Company** can have multiple **Users**

---

## Data Model Requirements

### `User` table

 `user_id`         : This is the unique id  
 `email`           : This is the unique email used to log in  
 `password`        : This is the password used to log in  
 `role`            : System Administrator, Warehouse Manager, or Employee Manager  
 `employee_id`     : This is the employee this login belongs to  
 `created_at`      : This is the time when the user was created

---

## Acceptance Criteria

### AC-N20.1 — Log in

#### Scenario: User logs in
*   **Given** a user exists with email manager@warehouse.com and a password
*   **When**  the user enters that email and password
*   **Then**  the system logs the user in
*   **And**   displays the screens for that role

#### Scenario: Wrong password
*   **Given** a user exists with email manager@warehouse.com
*   **When**  the user enters manager@warehouse.com and the wrong password
*   **Then**  the user is not logged in
*   **And**   the system displays "Invalid email or password"

#### Scenario: Wrong email
*   **Given** no user has email nobody@warehouse.com
*   **When**  a user attempts to log in with nobody@warehouse.com
*   **Then**  the user is not logged in
*   **And**   the system displays "Invalid email or password"

### AC-N20.2 — Log out

#### Scenario: User logs out
*   **Given** the user is logged in
*   **When**  the user selects Log out
*   **Then**  the user is logged out
*   **And**   the login screen is displayed

### AC-N20.3 — Add a user

#### Scenario: Add a warehouse manager
*   **Given** the System Administrator is authorized
*   **When**  the System Administrator enters a unique email, a password, and role Warehouse Manager
*   **Then**  the system saves the user
*   **And**   that warehouse manager can log in

#### Scenario: Duplicate email
*   **Given** a user with email manager@warehouse.com already exists
*   **When**  the System Administrator tries to add another user with manager@warehouse.com
*   **Then**  the new user is not saved
*   **And**   the system displays "Duplicate email"

#### Scenario: Unauthorized add
*   **Given** the user is not authorized to add a user
*   **When**  the user attempts to add a user
*   **Then**  the user is not saved
*   **And**   the system displays "You are not authorized to manage users"

### AC-N20.4 — Block users who are not logged in

#### Scenario: Not logged in
*   **Given** the user is not logged in
*   **When**  the user attempts to view or change company, warehouse, or employee information
*   **Then**  the change is not saved
*   **And**   the login screen is displayed
