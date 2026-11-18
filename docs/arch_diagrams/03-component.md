# C4 Level 3 — API components

Inside the Express API. Groups follow the [feature catalog](../../features/README.md) build order, not extra modules.

```mermaid
C4Component
title Warehouse Management System — API components

Container_Boundary(api, "API (Express)") {
    Component(auth, "Auth", "N20", "Login, logout, forgot password, add user. Issues Bearer tokens. Role checks.")
    Component(setup, "Setup", "N01–N07", "Company, warehouse, employee, supplier, items, inventory, customer (retailer records).")
    Component(inbound, "Inbound", "N08, N11, N12", "Supplier order → receive supplier goods → put away. Inventory goes up on put away.")
    Component(outbound, "Outbound", "N09, N13, N10, N14, N15", "Record store order → pick → route → ship → deliver. Inventory goes down on pick. Retailer does not call these APIs.")
    Component(reports, "Reports", "N16–N19", "Out of stock, supplier did not ship, delivery does not match ship, monthly shipping. View only.")
}

ContainerDb(db, "MySQL", "Tables named in each feature Data Model")
Container(web, "Web app", "Vue screens call /api")

Rel(web, auth, "POST /api login, users")
Rel(web, setup, "CRUD /api company, warehouses, …")
Rel(web, inbound, "/api supplier-orders, receives, put-aways")
Rel(web, outbound, "/api customer-orders, picks, routes, ships, deliveries")
Rel(web, reports, "GET report routes")
Rel(auth, db, "Users")
Rel(setup, db, "Setup tables")
Rel(inbound, db, "Inbound tables + inventory")
Rel(outbound, db, "Outbound tables + inventory")
Rel(reports, db, "Read stock, receive, ship, deliver")
```

## Operational flow (same as the catalog)

```mermaid
flowchart LR
  subgraph inbound [Inbound]
    SO[Supplier order N08]
    R[Receive N11]
    PA[Put away N12]
    SO --> R --> PA
  end
  subgraph outbound [Outbound]
    CO[Record store order N09]
    PK[Pick N13]
    RT[Route N10]
    SH[Ship N14]
    DL[Deliver N15]
    CO --> PK --> RT --> SH --> DL
  end
  PA -->|stock up| INV[Inventory N05]
  PK -->|stock down| INV
```

## What this level does not decide

Column choices such as supplier number, warehouse on an order, order lines, or stores on a route belong in the feature Data Model. This diagram only changes if a new system or container is added.
