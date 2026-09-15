# Shwe Zhan 3D — PostgreSQL production deployment

This version replaces the Render-ephemeral `data.json` storage with PostgreSQL.

## Render
1. Push this project to GitHub.
2. In Render, create a Blueprint from the repository, or create a PostgreSQL database and a Web Service.
3. The included `render.yaml` defines both. Set `OWNER_ADMIN_PASSWORD` in Render; do not commit it.
4. Deploy the web service with `npm install` and `npm start`.
5. Health check: `/api/health`.

## Important
- Existing data in an old Render instance cannot be recreated from this source code if it was already lost by an ephemeral filesystem reset.
- If a legacy `data.json` exists beside the service at startup and the PostgreSQL database is empty, the server attempts a one-time migration.
- User accounts remain approved until an admin revokes approval.
- Each account owns its own projects; max 10 projects per account, with the oldest removed when creating the 11th.
- Owner Admin is bootstrapped from `OWNER_ADMIN_USERNAME` / `OWNER_ADMIN_PASSWORD`.
- Secrets should be stored in Render Environment Variables.
