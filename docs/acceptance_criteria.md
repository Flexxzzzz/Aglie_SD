# Agile Acceptance Criteria & User Stories

## Easy Exchange — Currency Exchange Comparison Web App

**Document Version:** 1.0.0  
**Status:** Approved  
**Date:** September 2026  
**Project Team:**  
* Ye Zayar Aung (Avax) — `6705140012`  
* Paing Thu Kha Kyaw (Flexx) — `6705140018`  
* Aung Chan Myae (Rowan) — `6705140035`  
**Repository Path:** `Lab_Agile/docs/acceptance_criteria.md`  

---

## 1. Overview & Framework

This document outlines the user stories, acceptance criteria, and quality governance rules for the **Easy Exchange** web application. In accordance with Agile and Scrum principles, each story follows standard persona-driven templates and defines concrete, verifiable acceptance criteria using the **Behavior-Driven Development (BDD)** Gherkin format (`Given - When - Then`).

### 1.1 Agile Quality Gates

#### Definition of Ready (DoR)
A user story is Ready for sprint planning when:
1. The user story is clearly phrased with business value stated.
2. Acceptance criteria are clearly defined in BDD format.
3. Dependencies (APIs, designs, database schemas) are identified and unblocked.
4. Story points are estimated by the engineering team.
5. Test scenarios including edge cases are agreed upon.

#### Definition of Done (DoD)
A user story is Done when:
1. All functional acceptance criteria are verified and passing.
2. Code is reviewed and approved via Pull Request by at least one peer.
3. Unit test coverage meets or exceeds 80% for business logic.
4. End-to-End or manual smoke tests succeed on staging.
5. No unresolved High or Critical severity bugs remain.
6. Documentation and API contracts are updated in `Lab_Agile/docs/`.
7. Code is merged into the `main` branch.

---

## 2. Epics & User Stories

```
+-----------------------------------------------------------------------------------+
|                            Easy Exchange Epic Hierarchy                           |
+-----------------------------------------------------------------------------------+
|  Epic 1: Currency Rate Comparison                                                 |
|    - US-01: Side-by-Side Rate Grid                                                |
|    - US-02: Sort & Filter Options                                                 |
|  Epic 2: Best Rate Finder & Recommendation                                        |
|    - US-03: Visual Highlighting of Best Rates                                     |
|    - US-04: Rate Freshness & Stale Warnings                                       |
|  Epic 3: Interactive Currency Calculator                                          |
|    - US-05: Real-time Multi-Shop Calculation                                      |
|    - US-06: Reverse / Target Conversion                                           |
|    - US-07: Potential Savings Display                                             |
|  Epic 4: Exchange Shop Locator & Map                                              |
|    - US-08: Interactive Map with Location Pins                                    |
|    - US-09: Geolocation & Distance Sorting                                        |
|    - US-10: Branch Detail Card & Directions                                       |
|  Epic 5: Administration & Rate Management                                         |
|    - US-11: Authenticated Rate Publishing                                         |
|    - US-12: Rate Change Audit Logging                                             |
+-----------------------------------------------------------------------------------+
```

---

### Epic 1: Currency Rate Comparison

#### User Story US-01: Side-by-Side Rate Comparison Matrix
> **As a** student or international traveler,  
> **I want to** view foreign exchange rates from multiple exchange shops side-by-side in a single table,  
> **So that** I don't have to waste time visiting multiple websites or physical counters.

* **Scenario 1: Default Comparison View**
  * **Given** a user navigates to the Easy Exchange homepage,
  * **When** the page finishes loading,
  * **Then** the table displays at least 5 major exchange shops (e.g., SuperRich, Vasu, Siam Exchange),
  * **And** shows the default currency pair (USD to THB),
  * **And** displays columns for: Shop Name, Branch Location, Buy Rate, Sell Rate, Spread, and Last Updated.

* **Scenario 2: Changing Currency Pair**
  * **Given** the user is viewing the comparison table,
  * **When** the user selects "EUR" from the currency dropdown,
  * **Then** the table re-renders within 300 ms showing EUR to THB rates for all participating shops,
  * **And** formatting adheres to standard 2-4 decimal places (e.g., `38.25`).

---

#### User Story US-02: Sorting and Filtering Shops
> **As a** budget-conscious user,  
> **I want to** sort the exchange shops by the most favorable rate or distance,  
> **So that** I can immediately identify where I get the most value.

* **Scenario 1: Sorting by Highest Buy Rate**
  * **Given** a user is selling USD to buy THB,
  * **When** the user clicks the "Buy Rate" column header,
  * **Then** the table sorts rows in descending order (highest payout first),
  * **And** displays an upward sorting indicator arrow.

