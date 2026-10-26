# Feature Specifications

Spec-driven development (SDD) source of truth for **this** application.  
No application code may be written unless it maps to a requirement in one of these files.

**Methodology:** [framework.md](./framework.md) — how to write, trace, and ship feature specs.  
**Student guide (requirements):** [writing-feature-requirements.md](./writing-feature-requirements.md) — stories, FRs, initial data model, Gherkin AC.  
**Student guide (design):** [writing-feature-design.md](./writing-feature-design.md) — ownership, API, screens, test map, DoD, out of scope.  
**Student guide (living reference):** [reference/writing-living-reference.md](./reference/writing-living-reference.md) — update api / data-model / behavior in the same PR.

*(Examples in the writing guides often cite the OC CS Speckit Todo sample app — use them as patterns for your product.)*

**Sprints** live in your agile tool — they are **not** part of these specs.

## Feature catalog

Warehouse operations (this is the flow Copilot asked for): **supplier ordering (N08)** → **receiving (N11)** → **put away (N12)** → **store/retailer orders (N09)** → **picking (N13)** → **shipping (N14)** → **delivery (N15)** / **route (N10)**.

| ID | File | Branch | Depends on |
|----|------|--------|------------|
| N20 | [feature_20_authentication.md](feature_20_authentication.md) | `feature/20-authentication` | — |
| N01 | [feature_01_Company_maintinence.md](feature_01_Company_maintinence.md) | `feature/1-company` | — |
| N02 | [feature_02_Warehouse__maintinence.md](feature_02_Warehouse__maintinence.md) | `feature/2-warehouse` | Company |
| N03 | [feature_03_Supplier__maintinence.md](feature_03_Supplier__maintinence.md) | `feature/3-supplier` | Company |
| N04 | [feature_04_Items__maintinence.md](feature_04_Items__maintinence.md) | `feature/4-items` | Inventory |
| N05 | [feature_05_Inventory__maintinence.md](feature_05_Inventory__maintinence.md) | `feature/5-inventory` | Warehouse, Items |
| N06 | [feature_06_Employee__maintinence.md](feature_06_Employee__maintinence.md) | `feature/6-employee` | Company |
| N07 | [feature_07_Customer__maintinence.md](feature_07_Customer__maintinence.md) | `feature/7-customer` | Company |
| N08 | [feature_08_Supplier_order_Management.md](feature_08_Supplier_order_Management.md) | `feature/8-supplier-order` | Supplier, Inventory, Items |
| N09 | [feature_09_Customer_Order_Management.md](feature_09_Customer_Order_Management.md) | `feature/9-customer-order` | Customer, Inventory, Items |
| N10 | [feature_10_route_maintenence.md](feature_10_route_maintenence.md) | `feature/10-route` | Customer Order, Customer, Deliver |
| N11 | [feature_11_receiving.md](feature_11_receiving.md) | `feature/11-receiving` | Supplier, Supplier Order, Items |
| N12 | [feature_12_put_away.md](feature_12_put_away.md) | `feature/12-put-away` | Warehouse, Items, Inventory, Supplier Order, Receiving |
| N13 | [feature_13_picking.md](feature_13_picking.md) | `feature/13-picking` | Warehouse, Items, Inventory, Customer Order |
| N14 | [feature_14_ship_customer_order.md](feature_14_ship_customer_order.md) | `feature/14-ship-customer-order` | Customer Order, Picking, Customer |
| N15 | [feature_15_deliver_customer_order.md](feature_15_deliver_customer_order.md) | `feature/15-deliver-customer-order` | Ship, Customer Order, Customer |
| N16 | [feature_16_out_of_stock.md](feature_16_out_of_stock.md) | `feature/16-out-of-stock` | Items, Inventory |
| N17 | [feature_17_supplier_did_not_ship.md](feature_17_supplier_did_not_ship.md) | `feature/17-supplier-did-not-ship` | Supplier, Supplier Order, Receiving |
| N18 | [feature_18_delivery_does_not_match_ship.md](feature_18_delivery_does_not_match_ship.md) | `feature/18-delivery-does-not-match-ship` | Ship, Deliver, Route, Customer Order |
| N19 | [feature_19_monthly_shipping_quantities.md](feature_19_monthly_shipping_quantities.md) | `feature/19-monthly-shipping-quantities` | Ship, Items |

New features: follow [framework.md](./framework.md#feature-spec-template) — **Status**, **Input**, **FR-00N**, **SC-00N**, **Key Entities**, Gherkin, **Agent implementation request**, **Definition of Done**.

**Branch roles:** `main` = scaffold-only starter kit · `dev` = integration · `feature/N-*` = feature work (branch from `dev`).

## Living reference

Keep snapshots in sync when schema, API, or product rules change — **in the same PR as implementation** (required DoD; see [Merge checklist + Agility sync](./framework.md#merge-checklist--agility-sync)). Each `feature-N-*.md` includes an **Agent implementation request** block so Cursor updates reference during implementation ([framework.md](./framework.md#agent-implementation-request)). Spec evolution after merge: [prefer a new feature delta](./framework.md#spec-evolution-after-merge).

| File | Purpose |
|------|---------|
| [reference/README.md](./reference/README.md) | How to maintain reference docs |
| [reference/writing-living-reference.md](./reference/writing-living-reference.md) | Student guide — writing/updating living reference |
| [reference/data-model.md](./reference/data-model.md) | Current database tables (update in feature PR when schema changes) |
| [reference/api.md](./reference/api.md) | Current REST API (update in feature PR when API changes) |
| [reference/behavior.md](./reference/behavior.md) | Current product rules (update in feature PR when rules change) |

## Related

- Cursor rules: `.cursor/rules/`
- ADRs: `docs/adr/`
- Quality attributes (NFRs): `docs/nfr/`
- Starter kit notes: `docs/STARTER-KIT.md`
