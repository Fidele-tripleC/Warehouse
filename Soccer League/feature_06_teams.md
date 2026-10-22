# Feature: Teams

**Feature ID:**        N06  
**Branch pattern:**    `feature/6-teams`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing teams with a manager, players, a location, and a max number of players. Football, Softball, and Basketball each have a Men team and a Women team.  
**Depends on:**        [Leagues](feature_03_leagues.md), [Authentication](feature_01_authentication.md), [Locations](feature_08_locations.md)  
**Related:**           [Players](feature_07_players.md), [Games](feature_05_games.md), [Display](feature_11_display.md)

---

## User Stories

### US-N06.1: View Teams
**As a**        An Owner  
**I want to**   View all teams  
**So that**     I can see the teams maintained by the league.  
**Priority:**               P1  
**Independent test:**    Select View Teams and verify that the system displays all existing teams and their manager.  
**Acceptance scenarios:**   See AC-N06.1

### US-N06.2: Add Team
**As a**        Owner  
**I want to**   add a team  
**So that**     the league has teams that can play each other  
**Priority:**               P1  
**Independent test:**    Enter a league and an approved manager and save it. Verify that the new team appears in the team list.  
**Acceptance scenarios:**   See AC-N06.2

### US-N06.3: Assign a location
**As a**        Owner  
**I want to**   assign a location to a team  
**So that**     the team has a home place to play  
**Priority:**               P1  
**Independent test:**    Assign a location to a team and identify that the location is saved and displayed.  
**Acceptance scenarios:**   See AC-N06.3

---

## Functional Requirements

- **FR-029**: System Must allow the Owner to view the teams that the league has
- **FR-030**: System Must allow an authorised Owner to create a team with an approved manager.
- **FR-031**: System Must prevent a team from being saved when the manager is not approved and display "Manager is not approved".
- **FR-032**: System Must allow a team to be associated with a location.
- **FR-033**: System Must save the maximum number of players on the team.
- **FR-034**: System Must allow the team manager to view the team after login.
- **FR-035**: System Must allow a Men team and a Women team for Football, Softball, and Basketball.

---

## Key Entities

- **Team**: a team in a league. It has a manager and players.
- **League**: the league for that team
- **Location**: the home place of the team

- **relationships**
- one **League** can have many **Teams**
- one **Team** has one **Manager**
- one **Team** can have one **Location**
- one **Team** can have many **Players**

---

## Initial Data Model

### `Team` table

 `team_id`         : This is the unique id  
 `team_name`       : This is the name of the Team  
 `league_id`       : This is the league the team belongs to  
 `manager_id`      : This is the approved manager  
 `location_id`     : This is the home location  
 `max_players`     : This is the maximum number of players  
 `created_at`      : This is the time when the team was created

---

## Gherkin AC

### AC-N06.1 — View Teams

#### Scenario: View existing Teams
*   **Given** teams exist in the system
*   **When**  the Owner selects View Teams
*   **Then**  The system displays the teams
*   **And**   Displays the league and the manager

#### Scenario: No team
*   **Given** No team exists
*   **When**  the Owner selects View Teams
*   **Then**  the team list is empty
*   **And**   the system displays "No teams are available"

### AC-N06.2 — Add team

#### Scenario: Add team
*   **Given** The Owner is authorized
*   **And**   a league exists
*   **And**   an approved manager exists
*   **When**  The Owner enters valid team information
*   **Then**  the system saves the team
*   **And**   associates it with the league
*   **And**   the new team appears in the team list

#### Scenario: Manager is not approved
*   **Given** a Manager is not approved
*   **When**  the Owner tries to create a team with that manager
*   **Then**  the new team is not saved
*   **And**   the system displays "Manager is not approved"

### AC-N06.3 — Assign a location

#### Scenario: Associate Location
*   **Given**  a team exists
*   **And**    a location exists
*   **When**   the Owner assigns the location to the team
*   **Then**   a location is linked to the team
*   **And**    The association is saved
*   **And**    the team details show the associated location

