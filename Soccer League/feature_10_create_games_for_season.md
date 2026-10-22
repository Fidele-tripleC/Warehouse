# Feature: Create Games for a Season

**Feature ID:**        N10  
**Branch pattern:**    `feature/10-create-games-for-season`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating games for a season. Each game gets a location and a ref. Fall league has 10 games. Each team plays eighteen games.  
**Depends on:**        [Seasons](feature_04_seasons.md), [Teams](feature_06_teams.md), [Games](feature_05_games.md), [Locations](feature_08_locations.md), [Refs](feature_09_refs.md)  
**Related:**           [Display](feature_11_display.md), [Email](feature_12_email.md)

---

## User Stories

### US-N10.1: Create games for a season
**As a**        An Owner  
**I want to**   create games for a season  
**So that**     the teams in that season have games to play.  
**Priority:**               P1  
**Independent test:**    Create games for a season that has teams. Verify that games appear for that season.  
**Acceptance scenarios:**   See AC-N10.1

### US-N10.2: Put location on the games
**As a**        Owner  
**I want to**   put a location on each game  
**So that**     the season games have a place to play  
**Priority:**               P1  
**Independent test:**    Create games for a season and assign a location. Verify each game shows a location.  
**Acceptance scenarios:**   See AC-N10.2

### US-N10.3: Put a ref on the games
**As a**        Owner  
**I want to**   put a ref on each game  
**So that**     a referee will work the game  
**Priority:**               P1  
**Independent test:**    Assign a ref from the list to a season game. Verify the game shows the ref.  
**Acceptance scenarios:**   See AC-N10.3

---

## Functional Requirements

- **FR-057**: System Must allow an authorised Owner to create games for a season.
- **FR-058**: System Must create 10 games when the season is Fall league set to 10 games.
- **FR-059**: System Must create eighteen games for each team when the season is set to 18 games.
- **FR-060**: System Must put a location on each game created for the season.
- **FR-061**: System Must put a ref on each game created for the season.
- **FR-062**: System Must prevent creating games when the season has fewer than two teams and display "Season needs at least two teams".
- **FR-063**: System Must prevent putting the same ref on two games on the same date and display "Ref already scheduled at this time".
- **FR-064**: System Must prevent putting a user who is not a ref on a game and display "User is not a ref".

---

## Key Entities

- **Season**: the season the games are made for.
- **Game**: a game for that season. It has a location and a ref.
- **Location**: the place the game is played.
- **Ref**: the referee who works the game.

- **relationships**
- one **Season** can have many **Games**
- one **Game** has one **Location**
- one **Game** has one **Ref**

---

## Initial Data Model

### `Game` table

 `game_id`         : This is the unique id  
 `season_id`       : This is the season of the game  
 `home_team_id`    : This is the home team  
 `away_team_id`    : This is the away team  
 `location_id`     : This is the location of the game  
 `ref_id`          : This is the ref for the game  
 `game_date`       : This is the date of the game  
 `created_at`      : This is the time when the game was created

---

## Gherkin AC

### AC-N10.1 — Create games for a season

#### Scenario: Create eighteen games
*   **Given** The Owner is authorized
*   **And**   the season has at least two teams
*   **And**   the season is set to 18 games per team
*   **When**  The Owner creates games for the season
*   **Then**  the system saves the games
*   **And**   each team plays eighteen games

#### Scenario: Fall league 10 games
*   **Given** a Fall league season is set to 10 games
*   **And**   the season has at least two teams
*   **When**  The Owner creates games for the season
*   **Then**  10 games are saved

#### Scenario: Not enough teams
*   **Given** the season has fewer than two teams
*   **When**  the Owner tries to create games for the season
*   **Then**  the games are not saved
*   **And**   the system displays "Season needs at least two teams"

### AC-N10.2 — Put location on the games

#### Scenario: Assign location
*   **Given** games were created for a season
*   **And**   a location exists
*   **When**  The Owner puts the location on a game
*   **Then**  the game shows the location

### AC-N10.3 — Put a ref on the games

#### Scenario: Assign ref
*   **Given** The Owner is authorized
*   **And**   a ref exists
*   **And**   a game exists for the season
*   **When**  The Owner puts the ref on the game
*   **Then**  the system saves the ref on the game

#### Scenario: User is not a ref
*   **Given** a user with role Manager exists
*   **When**  the Owner tries to put that user on a game
*   **Then**  the game is not changed
*   **And**   the system displays "User is not a ref"

#### Scenario: Ref already scheduled
*   **Given** a ref is already on a game on a date
*   **When**  the Owner tries to put the same ref on another game on that date
*   **Then**  the game is not changed
*   **And**   the system displays "Ref already scheduled at this time"

