# Feature: Seasons

**Feature ID:**        N04  
**Branch pattern:**    `feature/4-seasons`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing seasons so the Owner can manage the games season  
**Depends on:**        [Leagues](feature_03_leagues.md)  
**Related:**           [Games](feature_05_games.md), [Create Games for a Season](feature_10_create_games_for_season.md), [Display](feature_11_display.md)

---

## User Stories

### US-N04.1: View Seasons
**As a**        An Owner  
**I want to**   View all seasons  
**So that**     I can see the seasons maintained for each league.  
**Priority:**               P1  
**Independent test:**    Select View Seasons and verify that the system displays all existing seasons and their dates.  
**Acceptance scenarios:**   See AC-N04.1

### US-N04.2: Add Season
**As a**        Owner  
**I want to**   add a season  
**So that**     I can manage games for Fall league in that time  
**Priority:**               P1  
**Independent test:**    Enter a start date and an end date for a league and save it. Verify that the new season appears in the season list.  
**Acceptance scenarios:**   See AC-N04.2

### US-N04.3: edit Season
**As a**        Owner  
**I want to**   Edit season information  
**So that**     season dates remain accurate  
**Priority:**               P1  
**Independent test:**    Change an existing season end date and identify that the updated date is saved and displayed.  
**Acceptance scenarios:**   See AC-N04.3

---

## Functional Requirements

- **FR-020**: System Must allow the Owner to view the seasons that the leagues have
- **FR-021**: System Must allow an authorised Owner to create a season with a start date and an end date.
- **FR-022**: System Must prevent a season from being saved when the end date is before the start date and display "End date must be after start date".
- **FR-023**: System must allow an authorised Owner to edit the information of an existing Season when needed
- **FR-024**: System Must save games per team on the season (10 for Fall league or 18 when each team plays eighteen games).

---

## Key Entities

- **Season**: the time when games are played for a league.
- **League**: the league for that season

- **relationships**
- one **League** can have many **Seasons**
- one **Season** can have many **Games**

---

## Initial Data Model

### `Season` table

 `season_id`       : This is the unique id  
 `season_name`     : This is the name of the Season  
 `league_id`       : This is the league the season belongs to  
 `start_date`      : This is the start date  
 `end_date`        : This is the end date  
 `games_per_team`  : 10 for Fall league or 18 for eighteen games  
 `created_at`      : This is the time when the season was created

---

## Gherkin AC

### AC-N04.1 — View Seasons

#### Scenario: View existing Seasons
*   **Given** seasons exist in the system
*   **When**  the Owner selects View Seasons
*   **Then**  The system displays the seasons
*   **And**   Displays the league, start date, and end date

#### Scenario: No season
*   **Given** No season exists
*   **When**  the Owner selects View Seasons
*   **Then**  the season list is empty
*   **And**   the system displays "No seasons are available"

### AC-N04.2 — Add season

#### Scenario: Add season
*   **Given** The Owner is authorized
*   **And**   Fall league exists
*   **When**  The Owner enters a start date and an end date
*   **Then**  the system saves the season
*   **And**   associates it with the league
*   **And**   the new season appears in the season list

#### Scenario: End date before start date
*   **Given** the Owner is adding a season
*   **When**  the end date is before the start date
*   **Then**  the new season is not saved
*   **And**   the system displays "End date must be after start date"

### AC-N04.3 — Edit Season

#### Scenario: Edit season
*   **Given**  A season exists
*   **When**  The Owner edits its information
*   **Then**  the system saves the updated information
*   **And**   displays the updated season

