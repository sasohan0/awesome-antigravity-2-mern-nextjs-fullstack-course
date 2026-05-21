# Module 10: Deployment and Production Readiness — Ship the MERN App Safely

**File Name:** `12-module-10-deployment-production-readiness.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 6–9 hours  
**Recommended After:** Module 9: Testing, Browser Verification and QA  
**Main Goal:** Deploy the full-stack MERN project, configure production environment variables, connect frontend/backend/database, run production smoke tests, fix deployment issues, and prepare a portfolio-ready submission.

---

## Module purpose

You have now planned, built, integrated, and tested your MERN app.

Now you need to deploy it.

Deployment means making the project accessible online through live URLs.

For this course, the recommended deployment stack is:

```txt
Frontend: Vercel
Backend: Render
Database: MongoDB Atlas
Repository: GitHub
```

This module teaches you how to prepare the project for production and deploy it safely.

You will learn:

- How to prepare the GitHub repository
- How to clean environment variables
- How to deploy React/Vite frontend to Vercel
- How to deploy Express backend to Render
- How to connect MongoDB Atlas to deployed backend
- How to configure CORS for deployed URLs
- How to update frontend API URL for production
- How to run production smoke tests
- How to check logs
- How to fix common deployment errors
- How to prepare final README and submission evidence
- How to avoid exposing secrets

The goal is not only to “get a link.”

The goal is to ship a project that works reliably and can be shown to recruiters, mentors, and interviewers.

---

## Deployment mindset

A deployed project must be:

```txt
Working
Secure enough for a student project
Documented
Tested
Demo-friendly
Easy to evaluate
```

Do not deploy broken work and hope nobody notices.

Your live project should allow a reviewer to:

- Open the frontend
- Register or use demo credentials
- Browse data
- Complete the main user flow
- Test admin features
- Understand the tech stack
- Read the README
- See screenshots
- Run locally if needed

---

## What you will deploy

A typical final project will have:

```txt
GitHub repository
Frontend live URL
Backend live URL
MongoDB Atlas database
README.md
.env.example files
Screenshots
Demo credentials
Deployment notes
QA signoff
```

Recommended deployment architecture:

```txt
User browser
↓
Vercel frontend
↓
Render backend API
↓
MongoDB Atlas database
```

---

## Important warning about secrets

Never commit these to GitHub:

```txt
.env
MongoDB URI
JWT secret
Database password
API keys
Private tokens
Service credentials
```

You should commit only:

```txt
.env.example
README instructions
Placeholder values
```

Bad:

```env
MONGODB_URI=mongodb+srv://realuser:realpassword@cluster.mongodb.net/app
JWT_SECRET=real_secret_key_here
```

Good:

```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/database-name
JWT_SECRET=replace_with_long_random_secret
```

---

## Deployment order

Use this order:

```txt
1. Clean repository
2. Verify local build
3. Prepare env examples
4. Push latest code to GitHub
5. Prepare MongoDB Atlas
6. Deploy backend to Render
7. Test backend live URL
8. Deploy frontend to Vercel
9. Set frontend production API URL
10. Update backend CORS CLIENT_URL
11. Run production smoke tests
12. Fix deployment bugs
13. Update README
14. Final submission
```

Do not deploy frontend first if backend API is not working.

---

# Part 1: Pre-deployment cleanup

Before deploying, clean your project.

## Root checklist

Run from project root:

```bash
git status
```

Check:

```txt
1. No unwanted files
2. No .env files staged
3. No node_modules staged
4. No dist/build folders staged unless intentionally needed
5. README exists
6. .gitignore exists
7. client/.env.example exists
8. server/.env.example exists
```

---

## Recommended root `.gitignore`

Create/update:

```txt
.gitignore
```

Content:

```gitignore
node_modules
dist
build
.env
.env.local
.env.development.local
.env.production.local
.DS_Store
.vscode/settings.json
coverage
playwright-report
test-results
```

If you use both `client/` and `server/`, this root `.gitignore` helps cover both.

---

## Local build verification

Before deployment, build locally.

Frontend:

```bash
cd client
npm install
npm run build
```

Backend:

```bash
cd server
npm install
npm run build
npm start
```

If local build fails, deployment will likely fail.

Fix local build first.

---

## Type check

If your project includes typecheck scripts:

```bash
cd client
npm run typecheck
```

```bash
cd server
npm run typecheck
```

If no typecheck script exists, add one if possible:

```json
{
  "scripts": {
    "typecheck": "tsc --noEmit"
  }
}
```

---

## Production-readiness docs

Create these docs before deployment:

```txt
docs/DEPLOYMENT_PLAN.md
docs/PRODUCTION_ENV_CHECKLIST.md
docs/DEPLOYMENT_COMMANDS.md
docs/VERCEL_DEPLOYMENT_GUIDE.md
docs/RENDER_DEPLOYMENT_GUIDE.md
docs/MONGODB_ATLAS_DEPLOYMENT_NOTES.md
docs/PRODUCTION_SMOKE_TEST_PLAN.md
docs/PRODUCTION_SMOKE_TEST_REPORT.md
docs/DEPLOYMENT_BUG_LOG.md
docs/FINAL_SUBMISSION_CHECKLIST.md
```

---

# Part 2: Production environment plan

You need separate local and production environment values.

## Local frontend env

```txt
client/.env
```

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

## Production frontend env on Vercel

```env
VITE_API_BASE_URL=https://your-backend.onrender.com/api
```

Do not use:

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

in production.

A deployed frontend cannot call your local computer’s `localhost`.

---

## Local backend env

```txt
server/.env
```

```env
NODE_ENV=development
PORT=5000
CLIENT_URL=http://localhost:5173
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/localbites
JWT_SECRET=your_long_local_secret
JWT_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=10
```

## Production backend env on Render

```env
NODE_ENV=production
PORT=10000
CLIENT_URL=https://your-frontend.vercel.app
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/localbites
JWT_SECRET=your_long_production_secret
JWT_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=10
```

Important:

```txt
Render often provides a PORT automatically. If your code uses process.env.PORT through env config, it should work.
```

---

## Production env checklist

Create:

```txt
docs/PRODUCTION_ENV_CHECKLIST.md
```

Template:

```md
# Production Environment Checklist

