# Feature: Refs

**Feature ID:**        N09  
**Branch pattern:**    `feature/9-refs`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing the list of referees. A ref is put on a game.  
**Depends on:**        [Authentication](feature_01_authentication.md)  
**Related:**           [Games](feature_05_games.md), [Create Games for a Season](feature_10_create_games_for_season.md), [Email](feature_12_email.md)

---

## User Stories

### US-N09.1: View Refs
**As a**        An Owner  
**I want to**   View all refs  
**So that**     I can see the list of referees maintained by the league.  
**Priority:**               P1  
**Independent test:**    Select View Refs and verify that the system displays all existing refs and their information.  
**Acceptance scenarios:**   See AC-N09.1

### US-N09.2: Add Ref
**As a**        Owner  
**I want to**   add a ref  
**So that**     I can put them on a game  
**Priority:**               P1  
**Independent test:**    Enter valid ref information and save it. Verify that the new ref appears in the referee list.  
**Acceptance scenarios:**   See AC-N09.2

### US-N09.3: edit Ref
**As a**        Owner  
**I want to**   Edit ref information  
**So that**     ref information remains accurate  
**Priority:**               P1  
**Independent test:**    Change an existing ref name and identify that the updated name is saved and displayed.  
**Acceptance scenarios:**   See AC-N09.3

---

## Functional Requirements

- **FR-052**: System Must allow the Owner to view the refs that the league has
- **FR-053**: System Must allow an authorised Owner to create a ref with a unique email.
- **FR-054**: System Must allow a ref to log in with role Ref after the Owner adds them.
- **FR-055**: System must allow an authorised Owner to edit the information of an existing Ref when needed
- **FR-056**: System Must prevent unauthorized users from adding or editing a ref.

---

## Key Entities

- **Ref**: a referee on the list.
- **User**: the login for the ref
- **Game**: a ref is put on a game

- **relationships**
- one **Ref** is one **User** with role Ref
- one **Ref** can work many **Games**

---

## Initial Data Model

### `Ref` table

 `ref_id`          : This is the unique id  
 `user_id`         : This is the user with role Ref  
 `ref_name`        : This is the name of the Ref  
 `email`           : This is the unique email  
 `created_at`      : This is the time when the ref was created

---

## Gherkin AC

### AC-N09.1 — View Refs

#### Scenario: View existing Refs
*   **Given** refs exist in the system
*   **When**  the Owner selects View Refs
*   **Then**  The system displays the refs
*   **And**   Displays their current information

#### Scenario: No ref
*   **Given** No ref exists
*   **When**  the Owner selects View Refs
*   **Then**  the ref list is empty
*   **And**   the system displays "No refs are available"

### AC-N09.2 — Add ref

#### Scenario: Add ref
*   **Given** The Owner is authorized
*   **When**  The Owner enters valid ref information
*   **Then**  the system saves the ref
*   **And**   the new ref appears in the referee list

#### Scenario: Duplicate email
*   **Given** a ref with email ref@league.com already exists
*   **When**  the Owner tries to create another ref with the same email
*   **Then**  the new ref is not saved
*   **And**   the system displays "Duplicate email"

### AC-N09.3 — Edit Ref

#### Scenario: Edit ref
*   **Given**  A ref exists
*   **When**  The Owner edits its information
*   **Then**  the system saves the updated information
*   **And**   displays the updated ref

