# Template.md — API & Data Contract

> The **what**: every endpoint, payload, response/error shape, and data schema.
> Companion to [`Style.md`](./Style.md) (the *how*). Update this file **first**
> when adding or changing any endpoint or schema — code and contract must never
> drift. Both are enforced in review and by CI (`workflows/contract-check.yml`).

TODO: Replace every placeholder below with the project's real contract.

## 1. Conventions
- Base path: TODO (e.g. `/api`).
- Content type: TODO (e.g. `application/json`).
- Auth: TODO (how requests are authenticated).

## 2. Data schema
TODO: Document the locked schema. List each table/collection, its columns/fields,
types, and notes. Call out anything that must never change without team agreement,
and any field written only by the system (never by hand).

| field | type | notes |
|---|---|---|
| TODO | TODO | TODO |

## 3. Endpoints
TODO: One row per endpoint.

| Method | Route | Request | Response |
|---|---|---|---|
| GET | `/TODO` | — | `{ TODO }` |
| POST | `/TODO` | `{ TODO }` | `{ TODO }` |

### Sample payloads
TODO: For each non-trivial endpoint, give a concrete request and response example.

```http
POST /TODO
Content-Type: application/json

{ "TODO": "..." }
```
```json
{ "TODO": "..." }
```

## 4. Querying / usage standards
TODO: How clients should query (pagination, filtering, limits, sorting). Bound all
user-supplied numeric params to a sane range.

## 5. Helper / function signatures
TODO: If the project exposes shared helpers (SQL functions, RPCs, service methods),
document their exact signatures here so callers and the contract stay in sync.

| Name | Signature | Returns |
|---|---|---|
| TODO | `TODO(arg type, ...)` | TODO |

## 6. Error conventions
- All errors return one structured shape — TODO (e.g. `{ "error": "message" }`).
- Status codes: TODO (e.g. `400` bad input, `404` not found, `413` too large,
  `415` unsupported type, `500` only for truly unexpected failures).
- Never leak a stack trace to the client.