## Frontend: Vercel

- [ ] `VITE_API_BASE_URL` is set
- [ ] Value points to deployed backend `/api`
- [ ] No private secrets added to frontend env
- [ ] Frontend was redeployed after env change

## Backend: Render

- [ ] `NODE_ENV=production`
- [ ] `CLIENT_URL` points to deployed frontend URL
- [ ] `MONGODB_URI` is set
- [ ] `JWT_SECRET` is set and strong
- [ ] `JWT_EXPIRES_IN` is set
- [ ] `BCRYPT_SALT_ROUNDS` is set
- [ ] Backend was redeployed after env change

## MongoDB Atlas

- [ ] Database user exists
- [ ] Password is saved securely
- [ ] Network access allows deployed backend
- [ ] Connection string uses correct database name
- [ ] Test data exists or seed process is documented

## GitHub

- [ ] `.env` is ignored
- [ ] `.env.example` is committed
- [ ] README has setup instructions
```

---

# Part 3: MongoDB Atlas production setup

MongoDB Atlas will host the production database.

## Atlas checklist

```txt
1. Create or open Atlas project
2. Create cluster
3. Create database user
4. Add network access
5. Copy connection string
6. Replace username/password/database
7. Add URI to Render env
8. Test backend connection
```

---

## Network access warning

Atlas requires network access rules.

For local development, you may add your current IP.

For deployed backend, you need the deployment provider to access the cluster.

Depending on hosting plan and provider, you may need:

```txt
Option 1: Use provider static outbound IP if available
Option 2: Temporarily allow access from anywhere: 0.0.0.0/0
```

Security warning:

```txt
0.0.0.0/0 is easier for student projects but less secure.
Use strong database credentials.
Use least privilege where possible.
Do not reuse passwords.
```

For a beginner portfolio project, many students use `0.0.0.0/0` because free platforms may not provide stable outbound IPs. But document this as a known limitation.

---

## Connection string checklist

Your MongoDB URI should look like:

```txt
mongodb+srv://username:password@cluster.mongodb.net/database-name
```

Check:

```txt
1. Username is correct
2. Password is correct
3. Special characters in password are URL-encoded
4. Database name is correct
5. No angle brackets remain
6. URI is not committed to GitHub
```

---

## MongoDB production notes file

Create:

```txt
docs/MONGODB_ATLAS_DEPLOYMENT_NOTES.md
```

Template:

```md
# MongoDB Atlas Deployment Notes

## Cluster
-

## Database name
-

## Collections
- users
- foods
- orders

## Network access decision
-

## Security notes
- Database URI is stored only in Render environment variables.
- `.env` is not committed.
- Database user has password authentication.
- 0.0.0.0/0 is used only if required by hosting limitation.

## Test data
-

## Connection test result
Pass / Fail
```

---

# Part 4: Deploy backend to Render

The backend should be deployed first.

## Backend requirements

Your server should have:

```txt
server/package.json
server/src/server.ts
server/src/app.ts
server/tsconfig.json
server/.env.example
```

Recommended `server/package.json` scripts:

```json
{
  "scripts": {
    "dev": "tsx watch src/server.ts",
    "build": "tsc",
    "start": "node dist/server.js",
    "typecheck": "tsc --noEmit"
  }
}
```

If your backend is plain JavaScript instead of TypeScript, adjust commands accordingly.

---

## Render setup steps

1. Push code to GitHub.
2. Go to Render.
3. Create **New Web Service**.
4. Connect GitHub repository.
5. Select the repository.
6. Configure root directory.

If your repo structure is:

```txt
project-root/
  client/
  server/
