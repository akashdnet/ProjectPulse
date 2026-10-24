# ProjectPulse (Monorepo)

A fullstack application for student project submission and mentor review dashboard.

---

## 📁 Repository Structure

```text
Project-Puls/
├── client/                     # Next.js 15 Frontend (App Router, Tailwind CSS, TypeScript)
│   ├── src/
│   ├── package.json
│   ├── vercel.json
│   └── .env.example
├── server/                     # Express & Prisma Backend (TypeScript, PostgreSQL)
│   ├── src/
│   ├── prisma/
│   ├── api/
│   ├── package.json
│   ├── vercel.json
│   └── .env.example
├── .gitignore
├── package.json                # Root package.json with unified execution scripts
└── README.md                   # Monorepo documentation & setup guide
```

---

## 🚀 Getting Started (Local Development)

### 1. Install All Dependencies
To install dependencies for root, client, and server in one go:
```bash
npm run install:all
```

Or manually:
```bash
# In client
cd client && npm install

# In server
cd server && npm install
```

### 2. Environment Setup

* **Server Environment (`server/.env`):**
  ```env
  DATABASE_URL="postgresql://user:password@host:5432/dbname?sslmode=require"
  PORT=5000
  JWT_SECRET="your_jwt_secret_key"
  JWT_EXPIRES_IN="7d"
  CORS_ORIGIN="http://localhost:3000"
  ```

* **Client Environment (`client/.env.local`):**
  ```env
  NEXT_PUBLIC_API_URL="http://localhost:5000/api/v1"
  ```

### 3. Run Development Servers (From Root)

You can run both frontend and backend concurrently or run them individually from the root directory:

| Command | Action |
| :--- | :--- |
| `npm run dev` | Runs **both** Backend and Frontend concurrently |
| `npm run dev:server` | Runs **Backend only** (`http://localhost:5000`) |
| `npm run dev:client` | Runs **Frontend only** (`http://localhost:3000`) |
| `npm run build` | Builds both backend and frontend for production |

---

## 🌐 Deploying to Vercel (Step-by-Step)

Because this repository is a **Monorepo**, you will create **two projects** in Vercel from this single GitHub repository.

---

### Step 1: Deploy Backend (`server`) to Vercel

1. Go to your [Vercel Dashboard](https://vercel.com/) and click **"Add New..." > "Project"**.
2. Select your GitHub repository (`Project-Puls`) and click **Import**.
3. **Configure Project:**
   * **Project Name:** `project-pulse-server` (or your preferred name)
   * **Root Directory:** Click **Edit** and select **`server`**.
   * **Framework Preset:** Select **Other**.
4. **Environment Variables:**
   Add your production variables:
   * `DATABASE_URL`: Your hosted PostgreSQL connection string (Neon / Supabase).
   * `JWT_SECRET`: A strong secret key.
   * `JWT_EXPIRES_IN`: e.g., `7d`
   * `CORS_ORIGIN`: `*` (or your frontend Vercel domain once deployed).
5. Click **Deploy**.
6. Once deployed, note down the deployed API URL (e.g., `https://project-pulse-server.vercel.app`).

---

### Step 2: Deploy Frontend (`client`) to Vercel

1. In Vercel Dashboard, click **"Add New..." > "Project"** again.
2. Select the **same GitHub repository** (`Project-Puls`) and click **Import**.
3. **Configure Project:**
   * **Project Name:** `project-pulse-client`
   * **Root Directory:** Click **Edit** and select **`client`**.
   * **Framework Preset:** **Next.js** (auto-detected).
4. **Environment Variables:**
   * `NEXT_PUBLIC_API_URL`: Your backend Vercel URL with API path, e.g.:
     ```
     https://project-pulse-server.vercel.app/api/v1
     ```
5. Click **Deploy**.
6. Your Next.js frontend is now live!

---

## 🌿 Git Branches

* **`main`**: Production-ready monorepo containing both `client/` and `server/`.
* **`backend`**: Dedicated branch containing backend implementation commits.
* **`frontend`**: Dedicated branch containing frontend implementation commits.
