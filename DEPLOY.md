# Free deployment guide (demo setup)

Stack: **TiDB Cloud Starter** (MySQL-compatible DB) + **Render** (backend, Docker) + **Netlify / Cloudflare Pages** (frontend).
Free-tier limits change; check each provider's current plan. Free backends sleep when idle, so the first request after a pause is slow.

## 1. Database (TiDB Cloud Starter)
1. Create a free Starter cluster, then create a database named `oms_db`.
2. Copy the host, port, username and password from the "Connect" dialog.
3. JDBC URL format (TLS is required):
   `jdbc:mysql://<HOST>:4000/oms_db?sslMode=VERIFY_IDENTITY`

## 2. Backend (Render, Docker)
New > Web Service > this repo > Root Directory `backend` > Runtime **Docker** > Instance type **Free**.

Environment variables:
| Name | Value |
|---|---|
| `DB_URL` | the JDBC URL above |
| `DB_USERNAME` | TiDB username |
| `DB_PASSWORD` | TiDB password |
| `JWT_SECRET` | random string, 32+ characters |
| `CORS_ORIGIN` | your frontend URL, e.g. `https://oorderflow.netlify.app` (no trailing slash) |

## 3. Frontend (Netlify or Cloudflare Pages)
- Base/root directory: `frontend`
- Build command: `npm run build`
- Publish directory: `dist`
- Environment variable: `VITE_API_URL` = your Render backend URL (no trailing slash)

## 4. After it is live
1. Open the site and **register your own account first** - the first user becomes ADMIN.
2. Update `CORS_ORIGIN` on Render if your frontend URL changed, then redeploy.