```

Set root directory:

```txt
server
```

Recommended settings:

| Render field | Value |
|---|---|
| Runtime | Node |
| Root Directory | `server` |
| Build Command | `npm install && npm run build` |
| Start Command | `npm start` |
| Environment | Node |
| Branch | `main` |

Add environment variables in Render dashboard.

---

## Render environment variables

Add:

```env
NODE_ENV=production
CLIENT_URL=https://your-frontend.vercel.app
MONGODB_URI=mongodb+srv://...
JWT_SECRET=...
JWT_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=10
```

Do not wrap values in quotes unless the provider specifically requires it.

---

## Render backend test

After deployment, Render will provide a URL like:

```txt
https://your-backend.onrender.com
```

Test:

```txt
https://your-backend.onrender.com/health
```

Expected:

```json
{
  "success": true,
  "message": "Server is healthy"
}
```

Test API base:

```txt
https://your-backend.onrender.com/api/foods
```

Expected:

```txt
200 OK with food array, or empty array.
```

---

## Common Render backend issues

| Issue | Likely cause | Fix |
|---|---|---|
| Build failed | TypeScript error | Run `npm run build` locally and fix |
| Start failed | Wrong start command | Use `node dist/server.js` through `npm start` |
| MongoDB connection failed | Wrong URI/network access | Check Atlas URI/IP access |
| Health route 404 | Wrong path or app not started | Check routes/server logs |
| Env var undefined | Missing Render env value | Add env and redeploy |
| CORS blocked | CLIENT_URL wrong | Update backend env to frontend URL |
| App sleeps on free plan | Free instance limitation | Wait for cold start or upgrade |

---

## Render deployment guide file

Create:

```txt
docs/RENDER_DEPLOYMENT_GUIDE.md
```

Template:

```md
# Render Deployment Guide

## Service type
Web Service

## Root directory
server

## Build command
```bash
npm install && npm run build
```

## Start command
```bash
npm start
```

## Environment variables
- NODE_ENV
- CLIENT_URL
- MONGODB_URI
- JWT_SECRET
- JWT_EXPIRES_IN
- BCRYPT_SALT_ROUNDS

## Live backend URL
-

## Health check URL
-

## Deployment result
Pass / Fail

## Issues found
-

## Fixes applied
-
```

---

# Part 5: Deploy frontend to Vercel

After backend is deployed and tested, deploy frontend.

## Frontend requirements

Your frontend should have:

```txt
client/package.json
client/vite.config.ts
client/src/
client/.env.example
```

Recommended `client/package.json` scripts:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc -b && vite build",
    "preview": "vite preview"
  }
}
```

If your project uses a different build script, make sure it works locally.

---

## Vercel setup steps

1. Push code to GitHub.
2. Go to Vercel.
3. Add New Project.
4. Import GitHub repository.
5. Configure project.

If repo structure is:

```txt
project-root/
  client/
  server/
```

Set root directory:

```txt
client
```

Recommended settings:

| Vercel field | Value |
|---|---|
| Framework Preset | Vite |
| Root Directory | `client` |
| Build Command | `npm run build` |
| Output Directory | `dist` |
| Install Command | `npm install` |

---

## Vercel environment variables

Add:

```env
VITE_API_BASE_URL=https://your-backend.onrender.com/api
```

Important:

```txt
Vite browser-side environment variables must be prefixed with VITE_.
```

After adding or changing environment variables, redeploy the frontend.

---

## Frontend live test

Open:

```txt
https://your-frontend.vercel.app
```

Check:

```txt
1. Home page loads
2. No console error
3. Network requests go to Render backend
4. Login/register work
5. Foods load from backend
6. Checkout works
7. Admin pages work
```

---

## Common Vercel frontend issues

| Issue | Likely cause | Fix |
|---|---|---|
| Build failed | TypeScript/build error | Run `npm run build` locally |
| Blank page | Runtime JS error | Check browser console |
| API still calls localhost | Wrong `VITE_API_BASE_URL` | Set Vercel env and redeploy |
| Routes show 404 on refresh | SPA rewrite missing | Add `vercel.json` rewrite |
| Env variable undefined | Missing `VITE_` prefix or no redeploy | Fix env name and redeploy |
| CORS blocked | Backend CLIENT_URL wrong | Update Render env and redeploy backend |

---

## SPA refresh fix for Vite

If your Vercel deployment gives 404 on route refresh like:

```txt
/admin
/menu/123
```

Create:

```txt
client/vercel.json
```

Content:

```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/"
    }
  ]
}
```

Then commit and redeploy.

---

## Vercel deployment guide file

Create:

```txt
docs/VERCEL_DEPLOYMENT_GUIDE.md
```

Template:

```md
# Vercel Deployment Guide

## Project type
Vite React frontend

## Root directory
client

## Build command
```bash
npm run build
```

## Output directory
```txt
dist
```

## Environment variables
- VITE_API_BASE_URL

## Live frontend URL
-

## Deployment result
Pass / Fail

## Issues found
-

## Fixes applied
-
```

---

# Part 6: Production CORS update

After frontend deployment, update backend `CLIENT_URL`.

Local value:

```env
CLIENT_URL=http://localhost:5173
```

Production value:

```env
CLIENT_URL=https://your-frontend.vercel.app
```

If backend must support both local and production, update CORS config carefully.

Simple option for one allowed origin:

```ts
app.use(
  cors({
    origin: env.CLIENT_URL,
    credentials: true,
  })
);
```

Multi-origin option:

```ts
const allowedOrigins = env.CLIENT_URL.split(",");

app.use(
  cors({
    origin(origin, callback) {
      if (!origin || allowedOrigins.includes(origin)) {
        callback(null, true);
        return;
      }

      callback(new Error("Not allowed by CORS"));
    },
    credentials: true,
  })
);
```

Then set:

```env
CLIENT_URL=http://localhost:5173,https://your-frontend.vercel.app
```

Only use this if your env parser allows comma-separated strings.

---

