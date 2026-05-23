# Bonus Module: Reusable SKILL.md Library — Build Personal AI Skills You Can Use Across Any MERN Project

**File Name:** `16-bonus-module-reusable-skill-md-library.md`  
**Module Type:** Bonus / Advanced Productivity Module  
**Target Learners:** Junior MERN Stack Developers who want to reuse Antigravity workflows across multiple projects  
**Estimated Time:** 5–8 hours  
**Recommended After:** Module 4: `SKILL.md` Mastery, or after completing the Final Assignment  
**Main Goal:** Build a reusable personal library of `SKILL.md` files for planning, UI, frontend, backend, testing, deployment, README writing, and interview preparation so that students can use Antigravity more consistently across any MERN or Next.js project.

---

## Module purpose

In Module 4, you learned how `SKILL.md` works.

This bonus module turns that knowledge into a reusable personal library.

The goal is to create a repeatable set of Antigravity skills that you can copy into any project and immediately use for:

- Project planning
- Architecture review
- Figma-to-code implementation
- React UI polish
- Express API review
- MongoDB schema review
- Full-stack integration
- Browser verification
- Testing strategy
- Deployment readiness
- README generation
- Portfolio/interview preparation

This module is highly practical.

You will not only read about skills.

You will build your own reusable skill library.

---

## Why this module matters

Most students use AI tools with repeated long prompts.

Example:

```txt
Please review my MERN architecture. Check frontend, backend, database, auth, routes, API contract, folder structure, security, and deployment...
```

They rewrite the same instructions again and again.

That wastes time, tokens, and attention.

A reusable `SKILL.md` library solves this.

Instead of repeating long prompts, you create:

```txt
.agent/skills/mern-architecture-review/SKILL.md
.agent/skills/react-ui-polish/SKILL.md
.agent/skills/express-api-quality-review/SKILL.md
.agent/skills/browser-verification/SKILL.md
.agent/skills/deployment-readiness-review/SKILL.md
```

Then you can ask:

```txt
Use the mern-architecture-review skill to review this project.
```

or:

```txt
Use the browser-verification skill to test the checkout flow.
```

The agent gets a structured workflow instead of vague instructions.

---

## Skills mindset

A skill is not just a prompt.

A good skill is a reusable operating procedure.

It should tell Antigravity:

```txt
When to use this skill
What files to inspect
What questions to ask
What not to change
What output format to produce
What safety rules to follow
What evidence to collect
How to verify the result
```

Bad skill:

```txt
Help me build better apps.
```

Good skill:

```txt
Review a MERN app architecture by checking project docs, frontend structure, backend modules, database schema, auth flow, authorization matrix, API contract, testing plan, deployment plan, and return a prioritized risk/fix report without editing files.
```

---

## Official model of Antigravity skills

Antigravity skills are designed as reusable task-specific instructions.

A typical skill package includes:

```txt
skill-folder/
  SKILL.md
  scripts/ optional
  references/ optional
  assets/ optional
```

For this course, we will mainly use:

```txt
skill-folder/
  SKILL.md
```

Optional advanced students can add:

```txt
references/
templates/
checklists/
scripts/
```

---

## Project-specific vs global skills

You can organize skills in two ways.

## Project-specific skills

Use when the skill belongs to one project.

Example:

```txt
project-name/
  .agent/
    skills/
      mern-architecture-review/
        SKILL.md
      express-api-quality-review/
        SKILL.md
```

Best for:

```txt
1. Project-specific architecture rules
2. Company assignment requirements
3. Project-specific naming conventions
4. Project-specific deployment rules
5. Course/final assignment work
```

## Global reusable skills

Use when you want the skill available across projects.

Example:

```txt
~/.gemini/antigravity/skills/
  react-ui-polish/
    SKILL.md
  portfolio-readme-generator/
    SKILL.md
```

Best for:

```txt
1. Personal reusable workflows
2. Common UI review
3. General README generation
4. General testing strategy
5. General deployment review
```

Important:

```txt
If your Antigravity version or workspace uses a slightly different folder convention, keep the structure consistent with the version you are using.
```

In this course repository, we will use:

```txt
.agent/skills/
```

for project-specific skill examples.

---

# Part 1: Skill library structure

Create this structure in your course/final project repo:

```txt
.agent/
  skills/
    SKILL_INDEX.md

    01-project-planning-review/
      SKILL.md

    02-mern-architecture-review/
      SKILL.md

    03-figma-to-react-implementation/
      SKILL.md

    04-react-ui-polish/
      SKILL.md

    05-frontend-state-route-review/
      SKILL.md

    06-express-api-quality-review/
      SKILL.md

    07-mongodb-schema-review/
      SKILL.md

    08-auth-authorization-review/
      SKILL.md

    09-fullstack-integration-debugger/
      SKILL.md

    10-browser-verification/
      SKILL.md

    11-test-plan-generator/
      SKILL.md

    12-deployment-readiness-review/
      SKILL.md

    13-portfolio-readme-generator/
      SKILL.md

    14-interview-project-explainer/
      SKILL.md
```

For beginners, start with the first five.

For strong students, build all fourteen.

---

## Skill naming rules

Use clear names.

Good:

```txt
express-api-quality-review
react-ui-polish
deployment-readiness-review
portfolio-readme-generator
```

Bad:

```txt
skill1
helper
ai-thing
my-prompt
fixer
```

Use lowercase folder names with hyphens.

---

## Skill index file

Create:

```txt
.agent/skills/SKILL_INDEX.md
```

Template:

```md
# SKILL_INDEX

This folder contains reusable Antigravity skills for MERN and Next.js full-stack projects.

## How to use

Ask Antigravity:

```txt
Use the [skill-name] skill to [task].
```

Example:

```txt
Use the express-api-quality-review skill to review my backend routes against docs/API_CONTRACT.md.
```

## Available skills

| Skill | Purpose | Use when |
|---|---|---|
| project-planning-review | Review specs and scope before coding | Before implementation |
| mern-architecture-review | Review full-stack architecture | Before or during build |
| figma-to-react-implementation | Convert design sections into React/Tailwind | During UI build |
| react-ui-polish | Improve UI consistency/responsiveness | After UI implementation |
| frontend-state-route-review | Review React state, routes, protected pages | After frontend foundation |
| express-api-quality-review | Review Express APIs | After backend routes |
| mongodb-schema-review | Review Mongoose schemas and indexes | Before backend testing |
| auth-authorization-review | Review auth/role protection | Before integration |
| fullstack-integration-debugger | Debug frontend/backend integration | During integration |
| browser-verification | Verify app flows in browser | Before deployment |
| test-plan-generator | Generate QA/API/E2E test plan | Before final QA |
| deployment-readiness-review | Review production readiness | Before deployment |
| portfolio-readme-generator | Create strong README | Before submission |
| interview-project-explainer | Prepare interview explanations | After final project |
```

