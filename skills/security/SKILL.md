---
name: sql-injection-prevention
description: Prevent SQL injection by enforcing prepared statements and parameterized queries, safe dynamic SQL patterns, and input validation across backend codebases. Use when auditing or updating database query code (raw SQL, query builders, ORMs), API endpoints, or data-access layers that touch SQL.
---

# SQL Injection Prevention

## Quick Start
- Replace string-concatenated SQL with parameterized queries.
- Ensure every user-controlled value is passed as a bound parameter.
- For dynamic identifiers (table/column/order), use strict allowlists, never parameters.

## Workflow
1. Inventory query entry points (DAO/repository layers, route handlers, services).
2. Identify any SQL strings built with concatenation or template literals.
3. Convert each query to prepared statements or parameterized APIs provided by the DB driver or ORM.
4. For dynamic SQL (filters, order, pagination), use allowlists and safe builders.
5. Add tests that attempt injection and confirm safe behavior.

## Required Patterns
- Use placeholders (`?`, `$1`, `:name`) with separate parameter arrays/objects.
- Never interpolate user input directly into SQL strings.
- Avoid `SELECT ... WHERE id IN (${ids})`; use array parameters or build placeholders from validated arrays.
- Keep multi-statement execution disabled unless explicitly required.

## Safe Dynamic SQL
- Identifiers (table/column): map input to known constants via allowlists.
- ORDER BY: map `sort` and `direction` to allowed pairs.
- LIMIT/OFFSET: pass as numeric parameters; validate and clamp.
- LIKE: escape wildcard characters or use parameterized patterns with `ESCAPE`.

## ORM / Query Builder Guidance
- Prefer ORM/query-builder methods over raw SQL.
- If raw SQL is required, use the ORM's parameter binding API.
- Do not use manual escaping as a substitute for parameters.

## Red Flags
- String concatenation or template literals building SQL.
- Manual escaping functions used instead of parameters.
- Unbounded `IN (...)` lists or unvalidated `ORDER BY` inputs.
- DB users with excessive privileges.

## Testing Checklist
- Attempt classic payloads (`' OR 1=1 --`, `"; DROP TABLE ...`).
- Verify that payloads are treated as data (no query structure change).
- Add regression tests for endpoints with filters and sorting.

## Review Checklist
- Every SQL execution uses bound parameters.
- All dynamic identifiers are allowlisted.
- No raw string SQL with user input.
- Input validation exists for pagination, sorting, and filtering.
- Least-privilege DB credentials are used.