* **Scenario 2: Filtering by Open Counters Only**
  * **Given** a user is searching for money exchange at 19:30 on a Sunday,
  * **When** the user toggles the "Open Now" filter switch,
  * **Then** shops whose operating hours indicate they are currently closed are filtered out,
  * **And** a count of active shops (e.g., "Showing 4 of 12 locations") is displayed.

---

### Epic 2: Best Rate Finder & Recommendation

#### User Story US-03: Visual Highlighting of Best Rates
> **As a** user in a hurry,  
> **I want to** clearly see which shop offers the best rate at a glance,  
> **So that** I can make a quick decision without scanning every single number.

* **Scenario 1: Best Rate Badge Rendering**
  * **Given** the comparison table has loaded multiple shop rates,
  * **When** the rates are evaluated by the recommendation engine,
  * **Then** the shop offering the maximum THB payout for the selected pair is badged with a green "Best Rate" tag,
  * **And** the corresponding row or card is highlighted with a subtle accent border.

* **Scenario 2: Equal Best Rates Handling**
  * **Given** two or more shops offer the identical highest rate,
  * **When** the recommendation engine renders,
  * **Then** both shops are labeled with the "Best Rate" badge,
  * **And** secondary sorting prioritizes the shop closest in geographical distance to the user.

---

#### User Story US-04: Rate Freshness & Stale Rate Warning
> **As a** customer,  
> **I want to** know when the exchange rates were last updated,  
> **So that** I do not rely on obsolete rates that might have changed at the counter.

* **Scenario 1: Recently Updated Rates**
  * **Given** a shop updated its rate sheet 2 hours ago,
  * **When** the user views the shop card,
  * **Then** the timestamp indicates "Updated 2 hours ago" in neutral or green text.

* **Scenario 2: Stale Rates (> 24 hours)**
  * **Given** a shop has not updated its rates in over 24 hours,
  * **When** the user views the comparison grid,
  * **Then** an amber warning icon appears beside the rate with tooltip: "Rate not updated in > 24 hours; verify in store",
  * **And** this shop is deprioritized from the default "Best Rate" badge.

---

### Epic 3: Interactive Currency Calculator

#### User Story US-05: Real-Time Multi-Shop Calculation
> **As a** foreign student with $350 USD,  
> **I want to** enter my exact dollar amount into a calculator,  
> **So that** I see exactly how many Baht I will receive at each shop.

* **Scenario 1: Dynamic Recalculation as User Types**
  * **Given** the user is on the Calculator tab,
  * **When** the user enters `350` into the input field,
  * **Then** every shop's expected total updates instantly (e.g., `350 × 36.40 = 12,740.00 THB`),
  * **And** no page reload or manual "Calculate" button click is required.

* **Scenario 2: Negative or Invalid Input**
  * **Given** the calculator input field,
  * **When** the user types negative numbers (`-50`), letters (`abc`), or special characters,
  * **Then** the input field displays an inline validation message: "Please enter a valid positive number",
  * **And** the calculation output remains at `0.00`.

---

#### User Story US-06: Bidirectional Conversion Mode
> **As a** traveler who needs exactly 10,000 THB for accommodation,  
> **I want to** input my target currency amount,  
> **So that** I know how many US Dollars or Euros I need to bring to the counter.

* **Scenario 1: Reverse Calculation Mode**
  * **Given** the user switches calculation mode to "I need THB",
  * **When** the user enters `10,000 THB`,
  * **Then** the system divides by each shop's sell rate,
  * **And** displays the exact foreign currency needed (e.g., `$274.73 USD`), rounded to standard currency increments.

---

#### User Story US-07: Potential Savings Calculation
> **As a** budget-conscious student,  
> **I want to** see the total difference between the best rate and the worst/average rate,  
> **So that** I know how much money I save by choosing the best shop.

* **Scenario 1: Displaying Net Savings**
  * **Given** a user inputs $1,000 USD to exchange to THB,
  * **When** the calculation completes,
  * **Then** a banner displays: *"By choosing SuperRich over Airport Kiosk, you save 1,450 THB ($40 USD)"*.

---

### Epic 4: Exchange Shop Locator & Map Integration

#### User Story US-08: Interactive Map with Location Pins
> **As a** tourist walking around Bangkok,  
> **I want to** see exchange shops displayed on an interactive map,  
> **So that** I can easily find which shop is on my walking route.

* **Scenario 1: Map Initialization**
  * **Given** the user navigates to the "Shop Map" view,
  * **When** the map loads,
  * **Then** an interactive Leaflet/Mapbox canvas is rendered,
  * **And** pins represent physical branch locations,
  * **And** pins are color-coded (e.g., Green for Best Rate shop, Blue for standard verified shops).