---

# Part 2: Universal SKILL.md template

Every skill should follow a consistent pattern.

Use this template:

```md
---
name: skill-name-here
description: Short description of when the agent should use this skill.
---

# Skill: Skill Name Here

## Purpose

Explain what this skill does.

## When to use

Use this skill when:
- 
- 
- 

## Inputs to inspect

Read these files if available:
- 
- 
- 

## Rules

- Do not edit files unless explicitly asked.
- First analyze.
- Return a clear report.
- Keep changes scoped.
- Do not remove security/auth/validation.
- Do not invent features.
- Do not claim unverified behavior.

## Workflow

1. Inspect relevant files.
2. Compare against docs/specs.
3. Identify risks.
4. Prioritize issues.
5. Suggest fixes.
6. Provide verification steps.

## Output format

Return:

```md
# [Skill Name] Report

## Summary
-

## What is working
-

## Issues found
-

## Critical fixes
-

## Recommended improvements
-

## Files reviewed
-

## Verification steps
-
```

## Completion criteria

This skill is complete when:
- Issues are clearly identified.
- Fixes are prioritized.
- Verification steps are provided.
```

---

## Frontmatter rule

At minimum, include:

```yaml
---
name: skill-name
description: What this skill does and when to use it.
---
```

The description matters because it helps the agent match the skill to the user’s intent.

Write a description that is short but specific.

Weak description:

```yaml
description: Helps with code.
```

Strong description:

```yaml
description: Reviews Express.js REST API routes, controllers, services, validation, auth middleware, response format, and API contract alignment for MERN projects.
```

---

# Part 3: Core reusable skills

The following skills are ready to copy into your project.

---

## Skill 1: Project planning review

Create:

```txt
.agent/skills/01-project-planning-review/SKILL.md
```

Content:

```md
---
name: project-planning-review
description: Reviews project planning documents before implementation, including project brief, PRD, user stories, acceptance criteria, feature scope, API contract, database schema, authorization matrix, risk register, and task breakdown.
---

# Skill: Project Planning Review

## Purpose

Use this skill to review whether a MERN or Next.js project is ready for implementation.

The goal is to prevent vague requirements, oversized scope, missing API contracts, weak data models, and unclear authorization rules before code is written.

## When to use

Use this skill when:
- Starting a new project
- Preparing a company assignment
- Reviewing a final assignment plan
- Checking whether requirements are clear enough for Antigravity
- Reducing scope before implementation

## Inputs to inspect

Read these files if available:

- `docs/PROJECT_BRIEF.md`
- `docs/PRD.md`
- `docs/USER_STORIES.md`
- `docs/ACCEPTANCE_CRITERIA.md`
- `docs/FEATURE_SCOPE.md`
- `docs/PAGE_ROUTE_MAP.md`
- `docs/API_CONTRACT.md`
- `docs/DATABASE_SCHEMA.md`
- `docs/AUTHORIZATION_MATRIX.md`
- `docs/IMPLEMENTATION_PLAN.md`
- `docs/TASK_BREAKDOWN.md`
- `docs/RISK_REGISTER.md`
- `README.md`

## Rules

- Do not write app code.
- Do not expand scope unless necessary.
- Do not invent requirements.
- Identify missing decisions.
- Prefer realistic junior-developer scope.
- Flag features that should be out of scope.
- Return a readiness verdict.

## Workflow

1. Read the planning docs.
2. Identify project goal, user roles, and main flows.
3. Check if features are clear and testable.
4. Check if API contract and database schema are aligned.
5. Check if authorization rules are specific.
6. Check if task breakdown is realistic.
7. Identify missing or risky items.
8. Return a prioritized readiness report.

## Output format

Return:

```md
# Project Planning Review Report

## Readiness verdict
Ready / Almost ready / Not ready

## Summary
-

## Strong parts
-

## Missing decisions
-

## Scope risks
-

## API/database alignment issues
-

## Authorization gaps
-

## Must-fix before coding
1.
2.
3.

## Nice-to-have improvements
-

## Recommended implementation order
1.
2.
3.

## Files reviewed
-
```

## Completion criteria

This skill is complete when the project has a clear buildable scope, role model, API contract, database schema, and implementation order.
```

---

## Skill 2: MERN architecture review

Create:

```txt
.agent/skills/02-mern-architecture-review/SKILL.md
```

Content:

```md
---
name: mern-architecture-review
description: Reviews MERN full-stack architecture, including frontend structure, backend modules, database schema, auth flow, API contract, deployment boundaries, and code ownership.
---

# Skill: MERN Architecture Review

## Purpose

Use this skill to review the architecture of a MERN project before or during implementation.

The goal is to make sure the project has clean separation between frontend, backend, database, authentication, authorization, and deployment.

## When to use

Use this skill when:
- Starting implementation
- Reviewing generated architecture
- Refactoring a messy MERN project
- Preparing for final assignment review
- Preparing for interview explanation

## Inputs to inspect

Read these files/folders if available:

- `docs/ARCHITECTURE_OVERVIEW.md`
- `docs/FRONTEND_ARCHITECTURE.md`
- `docs/BACKEND_ARCHITECTURE.md`
- `docs/DATABASE_ARCHITECTURE.md`
- `docs/API_CONTRACT.md`
- `docs/DATABASE_SCHEMA.md`
- `docs/AUTH_FLOW.md`
- `docs/AUTHORIZATION_MATRIX.md`
- `docs/DATA_FLOW.md`
- `docs/ERROR_FLOW.md`
- `client/src/`
- `server/src/`
- `README.md`

## Rules

- Do not edit files unless explicitly asked.
- Do not rewrite the app.
- Do not remove auth, validation, or error handling.
- Flag architecture risks clearly.
- Prioritize fixes by impact.
- Keep feedback practical for junior developers.

## Workflow

1. Inspect docs and folder structure.
2. Identify frontend architecture.
3. Identify backend architecture.
4. Check API/data flow consistency.
5. Check auth and authorization boundaries.
6. Check database schema alignment.
7. Check deployment boundaries.
8. Return architecture risk report.

## Output format

Return:

```md
# MERN Architecture Review Report

## Overall verdict
Strong / Acceptable / Risky / Not ready

## Architecture summary
-

## What is working
-

## Frontend architecture issues
-

## Backend architecture issues
-

## Database/schema issues
-

## Auth/authorization issues
-

## Data flow issues
-

