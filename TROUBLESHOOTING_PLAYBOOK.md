# Troubleshooting Playbook

Use this file when students get stuck during the Antigravity 2.0 MERN + Next.js course.

---

## Rule before debugging

Do not randomly change files.

Use this process:

```txt
1. Reproduce the issue
2. Read the exact error
3. Identify where it happens
4. Check recent changes
5. Fix the smallest possible thing
6. Retest
7. Document the bug
```

---

## GitHub push problems

### Problem: remote already exists

```bash
git remote -v
git remote set-url origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

### Problem: GitHub repo has README already

```bash
git pull origin main --rebase
git push -u origin main
```

### Problem: branch mismatch

```bash
git branch -M main
git push -u origin main
```

### Problem: accidentally staged unwanted files

```bash
git status
git reset
```

Then update `.gitignore`.

---

## Node/npm problems

### Check versions

```bash
node -v
npm -v
```

Use Node LTS if possible.

### Clean install

```bash
rm -rf node_modules package-lock.json
npm install
```

On Windows PowerShell:

```powershell
Remove-Item -Recurse -Force node_modules
Remove-Item package-lock.json
npm install
```

---

## Vite/React problems

### Dev server not starting

```bash
cd client
npm install
npm run dev
```

Check:

```txt
1. Correct folder
2. package.json exists
3. dependencies installed
4. port conflict
```

### Build fails

```bash
npm run build
```

Common causes:

```txt
TypeScript error
Wrong import path
Missing component export
Unused broken file
Case-sensitive path issue
```

---

## Tailwind problems

### Tailwind classes not working

Check:

```txt
1. Tailwind installed
2. CSS imports Tailwind
3. Vite config includes plugin if using current Tailwind setup
4. Class names are not dynamically broken
5. Dev server restarted
```

---

## React Router problems

### Page refresh gives 404 after deployment

For Vercel + Vite SPA, add:

```txt
client/vercel.json
```

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

---

## Express backend problems

### Server not starting

Check:

```bash
cd server
npm install
npm run dev
```

Common causes:

```txt
Missing .env
Wrong import path
TypeScript config issue
Port already in use
MongoDB connection failure
```

### Health route not working

Check:

```txt
1. app.get("/health") exists
2. server is running
3. correct port
4. correct URL
```

---

## MongoDB problems

### MongoDB connection failed

Check:

```txt
1. MONGODB_URI exists
2. Username/password correct
3. Password special characters URL-encoded
4. Atlas network access configured
5. Cluster active
6. Database user has permission
```

### Duplicate email error

Expected if the same user registers again.

Fix:

```txt
Use a new email
or
Delete test user from database
or
Handle duplicate error cleanly
```

---

## Auth problems

### 401 Authentication required

Check:

```txt
1. User logged in
2. Token saved
3. Authorization header sent
4. Header format: Bearer <token>
5. Backend JWT secret matches token issuer
```

### 403 Forbidden

Check:

```txt
1. User role is not admin
2. Admin route requires admin
3. Database user role is correct
4. Frontend is not pretending user is admin
```

---

## CORS problems

### Browser says CORS blocked

Check backend:

```env
CLIENT_URL=http://localhost:5173
```

For deployed frontend:

```env
CLIENT_URL=https://your-frontend.vercel.app
```

Check Express:

```ts
app.use(cors({ origin: env.CLIENT_URL, credentials: true }));
```

Restart backend after env changes.

---

## API response shape problems

Backend may return:

```json
{
  "success": true,
  "message": "OK",
  "data": []
}
```

Frontend should use:

```ts
json.data
```

If food list is blank, inspect Network tab response.

---

## Form validation problems

HTML inputs return strings.

Convert number fields:

```ts
price: Number(form.price)
quantity: Number(form.quantity)
```

---

## Vercel deployment problems

### API calls localhost in production

Set Vercel env:

```env
VITE_API_BASE_URL=https://your-backend.onrender.com/api
```

Redeploy.

### Env variable undefined

Check:

```txt
1. It starts with VITE_ for Vite frontend
2. It is set in Vercel dashboard
3. Deployment restarted after adding it
```

---

## Render deployment problems

### Build failed

Run locally:

```bash
cd server
npm run build
```

Fix local build first.

### Start command wrong

Recommended:

```bash
npm start
```

with package script:

```json
"start": "node dist/server.js"
```

### Free tier cold start

First request can be slow. Wait and retry.

---

## Antigravity problems

### Agent changes too many files

Use:

```txt
Stop. List all changed files. Revert unrelated changes. Continue only with the requested file.
```

### Agent wants to run risky command

Ask:

```txt
Explain the command, risk, affected files, and safer alternative. Do not run yet.
```

### Agent loses context

Create/update:

```txt
PROJECT_CONTEXT.md
NEXT_STEPS.md
DECISIONS.md
ERROR_LOG.md
```

Then prompt:

```txt
Read PROJECT_CONTEXT.md and NEXT_STEPS.md first. Continue only from the next step.
```

---

## NotebookLM problems

### Answers are weak

Fix:

```txt
Add better sources
Ask narrower questions
Tell it to answer only from sources
```

Prompt:

```txt
Use only the uploaded sources. If the answer is not clearly found, say "Not clearly found in the sources."
```

---

## Debugging prompt for Antigravity

```txt
Debug this issue.

Error:
[paste exact error]

Context:
[what I was doing]

Rules:
- Do not edit files yet.
- Explain likely cause.
- Identify exact files involved.
- Suggest smallest safe fix.
- Give retest steps.
```

---

## Bug log format

Add every solved issue to:

```txt
docs/BUG_LOG.md
```

```md
| ID | Bug | Cause | Fix | Retest result |
|---|---|---|---|---|
| BUG-001 | Login failed | Token not sent | Added Authorization header | Pass |
```
