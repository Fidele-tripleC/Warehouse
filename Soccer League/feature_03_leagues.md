# Feature: Leagues

**Feature ID:**        N03  
**Branch pattern:**    `feature/3-leagues`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing Fall league under a sport. Football Men, Football Women, Softball Men, Softball Women, Basketball Men, and Basketball Women each can have Fall league.  
**Depends on:**        [Sports](feature_02_sports.md), [Authentication](feature_01_authentication.md)  
**Related:**           [Seasons](feature_04_seasons.md), [Teams](feature_06_teams.md), [Create Games for a Season](feature_10_create_games_for_season.md), [Display](feature_11_display.md)

---

## User Stories

### US-N03.1: View Leagues
**As a**        An Owner  
**I want to**   View all leagues  
**So that**     I can see the leagues maintained under each sport.  
**Priority:**               P1  
**Independent test:**    Select View Leagues and verify that the system displays all existing leagues and their sport.  
**Acceptance scenarios:**   See AC-N03.1

### US-N03.2: Add League
**As a**        Owner  
**I want to**   add a league  
**So that**     Football Men, Football Women, Softball Men, Softball Women, Basketball Men, and Basketball Women can each have Fall league  
**Priority:**               P1  
**Independent test:**    Enter Fall league under Football Men and save it. Verify that Fall league appears in the league list.  
**Acceptance scenarios:**   See AC-N03.2

### US-N03.3: edit League
**As a**        Owner  
**I want to**   Edit league information  
**So that**     league information remains accurate  
**Priority:**               P1  
**Independent test:**    Change an existing league name and identify that the updated name is saved and displayed.  
**Acceptance scenarios:**   See AC-N03.3

---

## Functional Requirements

- **FR-015**: System Must allow the Owner to view the leagues that the sports have
- **FR-016**: System Must allow an authorised Owner to create Fall league under a sport.
- **FR-017**: System Must prevent a league from being saved when no sport is selected and display "Sport is required".
- **FR-018**: System must allow an authorised Owner to edit the information of an existing League when needed
- **FR-019**: System Must prevent unauthorized users from adding or editing a league.

---

## Key Entities

- **League**: Fall league for a sport.
- **Sport**: the sport for that league

- **relationships**
- one **Sport** can have many **Leagues**
- one **League** can have many **Teams** and many **Seasons**

---

## Initial Data Model

### `League` table

 `league_id`       : This is the unique id  
 `league_name`     : This is the name of the League  
 `sport_id`        : This is the sport the league belongs to  
 `created_at`      : This is the time when the league was created

---

## Gherkin AC

### AC-N03.1 — View Leagues

#### Scenario: View existing Leagues
*   **Given** leagues exist in the system
*   **When**  the Owner selects View Leagues
*   **Then**  The system displays the leagues
*   **And**   Displays the sport for each league

#### Scenario: No league
*   **Given** No league exists
*   **When**  the Owner selects View Leagues
*   **Then**  the league list is empty
*   **And**   the system displays "No leagues are available"

### AC-N03.2 — Add league

#### Scenario: Add league
*   **Given** The Owner is authorized
*   **And**   Football Men exists
*   **When**  The Owner enters Fall league under Football Men
*   **Then**  the system saves the league
*   **And**   associates it with Football Men
*   **And**   the new league appears in the league list

#### Scenario: Sport is missing
*   **Given** the Owner is adding a league
*   **When**  no sport is selected
*   **Then**  the new league is not saved
*   **And**   the system displays "Sport is required"

### AC-N03.3 — Edit League

#### Scenario: Edit league
*   **Given**  A league exists
*   **When**  The Owner edits its information
*   **Then**  the system saves the updated information
*   **And**   displays the updated league