## Deployment boundary issues
-

## Must-fix items
1.
2.
3.

## Recommended improvements
-

## Interview explanation points
-

## Files reviewed
-
```

## Completion criteria

This skill is complete when architecture risks are clear and the project has a safe implementation path.
```

---

## Skill 3: Figma-to-React implementation

Create:

```txt
.agent/skills/03-figma-to-react-implementation/SKILL.md
```

Content:

```md
---
name: figma-to-react-implementation
description: Converts Figma or design references into scoped React, TypeScript, and Tailwind implementation plans, including design tokens, component maps, responsive behavior, and visual QA.
---

# Skill: Figma-to-React Implementation

## Purpose

Use this skill to convert a Figma design, screenshot, or website-inspired layout into a controlled React + TypeScript + Tailwind implementation plan.

The goal is not to blindly generate UI. The goal is to extract design information, plan components, implement one section at a time, and verify visually.

## When to use

Use this skill when:
- Implementing a Figma design
- Rebuilding a landing page section
- Creating UI from a screenshot
- Preparing a frontend assignment
- Improving portfolio UI quality

## Inputs to inspect

Read these files if available:

- `docs/DESIGN_SOURCE.md`
- `docs/DESIGN_SYSTEM.md`
- `docs/UI_SPEC.md`
- `docs/COMPONENT_MAP.md`
- `docs/RESPONSIVE_PLAN.md`
- `docs/ASSET_PLAN.md`
- `docs/FIGMA_TO_CODE_PLAN.md`
- `docs/VISUAL_QA_CHECKLIST.md`
- `design/screenshots/`
- Relevant Figma/design link

## Rules

- Do not implement the full design at once.
- Analyze before coding.
- Extract design tokens first.
- Implement one section/component at a time.
- Do not copy copyrighted brand assets.
- Use original content if replicating a public website.
- Use semantic HTML where possible.
- Verify desktop and mobile after implementation.

## Workflow

1. Inspect design source.
2. Extract colors, typography, spacing, radius, shadows.
3. Identify sections and reusable components.
4. Create responsive behavior plan.
5. Identify assets and replacement needs.
6. Create section implementation plan.
7. Implement only the approved section.
8. Return visual QA checklist.

## Output format

Return:

```md
# Figma-to-React Implementation Report

## Target design/source
-

## Design tokens
-

## Component map
-

## Responsive plan
-

## Assets needed
-

## Implementation order
1.
2.
3.

## Current task scope
-

## Files to create/edit
-

## Risks
-

## Visual QA checklist
-
```

## Completion criteria

This skill is complete when one scoped UI section can be implemented and visually verified without rewriting unrelated code.
```

---

## Skill 4: React UI polish

Create:

```txt
.agent/skills/04-react-ui-polish/SKILL.md
```

Content:

```md
---
name: react-ui-polish
description: Reviews and improves React + TypeScript + Tailwind UI for spacing, typography, responsiveness, component reuse, accessibility, visual consistency, and portfolio polish.
---

# Skill: React UI Polish

## Purpose

Use this skill to improve frontend UI quality after initial implementation.

The goal is to make the UI look professional, responsive, consistent, and portfolio-ready.

## When to use

Use this skill when:
- A page works but looks basic
- UI spacing is inconsistent
- Mobile layout is weak
- Components are duplicated
- Visual hierarchy is unclear
- Final project needs polish

## Inputs to inspect

Read these files/folders if available:

- `client/src/components/`
- `client/src/pages/`
- `client/src/app/` for Next.js
- `docs/DESIGN_SYSTEM.md`
- `docs/COMPONENT_MAP.md`
- `docs/RESPONSIVE_PLAN.md`
- `docs/VISUAL_QA_REPORT.md`
- Screenshots if available

## Rules

- Do not change business logic.
- Do not edit backend.
- Do not add unnecessary packages.
- Do not rewrite entire pages unless explicitly approved.
- Prefer small targeted improvements.
- Preserve accessibility.
- Keep design consistent with the design system.

## Workflow

1. Inspect target page/component.
2. Check layout, spacing, typography, colors, cards, buttons, forms.
3. Check responsiveness.
4. Check accessibility basics.
5. Identify duplicated UI.
6. Suggest minimal polish changes.
7. If asked to edit, change only scoped files.
8. Provide before/after verification steps.

## Output format

Return:

```md
# React UI Polish Report

## Target area
-

## Visual quality verdict
Strong / Acceptable / Needs polish / Weak

## What looks good
-

## Issues found
-

## Priority fixes
1.
2.
3.

## Responsive issues
-

## Accessibility issues
-

## Suggested scoped changes
-

## Files to edit
-

## Verification steps
-
```

## Completion criteria

This skill is complete when the UI has clearer hierarchy, better spacing, stronger responsiveness, and no unnecessary logic changes.
```

---

## Skill 5: Frontend state and route review

Create:

```txt
.agent/skills/05-frontend-state-route-review/SKILL.md
```

Content:

```md
---
name: frontend-state-route-review
description: Reviews React frontend routing, protected routes, admin routes, state ownership, context usage, API service separation, and UI states in MERN or Next.js projects.
---

# Skill: Frontend State and Route Review

## Purpose

Use this skill to review whether frontend state and routes are organized correctly.

The goal is to prevent broken navigation, weak route protection, messy state, duplicated API calls, and unclear user/admin flows.

## When to use

Use this skill when:
- Frontend routes are implemented
- Protected routes are added
- AuthContext or CartContext is created
- API service files are introduced
- Admin/customer route behavior must be verified

## Inputs to inspect

Read these files/folders if available:

- `client/src/routes/`
- `client/src/context/`
- `client/src/services/`
- `client/src/pages/`
- `client/src/components/layout/`
- `client/src/types/`
- `docs/FRONTEND_STATE_PLAN.md`
- `docs/FRONTEND_ROUTE_TEST_PLAN.md`
- `docs/AUTHORIZATION_MATRIX.md`

## Rules

- Do not edit backend.
- Do not remove protected routes.
- Do not move state randomly.
- Check role-based frontend behavior.
- Remember backend must still enforce security.
- Return route/state risks clearly.

## Workflow

1. Inspect route tree.
2. Identify public/protected/admin routes.
3. Check auth state.
4. Check role checks.
5. Check cart or user-flow state.
6. Check API service separation.
7. Check loading/error/empty states.
8. Return route/state review.

## Output format

Return:

```md
# Frontend State and Route Review

## Overall verdict
-

## Route groups
-

## State ownership
-

## Auth/protected route issues
-

## Admin route issues
-

## API service issues
-

## UI state issues
-

