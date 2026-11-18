# Quality attributes

App-wide non-functional targets for **this** product.

**Teaching policy:** Specs say *what* to build. This table says *how good* the system should be. Only **Accepted** rows (and feature **Requirements (FR-00N)** / **Success Criteria (SC-00N)**) constrain implementation. **Deferred** is the quality backlog / example. **Out of scope** is what not to build. See [`.cursor/rules/quality-attributes.mdc`](../../.cursor/rules/quality-attributes.mdc).

## Column meanings

| Column | Meaning |
|--------|---------|
| **Target** | Measure or bar — prefer a **number**. Illustrative until Status is **Accepted** and tests enforce it. |
| **Approach** | How the target is realized or limited |
| **Status** | **Accepted** / **Accepted (minimal)** / **Deferred** / **Out of scope** (see below) |
| **Links** | ADR (why), Cursor rule (how), code path, or **—** |

## Status values

| Status | Meaning |
|--------|---------|
| **Accepted** | In force — do not regress |
| **Accepted (minimal)** | Thin bar in force — do not expand |
| **Deferred** | Documented example — not a coding requirement unless a feature spec says so |
| **Out of scope** | Do not invent |

## Links column

| Link type | When |
|-----------|------|
| ADR | Approach decision |
| Cursor rule | Day-to-day agent/code constraint |
| Code path | Concrete implementation |
| **—** | No artifact yet |

| Attribute | Target | Approach | How we verify | Status | Links |
|-----------|--------|----------|---------------|--------|-------|
| **Security** | Protected `/api` routes need a Bearer token; only SA, WM, and Employee Manager log in | JWT/session Bearer; warehouse-scoped records ([ADR-0002](../adr/0002-warehouse-ownership.md), [ADR-0003](../adr/0003-auth-roles-no-retailer-login.md)) | Auth tests in N20; unauthorized cases in features | Accepted | [security.mdc](../../.cursor/rules/security.mdc), [auth-patterns.mdc](../../.cursor/rules/auth-patterns.mdc) |
| **Reliability** | Happy-path writes succeed in mapped Gherkin tests | Feature specs + `npm test` | | Deferred | |
| **Availability** | Single lab/demo host | One process, no cluster | | Out of scope | |
| **Performance** | Local API is fine for class demo | No cache layer | | Deferred | |
| **Observability** | Unhandled errors logged | Winston in `backend/app/config/logger.js` | Log files under `backend/logs/` | Accepted (minimal) | [logger.js](../../backend/app/config/logger.js) |
| **Usability** | Role menus after login; core path is login then warehouse work | Vue screens in `docs/ui/` | Manual screen check | Deferred | |
| **Accessibility (a11y)** | Aim readable labels on primary forms | Vuetify defaults | | Deferred | |
| **Internationalization (i18n)** | English only | | | Out of scope | |
| **Maintainability** | Gherkin mapped before merge; `npm test` green | Feature specs as source of truth | Merge checklist; `npm test` | Accepted | [framework.md](../../features/framework.md), [quality-attributes.mdc](../../.cursor/rules/quality-attributes.mdc) |

---

## Feature-local NFRs

If only one feature needs a bar:

1. Put it in that feature’s **Requirements (FR-00N)** or **Success Criteria (SC-00N)**.
2. Add Gherkin when tests must prove it.
3. Optionally link from a row here (“see Feature N **FR-00N** / **SC-00N**”).

See [feature spec template](../../features/framework.md#feature-spec-template) in the teaching repo.

---

## Changing a bar

1. Edit **Target**, **Approach**, **Status**, **Links**. Prefer a number in **Target**.
2. **Approach** change → [ADR](../adr/README.md); add to **Links**.
3. Agent coding constraint → `.cursor/rules/`; add to **Links**.
4. API/schema change → `features/reference/` in the same feature PR ([Agent implementation request](../../features/framework.md#agent-implementation-request)).
5. **Deferred** → **Accepted** only with matching verification.
