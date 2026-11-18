# ADR-0003: Bearer login, three roles, no retailer or supplier login

**Status:** Accepted  
**Date:** 2026-11-17  
**Deciders:** Fidele Hakizimana

## Context

Stores send orders and suppliers send goods, but this product is the warehouse system only. Login must be simple and match N20.

## Decision

- Login is email + password. The API uses **Bearer** tokens.
- Roles that can log in: **System Administrator**, **Warehouse Manager**, **Employee Manager**.
- Names like Purchasing Agent or Procurement Manager in older text mean **Warehouse Manager**.
- Retailers and suppliers do **not** get accounts. The warehouse records store orders (N09) and supplier receive (N11).

## Consequences

### Positive
- One auth model.
- No store portal or supplier portal to build.

### Negative / tradeoffs
- A store cannot look up its own order in this app.

## Alternatives considered

| Option | Why not |
|--------|---------|
| Retailer login | Out of scope; N09 is warehouse-recorded |
| Supplier login | Out of scope; N11 is warehouse-recorded |

## Related artifacts

- Feature: [N20 Authentication](../../features/feature_20_authentication.md)
- Cursor rules: `.cursor/rules/auth-patterns.mdc`, `.cursor/rules/security.mdc`