## Must-fix before integration
1.
2.
3.

## Verification checklist
-
```

## Completion criteria

This skill is complete when route behavior and state ownership are clear and safe for full-stack integration.
```

---

## Skill 6: Express API quality review

Create:

```txt
.agent/skills/06-express-api-quality-review/SKILL.md
```

Content:

```md
---
name: express-api-quality-review
description: Reviews Express.js REST API quality for MERN projects, including routes, controllers, services, validation, auth middleware, role checks, response format, and API contract alignment.
---

# Skill: Express API Quality Review

## Purpose

Use this skill to review a Node.js/Express backend before integration.

The goal is to ensure APIs are consistent, validated, secure, and aligned with the documented contract.

## When to use

Use this skill when:
- Backend routes are created
- API testing is about to start
- Frontend integration is about to start
- Admin APIs need security review
- Backend bugs appear during integration

## Inputs to inspect

Read these files/folders if available:

- `server/src/routes/`
- `server/src/modules/`
- `server/src/controllers/`
- `server/src/services/`
- `server/src/middlewares/`
- `server/src/models/`
- `server/src/utils/`
- `docs/API_CONTRACT.md`
- `docs/DATABASE_SCHEMA.md`
- `docs/AUTHORIZATION_MATRIX.md`
- `docs/BACKEND_API_TEST_PLAN.md`

## Rules

- Do not edit files unless explicitly asked.
- Do not remove auth or validation.
- Do not expose secrets.
- Check status codes.
- Check response shape.
- Check admin route protection.
- Check error handling.
- Return specific endpoint-level issues.

## Workflow

1. Inspect API contract.
2. Inspect route definitions.
3. Check controller/service separation.
4. Check validation.
5. Check authentication and authorization.
6. Check response format.
7. Check error handling.
8. Check database model alignment.
9. Return API quality report.

## Output format

Return:

```md
# Express API Quality Review Report

## Overall verdict
-

## API contract alignment
-

## Route issues
-

## Controller/service issues
-

## Validation issues
-

## Auth/authorization issues
-

## Response format issues
-

## Error handling issues
-

## Must-fix endpoints
| Endpoint | Issue | Priority |
|---|---|---|

## API test checklist
-
```

## Completion criteria

This skill is complete when backend APIs are ready for manual API testing and frontend integration.
```

---

## Skill 7: MongoDB schema review

Create:

```txt
.agent/skills/07-mongodb-schema-review/SKILL.md
```

Content:

