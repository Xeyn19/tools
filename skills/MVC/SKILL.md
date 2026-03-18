---
name: mvc-layout-scaffold
description: Scaffold or recreate the MVC backend layout used in this repo (backend/config/db.js, backend/middleware/authmiddleware.js, backend/utils/token.js, backend/routes/index.js, backend/app.js, backend/server.js). Use when a user wants to generate the same MVC structure automatically in a new project or restore missing backend folders/files.
---

# MVC Layout Scaffold

## Quick Start
- Create the `backend/` folder with `config/`, `middleware/`, `model/`, `controller/`, `utils/`, and `routes/` subfolders.
- Add `config/db.js`, `middleware/authmiddleware.js`, `utils/token.js`, and `routes/index.js` using the project templates.
- Add `app.js` and `server.js` for the Express app and server bootstrap.
- Verify import paths from your server entry point and adjust if your structure differs.

## Target Structure
```
backend/
  config/
    db.js
  middleware/
    authmiddleware.js
  model/
  controller/
  utils/
    token.js
  routes/
    index.js
  app.js
  server.js
```

## Workflow
1. Create the folder tree under `backend/`.
2. Populate each file using the current repo versions as the baseline.
3. Add domain modules under `model/` and `controller/` as needed.
4. Update any relative imports to match the host app structure.
5. Confirm environment variables and dependencies are present.

## File Content Guidance
- `backend/config/db.js`: MySQL connection pool + `testConnection` helper.
- `backend/middleware/authmiddleware.js`: verify Bearer token and attach `req.user`.
- `backend/utils/token.js`: access/refresh token helpers with env-based secrets.
- `backend/routes/index.js`: compose route modules (`/recipes`, `/auth`, `/register`, `/login`, `/jobs`, `/dashboard`, `/profile`).
- `backend/app.js`: Express app with CORS, JSON parsing, static uploads, `/api` router mount.
- `backend/server.js`: start server, call `testConnection`, and log listening URL.

## Integration Checks
- Ensure `backend/app.js` imports the router from `backend/routes/index.js`.
- Ensure `backend/server.js` imports `testConnection` from `backend/config/db.js`.
- Ensure `backend/middleware/authmiddleware.js` imports token helpers from `backend/utils/token.js`.
- Verify `ACCESS_TOKEN_SECRET`, `REFRESH_TOKEN_SECRET`, DB env vars exist.
- Install deps: `express`, `cors`, `mysql2`, `jsonwebtoken`, `dotenv`.

## Review Checklist
- Folder structure matches target structure.
- All imports resolve with your app paths.
- Tokens and DB connection load from environment.
- Router mounts correctly under `/api`.
- Server starts and logs the listening URL.