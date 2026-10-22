# Feature: Locations

**Feature ID:**        N08  
**Branch pattern:**    `feature/8-locations`  
**Status:**            Draft  
**Created:**           2026-10-19  
**Input:**             Creating, Viewing, and editing locations. Teams have a location. Games use a location.  
**Depends on:**        [Authentication](feature_01_authentication.md)  
**Related:**           [Teams](feature_06_teams.md), [Games](feature_05_games.md), [Create Games for a Season](feature_10_create_games_for_season.md)

---

## User Stories

### US-N08.1: View Locations
**As a**        An Owner  
**I want to**   View all locations  
**So that**     I can see the places maintained for games.  
**Priority:**               P1  
**Independent test:**    Select View Locations and verify that the system displays all existing locations and their address.  
**Acceptance scenarios:**   See AC-N08.1

### US-N08.2: Add Location
**As a**        Owner  
**I want to**   add a location  
**So that**     teams and games have a place to play  
**Priority:**               P1  
**Independent test:**    Enter valid location information and save it. Verify that the new location appears in the location list.  
**Acceptance scenarios:**   See AC-N08.2

### US-N08.3: edit Location
**As a**        Owner  
**I want to**   Edit location information  
**So that**     location information remains accurate  
**Priority:**               P1  
**Independent test:**    Change an existing location address and identify that the updated address is saved and displayed.  
**Acceptance scenarios:**   See AC-N08.3

---

## Functional Requirements

- **FR-048**: System Must allow the Owner to view the locations that the league has
- **FR-049**: System Must allow an authorised Owner to create a location with a unique name and an address.
- **FR-050**: System must allow an authorised Owner to edit the information of an existing Location when needed
- **FR-051**: System Must prevent unauthorized users from adding or editing a location.

---

## Key Entities

- **Location**: the place a game is played.
- **Team**: a team can have a home location
- **Game**: a game is played at a location

- **relationships**
- one **Location** can be used by many **Games**
- one **Location** can be the home of many **Teams**

---

## Initial Data Model

### `Location` table

 `location_id`     : This is the unique id  
 `location_name`   : This is the unique name of the Location  
 `address`         : This is the Physical location  
 `created_at`      : This is the time when the location was created

---

## Gherkin AC

### AC-N08.1 — View Locations

#### Scenario: View existing Locations
*   **Given** locations exist in the system
*   **When**  the Owner selects View Locations
*   **Then**  The system displays the locations
*   **And**   Displays their current information

#### Scenario: No location
*   **Given** No location exists
*   **When**  the Owner selects View Locations
*   **Then**  the location list is empty
*   **And**   the system displays "No locations are available"

### AC-N08.2 — Add location

#### Scenario: Add location
*   **Given** The Owner is authorized
*   **When**  The Owner enters valid location information
*   **Then**  the system saves the location
*   **And**   the new location appears in the location list

#### Scenario: Duplicate location name
*   **Given** a location named North Field already exists
*   **When**  the Owner tries to create another location with the same name
*   **Then**  the new location is not saved
*   **And**   the system displays "Duplicate location name"

### AC-N08.3 — Edit Location

#### Scenario: Edit location
*   **Given**  A location exists
*   **When**  The Owner edits its information
*   **Then**  the system saves the updated information
*   **And**   displays the updated location