```md
---
name: mongodb-schema-review
description: Reviews MongoDB/Mongoose schemas, relationships, indexes, validation, ownership, snapshot fields, and alignment with API/data requirements for MERN projects.
---

# Skill: MongoDB Schema Review

## Purpose

Use this skill to review database schema quality before API testing or full-stack integration.

The goal is to prevent weak models, missing relationships, inconsistent IDs, missing indexes, and broken order/booking history.

## When to use

Use this skill when:
- Mongoose models are created
- Database schema docs are written
- Order/booking/enrollment models are designed
- Admin queries are slow or unclear
- API response shape is inconsistent

## Inputs to inspect

Read these files if available:

- `docs/DATABASE_SCHEMA.md`
- `docs/API_CONTRACT.md`
- `docs/DATA_FLOW.md`
- `server/src/modules/**/**/*.model.ts`
- `server/src/models/`
- `server/src/types/`

## Rules

- Do not change database schema without explaining migration impact.
- Check required fields.
- Check references.
- Check status fields.
- Check indexes.
- Check timestamps.
- Check snapshot fields for submissions/orders.
- Check password hiding for User.
- Flag breaking changes.

## Workflow

1. Inspect schema docs.
2. Inspect Mongoose models.
3. Compare models with API contract.
4. Check relationships.
5. Check validation and indexes.
6. Check submission/order snapshot strategy.
7. Check ID consistency.
8. Return schema review.

## Output format

Return:

```md
# MongoDB Schema Review Report

## Overall verdict
-

## Model summary
-

## Alignment with database docs
-

## Required field issues
-

## Relationship/reference issues
-

## Validation issues
-

## Index recommendations
-

## Snapshot/history issues
-

## Breaking change warnings
-

## Recommended fixes
1.
2.
3.
```

## Completion criteria

This skill is complete when schemas support the app flows, APIs, history records, and admin queries safely.
```

---

## Skill 8: Auth and authorization review

Create:

```txt
.agent/skills/08-auth-authorization-review/SKILL.md
```

Content:

```md
---
name: auth-authorization-review
description: Reviews authentication and role-based authorization across frontend routes, backend APIs, JWT/session handling, password hashing, admin permissions, and ownership rules.
---

# Skill: Auth and Authorization Review

## Purpose

Use this skill to review whether authentication and authorization are implemented safely.

The goal is to prevent insecure admin APIs, missing token checks, password leaks, and broken user ownership rules.

## When to use

Use this skill when:
- Register/login are implemented
- Protected routes are added
- Admin APIs are created
- Backend integration begins
- Final project security review is needed

## Inputs to inspect

Read these files if available:

- `docs/AUTH_FLOW.md`
- `docs/AUTHORIZATION_MATRIX.md`
- `docs/BACKEND_SECURITY_CHECKLIST.md`
- `client/src/context/AuthContext.tsx`
- `client/src/routes/`
- `server/src/modules/auth/`
- `server/src/modules/users/`
- `server/src/middlewares/auth.middleware.ts`
- `server/src/middlewares/role.middleware.ts`
- API route files

## Rules

- Backend authorization is mandatory.
- Frontend hiding is not security.
- Never return passwords.
- Never commit secrets.
- Check token storage and Authorization header.
- Check users can only access their own data.
- Check admin role cannot be self-assigned from public request body.

## Workflow

1. Review auth flow.
2. Review register/login implementation.
3. Review password hashing and response sanitization.
4. Review frontend route guards.
5. Review backend auth middleware.
6. Review backend admin role checks.
7. Review ownership rules.
8. Review negative tests.
9. Return security report.

## Output format

Return:

```md
# Auth and Authorization Review Report

## Security verdict
Strong / Acceptable / Risky / Insecure

## Auth flow summary
-

## Password handling
-

## Token/session handling
-

## Frontend route protection
-

## Backend API protection
-

## Admin authorization
-

## User ownership rules
-

## Critical security issues
1.
2.
3.

## Required negative tests
-
```

## Completion criteria

This skill is complete when visitor/customer/admin access rules are enforced on both frontend and backend, with backend security as the source of truth.
```

---

## Skill 9: Full-stack integration debugger

Create:

```txt
.agent/skills/09-fullstack-integration-debugger/SKILL.md
```

Content:

```md
---
name: fullstack-integration-debugger
description: Diagnoses MERN full-stack integration bugs involving API base URLs, CORS, JWT headers, response shape, ID mismatch, form payloads, loading/error states, and frontend-backend data flow.
---

# Skill: Full-Stack Integration Debugger

## Purpose

Use this skill to debug issues that happen when a React frontend connects to an Express/MongoDB backend.

The goal is to identify whether a bug is caused by frontend state, API client, backend route, auth header, CORS, env variables, response shape, or database data.

## When to use

Use this skill when:
- Frontend works with mock data but fails with backend
- API works in Postman but fails in browser
- CORS error appears
- 401/403/404/500 happens
- Food/listing/order data is blank
- Checkout/order fails
- Admin APIs fail from frontend

## Inputs to inspect

Read these files if available:

- `docs/FULLSTACK_INTEGRATION_PLAN.md`
- `docs/API_CLIENT_PLAN.md`
- `docs/ENV_AND_CORS_CHECKLIST.md`
- `docs/INTEGRATION_BUG_LOG.md`
- `client/src/lib/api.ts`
- `client/src/services/`
- `client/src/context/AuthContext.tsx`
- Relevant frontend page
- Relevant backend route/controller/service
- Browser console/network evidence
- Backend logs

## Rules

- Do not guess.
- Use evidence from console, network tab, API response, and logs.
- Identify exact failing request.
- Check request URL, method, headers, body, status, and response.
- Do not change API contract unless necessary.
- Fix one bug at a time.
- Record bug and fix.

## Workflow

1. Identify the failing flow.
2. Inspect browser console.
3. Inspect network request.
4. Check API base URL.
5. Check CORS.
6. Check Authorization header.
7. Check request payload.
8. Check backend route.
9. Check response shape.
10. Suggest smallest safe fix and retest steps.

## Output format

Return:

```md
# Full-Stack Integration Debug Report

## Bug summary
-

## Failing flow
-

## Evidence
-

## Likely cause
-

## Files involved
-

## Request/response analysis
-

## Smallest safe fix
-

## Retest steps
-

## Bug log entry
| Bug | Cause | Fix | Status |
|---|---|---|---|
```

## Completion criteria

This skill is complete when the exact cause is identified and the retest path is clear.
```

---

## Skill 10: Browser verification

Create:

```txt
.agent/skills/10-browser-verification/SKILL.md
```

Content:

```md
---
name: browser-verification
description: Verifies MERN or Next.js app behavior in the browser by checking routes, user flows, admin flows, console errors, network requests, responsiveness, loading/error states, and visual issues.
---

# Skill: Browser Verification

## Purpose

Use this skill to verify whether the app works in the browser like a real user would use it.

The goal is to avoid saying "done" just because code was generated.

## When to use

Use this skill when:
- Frontend pages are implemented
- Full-stack integration is complete
- A bug needs reproduction
- Project is ready for QA
- Project is ready for deployment
- Live deployment needs smoke testing

## Inputs to inspect

Use available browser tools and read:

- `docs/BROWSER_TEST_REPORT.md`
- `docs/FULLSTACK_BROWSER_QA_REPORT.md`
- `docs/QA_CHECKLIST.md`
- `docs/BUG_LOG.md`
- `docs/PRODUCTION_SMOKE_TEST_REPORT.md`
- Local or live frontend URL
- Backend URL if needed

## Rules

- Do not edit files during verification unless explicitly asked.
- Test exact flows.
- Check console.
- Check network.
- Check mobile width.
- Capture evidence if available.
- Report pass/fail clearly.
- Create bug entries for failures.

## Workflow

1. Open the app.
2. Test route-by-route.
3. Test visitor flow.
4. Test login/register.
5. Test user action flow.
6. Test admin flow.
7. Test unauthorized behavior.
8. Check console errors.
9. Check network errors.
10. Check mobile responsiveness.
11. Return QA report.

## Output format

Return:

```md
# Browser Verification Report

## Environment
Local / Deployed

## URLs tested
-

## Flows tested
| Flow | Result | Notes |
|---|---|---|

## Console errors
-

## Network errors
-

## Mobile issues
-

## UI/visual issues
-

## Bugs found
-

## Final verdict
Pass / Conditional pass / Fail
```

## Completion criteria

This skill is complete when tested flows have clear pass/fail status and all blocking bugs are documented.
```

---

## Skill 11: Test plan generator

Create:

```txt
.agent/skills/11-test-plan-generator/SKILL.md
```

Content:

```md
---
name: test-plan-generator
description: Generates a practical testing strategy for MERN or Next.js projects, including manual browser QA, API tests, authorization tests, component tests, E2E tests, Lighthouse, bug log, and regression checklist.
---

# Skill: Test Plan Generator

## Purpose

Use this skill to create a realistic testing plan for a full-stack project.

The goal is to ensure critical user/admin flows are tested without creating unnecessary enterprise-level complexity.

## When to use

Use this skill when:
- App features are mostly implemented
- Backend APIs are ready
- Full-stack integration is done
- Final assignment QA is starting
- Project is close to deployment

## Inputs to inspect

Read these files if available:

- `docs/API_CONTRACT.md`
- `docs/AUTHORIZATION_MATRIX.md`
- `docs/FEATURE_SCOPE.md`
- `docs/PAGE_ROUTE_MAP.md`
- `docs/TESTING_STRATEGY.md`
- `docs/QA_CHECKLIST.md`
- `docs/BUG_LOG.md`
- `client/src/`
- `server/src/`

## Rules

- Include happy paths and negative tests.
- Include visitor/customer/admin role tests.
- Include API and browser tests.
- Include mobile/responsive checks.
- Include bug log and regression checks.
- Keep the plan practical for junior developers.
- Do not invent unsupported features.

## Workflow

1. Identify app features.
2. Identify user roles.
3. Identify critical flows.
4. Create manual QA plan.
5. Create API test plan.
6. Create authorization tests.
7. Suggest component tests.
8. Suggest E2E tests.
9. Add Lighthouse/accessibility checks.
10. Return testing deliverables.

## Output format

Return:

```md
# Test Plan

## Critical flows
-

## Manual browser QA
-

## API tests
-

## Authorization tests
-

## Component tests
-

## E2E tests
-

## Lighthouse/accessibility checks
-

## Regression checklist
-

## Required test evidence
-
```

## Completion criteria

This skill is complete when the project has a clear QA path from manual testing to final signoff.
```

---

## Skill 12: Deployment readiness review

Create:

```txt
.agent/skills/12-deployment-readiness-review/SKILL.md
```

Content:

```md
---
name: deployment-readiness-review
description: Reviews MERN or Next.js project readiness for deployment, including build scripts, env variables, Git hygiene, CORS, API URLs, MongoDB Atlas, Vercel/Render settings, secrets, README, and smoke tests.
---

# Skill: Deployment Readiness Review

## Purpose

Use this skill to check whether a project is ready for production deployment.

The goal is to catch deployment blockers before pushing to Vercel, Render, or another platform.

## When to use

Use this skill when:
- Local app works
- QA is mostly complete
- Preparing Vercel/Render deployment
- Deployment failed
- Updating README before submission

## Inputs to inspect

Read these files if available:

- `package.json`
- `client/package.json`
- `server/package.json`
- `.gitignore`
- `client/.env.example`
- `server/.env.example`
- `client/src/lib/api.ts`
- `server/src/app.ts`
- `server/src/config/env.ts`
- `README.md`
- `docs/DEPLOYMENT_PLAN.md`
- `docs/PRODUCTION_ENV_CHECKLIST.md`
- `docs/PRODUCTION_SMOKE_TEST_PLAN.md`

## Rules

- Do not expose secrets.
- Do not commit `.env`.
- Check local build first.
- Check hardcoded localhost URLs.
- Check CORS production URL.
- Check frontend production API URL.
- Check backend start command.
- Check database network access notes.
- Return blockers clearly.

## Workflow

1. Check Git hygiene.
2. Check build scripts.
3. Check env examples.
4. Check API URL strategy.
5. Check CORS strategy.
6. Check database deployment readiness.
7. Check platform settings.
8. Check README.
9. Return readiness verdict and fixes.

## Output format

Return:

```md
# Deployment Readiness Review

## Verdict
Ready / Almost ready / Not ready

## Blocking issues
1.
2.
3.

## Frontend deployment checklist
-

## Backend deployment checklist
-

## Database checklist
-

## Env/secrets checklist
-

## CORS/API URL risks
-

## README/submission issues
-

## Smoke test plan
-
```

## Completion criteria

This skill is complete when the project has no blocking deployment issue and smoke test steps are clear.
```

---

## Skill 13: Portfolio README generator

Create:

```txt
.agent/skills/13-portfolio-readme-generator/SKILL.md
```

Content:

```md
---
name: portfolio-readme-generator
description: Creates or improves a portfolio-ready GitHub README for MERN or Next.js projects, including summary, live links, demo credentials, features, tech stack, screenshots, setup, env variables, APIs, testing, deployment, limitations, and future improvements.
---

# Skill: Portfolio README Generator

## Purpose

Use this skill to create or improve a README that recruiters, mentors, and interviewers can quickly understand and test.

The goal is to make the project presentable without exaggerating features.

## When to use

Use this skill when:
- Final project is complete
- Deployment is complete
- GitHub repository needs polish
- Preparing job applications
- Preparing portfolio submission

## Inputs to inspect

Read these files if available:

- `README.md`
- `docs/PROJECT_BRIEF.md`
- `docs/PRD.md`
- `docs/FEATURE_SCOPE.md`
- `docs/API_CONTRACT.md`
- `docs/ARCHITECTURE_OVERVIEW.md`
- `docs/TESTING_STRATEGY.md`
- `docs/PRODUCTION_SMOKE_TEST_REPORT.md`
- `docs/FINAL_SUBMISSION_CHECKLIST.md`
- Screenshots folder

## Rules

- Do not invent features.
- Do not expose secrets.
- Do not use real personal passwords.
- Include honest known limitations.
- Make live links and demo credentials easy to find.
- Keep setup instructions accurate.
- Mention testing evidence.
- Mention deployment stack.

## Workflow

1. Identify project value.
2. Identify roles and features.
3. Identify tech stack.
4. Identify live links and demo credentials.
5. Identify setup steps.
6. Identify env variables.
7. Identify API overview.
8. Identify testing/deployment evidence.
9. Draft or improve README.

## Output format

Return a README with these sections:

```md
# Project Name

## Summary

## Live Links

## Demo Credentials

## Features

## Tech Stack

## Screenshots

## Folder Structure

## Local Setup

## Environment Variables

## API Overview

## User Roles

## Testing and QA

## Deployment

## Known Limitations

## Future Improvements

## Learning Reflection
```

## Completion criteria

This skill is complete when the README is accurate, testable, recruiter-friendly, and honest.
```

---

## Skill 14: Interview project explainer

Create:

```txt
.agent/skills/14-interview-project-explainer/SKILL.md
```

Content:

```md
---
name: interview-project-explainer
description: Helps developers prepare interview-ready explanations for MERN or Next.js projects, including 30-second pitch, technical architecture, frontend flow, backend flow, database design, auth, testing, deployment, AI usage, bugs, and STAR stories.
---

# Skill: Interview Project Explainer

## Purpose

Use this skill to prepare confident interview explanations for a finished project.

The goal is to help the developer explain the project clearly without sounding like they blindly used AI.

## When to use

Use this skill when:
- Final project is complete
- Preparing mock interviews
- Updating resume/portfolio
- Writing LinkedIn project post
- Practicing project walkthrough

## Inputs to inspect

Read these files if available:

- `README.md`
- `docs/PORTFOLIO_CASE_STUDY.md`
- `docs/FINAL_ASSIGNMENT_REFLECTION.md`
- `docs/API_TEST_REPORT.md`
- `docs/BUG_LOG.md`
- `docs/PRODUCTION_SMOKE_TEST_REPORT.md`
- `docs/AI_USAGE_DISCLOSURE.md`
- `docs/INTERVIEW_PROJECT_EXPLANATION.md`

## Rules

- Do not exaggerate.
- Do not claim features that do not exist.
- Explain AI usage responsibly.
- Emphasize personal understanding and verification.
- Include one real bug and fix.
- Include known limitations.
- Keep answers concise and interview-friendly.

## Workflow

1. Identify project summary.
2. Identify user roles and main flows.
3. Explain frontend architecture.
4. Explain backend architecture.
5. Explain database schema.
6. Explain auth/authorization.
7. Explain testing/deployment.
8. Identify one bug story.
9. Prepare 30-second and 1-minute answers.
10. Prepare technical Q&A.

## Output format

Return:

```md
# Interview Project Explanation

## 30-second pitch
-

## 1-minute explanation
-

## Technical architecture
-

## Frontend flow
-

## Backend flow
-

## Database design
-

## Auth and authorization
-

## Testing and QA
-

## Deployment
-

## AI usage explanation
-

## One bug and solution
-

## Known limitations
-

## 10 likely interview questions and answers
-
```

## Completion criteria

This skill is complete when the developer can explain the project confidently in a technical interview.
```

---

# Part 4: How to install/copy your personal skill library

## Option 1: Copy into project

For each project, copy:

```txt
.agent/skills/
```

into the project root.

Use this when:

```txt
You want project-specific skills committed with the repository.
```

This is ideal for final assignment projects.

---

## Option 2: Keep a personal global library

Create a personal skills repository:

```txt
awesome-antigravity-personal-skills/
  skills/
    react-ui-polish/
      SKILL.md
    express-api-quality-review/
      SKILL.md
    deployment-readiness-review/
      SKILL.md
```

Then copy selected skills into new projects.

Use this when:

```txt
You want your own reusable skills across all future projects.
```

---

## Option 3: Build a GitHub template repo

Create a GitHub template repository:

```txt
mern-antigravity-skills-template
```

Structure:

```txt
.agent/
  skills/
    SKILL_INDEX.md
    project-planning-review/
    mern-architecture-review/
    react-ui-polish/
    express-api-quality-review/
    browser-verification/
docs/
  SKILL_TEST_REPORT.md
README.md
```

Then students can create a new project from the template.

---

# Part 5: Skill testing workflow

A skill is not complete until you test it.

Create:

```txt
docs/SKILL_TEST_REPORT.md
```

Template:

```md
# SKILL_TEST_REPORT

## Skill tested
-

## Test project
-

## Test prompt
-

## Expected behavior
-

## Actual behavior
-

## What worked
-

## What failed
-

## Prompt/description improvements needed
-

## Updated skill?
Yes / No

## Final verdict
Pass / Needs revision / Fail
```

---

## Skill test prompt template

Use this:

```txt
Use the [skill-name] skill.

Task:
[Write task]

Rules:
- Analyze first.
- Do not edit files yet.
- Return the skill's expected report format.
```

Example:

```txt
Use the express-api-quality-review skill.

Task:
Review my backend APIs against docs/API_CONTRACT.md and docs/AUTHORIZATION_MATRIX.md.

Rules:
- Analyze first.
- Do not edit files yet.
- Return the Express API Quality Review Report format.
```

---

# Part 6: Skill improvement loop

Skills should improve over time.

Use this loop:

```txt
Use skill
→ Review output
→ Identify missing instruction
→ Update SKILL.md
→ Test again
→ Save improved version
```

Example:

If `react-ui-polish` keeps changing business logic, add:

```txt
Do not change business logic.
Do not edit API services.
Only adjust UI components and styling unless explicitly approved.
```

If `deployment-readiness-review` forgets CORS, add:

```txt
Always inspect backend CORS config and production CLIENT_URL.
```

If `express-api-quality-review` forgets status codes, add:

```txt
Check expected status codes for every endpoint.
```

---

# Part 7: Skill quality checklist

Use this checklist for each skill.

```md
# Skill Quality Checklist

- [ ] Skill has clear name
- [ ] Skill has specific description
- [ ] Skill says when to use it
- [ ] Skill lists inputs/files to inspect
- [ ] Skill has safety rules
- [ ] Skill has step-by-step workflow
- [ ] Skill has output format
- [ ] Skill has completion criteria
- [ ] Skill avoids vague instructions
- [ ] Skill avoids asking for broad rewrites
- [ ] Skill includes verification steps
- [ ] Skill has been tested once
```

---

# Part 8: Using skills with NotebookLM

NotebookLM can help improve your skills.

Add these sources:

```txt
1. This module file
2. Your SKILL.md files
3. Antigravity official skills docs
4. Antigravity skills codelab
5. Your project docs
6. Your bug logs
7. Your final assignment reflection
```

Then use these prompts.

## NotebookLM Prompt 1: Skill library reviewer

```txt
Review my reusable Antigravity SKILL.md library.

Check:
1. Are skill names clear?
2. Are descriptions specific enough?
3. Are inputs/files to inspect clear?
4. Are safety rules strong?
5. Are workflows practical?
6. Are output formats consistent?
7. Which skills are too broad?
8. Which skills are missing?
9. How can I improve this library for MERN projects?

Return a prioritized improvement report.
```

---

## NotebookLM Prompt 2: Skill test plan

```txt
Create a test plan for my Antigravity skill library.

For each skill, provide:
1. Test prompt
2. Expected output
3. Files needed
4. Failure signs
5. Improvement suggestions
```

---

## NotebookLM Prompt 3: Convert repeated prompts into skills

```txt
Analyze my repeated Antigravity prompts and convert them into reusable SKILL.md files.

For each new skill:
1. Name
2. Description
3. When to use
4. Inputs to inspect
5. Safety rules
6. Workflow
7. Output format
8. Completion criteria
```

---

# Part 9: Required official/resource links

Add these to NotebookLM or notes:

| Resource | Link | Why it matters |
|---|---|---|
| Antigravity Agent Skills docs | https://antigravity.google/docs/skills | Official skills concept and structure |
| Authoring Google Antigravity Skills codelab | https://codelabs.developers.google.com/getting-started-with-antigravity-skills | Hands-on skill authoring guidance |
| Autonomous AI Developer Pipelines codelab | https://codelabs.developers.google.com/autonomous-ai-developer-pipelines-antigravity | Shows agents/skills/workflow orchestration patterns |
| Antigravity home/docs | https://antigravity.google/docs/home | General Antigravity documentation hub |
| Google Codelabs | https://codelabs.developers.google.com/ | Additional Google developer tutorials |
| Markdown Guide | https://www.markdownguide.org/basic-syntax/ | Useful for writing clean SKILL.md files |
| GitHub README docs | https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes | Useful for documenting your skill library repo |

---

# Part 10: Required video resources

Watch at least two videos.

Search YouTube:

```txt
Google Antigravity skills tutorial
Antigravity SKILL.md tutorial
Google Antigravity agents.md skills.md workflow
How to create reusable AI coding prompts
AI coding agent workflow skills
Antigravity skills codelab walkthrough
```

Recommended video types:

| Video type | Why |
|---|---|
| Antigravity skills tutorial | Understand skill creation visually |
| Antigravity codelab walkthrough | Learn official workflow in action |
| AI coding agent workflow tutorial | Understand reusable workflows |
| Prompt-to-skill conversion tutorial | Learn how to reduce repeated prompts |
| Code review automation with AI agents | Learn quality-control workflows |

---

## Video learning notes

Create:

```txt
docs/notebooklm/bonus-reusable-skill-library-video-learning-notes.md
```

Use this format:

```md
# Bonus Reusable SKILL.md Library Video Learning Notes

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

# Part 11: Practice tasks

## Practice Task 1: Create skill folders

Create:

```txt
.agent/skills/
```

Then create at least five skills:

```txt
project-planning-review
mern-architecture-review
react-ui-polish
express-api-quality-review
browser-verification
```

---

## Practice Task 2: Create SKILL_INDEX

Create:

```txt
.agent/skills/SKILL_INDEX.md
```

List every skill, purpose, and when to use it.

---

## Practice Task 3: Test one planning skill

Use:

```txt
project-planning-review
```

Test prompt:

```txt
Use the project-planning-review skill to review my project docs.

Rules:
- Analyze first.
- Do not edit files yet.
- Return the expected report format.
```

Save result in:

```txt
docs/SKILL_TEST_REPORT.md
```

---

## Practice Task 4: Test one coding review skill

Use either:

```txt
express-api-quality-review
react-ui-polish
mongodb-schema-review
```

Save result in:

```txt
docs/SKILL_TEST_REPORT.md
```

---

## Practice Task 5: Improve a skill

After testing, update one skill based on what went wrong.

Example:

```txt
The skill changed code without permission.
```

Fix:

```txt
Add rule: Do not edit files unless explicitly asked.
```

---

## Practice Task 6: Create personal skill repo

Create a new repo:

```txt
awesome-antigravity-mern-skills
```

Add:

```txt
README.md
skills/
examples/
docs/SKILL_TEST_REPORT.md
```

---

## Practice Task 7: Use a skill in final project

Copy at least five skills into your final assignment repo.

Document usage in:

```txt
docs/ANTIGRAVITY_USAGE_LOG.md
```

---

## Practice Task 8: Convert repeated prompt into skill

Find one long prompt you repeatedly use.

Convert it into a new skill.

Recommended examples:

```txt
job-assignment-requirements-review
nextjs-migration-review
resume-project-bullet-generator
figma-ui-replication-review
```

---

## Practice Task 9: Create skill checklist

Create:

```txt
docs/SKILL_QUALITY_CHECKLIST.md
```

Complete it for each skill.

---

## Practice Task 10: Reflection

Create:

```txt
docs/reflections/16-bonus-module-reusable-skill-md-library-reflection.md
```

Use the template below.

---

# Required deliverables

Submit:

```txt
1. .agent/skills/SKILL_INDEX.md
2. At least 5 skill folders with SKILL.md
3. Recommended: all 14 skills
4. docs/SKILL_TEST_REPORT.md
5. docs/SKILL_QUALITY_CHECKLIST.md
6. docs/ANTIGRAVITY_USAGE_LOG.md update
7. NotebookLM skill library review screenshot
8. NotebookLM skill test plan screenshot
9. Video learning notes
10. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/16-bonus-module-reusable-skill-md-library-reflection.md
```

Use:

```md
# Reflection: Bonus Module - Reusable SKILL.md Library

## Skills I created
-

## Why I selected these skills
-

## Skill I tested first
-

## What worked well
-

## What did not work well
-

## Skill improvement I made
-

## How this will save tokens/time
-

## How this will improve project quality
-

## How I will reuse these skills in future projects
-

## What Antigravity helped with
-

## What I had to correct manually
-
```

---

# Quiz

## Multiple choice

**1. What is the main purpose of a reusable `SKILL.md` library?**

A. To avoid learning code  
B. To package repeatable AI workflows for consistent use across projects  
C. To replace GitHub  
D. To store private passwords  

Correct answer: **B**

---

**2. What should a good skill description do?**

A. Clearly explain what the skill does and when it should be used  
B. Say only "help me"  
C. Include secret keys  
D. Avoid task details  

Correct answer: **A**

---

**3. Which file should summarize all available skills?**

A. `SKILL_INDEX.md`  
B. `.env`  
C. `node_modules`  
D. `dist/index.js`  

Correct answer: **A**

---

**4. What should a skill do before editing files?**

A. Analyze and report first, unless explicitly asked to edit  
B. Rewrite the full project immediately  
C. Delete old docs  
D. Commit secrets  

Correct answer: **A**

---

**5. Which skill would review Express routes, controllers, validation, and auth middleware?**

A. `express-api-quality-review`  
B. `react-ui-polish`  
C. `portfolio-readme-generator`  
D. `interview-project-explainer`  

Correct answer: **A**

---

**6. Why test a skill?**

A. To verify it triggers the right workflow and produces useful output  
B. To avoid reading the output  
C. To delete the project  
D. To publish secrets  

Correct answer: **A**

---

**7. What should you do if a skill keeps making broad edits?**

A. Add stricter scope and safety rules  
B. Let it rewrite everything  
C. Remove all instructions  
D. Add database password  

Correct answer: **A**

---

**8. What should not be included inside a public skill library?**

A. Private secrets or credentials  
B. Output formats  
C. Safety rules  
D. Workflow steps  

Correct answer: **A**

---

**9. What is a good use for `browser-verification` skill?**

A. Testing app flows, console errors, network errors, and mobile layout  
B. Creating MongoDB passwords  
C. Replacing all QA  
D. Writing unrelated essays  

Correct answer: **A**

---

**10. What is the best mindset for reusable skills?**

A. Treat them as repeatable operating procedures  
B. Treat them as random one-line prompts  
C. Treat them as database backups  
D. Treat them as hidden secrets  

Correct answer: **A**

---

## Short-answer questions

1. What is a reusable `SKILL.md` library?
2. What is the difference between a prompt and a skill?
3. What should every skill include?
4. What are five skills useful for MERN projects?
5. Why should a skill include safety rules?
6. Why should a skill include output format?
7. How can skills reduce token usage?
8. How can skills improve project quality?
9. How do you test a skill?
10. How will you reuse your skills in future projects?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Folder structure | `.agent/skills/` created correctly |
| Skill index | `SKILL_INDEX.md` lists skills clearly |
| Minimum skills | At least 5 useful skills created |
| Recommended skills | 14-skill library created |
| Skill quality | Each skill has name, description, rules, workflow, output format |
| Safety | Skills prevent uncontrolled broad edits |
| Testing | At least 2 skills tested |
| Improvement loop | At least 1 skill improved after test |
| Reuse plan | Student explains how to reuse in future projects |
| NotebookLM evidence | Skill review and test plan generated |
| Reflection | Student explains skill library value clearly |

---

# Completion standard

You complete this bonus module only when you can confidently say:

```txt
I can build, test, improve, and reuse a personal Antigravity SKILL.md library that helps me plan, review, build, test, deploy, document, and explain MERN or Next.js projects with consistent AI-assisted workflows.
```

After completing this module, copy your best skills into every serious project before starting implementation.