# Part 7: Production smoke testing

Smoke testing means checking that the deployed app basically works.

Create:

```txt
docs/PRODUCTION_SMOKE_TEST_PLAN.md
```

Template:

```md
# Production Smoke Test Plan

## Live URLs

Frontend:
-

Backend:
-

## Tests

| Test | Expected | Status |
|---|---|---|
| Frontend opens | Home page loads | Pending |
| Backend health | `/health` returns success | Pending |
| API foods | `/api/foods` returns data/array | Pending |
| Register | New user can register | Pending |
| Login | User can login | Pending |
| Menu | Foods load from backend | Pending |
| Details | Details page loads | Pending |
| Cart | Add/update/remove works | Pending |
| Checkout | Order created | Pending |
| My orders | User sees own orders | Pending |
| Admin foods | Admin can manage foods | Pending |
| Admin orders | Admin can update status | Pending |
| Customer blocked | Customer cannot access admin | Pending |
| Mobile | Main pages work on mobile | Pending |
| Refresh routes | `/menu`, `/admin` refresh works | Pending |
```

---

## Smoke test report

Create:

```txt
docs/PRODUCTION_SMOKE_TEST_REPORT.md
```

Template:

```md
# Production Smoke Test Report

## Date
-

## Frontend URL
-

## Backend URL
-

## Browser
-

## Test accounts

Customer:
-

Admin:
-

## Results

| Flow | Result | Notes |
|---|---|---|
| Backend health | Pass/Fail |  |
| Frontend home | Pass/Fail |  |
| Register | Pass/Fail |  |
| Login | Pass/Fail |  |
| Browse foods | Pass/Fail |  |
| Place order | Pass/Fail |  |
| My orders | Pass/Fail |  |
| Admin food management | Pass/Fail |  |
| Admin order management | Pass/Fail |  |
| Authorization failure | Pass/Fail |  |
| Mobile layout | Pass/Fail |  |
| Route refresh | Pass/Fail |  |

## Console errors
-

## Network errors
-

## CORS issues
-

## Bugs found
-

## Fixes applied
-

## Final verdict
Pass / Conditional pass / Fail
```

---

# Part 8: Deployment bug log

Create:

```txt
docs/DEPLOYMENT_BUG_LOG.md
```

Template:

```md
# Deployment Bug Log

| ID | Bug | Platform | Cause | Fix | Status |
|---|---|---|---|---|---|
| DEP-001 | Frontend calls localhost API | Vercel | Wrong env variable | Set VITE_API_BASE_URL to Render URL and redeployed | Fixed |
| DEP-002 | CORS blocked | Render | CLIENT_URL still localhost | Updated CLIENT_URL to Vercel URL | Fixed |
| DEP-003 | Backend crash | Render | Missing JWT_SECRET | Added env variable and redeployed | Fixed |
| DEP-004 | MongoDB connection failed | Atlas/Render | IP access blocked | Updated Atlas network access | Fixed |
```

---

## Common deployment bugs

### Bug 1: Frontend calls localhost

Symptom:

```txt
Failed to fetch http://localhost:5000/api/foods
```

Cause:

```txt
Vercel production env is missing or wrong.
```

Fix:

```txt
Set VITE_API_BASE_URL=https://your-backend.onrender.com/api
Redeploy frontend.
```

---

### Bug 2: CORS blocked in production

Symptom:

```txt
Access to fetch at backend from frontend has been blocked by CORS policy.
```

Cause:

```txt
Backend CLIENT_URL does not match frontend live URL.
```

Fix:

```txt
Set CLIENT_URL=https://your-frontend.vercel.app
Redeploy backend.
```

---

### Bug 3: Backend health works but API fails

Possible causes:

```txt
MongoDB connection failed
Missing env variables
Validation crash
Wrong route prefix
```

Fix:

```txt
Check Render logs.
Check MONGODB_URI.
Check API route paths.
```

---

### Bug 4: Vercel route refresh 404

Symptom:

```txt
Opening /admin directly gives 404.
```

Fix:

```txt
Add client/vercel.json rewrite to /
Redeploy frontend.
```

---

### Bug 5: Render service sleeps

Symptom:

```txt
First request is slow.
```

Cause:

```txt
Free instance cold start.
```

Fix:

```txt
Wait for startup.
Mention as known limitation.
Upgrade if needed.
```

---

### Bug 6: MongoDB password issue

Symptom:

```txt
Authentication failed.
```

Fix:

```txt
Check database username/password.
URL-encode special characters.
Update Render env variable.
Redeploy backend.
```

---

### Bug 7: Build fails on platform but works locally

Possible causes:

```txt
Wrong root directory
Missing dependency
Case-sensitive file path issue
Node version mismatch
Wrong build command
```

Fix:

```txt
Check platform build logs.
Run clean install locally.
Check import path casing.
Set Node version if needed.
```

---

# Part 9: Node version stability

Deployment platforms may use newer Node versions than your local machine.

Create:

```txt
server/.node-version
client/.node-version
```

Recommended:

```txt
20
```

or use the same LTS version you tested locally.

Alternative in `package.json`:

```json
{
  "engines": {
    "node": ">=20 <25"
  }
}
```

Keep it realistic and compatible with your dependencies.

---

# Part 10: README production update

