# ADR-0002: Warehouse owns records (not company_id on every table)

**Status:** Accepted  
**Date:** 2026-11-17  
**Deciders:** Fidele Hakizimana

## Context

N01 allows more than one company record. That can look like a multi-company product, which would put `company_id` on almost every table. This app is for Fidele Warehouse Co. Stock, orders, and routes belong to a warehouse, not to a tenant company on every row.

## Decision

- `company_id` lives on company, warehouse, and user (and employee where the spec already has it).
- `company_id` is **not** copied onto supplier, item, inventory, orders, receive, put away, pick, route, ship, or deliver.
- Supplier orders and customer orders store **`warehouse_id`**.
- One running system. Warehouse Manager works in that warehouse’s data.

## Consequences

### Positive
- Tables stay smaller.
- It is clear which warehouse an order is for.

### Negative / tradeoffs
- This is not a SaaS product where every table is filtered by company.

## Alternatives considered

| Option | Why not |
|--------|---------|
| `company_id` on every table | We are not building multi-company SaaS |
| No warehouse on orders | Then receive, pick, and stock cannot tell which building |

## Related artifacts

- Features: N01, N02, N08, N09, N10
- Quality: security / ownership in `docs/nfr/quality-attributes.md`
