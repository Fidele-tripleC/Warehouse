# Feature: Players

**Feature ID:**        N07  
**Branch pattern:**    `feature/7-players`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing players that a manager adds to their own team  
**Depends on:**        [Teams](feature_06_teams.md), [Authentication](feature_01_authentication.md)  
**Related:**           [Games](feature_05_games.md), [Display](feature_11_display.md)

---

## User Stories

### US-N07.1: View Players
**As a**        A Manager  
**I want to**   View my players  
**So that**     I can see the players maintained on my team.  
**Priority:**               P1  
**Independent test:**    Select View Players and verify that the system displays the players on that manager team.  
**Acceptance scenarios:**   See AC-N07.1

### US-N07.2: Add Player
**As a**        Manager  
**I want to**   add my own players  
**So that**     my team has players for the games  
**Priority:**               P1  
**Independent test:**    Enter valid player information and save it. Verify that the new player appears on the team.  
**Acceptance scenarios:**   See AC-N07.2

### US-N07.3: edit Player
**As a**        Manager  
**I want to**   Edit player information  
**So that**     player information remains accurate  
**Priority:**               P1  
**Independent test:**    Change an existing player name and identify that the updated name is saved and displayed.  
**Acceptance scenarios:**   See AC-N07.3

---

## Functional Requirements

- **FR-035**: System Must allow an approved Manager to view the players on the manager team
- **FR-036**: System Must allow an authorised Manager to add a player to the manager own team.
- **FR-037**: System Must prevent a manager from adding a player to another manager team.
- **FR-038**: System Must prevent adding a player when the team is at the maximum number of players and display "Team is at maximum number of players".
- **FR-039**: System Must prevent a manager who is not approved from adding a player and display "Manager is not approved".
- **FR-040**: System must allow an authorised Manager to edit the information of an existing Player when needed

---

## Key Entities

- **Player**: a person on a team. Each player has their own statistics.
- **Team**: the team the player is on

- **relationships**
- one **Team** can have many **Players**
- one **Player** belongs to one **Team**

---

## Initial Data Model

### `Player` table

 `player_id`       : This is the unique id  
 `player_name`     : This is the name of the Player  
 `team_id`         : This is the team the player belongs to  
 `email`           : This is the email of the player  
 `created_at`      : This is the time when the player was created

---

## Gherkin AC

### AC-N07.1 — View Players

#### Scenario: View existing Players
*   **Given** players exist on the manager team
*   **When**  the Manager selects View Players
*   **Then**  The system displays the players
*   **And**   Displays their current information

#### Scenario: No player
*   **Given** No player exists on the team
*   **When**  the Manager selects View Players
*   **Then**  the player list is empty
*   **And**   the system displays "No players are available"

### AC-N07.2 — Add player

#### Scenario: Add player
*   **Given** The Manager is authorized
*   **And**   the manager is approved
*   **When**  The manager enters valid player information
*   **Then**  the system saves the player
*   **And**   associates it with the manager team
*   **And**   the new player appears in the player list

#### Scenario: Manager is not approved
*   **Given** the manager is not approved
*   **When**  the manager tries to add a player
*   **Then**  the new player is not saved
*   **And**   the system displays "Manager is not approved"

#### Scenario: Team is full
*   **Given** the team is at the maximum number of players
*   **When**  the manager tries to add another player
*   **Then**  the new player is not saved
*   **And**   the system displays "Team is at maximum number of players"

### AC-N07.3 — Edit Player

#### Scenario: Edit player
*   **Given**  A player exists on the manager team
*   **When**  The Manager edits its information
*   **Then**  the system saves the updated information
*   **And**   displays the updated player