Your README must be updated after deployment.

Minimum README sections:

```txt
1. Project title
2. Project summary
3. Live links
4. Demo credentials
5. Features
6. Tech stack
7. Screenshots
8. Folder structure
9. Local setup instructions
10. Environment variables
11. API overview
12. Deployment notes
13. Testing/QA notes
14. Known limitations
15. Future improvements
```

---

## Demo credentials section

Example:

```md
## Demo Credentials

### Customer
Email: customer@example.com  
Password: password123

### Admin
Email: admin@example.com  
Password: password123
```

Do not use your real personal password.

Use demo accounts created only for the project.

---

## Live links section

Example:

```md
## Live Links

Frontend: https://your-project.vercel.app  
Backend API: https://your-backend.onrender.com  
Health Check: https://your-backend.onrender.com/health
```

---

## Known limitations section

Be honest.

Example:

```md
## Known Limitations

- Payment gateway is not implemented.
- Render free instance may have cold starts.
- MongoDB Atlas network access is broad for demo deployment.
- Admin account is manually prepared for demo.
- Image upload is not implemented; image URLs are used.
```

This increases trust.

---

# Part 11: Final submission checklist

Create:

```txt
docs/FINAL_SUBMISSION_CHECKLIST.md
```

Template:

```md
# Final Submission Checklist

## Links
- [ ] GitHub repository link
- [ ] Live frontend link
- [ ] Live backend health link
- [ ] Demo credentials

## Documentation
- [ ] README.md updated
- [ ] .env.example files included
- [ ] API overview included
- [ ] Deployment notes included
- [ ] Known limitations included
- [ ] Screenshots included

## Functionality
- [ ] Register works
- [ ] Login works
- [ ] Browse items works
- [ ] Details page works
- [ ] Cart/checkout works
- [ ] My orders/history works
- [ ] Admin food/resource management works
- [ ] Admin order/status management works
- [ ] Customer blocked from admin

## Quality
- [ ] Desktop checked
- [ ] Mobile checked
- [ ] Console checked
- [ ] Network checked
- [ ] Smoke test completed
- [ ] Critical bugs fixed
- [ ] No secrets committed

## Final verdict
Ready / Needs fixes / Not ready
```

---

# Part 12: Deployment commands reference

Create:

```txt
docs/DEPLOYMENT_COMMANDS.md
```

Template:

```md
# Deployment Commands

## Frontend local

```bash
cd client
npm install
npm run dev
npm run build
npm run preview
```

## Backend local

```bash
cd server
npm install
npm run dev
npm run build
npm start
```

## Git

```bash
git status
git add .
git commit -m "prepare production deployment"
git push
```

## Frontend production env

```env
VITE_API_BASE_URL=https://your-backend.onrender.com/api
```

## Backend production env

```env
NODE_ENV=production
CLIENT_URL=https://your-frontend.vercel.app
MONGODB_URI=mongodb+srv://...
JWT_SECRET=...
JWT_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=10
```
```

---

# Part 13: Antigravity prompts for this module

## Prompt 1: Create deployment docs

```txt
I am doing Module 10: Deployment and Production Readiness.

Create these docs:
1. docs/DEPLOYMENT_PLAN.md
2. docs/PRODUCTION_ENV_CHECKLIST.md
3. docs/DEPLOYMENT_COMMANDS.md
4. docs/VERCEL_DEPLOYMENT_GUIDE.md
5. docs/RENDER_DEPLOYMENT_GUIDE.md
6. docs/MONGODB_ATLAS_DEPLOYMENT_NOTES.md
7. docs/PRODUCTION_SMOKE_TEST_PLAN.md
8. docs/PRODUCTION_SMOKE_TEST_REPORT.md
9. docs/DEPLOYMENT_BUG_LOG.md
10. docs/FINAL_SUBMISSION_CHECKLIST.md

Rules:
- Do not change app code yet.
- Use Vercel for frontend, Render for backend, MongoDB Atlas for database.
- Include env variables, build commands, start commands, CORS, smoke testing, and common bugs.
```

---

## Prompt 2: Pre-deployment review

```txt
Review the project for deployment readiness.

Check:
1. Frontend build script
2. Backend build/start scripts
3. .gitignore
4. .env.example files
5. Hardcoded localhost URLs
6. API base URL config
7. CORS config
8. MongoDB connection config
9. JWT secret usage
10. README completeness
11. Test/QA signoff

Do not edit files yet.

Return:
- Ready items
- Blocking issues
- Suggested fixes
- Deployment order
```

---

## Prompt 3: Fix hardcoded URLs

```txt
Search for hardcoded localhost URLs.

Check:
- client/src
- server/src
- README.md
- docs

Rules:
- Do not change documentation examples unless needed.
- App code should use env variables.
- Frontend should use VITE_API_BASE_URL.
- Backend should use CLIENT_URL for CORS.
- Report all hardcoded URLs before editing.
```

---

## Prompt 4: Prepare frontend for Vercel

```txt
Prepare frontend for Vercel deployment.

Check:
- client/package.json
- client/vite.config.ts
- client/.env.example
- client/vercel.json if needed
- frontend API base URL usage

Rules:
- Do not put real secrets in files.
- Add SPA rewrite if React Router routes need refresh support.
- Ensure build command works.
- Do not edit backend.
```

