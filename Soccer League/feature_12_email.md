# Feature: Email

**Feature ID:**        N12  
**Branch pattern:**    `feature/12-email`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Emailing Refs, Manager, and Player about upcoming games  
**Depends on:**        [Authentication](feature_01_authentication.md), [Refs](feature_09_refs.md), [Games](feature_05_games.md), [Teams](feature_06_teams.md), [Players](feature_07_players.md)  
**Related:**           [Create Games for a Season](feature_10_create_games_for_season.md)

---

## User Stories

### US-N12.1: Email Refs
**As a**        An Owner  
**I want to**   email the refs  
**So that**     the refs know the upcoming games they will work.  
**Priority:**               P1  
**Independent test:**    Send an email to a ref with an upcoming game and verify that the email is sent to the ref email.  
**Acceptance scenarios:**   See AC-N12.1

### US-N12.2: Email Manager
**As a**        Owner  
**I want to**   email the manager  
**So that**     the manager knows the upcoming games  
**Priority:**               P1  
**Independent test:**    Send an email to a manager who has a team in an upcoming game.  
**Acceptance scenarios:**   See AC-N12.2

### US-N12.3: Email Player
**As a**        Owner  
**I want to**   email the player  
**So that**     the player knows the upcoming games  
**Priority:**               P1  
**Independent test:**    Send an email to a player who has an email and is on a team in that game.  
**Acceptance scenarios:**   See AC-N12.3

---

## Functional Requirements

- **FR-072**: System Must allow an authorised Owner to email refs about upcoming games.
- **FR-073**: System Must allow an authorised Owner to email managers about upcoming games.
- **FR-074**: System Must allow an authorised Owner to email players about upcoming games.
- **FR-075**: System Must send the email to the email saved on that user or player.
- **FR-076**: System Must prevent sending when there is no email and display "Email is required".

---

## Key Entities

- **Email**: the message the Owner sends about an upcoming game.
- **Ref**: a referee who gets the email.
- **Manager**: a manager who gets the email.
- **Player**: a player who gets the email.

- **relationships**
- one **Game** can have many **Emails**
- one **Email** goes to a **Ref**, a **Manager**, or a **Player**

---

## Initial Data Model

### `Email` table

 `email_id`        : This is the unique id  
 `game_id`         : This is the upcoming game  
 `to_user_id`      : This is who the email went to  
 `subject`         : This is the subject  
 `sent_at`         : This is the time when the email was sent

---

## Gherkin AC

### AC-N12.1 — Email Refs

#### Scenario: Email a ref
*   **Given** The Owner is authorized
*   **And**   a ref is on an upcoming game
*   **And**   the ref has an email
*   **When**  The Owner emails the ref about the game
*   **Then**  the system sends the email
*   **And**   the email is sent to the ref email

#### Scenario: Email is missing
*   **Given** a ref has no email
*   **When**  the Owner tries to email the ref
*   **Then**  the email is not sent
*   **And**   the system displays "Email is required"

### AC-N12.2 — Email Manager

#### Scenario: Email a manager
*   **Given** a manager has a team in an upcoming game
*   **And**   the manager has an email
*   **When**  The Owner emails the manager
*   **Then**  the system sends the email
*   **And**   the email is sent to the manager email

### AC-N12.3 — Email Player

#### Scenario: Email a player
*   **Given** a player is on a team in an upcoming game
*   **And**   the player has an email
*   **When**  The Owner emails the player
*   **Then**  the system sends the email
*   **And**   the email is sent to the player email