---

#### User Story US-09: Geolocation & Distance Calculation
> **As a** mobile user,  
> **I want the** app to detect my location and sort shops by distance,  
> **So that** I don't have to travel unnecessarily far for a marginally better rate.

* **Scenario 1: User Grants Geolocation Permission**
  * **Given** the user clicks "Locate Me",
  * **When** the browser prompts for location and the user clicks "Allow",
  * **Then** a blue marker indicates the user's current position on the map,
  * **And** shop cards display distance in kilometers (e.g., "0.4 km away"),
  * **And** the list can be sorted by proximity.

* **Scenario 2: User Denies Geolocation Permission**
  * **Given** the user clicks "Locate Me",
  * **When** the user clicks "Block" or "Deny",
  * **Then** the app does not crash or freeze,
  * **And** displays a friendly banner: *"Location access disabled. Showing all city branches."*,
  * **And** defaults the map view to the city center (e.g., Siam / Central Bangkok).

---

#### User Story US-10: Shop Detail Card & Directions Link
> **As a** traveler,  
> **I want to** view detailed opening hours, telephone number, and click for directions,  
> **So that** I don't walk to a closed shop or get lost.

* **Scenario 1: Viewing Shop Details**
  * **Given** a user clicks a map pin or shop list item,
  * **When** the detail panel opens,
  * **Then** it shows the branch name, full street address, landmark notes, today's operating hours (e.g., `09:00 - 18:00`), and counter phone number.

* **Scenario 2: Launching Navigation**
  * **Given** the shop detail panel is open,
  * **When** the user clicks "Directions",
  * **Then** the application opens an external URL linking directly to Google Maps or Apple Maps with coordinates pre-populated.

---

### Epic 5: Administration & Rate Management

#### User Story US-11: Authenticated Rate Publishing
> **As an** exchange shop manager or system administrator,  
> **I want to** securely log in and update daily exchange rates,  
> **So that** customers see accurate, current pricing.

* **Scenario 1: Successful Rate Update**
  * **Given** an authenticated shop operator is logged in,
  * **When** they update the buy rate for USD to `36.50` and click "Publish",
  * **Then** the database updates immediately,
  * **And** the `last_updated` timestamp reflects the current time,
  * **And** public users see the new rate on their next fetch.

* **Scenario 2: Unauthorized Rate Change Attempt**
  * **Given** an unauthenticated client sends a `PUT /api/v1/rates`,
  * **When** the request lacks a valid JWT bearer token,
  * **Then** the API responds with HTTP status `401 Unauthorized`,
  * **And** no database records are modified.

---

#### User Story US-12: Rate Change Audit Trail
> **As a** system administrator,  
> **I want an** automated audit log for every rate alteration,  
> **So that** accidental or fraudulent rate inputs can be traced and corrected.

* **Scenario 1: Audit Log Generation**
  * **Given** any rate modification event,
  * **When** the database transaction completes,
  * **Then** an entry is written to `rate_history` storing: `shop_id`, `currency_code`, `old_rate`, `new_rate`, `modified_by`, and `timestamp`.

---

## 3. Acceptance Sign-off Matrix

| Story ID | Epic Title | Test Automation Type | Status | Verified By |
| :--- | :--- | :--- | :--- | :--- |
| **US-01** | Side-by-Side Comparison Grid | Automated E2E (Playwright) | Approved | Rowan (Tech Lead) |
| **US-02** | Sorting & Filtering | Unit / Integration (Jest) | Approved | Flexx (Backend) |
| **US-03** | Visual Best Rate Badge | Component Test (React Testing Library) | Approved | Rowan (Frontend) |
| **US-04** | Rate Freshness & Stale Warnings | Integration Test | Approved | Flexx (Backend) |
| **US-05** | Real-time Multi-Shop Calculator | Unit Test (Pure Functions) | Approved | Rowan (Frontend) |
| **US-06** | Reverse Currency Calculation | Unit Test (Math Edge Cases) | Approved | Flexx (Backend) |
| **US-07** | Potential Savings Display | Component Test | Approved | Avax (Product Owner) |
| **US-08** | Interactive Map with Pins | Visual E2E Test | Approved | Rowan (Frontend) |
| **US-09** | Geolocation & Proximity | Browser Mock Test | Approved | Rowan (Frontend) |
| **US-10** | Branch Details & Navigation | Component & Deep Link Test | Approved | Avax (Product Owner) |
| **US-11** | Authenticated Rate Publishing | API Security Test (Postman/Supertest) | Approved | Flexx (Backend) |
| **US-12** | Rate Change Audit Trail | Database Transaction Test | Approved | Flexx (Backend) |