---

## Prompt 5: Prepare backend for Render

```txt
Prepare backend for Render deployment.

Check:
- server/package.json
- server/tsconfig.json
- server/src/server.ts
- server/src/config/env.ts
- server/src/app.ts
- server/.env.example

Rules:
- Build command should work.
- Start command should run compiled server.
- Use process.env.PORT.
- Use CLIENT_URL for CORS.
- Do not expose secrets.
- Do not edit frontend unless required.
```

---

## Prompt 6: Diagnose deployment bug

```txt
Diagnose this deployment bug.

Platform:
Vercel / Render / MongoDB Atlas

Error log:
[Paste error]

Context:
[What I tried]

Rules:
- Explain likely cause.
- Identify exact file/env/platform setting involved.
- Suggest smallest safe fix.
- Tell me how to retest after fixing.
- Do not edit files yet.
```

---

## Prompt 7: Production smoke test

```txt
Run production smoke test guidance.

Live URLs:
Frontend: [paste]
Backend: [paste]

Test:
1. Backend /health
2. Frontend home
3. Register/login
4. Food list
5. Details page
6. Checkout/order
7. My orders
8. Admin food management
9. Admin order status
10. Customer blocked from admin
11. Mobile layout
12. Route refresh

Update:
- docs/PRODUCTION_SMOKE_TEST_REPORT.md
- docs/DEPLOYMENT_BUG_LOG.md

Do not edit files yet.
```

---

## Prompt 8: Final README update

```txt
Use the portfolio-readme-generator skill.

Read:
- docs/PROJECT_BRIEF.md
- docs/PRD.md
- docs/ARCHITECTURE_OVERVIEW.md
- docs/PRODUCTION_SMOKE_TEST_REPORT.md
- docs/FINAL_SUBMISSION_CHECKLIST.md

Update README.md.

Include:
1. Project summary
2. Live frontend link
3. Backend health link
4. Demo credentials
5. Features
6. Tech stack
7. Screenshots
8. Folder structure
9. Local setup
10. Env variables
11. API overview
12. Testing/QA
13. Deployment notes
14. Known limitations
15. Future improvements

Rules:
- Do not invent features.
- Do not expose secrets.
- Be honest about limitations.
```

---

# Part 14: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 12-module-10-deployment-production-readiness.md
2. Vercel Vite deployment docs
3. Vercel environment variables docs
4. Render Node/Express deployment docs
5. Render environment variables docs
6. MongoDB Atlas connection docs
7. MongoDB Atlas IP access list docs
8. Vite build/env docs
9. Your deployment logs
10. Your smoke test report
11. Your deployment bug log
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for MERN deployment and production readiness.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. What deployment means
2. Recommended architecture: Vercel + Render + MongoDB Atlas
3. Local vs production env variables
4. Frontend deployment to Vercel
5. Backend deployment to Render
6. MongoDB Atlas production setup
7. CORS in production
8. Production smoke testing
9. Deployment logs
10. Common deployment bugs
11. README finalization
12. Final submission checklist
```

---

## NotebookLM Prompt 2: Deployment Bug Diagnosis

```txt
Review my deployment bug log and smoke test report.

Classify issues into:
1. Frontend build
2. Backend build/start
3. Env variables
4. CORS
5. MongoDB Atlas
6. API URL
7. Route refresh
8. Auth/token
9. Cold start
10. README/documentation

For each issue:
- Explain likely cause
- Suggest fix
- Suggest retest step
```

---

## NotebookLM Prompt 3: Interview Explanation

```txt
Help me explain my deployment process in an interview.

Create:
1. 30-second answer
2. 1-minute answer
3. Technical explanation
4. Frontend deployment explanation
5. Backend deployment explanation
6. Database deployment explanation
7. Env/CORS explanation
8. One deployment bug and how I fixed it
9. Known limitations explained professionally
```

---

## NotebookLM Prompt 4: Final Submission Review

```txt
Review my final submission package.

Check:
1. README clarity
2. Live links
3. Demo credentials
4. Screenshots
5. Setup instructions
6. Env examples
7. Feature accuracy
8. Known limitations
9. Deployment notes
10. Whether a recruiter/mentor can test quickly

