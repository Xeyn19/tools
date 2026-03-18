# Tools

A small collection of frontend and backend building blocks for a job-tracking style app, plus Codex skills for common workflows.

**Contents**
- `app_react/`: React Router app shell and layout (sidebar + topbar).
- `context/`: Auth provider, protected route gate, and theme toggle.
- `middleware/`: Express auth middleware and JWT helpers.
- `MVC/`: MySQL connection pool and API route registry.
- `server_app/`: Express app and server bootstrap.
- `skills/`: Codex skills (`security/`, `responsive/`, `MVC/`).

**Skills**
- `skills/security/SKILL.md`: SQL injection prevention workflow (prepared statements, allowlists, tests).
- `skills/responsive/SKILL.md`: Responsive design guidance for layouts, typography, and media.
- `skills/MVC/SKILL.md`: MVC backend scaffold structure and integration checks.

**Required Helpers And Dependencies**
This repo contains snippets only. You will need to supply the surrounding project and dependencies.
- React app with `react-router-dom`.
- Backend with `express`, `cors`, `mysql2`, `jsonwebtoken`, and `dotenv`.
- Client helpers used by the auth context: `authenticatedFetch`, `getAccessToken`, `getStoredUser`, `saveAuthSession`, `updateStoredUser`, `clearAuthSession`.
- API route modules referenced by `MVC/routes/index.js`.

**Environment Variables**
- `ACCESS_TOKEN_SECRET`, `REFRESH_TOKEN_SECRET`
- `ACCESS_TOKEN_EXPIRES_IN` (default `15m`), `REFRESH_TOKEN_EXPIRES_IN` (default `7d`)
- `DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `DB_PORT`
- `PORT` (default `8000`)

**Wiring Notes**
- `server_app/app.js` expects the API router at `./routes/index.js`. In this repo it lives at `MVC/routes/index.js`. Move it or update the import to match your structure.
- `middleware/authmiddleware/authmiddleware.js` imports `../utils/token.js`. In this repo, the JWT helpers live at `middleware/JWT/token.js`. Update the import to your structure.
