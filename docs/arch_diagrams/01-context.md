# C4 Level 1 — System context

Who talks to the Warehouse Management System. People who **do not** get a login are outside the system.

```mermaid
C4Context
title Warehouse Management System — system context

Person(sa, "System Administrator", "Manages company records and adds users (N01, N20)")
Person(wm, "Warehouse Manager", "Runs warehouse work: stock, supplier orders, receive, put away, store orders, pick, route, ship, deliver, reports")
Person(em, "Employee Manager", "Maintains employee records (N06)")

System(wms, "Warehouse Management System", "Vue + Express + MySQL. Source of truth is the server. Auth: Bearer token.")

System_Ext(email, "Email", "Receives forgot-password codes (N20). Not a login for stores or suppliers.")
System_Ext(retailer, "Retailer store", "Sends a store order by other means. Does not log in. Warehouse records the order (N09).")
System_Ext(supplier, "Supplier company", "Sends goods. Does not log in. Warehouse records the supplier order and receive (N08, N11).")

Rel(sa, wms, "Logs in and uses Company / Add user")
Rel(wm, wms, "Logs in and uses warehouse menus")
Rel(em, wms, "Logs in and uses Employee")
Rel(wms, email, "Sends a reset code")
Rel(retailer, wm, "Sends order (outside the app)")
Rel(supplier, wm, "Sends shipment (outside the app)")
```

**Not in this picture**

- A store app or supplier portal
- GPS, drivers, or trucks as software systems
- Multi-region hosting
