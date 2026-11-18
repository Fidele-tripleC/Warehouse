# C4 Level 2 — Containers

How the system is split to run. Stack: Vue 3 + Vuetify, Express, Sequelize, MySQL.

```mermaid
C4Container
title Warehouse Management System — containers

Person(sa, "System Administrator")
Person(wm, "Warehouse Manager")
Person(em, "Employee Manager")

System_Boundary(wms, "Warehouse Management System") {
    Container(web, "Web app", "Vue 3, Vuetify 4, Axios, Vite", "Screens in the browser. Calls /api. Stores the Bearer token after login.")
    Container(api, "API", "Node, Express, Sequelize", "REST JSON. Authorization: Bearer. Errors: { message }. Ports under /api.")
    ContainerDb(db, "Database", "MySQL", "Users, company, warehouse, employees, suppliers, items, inventory, orders, receive, put away, picks, routes, ships, deliveries.")
}

System_Ext(email, "Email", "Forgot-password codes")

Rel(sa, web, "HTTPS")
Rel(wm, web, "HTTPS")
Rel(em, web, "HTTPS")
Rel(web, api, "JSON /api", "HTTPS")
Rel(api, db, "SQL", "Sequelize")
Rel(api, email, "Send reset code")
```

| Container | Lives in the repo | Notes |
|-----------|-------------------|--------|
| Web app | `frontend/` | Views, `*Services.js`, router |
| API | `backend/` | Routes, controllers, models, auth |
| Database | MySQL (`DB_NAME`) | Schema from feature Data Model sections |

Dev ports (project structure): frontend **8082**, API **3200**.