Return:
- Strong points
- Missing items
- Must-fix issues
- Final checklist
```

---

# Part 15: Required official/resource links

Add these to NotebookLM or module notes:

| Resource | Link | Why it matters |
|---|---|---|
| Vite build guide | https://vite.dev/guide/build | Understand production builds |
| Vite env variables | https://vite.dev/guide/env-and-mode | Understand `import.meta.env` and `VITE_` variables |
| Vercel Vite guide | https://vercel.com/docs/frameworks/frontend/vite | Vercel guidance for Vite apps |
| Vercel environment variables | https://vercel.com/docs/environment-variables | Manage frontend production env |
| Render Node/Express guide | https://render.com/docs/deploy-node-express-app | Deploy Express backend |
| Render environment variables | https://render.com/docs/configure-environment-variables | Manage backend production env |
| Render web services | https://render.com/docs/web-services | Build/start commands and service settings |
| Render Node version | https://render.com/docs/node-version | Control Node version |
| MongoDB connection strings | https://www.mongodb.com/docs/manual/reference/connection-string/ | Understand Atlas URI |
| MongoDB Atlas IP access list | https://www.mongodb.com/docs/atlas/security/ip-access-list/ | Configure network access |
| MDN Express deployment guide | https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Server-side/Express_Nodejs/deployment | Production Express considerations |
| MDN CORS guide | https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS | Understand browser CORS behavior |

---

# Part 16: Required video resources

Watch at least two videos.

Search YouTube:

```txt
Deploy Vite React app to Vercel environment variables
Deploy Node Express API to Render environment variables
Deploy MERN app Vercel Render MongoDB Atlas
MongoDB Atlas connection string deployment tutorial
Fix CORS error Vercel Render Express
Vercel React Router refresh 404 fix
Render Node.js deployment logs tutorial
```

Recommended video types:

| Video type | Why |
|---|---|
| Vite to Vercel deployment | Frontend deployment |
| Express to Render deployment | Backend deployment |
| MERN full deployment | End-to-end context |
| MongoDB Atlas setup | Database connection |
| CORS/env debugging | Common production issue |
| README/project submission | Portfolio polish |

---

## Video learning notes

Create:

```txt
docs/notebooklm/module-10-video-learning-notes.md
```

Use this format:

```md
# Module 10 Video Learning Notes

## Video 1
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### How I will apply this
1.
2.
3.

### Mistakes to avoid
1.
2.

---

## Video 2
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### How I will apply this
1.
2.
3.

### Mistakes to avoid
1.
2.
```

---

# Part 17: Practice tasks

## Practice Task 1: Local production build

Run:

```bash
cd client
npm run build
```

Run:

```bash
cd server
npm run build
npm start
```

Fix all build errors.

---

## Practice Task 2: Create deployment docs

Create all deployment documentation files listed in this module.

---

## Practice Task 3: Prepare MongoDB Atlas

Set up:

```txt
Database user
Network access
Connection string
Production database name
```

Update:

```txt
docs/MONGODB_ATLAS_DEPLOYMENT_NOTES.md
```

---

## Practice Task 4: Deploy backend to Render

Deploy backend and test:

```txt
/health
/api/foods
```

Update:

```txt
docs/RENDER_DEPLOYMENT_GUIDE.md
```

---

## Practice Task 5: Deploy frontend to Vercel

Deploy frontend with:

```txt
VITE_API_BASE_URL=https://your-backend.onrender.com/api
```

Update:

```txt
docs/VERCEL_DEPLOYMENT_GUIDE.md
```

---

## Practice Task 6: Fix production CORS

Update backend:

```txt
CLIENT_URL=https://your-frontend.vercel.app
```

Redeploy backend.

Verify browser requests work.

---

## Practice Task 7: Run smoke test

Complete:

```txt
docs/PRODUCTION_SMOKE_TEST_REPORT.md
```

Test user and admin flows.

---

## Practice Task 8: Fix deployment bugs

Complete:

```txt
docs/DEPLOYMENT_BUG_LOG.md
```

Record at least 2 deployment issues or observations.

Even if deployment is smooth, note:

```txt
Cold start
Route refresh
Env verification
CORS verification
```

---

## Practice Task 9: Update README

Update README with:

```txt
Live links
Demo credentials
Screenshots
Setup instructions
Deployment notes
Known limitations
```

---

## Practice Task 10: Final submission checklist

Complete:

```txt
docs/FINAL_SUBMISSION_CHECKLIST.md
```

Do not submit until it says:

```txt
Ready
```

---

# Part 18: Common deployment mistakes

## Mistake 1: Deploying without local build

Always run local build first.

---

## Mistake 2: Keeping frontend API as localhost

A deployed frontend cannot call your local backend.

Use deployed backend URL.

---

## Mistake 3: Forgetting to redeploy after env changes

Changing env variables usually requires redeployment.

---

## Mistake 4: Wrong root directory

For monorepo:

```txt
Vercel root: client
Render root: server
```

---

## Mistake 5: CORS still points to localhost

Production backend must allow production frontend.

---

## Mistake 6: Committing `.env`

Never commit secrets.

---

## Mistake 7: No smoke test

A live link is not enough.

Test the deployed flow.

---

## Mistake 8: README has fake features

Do not claim features that do not work.

---

## Mistake 9: No demo credentials

Reviewers should be able to test quickly.

---

## Mistake 10: Ignoring logs

Vercel and Render logs are the first place to inspect failures.

---

# Part 19: Quality bar

Minimum passing standard:

```txt
1. Frontend deployed.
2. Backend deployed.
3. Database connected.
4. Frontend can call backend.
5. CORS works.
6. Register/login works live.
7. Main user flow works live.
8. Admin flow works live.
9. README updated.
10. Smoke test report completed.
```

Strong standard:

```txt
1. Build passes locally before deployment.
2. Production env variables documented.
3. No secrets committed.
4. Route refresh works.
5. Mobile layout checked live.
6. Deployment bug log completed.
7. Known limitations are honest.
8. Screenshots included in README.
```

Advanced standard:

```txt
1. Custom domain optional.
2. Preview deployments understood.
3. GitHub Actions optional CI added.
4. Automated tests run before deployment.
5. Backend logs monitored.
6. Better database access restrictions used.
7. Seed script or demo data setup documented.
```

---

# Required deliverables for this module

Submit:

```txt
1. Live frontend URL
2. Live backend URL
3. Backend health URL
4. GitHub repository URL
5. client/.env.example
6. server/.env.example
7. Updated README.md
8. DEPLOYMENT_PLAN.md
9. PRODUCTION_ENV_CHECKLIST.md
10. DEPLOYMENT_COMMANDS.md
11. VERCEL_DEPLOYMENT_GUIDE.md
12. RENDER_DEPLOYMENT_GUIDE.md
13. MONGODB_ATLAS_DEPLOYMENT_NOTES.md
14. PRODUCTION_SMOKE_TEST_PLAN.md
15. PRODUCTION_SMOKE_TEST_REPORT.md
16. DEPLOYMENT_BUG_LOG.md
17. FINAL_SUBMISSION_CHECKLIST.md
18. Screenshots of Vercel deployment
19. Screenshots of Render deployment
20. Screenshot of backend health response
21. Screenshot of live frontend home page
22. Screenshot of successful live login/order/admin flow
23. NotebookLM Study Guide screenshot
24. NotebookLM deployment bug diagnosis screenshot
25. Video learning notes
26. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/12-module-10-deployment-production-readiness-reflection.md
```

Use this format:

```md
# Reflection: Module 10 - Deployment and Production Readiness

