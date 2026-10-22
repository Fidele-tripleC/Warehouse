# Feature: Games

**Feature ID:**        N05  
**Branch pattern:**    `feature/5-games`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing games. A game belongs to a season, has a result, has statistics, and can have a ref.  
**Depends on:**        [Seasons](feature_04_seasons.md), [Teams](feature_06_teams.md), [Locations](feature_08_locations.md)  
**Related:**           [Refs](feature_09_refs.md), [Create Games for a Season](feature_10_create_games_for_season.md), [Display](feature_11_display.md)

---

## User Stories

### US-N05.1: View Games
**As a**        An Owner  
**I want to**   View all games  
**So that**     I can see the games maintained for the season.  
**Priority:**               P1  
**Independent test:**    Select View Games and verify that the system displays all existing games and their information.  
**Acceptance scenarios:**   See AC-N05.1

### US-N05.2: Add Game
**As a**        Owner  
**I want to**   add a game  
**So that**     two teams play each other on a date at a location  
**Priority:**               P1  
**Independent test:**    Enter two teams, a date, and a location and save it. Verify that the new game appears in the game list.  
**Acceptance scenarios:**   See AC-N05.2

### US-N05.3: Enter Result
**As a**        A Manager  
**I want to**   enter scores  
**So that**     the game has a result  
**Priority:**               P1  
**Independent test:**    Enter a home score and an away score and save it. Verify that the result is saved with GameId.  
**Acceptance scenarios:**   See AC-N05.3

### US-N05.4: Enter Statistics
**As a**        A Manager  
**I want to**   enter statistics of the game  
**So that**     each player has their own statistics  
**Priority:**               P1  
**Independent test:**    Enter statistics for a player in a game. Verify game id, team id, and player id are saved.  
**Acceptance scenarios:**   See AC-N05.4

---

## Functional Requirements

- **FR-025**: System Must allow the Owner to view the games that the season has
- **FR-026**: System Must allow an authorised Owner to create a game with two different teams, a date, and a location.
- **FR-027**: System Must prevent a game from being saved when both teams are the same and display "Teams must be different".
- **FR-028**: System Must prevent a game from being saved when the two teams are not in the same league.
- **FR-029**: System Must allow an authorised Manager to enter a result with GameId, home score, and away score.
- **FR-030**: System Must prevent a score less than zero and display "Score cannot be less than zero".
- **FR-031**: System Must allow an authorised Manager to enter statistics with game id, team id, and player id.
- **FR-032**: System Must prevent a manager who is not approved from entering scores or statistics and display "Manager is not approved".

---

## Key Entities

- **Game**: two teams play each other in a season.
- **Result**: the scores of a game. Result has GameId.
- **Statistics**: the numbers for a player in a game. It has game id, team id, and player id.
- **Ref**: the referee on the game.
- **Location**: the place the game is played.

- **relationships**
- one **Season** can have many **Games**
- one **Game** has two **Teams**
- one **Game** has one **Location**
- one **Game** has one **Result**
- one **Game** can have many **Statistics**
- one **Ref** can work many **Games**

---

## Initial Data Model

### Game

 `game_id`           : This is the unique id  
 `season_id`         : This is the season of the game  
 `home_team_id`      : This is the home team  
 `away_team_id`      : This is the away team  
 `location_id`       : This is the place the game is played  
 `ref_id`            : This is the ref for the game  
 `game_date`         : This is the date of the game  
 `home_score`        : This is the home team score  
 `away_score`        : This is the away team score  
 `team_id`           : This is the team for player statistics  
 `player_id`         : This is the player for statistics  
 `statistics_value`  : This is the statistics entered for the player  
 `entered_by`        : This is the manager who entered scores or statistics  
 `created_at`        : This is the time it was created

---

## Gherkin AC

### AC-N05.1 — View Games

#### Scenario: View existing Games
*   **Given** games exist in the system
*   **When**  the Owner selects View Games
*   **Then**  The system displays the games
*   **And**   Displays the teams, date, and location

#### Scenario: No game
*   **Given** No game exists
*   **When**  the Owner selects View Games
*   **Then**  the game list is empty
*   **And**   the system displays "No games are available"

### AC-N05.2 — Add game

#### Scenario: Add game
*   **Given** The Owner is authorized
*   **And**   two teams exist in the same league
*   **And**   a location exists
*   **When**  The Owner enters valid game information
*   **Then**  the system saves the game
*   **And**   associates it with the season
*   **And**   the new game appears in the game list

#### Scenario: Same team
*   **Given** the Owner is adding a game
*   **When**  the home team and the away team are the same
*   **Then**  the new game is not saved
*   **And**   the system displays "Teams must be different"

### AC-N05.3 — Enter Result

#### Scenario: Enter scores
*   **Given** The Manager is authorized
*   **And**   the manager is approved
*   **And**   a game exists for the manager team
*   **When**  The manager enters a home score and an away score
*   **Then**  the system saves the result
*   **And**   associates it with the game

#### Scenario: Score less than zero
*   **Given** the manager is entering scores
*   **When**  a score is less than zero
*   **Then**  the result is not saved
*   **And**   the system displays "Score cannot be less than zero"

### AC-N05.4 — Enter Statistics

#### Scenario: Enter statistics
*   **Given** The Manager is authorized
*   **And**   the manager is approved
*   **And**   a player exists on the manager team
*   **When**  The manager enters statistics for that player in a game
*   **Then**  the system saves the statistics
*   **And**   associates it with the game, team, and player

#### Scenario: Manager is not approved
*   **Given** the manager is not approved
*   **When**  the manager tries to enter statistics
*   **Then**  the statistics are not saved
*   **And**   the system displays "Manager is not approved"

