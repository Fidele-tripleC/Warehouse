# Feature: Authentication

**Feature ID:**        N01  
**Branch pattern:**    `feature/1-authentication`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Logging in with email and password, adding users, and giving approval to a manager  
**Depends on:**        None  
**Related:**           [Sports](feature_02_sports.md), [Refs](feature_09_refs.md), [Display](feature_11_display.md)

---

## User Stories

### US-N01.1: Authentication
**As a**        An Owner, Manager, or Ref  
**I want to**   Log in with my email and password  
**So that**     I can use the league system as my role.  
**Priority:**               P1  
**Independent test:**    Enter a saved email and password and verify that the user gets into the system with that role.  
**Acceptance scenarios:**   See AC-N01.1

### US-N01.2: Log out
**As a**        A logged in user  
**I want to**   Log out  
**So that**     the next person on the computer is not still in my account.  
**Priority:**               P1  
**Independent test:**    Log in then select Log out and verify that the login screen is displayed.  
**Acceptance scenarios:**   See AC-N01.2

### US-N01.3: Add a user
**As a**        Owner  
**I want to**   Add Owner, Manager, and Ref  
**So that**     Owner, Manager, and Ref can log in as their role.  
**Priority:**               P1  
**Independent test:**    Add a Manager with a unique name, email, and password. Verify that the manager can log in. Add the same name again and verify the system displays "Duplicate user name".  
**Acceptance scenarios:**   See AC-N01.3

### US-N01.4: Approve a manager
**As a**        Owner  
**I want to**   Give approval to a manager  
**So that**     only that manager can add players, enter scores, and enter statistics of the game.  
**Priority:**               P1  
**Independent test:**    Approve a manager and verify that the manager can add a player after login.  
**Acceptance scenarios:**   See AC-N01.4

---

## Functional Requirements

- **FR-001**: System Must allow an Owner, Manager, or Ref to log in with email and password.
- **FR-002**: System Must log the user in when the email and password match a saved user.
- **FR-003**: System Must prevent login when the email or password is wrong and display "Invalid email or password".
- **FR-004**: System Must keep the user role after login (Owner, Manager, or Ref).
- **FR-005**: System Must allow a logged in user to log out.
- **FR-006**: System Must allow an authorised Owner to add a user with a unique name, unique email, password, and role Owner, Manager, or Ref.
- **FR-007**: System Must allow an authorised Owner to give approval to a manager.
- **FR-008**: System Must prevent a manager who is not approved from adding players, entering scores, or entering statistics.
- **FR-009**: System Must prevent adding a user when that user name already exists and display "Duplicate user name".

---

## Key Entities

- **User**: a person who logs in. The role is Owner, Manager, or Ref.
- **Approval**: the Owner says which manager can run a team.

- **relationships**
- one **User** has one **Role**
- one **Owner** can approve one or more **Managers**

---

## Initial Data Model

### `User` table

 `user_id`         : This is the unique id  
 `user_name`       : This is the unique name of the user  
 `email`           : This is the unique email used to log in  
 `password`        : This is the password used to log in  
 `role`            : Owner, Manager, or Ref  
 `approved`        : yes or no for a manager  
 `created_at`      : This is the time when the user was created

---

## Gherkin AC

### AC-N01.1 — Authentication

#### Scenario: User logs in
*   **Given** a user exists with email manager@league.com and a password
*   **When**  the user enters that email and password
*   **Then**  the system logs the user in
*   **And**   displays the screens for that role

#### Scenario: Wrong password
*   **Given** a user exists with email manager@league.com
*   **When**  the user enters manager@league.com and the wrong password
*   **Then**  the user is not logged in
*   **And**   the system displays "Invalid email or password"

#### Scenario: Wrong email
*   **Given** no user has email nobody@league.com
*   **When**  a user attempts to log in with nobody@league.com
*   **Then**  the user is not logged in
*   **And**   the system displays "Invalid email or password"

### AC-N01.2 — Log out

#### Scenario: User logs out
*   **Given** the user is logged in
*   **When**  the user selects Log out
*   **Then**  the user is logged out
*   **And**   the login screen is displayed

### AC-N01.3 — Add a user

#### Scenario: Add a manager
*   **Given** the Owner is authorized
*   **When**  the Owner enters a unique name, a unique email, a password, and role Manager
*   **Then**  the system saves the user
*   **And**   that manager can log in

#### Scenario: Duplicate user name
*   **Given** a user with that name already exists
*   **When**  the Owner tries to add another user with the same name
*   **Then**  the new user is not saved
*   **And**   the system displays "Duplicate user name"

#### Scenario: Duplicate email
*   **Given** a user with email owner@league.com already exists
*   **When**  the Owner tries to add another user with owner@league.com
*   **Then**  the new user is not saved
*   **And**   the system displays "Duplicate email"

### AC-N01.4 — Approve a manager

#### Scenario: Approve a manager
*   **Given** a user with role Manager exists
*   **And**   the manager is not approved
*   **When**  the Owner gives approval to the manager
*   **Then**  the manager is approved
*   **And**   the manager can add players

#### Scenario: Manager is not approved
*   **Given** a Manager is logged in and is not approved
*   **When**  the manager attempts to add a player
*   **Then**  the player is not saved
*   **And**   the system displays "Manager is not approved"