## What I deployed
-

## Frontend live link
-

## Backend live link
-

## Database setup
-

## Environment variables I configured
-

## CORS issue I checked/fixed
-

## Deployment bugs I faced
-

## How I fixed them
-

## Smoke test result
-

## README updates I made
-

## What Antigravity helped with
-

## What I had to verify manually
-

## Known limitations
-

## What I learned about production readiness
-
```

---

# Quiz

## Multiple choice

**1. What should be deployed first in this recommended workflow?**

A. Backend API  
B. README only  
C. CSS file only  
D. Figma design  

Correct answer: **A**

---

**2. What should production frontend `VITE_API_BASE_URL` point to?**

A. `http://localhost:5000/api`  
B. The deployed backend API URL  
C. GitHub repository URL  
D. MongoDB Atlas dashboard URL  

Correct answer: **B**

---

**3. Why must Vite frontend env variables start with `VITE_`?**

A. So Vite exposes them to browser-side code  
B. So MongoDB can connect  
C. So JWT signs tokens  
D. So Render can create users  

Correct answer: **A**

---

**4. What is the purpose of backend `CLIENT_URL`?**

A. Allow the correct frontend origin through CORS  
B. Store database password  
C. Replace JWT secret  
D. Build frontend assets  

Correct answer: **A**

---

**5. What should you never commit to GitHub?**

A. `.env` with real secrets  
B. `.env.example`  
C. README.md  
D. Screenshots  

Correct answer: **A**

---

**6. What should you do after changing environment variables on Vercel or Render?**

A. Redeploy the service if required  
B. Delete GitHub repository  
C. Ignore the change  
D. Remove README  

Correct answer: **A**

---

**7. What is a production smoke test?**

A. A quick check that critical live app flows work  
B. A color palette design  
C. A database schema only  
D. A Figma animation  

Correct answer: **A**

---

**8. Why might React routes show 404 on Vercel refresh?**

A. SPA rewrite is missing  
B. MongoDB password is too long  
C. Button color is wrong  
D. JWT is expired  

Correct answer: **A**

---

**9. What should be included in the README after deployment?**

A. Live links, demo credentials, setup, features, screenshots, env guide, limitations  
B. Only project title  
C. Real JWT secret  
D. Personal database password  

Correct answer: **A**

---

**10. What should you do if backend works locally but fails on Render?**

A. Check Render build/runtime logs and environment variables  
B. Guess randomly  
C. Delete frontend  
D. Ignore health route  

Correct answer: **A**

---

## Short-answer questions

1. What is the recommended deployment architecture for this course?
2. Why should backend be deployed before frontend?
3. What is the difference between local and production env variables?
4. What should `VITE_API_BASE_URL` be in production?
5. What should `CLIENT_URL` be in production?
6. What MongoDB Atlas settings are needed for deployment?
7. What is one common Vercel issue and its fix?
8. What is one common Render issue and its fix?
9. What should be included in a production smoke test?
10. What known limitation did you document?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Local build | Frontend and backend build locally |
| Git hygiene | No secrets/node_modules committed |
| MongoDB Atlas | Production DB connection works |
| Backend deployment | Render backend live and health route works |
| Frontend deployment | Vercel frontend live |
| Env variables | Production env variables configured |
| CORS | Deployed frontend can call backend |
| API URL | Frontend calls deployed backend, not localhost |
| Smoke test | User/admin flows tested live |
| Route refresh | React Router refresh works or limitation documented |
| README | Live links/demo/setup/screenshots/limitations included |
| Bug log | Deployment bugs documented and fixed |
| Final checklist | Submission checklist completed |
| NotebookLM evidence | Study guide and deployment review submitted |
| Reflection | Student explains deployment process clearly |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can deploy a full-stack MERN project with Vercel, Render, and MongoDB Atlas; configure production environment variables; fix CORS and API URL issues; run smoke tests; document deployment bugs; update README; and submit a working portfolio-ready project with live links and demo credentials.
```

After completing this file, continue to:

```txt
13-final-assignment.md
```
