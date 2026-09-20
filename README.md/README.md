# Easy Exchange 💱
### Currency Exchange Comparison Web App

> **Design Thinking to Agile Development Lab Project**  
> An open-source web application designed to help international students and travelers compare currency exchange rates, calculate payouts, and locate nearby exchange counters effortlessly.

---

## 👥 Project Team

| Member Name | Student ID | Nickname | Role |
| :--- | :--- | :--- | :--- |
| **Ye Zayar Aung** | `6705140012` | Avax | Product Owner / Project Lead |
| **Paing Thu Kha Kyaw** | `6705140018` | Flexx | Scrum Master / Backend Lead |
| **Aung Chan Myae** | `6705140035` | Rowan | Tech Lead / Frontend Lead |

---

## 📖 Project Documentation Index

All core project governance, specification, testing, and architecture documentation can be found in the [`docs/`](./docs) directory:

1. 📋 **[Project Charter](./docs/project_charter.md)**
   * Executive summary, problem definition, SMART objectives, project scope (in-scope vs out-of-scope), stakeholder analysis, team responsibilities, and Agile milestone roadmap.

2. 📐 **[Software Requirements Specification (SRS)](./docs/requirements_specification.md)**
   * Complete functional requirements (rate comparison matrix, dynamic calculator, best rate recommendation, map finder, vendor portal) and non-functional requirements (performance, security, usability, WCAG accessibility).

3. ✅ **[Acceptance Criteria & User Stories](./docs/acceptance_criteria.md)**
   * Persona-based Agile user stories with testable Acceptance Criteria written in BDD Gherkin (`Given-When-Then`) format, Definition of Ready (DoR), and Definition of Done (DoD).

4. 🗄️ **[Database Design Specification](./docs/database_design.md)**
   * Entity-Relationship (ER) diagram, complete data dictionary, indexing and spatial query optimization strategies, production-grade PostgreSQL DDL scripts, and initial seed fixtures.

---

## 💡 Problem & Solution Summary

### The Problem
* **Rate Comparison Difficulty:** Exchange shops post rates independently; students and travelers struggle to compare them.
* **Calculation Confusion:** Buy/sell spreads and bill denomination policies make manual calculations prone to costly errors.
* **Finding Convenient Locations:** Users often resort to poor airport or hotel exchange rates simply because they cannot find nearby competitive counters.
* **Time Consumption:** Manually checking multiple physical stalls or separate websites wastes valuable time.

### The Solution: Easy Exchange
* **Side-by-Side Rate Comparison:** Transparent, real-time comparison of buy and sell rates across top providers (SuperRich, Vasu, Siam Exchange, etc.).
* **Dynamic Currency Calculator:** Real-time conversion simulator showing exact payouts across each shop.
* **Best Rate Finder:** Automated algorithm tagging the best value counter.
* **Interactive Map Finder:** Geolocation-enabled map displaying physical shop locations, walking distance, opening hours, and one-click navigation directions.

---

## 🛠️ Architecture & Tech Stack

```
[ Frontend (PWA / SPA) ]
   - React / Next.js / Tailwind CSS
   - Leaflet / Mapbox GL (Interactive Mapping)
          │
          ▼ (REST / HTTPS)
[ Backend API ]
   - Node.js / Express / TypeScript (or FastAPI)
   - JWT Authentication (RBAC)
          │
          ▼
[ Database & Storage ]
   - PostgreSQL 15+ (Spatial Lat/Lng Indexing)
   - In-Memory Cache (Redis)
```

---

## 🚀 Repository Structure

```text
Lab_Agile/
├── README.md                          # Project overview and entry point
└── docs/                              # Formal agile documentation
    ├── README.md                      # Documentation index
    ├── project_charter.md             # Project Charter & Governance
    ├── requirements_specification.md  # Software Requirements Specification (SRS)
    ├── acceptance_criteria.md         # BDD User Stories & Acceptance Criteria
    └── database_design.md             # ER Diagram, Data Dictionary & DDL
```

---

## 📄 License & Attribution
Academic project developed for the Software Engineering / Agile Development Lab. Distributed under the [MIT License](LICENSE).
