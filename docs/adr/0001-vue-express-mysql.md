# ADR-0001: Vue 3, Express, and MySQL

**Status:** Accepted  
**Date:** 2026-11-17  
**Deciders:** Fidele Hakizimana

## Context

The warehouse app needs a browser UI, a JSON API, and a relational store. The course stack is already set in the constitution.

## Decision

Use Vue 3 (Vuetify, Axios) for the web app, Node/Express/Sequelize for the API, and MySQL for data.

## Consequences

### Positive
- Matches the starter kit and lab setup.
- One browser app and one API is enough for this product.

### Negative / tradeoffs
- Not a mobile native app.
- Not a separate service per warehouse function.

## Alternatives considered

| Option | Why not |
|--------|---------|
| Separate apps per role | Extra work; one Vue app with roles is enough |
| No SQL store | Orders and stock need tables |

## Related artifacts

- Feature specs: N20–N19 in `features/`
- Cursor rules: `.cursor/rules/constitution.mdc`
