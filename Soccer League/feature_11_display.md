# Feature: Display

**Feature ID:**        N11  
**Branch pattern:**    `feature/11-display`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Display Leagues, Seasons, Teams, Players, and Statistics for an Owner, Manager, or Ref.  
**Depends on:**        [Leagues](feature_03_leagues.md), [Seasons](feature_04_seasons.md), [Teams](feature_06_teams.md), [Players](feature_07_players.md), [Games](feature_05_games.md), [Authentication](feature_01_authentication.md)  
**Related:**           [Create Games for a Season](feature_10_create_games_for_season.md)

---

## User Stories

### US-N11.1: Display Leagues and Seasons
**As a**        An Owner, Manager, or Ref  
**I want to**   Display leagues and seasons  
**So that**     I can see what leagues are running.  
**Priority:**               P1  
**Independent test:**    Select Display Leagues and Display Seasons and verify that the system displays existing leagues and seasons.  
**Acceptance scenarios:**   See AC-N11.1

### US-N11.2: Display Teams and Players
**As a**        An Owner, Manager, or Ref  
**I want to**   Display teams and players  
**So that**     I can see who is on each team  
**Priority:**               P1  
**Independent test:**    Select Display Teams and Display Players and verify that teams and players are displayed.  
**Acceptance scenarios:**   See AC-N11.2

### US-N11.3: Display Statistics
**As a**        An Owner, Manager, or Ref  
**I want to**   Display statistics  
**So that**     I can see player statistics of the game  
**Priority:**               P1  
**Independent test:**    Select Display Statistics and verify that the system displays player statistics with game id, team id, and player id.  
**Acceptance scenarios:**   See AC-N11.3

---

## Functional Requirements

- **FR-065**: System Must allow an Owner, Manager, or Ref to display leagues
- **FR-066**: System Must allow an Owner, Manager, or Ref to display seasons
- **FR-067**: System Must allow an Owner, Manager, or Ref to display teams
- **FR-068**: System Must allow an Owner, Manager, or Ref to display players
- **FR-069**: System Must allow an Owner, Manager, or Ref to display statistics
- **FR-070**: System Must display "No records of the games" when no statistics or results exist.
- **FR-071**: System Must prevent a Ref from adding players, entering scores, or entering statistics and display "You are not authorized to enter scores".

---

## Key Entities

- **Display**: after login the Owner, Manager, or Ref can see leagues, seasons, teams, players, and statistics.
- **User**: the Owner, Manager, or Ref who is logged in.

- **relationships**
- one **User** can see many **Leagues**, **Seasons**, **Teams**, **Players**, and **Statistics**

---

## Gherkin AC

### AC-N11.1 — Display Leagues and Seasons

#### Scenario: Display leagues
*   **Given** the user is logged in
*   **And**   leagues exist in the system
*   **When**  the user selects Display Leagues
*   **Then**  The system displays the leagues
*   **And**   Displays the sport for each league

#### Scenario: Display seasons
*   **Given** the user is logged in
*   **And**   seasons exist in the system
*   **When**  the user selects Display Seasons
*   **Then**  The system displays the seasons
*   **And**   Displays the league and the dates

### AC-N11.2 — Display Teams and Players

#### Scenario: Display teams
*   **Given** the user is logged in
*   **And**   teams exist in the system
*   **When**  the user selects Display Teams
*   **Then**  The system displays the teams
*   **And**   Displays the league and the manager

#### Scenario: Display players
*   **Given** the user is logged in
*   **And**   players exist in the system
*   **When**  the user selects Display Players
*   **Then**  The system displays the players
*   **And**   Displays the team

### AC-N11.3 — Display Statistics

#### Scenario: Display statistics
*   **Given** the user is logged in
*   **And**   statistics exist in the system
*   **When**  the user selects Display Statistics
*   **Then**  The system displays the statistics
*   **And**   Displays the game, team, and player

#### Scenario: No records of the games
*   **Given** the user is logged in
*   **And**   No statistics exist
*   **When**  the user selects Display Statistics
*   **Then**  the list is empty
*   **And**   the system displays "No records of the games"

#### Scenario: Unauthorized update
*   **Given**  The user is logged in as Ref
*   **When**   the user attempts to enter scores
*   **Then**   the scores are not saved
*   **And**    the system displays "You are not authorized to enter scores"

