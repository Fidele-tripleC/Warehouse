# Feature: Sports

**Feature ID:**        N02  
**Branch pattern:**    `feature/2-sports`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing sports. The sports are Football, Softball, and Basketball. Each sport has a Men team and a Women team.  
**Depends on:**        [Authentication](feature_01_authentication.md)  
**Related:**           [Leagues](feature_03_leagues.md)

---

## User Stories

### US-N02.1: View Sports
**As a**        An Owner  
**I want to**   View all sports  
**So that**     I can see Football, Softball, and Basketball with Men and Women.  
**Priority:**               P1  
**Independent test:**    Select View Sports and verify that the system displays all existing sports and their information.  
**Acceptance scenarios:**   See AC-N02.1

### US-N02.2: Add Sport
**As a**        Owner  
**I want to**   add a sport  
**So that**     Football, Softball, and Basketball can each have a Men team and a Women team.  
**Priority:**               P1  
**Independent test:**    Enter Football Women and save it. Verify that Football Women appears in the sport list.  
**Acceptance scenarios:**   See AC-N02.2

### US-N02.3: edit Sport
**As a**        Owner  
**I want to**   Edit sport information  
**So that**     sport information remains accurate  
**Priority:**               P1  
**Independent test:**    Change an existing sport name and identify that the updated name is saved and displayed.  
**Acceptance scenarios:**   See AC-N02.3

---

## Functional Requirements

- **FR-010**: System Must allow the Owner to view the sports that the league has
- **FR-011**: System Must allow an authorised Owner to create a sport with a unique name.
- **FR-012**: System Must allow Football, Softball, and Basketball, and each of these sports has Men and Women.
- **FR-013**: System must allow an authorised Owner to edit the information of an existing Sport when needed
- **FR-014**: System Must prevent unauthorized users from adding or editing a sport.

---

## Key Entities

- **Sport**: Football, Softball, or Basketball. Each sport has Men and Women.
- **League**: Fall league for that sport

- **relationships**
- one **Sport** can have many **Leagues**
- one **Sport** has Men and Women

---

## Initial Data Model

### `Sport` table

 `sport_id`        : This is the unique id  
 `sport_name`      : This is the unique name of the sport  
 `gender`          : Men or Women  
 `created_at`      : This is the time when the sport was created

---

## Gherkin AC

### AC-N02.1 — View Sports

#### Scenario: View existing Sports
*   **Given** Football Men, Football Women, Softball Men, Softball Women, Basketball Men, and Basketball Women exist
*   **When**  the Owner selects View Sports
*   **Then**  The system displays those sports
*   **And**   Displays Men and Women for each sport

#### Scenario: No sport
*   **Given** No sport exists
*   **When**  the Owner selects View Sports
*   **Then**  the sport list is empty
*   **And**   the system displays "No sports are available"

### AC-N02.2 — Add sport

#### Scenario: Add Football Women
*   **Given** The Owner is authorized
*   **When**  The Owner enters Football Women
*   **Then**  the system saves the sport
*   **And**   Football Women appears in the sport list

#### Scenario: Duplicate sport name
*   **Given** Football Men already exists
*   **When**  the Owner tries to create Football Men again
*   **Then**  the new sport is not saved
*   **And**   the system displays "Football Men already exists"

### AC-N02.3 — Edit Sport

#### Scenario: Edit sport
*   **Given**  Football Men exists
*   **When**  The Owner edits its information
*   **Then**  the system saves the updated information
*   **And**   displays the updated sport

#### Scenario: Unauthorized update
*   **Given**  The user is not authorized to manage sports
*   **When**   the user attempts to add or edit a sport
*   **Then**   the sport is not changed
*   **And**    the system displays "You are not authorized to manage sports"

