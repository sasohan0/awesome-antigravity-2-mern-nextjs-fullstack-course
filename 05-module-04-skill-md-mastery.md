# Module 4: `SKILL.md` Mastery — Create Reusable Antigravity Skills for MERN Projects

**File Name:** `05-module-04-skill-md-mastery.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 4–6 hours  
**Recommended After:** Module 3: Codebase and Architecture Thinking  
**Main Goal:** Learn how to create focused `SKILL.md` files that make Antigravity follow repeatable development workflows.

---

## Module purpose

In the previous modules, you learned how to:

- Understand the bootcamp workflow
- Use NotebookLM for learning
- Use Antigravity safely
- Create project specifications
- Understand full-stack architecture

Now you will learn one of the most important Antigravity power-user skills:

```txt
Writing useful SKILL.md files.
```

A `SKILL.md` file gives Antigravity reusable instructions for a specific kind of task.

Instead of repeating the same long prompt again and again, you can create a skill once and reuse it whenever that task appears.

For example, instead of repeatedly saying:

```txt
Review my Express route, controller, service, validation, auth middleware, response format, and error handling. Make sure it follows my project architecture. Do not change unrelated files. Return a review report first.
```

You can create a skill called:

```txt
express-api-quality-review
```

Then use it whenever you need backend API review.

This module will teach you how to create skills for:

- MERN architecture review
- React UI polish
- Figma-to-code implementation
- Express API quality review
- MongoDB schema review
- Browser verification
- Testing plan generation
- Deployment readiness
- Portfolio README generation

The goal is to make Antigravity behave less like a random coding assistant and more like a disciplined project teammate.

---

## What is a skill?

A skill is a reusable instruction package.

In Antigravity and other modern agent systems, a skill usually lives in a folder and includes a `SKILL.md` file.

The skill tells the agent:

- What the skill is
- When to use it
- What inputs it needs
- What process it should follow
- What constraints it must obey
- What output format it should return
- What examples it can follow

A simple skill folder looks like this:

```txt
.agent/
  skills/
    express-api-quality-review/
      SKILL.md
```

A more advanced skill can include references:

```txt
.agent/
  skills/
    express-api-quality-review/
      SKILL.md
      references/
        api-quality-checklist.md
        response-format.md
```

In this bootcamp, you will mostly create skills with:

```txt
SKILL.md
references/
```

You will avoid scripts for now unless you understand exactly what they do.

---

## Why skills matter for junior MERN developers

Skills help junior developers because they:

1. Reduce repeated prompting.
2. Improve consistency.
3. Save quota.
4. Keep instructions close to the project.
5. Help Antigravity understand project standards.
6. Make tasks easier to review.
7. Reduce random output.
8. Encourage safe workflows.
9. Create reusable engineering habits.
10. Improve portfolio-quality development.

Without skills, every prompt becomes long and repetitive.

With skills, you can make Antigravity follow a specific pattern every time.

---

## Skills are not magic

A skill does not guarantee perfect work.

You still need to:

- Review the output
- Check file changes
- Test manually
- Verify in browser
- Check security
- Check build errors
- Commit carefully

Think of skills as reusable instructions.

Not as automatic quality guarantee.

---

## Skill mental model

A good skill answers these questions:

| Question | Why it matters |
|---|---|
| What task is this skill for? | Prevents broad/unfocused behavior |
| When should the agent use this skill? | Helps correct triggering |
| When should the agent not use it? | Prevents misuse |
| What inputs are required? | Avoids guessing |
| What workflow should be followed? | Creates consistency |
| What constraints must be obeyed? | Protects project quality |
| What output format is expected? | Makes result reviewable |
| What examples are included? | Helps the agent understand usage |

---

## Project-specific skills vs reusable skills

There are two types of skills.

### Project-specific skill

A project-specific skill mentions one exact project.

Example:

```txt
localbites-order-flow-review
```

It may include:

- LocalBites-specific roles
- LocalBites food/order models
- LocalBites routes
- LocalBites UI rules

This is useful for one project.

---

### Reusable skill

A reusable skill works across many projects.

Example:

```txt
express-api-quality-review
```

It focuses on general Express API quality:

- Routes
- Controllers
- Services
- Validation
- Auth
- Response format
- Error handling
- Status codes

Reusable skills are better for your personal skill library.

In this module, you will create **project-level skills** for the current project.

In the bonus module later, you will create a reusable skill library for all future projects.

---

## Recommended skill folder structure for this course

Inside your project, create:

```txt
.agent/
  skills/
    mern-architecture-review/
      SKILL.md
    react-ui-polish/
      SKILL.md
    figma-to-react-implementation/
      SKILL.md
    express-api-quality-review/
      SKILL.md
    mongodb-schema-review/
      SKILL.md
    browser-verification/
      SKILL.md
    test-plan-generator/
      SKILL.md
    deployment-readiness-review/
      SKILL.md
    portfolio-readme-generator/
      SKILL.md
```

If Antigravity uses a different skill directory in your setup, follow the current Antigravity instructions, but keep the same skill content.

---

## Anatomy of a `SKILL.md` file

A `SKILL.md` file has two major sections:

1. YAML frontmatter
2. Markdown instruction body

Example:

```md
---
name: express-api-quality-review
description: Use this skill when reviewing Express.js route, controller, service, validation, authentication, authorization, response format, and error handling quality for a MERN backend API. Do not use it for frontend UI review or database schema design only.
---

# Express API Quality Review

## Goal

Review Express API implementation for correctness, security, consistency, and maintainability.

## When to use

Use this skill when:
- Reviewing a new Express API endpoint
- Reviewing route/controller/service structure
- Checking validation and auth middleware
- Checking API response format

## Required inputs

- API contract
- Relevant route files
- Relevant controller files
- Relevant service files
- Validation schemas
- Auth/role middleware where relevant

## Workflow

1. Read the API contract.
2. Read only relevant backend files.
3. Compare implementation against contract.
4. Check validation.
5. Check authentication and authorization.
6. Check response format.
7. Check error handling.
8. Return a review report before suggesting edits.

## Constraints

- Do not edit files unless explicitly asked.
- Do not modify unrelated modules.
- Do not remove validation or auth.
- Do not expose secrets.
- Do not install packages without approval.

## Output format

Return:
1. Summary
2. Files reviewed
3. Contract match/mismatch
4. Security issues
5. Validation issues
6. Error handling issues
7. Required fixes
8. Final verdict
```

---

## YAML frontmatter

The top section is metadata.

```md
---
name: skill-name
description: Clear description of what the skill does and when to use it.
---
```

### `name`

The skill name should be:

- Short
- Specific
- Lowercase
- Hyphenated
- Task-focused

Good names:

```txt
mern-architecture-review
react-ui-polish
express-api-quality-review
mongodb-schema-review
browser-verification
```

Weak names:

```txt
coding-helper
good-skill
make-project-better
fullstack-master
do-everything
```

---

### `description`

The description is extremely important.

The description tells the agent when the skill is relevant.

Weak description:

```txt
Helps with backend.
```

Better description:

```txt
Use this skill when reviewing Express.js route, controller, service, validation, authentication, authorization, response format, and error handling quality for a MERN backend API. Do not use it for frontend UI review or database schema design only.
```

A strong description includes:

- Exact task
- Stack or domain
- When to use
- When not to use
- Keywords the agent can match

---

## Markdown instruction body

The body should include:

```txt
1. Goal
2. When to use
3. When not to use
4. Required inputs
5. Workflow
6. Quality checklist
7. Constraints
8. Output format
9. Example prompt
```

This makes the skill clear and reviewable.

---

## Universal `SKILL.md` template

Use this template for every skill:

```md
---
name: skill-name
description: Use this skill when [specific situation]. It helps with [specific task]. Do not use this skill for [clear non-use case].
---

# Skill Title

## Goal

Explain what this skill helps the agent do.

## When to use this skill

Use this skill when:
- ...

## When not to use this skill

Do not use this skill when:
- ...

## Required inputs

Before using this skill, the project should provide:
- ...

## Workflow

1. Read the required inputs.
2. Identify missing context.
3. Create a plan before editing.
4. List files that may be changed.
5. Ask for approval if the task is risky.
6. Execute only the requested scope.
7. Verify the result.
8. Summarize changes and remaining risks.

## Quality checklist

- [ ] Scope is clear
- [ ] No unrelated feature added
- [ ] Required files reviewed
- [ ] Risks identified
- [ ] Output is easy to review
- [ ] Verification step included

## Constraints

- Do not modify unrelated files.
- Do not install packages unless required and approved.
- Do not expose secrets.
- Do not remove tests or validation to make code pass.
- Do not claim success without verification.

## Output format

Return:

1. Summary
2. Files reviewed
3. Plan
4. Risks
5. Recommended changes
6. Verification steps
7. Final verdict

## Example prompt

Use this skill to [example task].

Inputs:
- [file 1]
- [file 2]

Goal:
- [goal]
```

---

# Part 1: Create `mern-architecture-review` skill

## Purpose

This skill reviews whether the project architecture is clear and consistent.

Create:

```txt
.agent/skills/mern-architecture-review/SKILL.md
```

Content:

```md
---
name: mern-architecture-review
description: Use this skill when reviewing MERN project architecture, including frontend structure, backend structure, database design, auth flow, authorization rules, data flow, error flow, and folder organization. Do not use it for detailed UI styling or single API endpoint review.
---

# MERN Architecture Review

## Goal

Review the full-stack MERN architecture for clarity, consistency, security, maintainability, and alignment with project requirements.

## When to use this skill

Use this skill when:
- Reviewing architecture docs before coding
- Checking if frontend/backend/database responsibilities are clear
- Checking if page routes match API and database design
- Reviewing auth and authorization architecture
- Reviewing data flow and error flow
- Preparing for implementation

## When not to use this skill

Do not use this skill when:
- Only polishing UI visuals
- Only reviewing one Express endpoint
- Only reviewing CSS/Tailwind
- Only writing README
- Only debugging a small runtime error

## Required inputs

Read relevant files such as:
- docs/PROJECT_BRIEF.md
- docs/PRD.md
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTHORIZATION_MATRIX.md
- docs/ARCHITECTURE_OVERVIEW.md
- docs/FRONTEND_ARCHITECTURE.md
- docs/BACKEND_ARCHITECTURE.md
- docs/DATA_FLOW.md
- docs/ERROR_FLOW.md

## Workflow

1. Read the project brief and PRD.
2. Identify user roles and core features.
3. Review frontend structure and route planning.
4. Review backend route/controller/service/model structure.
5. Review database collections and relationships.
6. Review authentication and authorization boundaries.
7. Review data flow for key user actions.
8. Review error flow and API response format.
9. Identify inconsistencies.
10. Return a review report before editing.

## Quality checklist

- [ ] User roles are clear
- [ ] Frontend and backend responsibilities are separated
- [ ] Routes match pages
- [ ] APIs match frontend needs
- [ ] Database schema supports required features
- [ ] Auth flow is clear
- [ ] Authorization is enforced server-side
- [ ] Data flow is understandable
- [ ] Error flow is consistent
- [ ] Scope is realistic

## Constraints

- Do not create app code unless explicitly asked.
- Do not modify unrelated files.
- Do not invent new major features.
- Do not weaken security.
- Do not remove auth or validation requirements.
- Do not claim the architecture is production-ready without noting risks.

## Output format

Return:
1. Architecture summary
2. Files reviewed
3. Strong parts
4. Missing parts
5. Inconsistencies
6. Security concerns
7. Required fixes before coding
8. Optional improvements
9. Final verdict: Ready / Needs revision / Not ready

## Example prompt

Use the mern-architecture-review skill.

Read:
- docs/PROJECT_BRIEF.md
- docs/PRD.md
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTHORIZATION_MATRIX.md
- docs/DATA_FLOW.md

Do not edit files yet.

Return an architecture review report.
```

---

# Part 2: Create `react-ui-polish` skill

## Purpose

This skill reviews React/Tailwind UI quality.

Create:

```txt
.agent/skills/react-ui-polish/SKILL.md
```

Content:

```md
---
name: react-ui-polish
description: Use this skill when reviewing or improving React and Tailwind CSS UI quality, including layout, spacing, responsiveness, typography, component reuse, visual hierarchy, loading states, empty states, and error states. Do not use it for backend API or database review.
---

# React UI Polish

## Goal

Review and improve React/Tailwind UI so it becomes clean, responsive, accessible, and portfolio-ready.

## When to use this skill

Use this skill when:
- Reviewing a page after implementation
- Improving spacing and layout
- Checking mobile responsiveness
- Checking visual hierarchy
- Checking component reuse
- Adding loading, empty, and error states
- Matching a Figma design

## When not to use this skill

Do not use this skill when:
- Reviewing backend routes
- Designing database schema
- Writing deployment config
- Changing auth logic
- Making broad full-project changes

## Required inputs

Read relevant files such as:
- Figma/design screenshots
- docs/DESIGN_SYSTEM.md
- docs/UI_SPEC.md
- Relevant page files
- Relevant component files
- Tailwind config if needed

## Workflow

1. Understand the page purpose.
2. Check layout structure.
3. Check spacing and alignment.
4. Check typography hierarchy.
5. Check mobile responsiveness.
6. Check color and contrast basics.
7. Check reusable component structure.
8. Check loading, empty, error, and success states.
9. Compare against Figma/design references if available.
10. Return a UI review before editing.

## Quality checklist

- [ ] Layout is clean
- [ ] Spacing is consistent
- [ ] Typography hierarchy is clear
- [ ] Buttons and links are visible
- [ ] Mobile layout works
- [ ] Components are reusable
- [ ] Loading state exists
- [ ] Empty state exists where needed
- [ ] Error state exists where needed
- [ ] No unnecessary UI complexity

## Constraints

- Do not edit backend files.
- Do not install UI libraries without approval.
- Do not change unrelated pages.
- Do not remove accessibility basics.
- Do not add heavy animations that hurt usability.
- Do not change business logic unless asked.

## Output format

Return:
1. UI summary
2. Files reviewed
3. Visual issues
4. Responsive issues
5. Component reuse issues
6. Missing UI states
7. Suggested fixes
8. Files to edit if approved
9. Final verdict

## Example prompt

Use the react-ui-polish skill.

Review:
- src/pages/MenuPage.tsx
- src/components/food/FoodCard.tsx
- docs/UI_SPEC.md

Do not edit yet.

Return a UI polish report.
```

---

# Part 3: Create `figma-to-react-implementation` skill

## Purpose

This skill guides Figma-to-React implementation.

Create:

```txt
.agent/skills/figma-to-react-implementation/SKILL.md
```

Content:

```md
---
name: figma-to-react-implementation
description: Use this skill when converting a Figma design, screenshot, or design specification into React, TypeScript, and Tailwind components. It helps extract design tokens, component structure, layout behavior, responsive rules, and implementation steps. Do not use it for backend API development.
---

# Figma to React Implementation

## Goal

Convert Figma/design references into clean React + TypeScript + Tailwind implementation while preserving layout, spacing, typography, responsiveness, and component structure.

## When to use this skill

Use this skill when:
- Implementing UI from a Figma file
- Implementing UI from a screenshot
- Creating components from a design system
- Planning responsive behavior
- Building a pixel-aligned section
- Translating design tokens into Tailwind classes

## When not to use this skill

Do not use this skill when:
- Reviewing backend APIs
- Designing database schema
- Writing authentication middleware
- Debugging deployment logs
- Creating unrelated UI without design reference

## Required inputs

Provide:
- Figma link or screenshot
- Target page/section name
- Existing design system if available
- Required responsive breakpoints
- Existing component files if editing
- Assets/icons/images if needed

## Workflow

1. Inspect the design reference.
2. Identify layout structure.
3. Extract design tokens:
   - colors
   - typography
   - spacing
   - radius
   - shadows
   - icons/assets
4. Identify reusable components.
5. Create a component tree.
6. Plan responsive behavior.
7. List files to create/edit.
8. Implement one section or component at a time.
9. Verify in browser.
10. Compare with design reference.

## Quality checklist

- [ ] Design tokens documented
- [ ] Component tree planned
- [ ] Layout matches reference
- [ ] Spacing is close to design
- [ ] Typography is consistent
- [ ] Mobile layout works
- [ ] Assets are handled correctly
- [ ] Components are reusable
- [ ] Browser verification completed

## Constraints

- Do not guess design values if Figma/inspect data is available.
- Do not use copyrighted assets without permission.
- Do not install packages without approval.
- Do not edit backend files.
- Do not implement more sections than requested.
- Do not claim pixel-perfect without visual comparison.

## Output format

Return:
1. Design summary
2. Extracted design tokens
3. Component tree
4. Responsive plan
5. Files to create/edit
6. Implementation plan
7. Verification checklist
8. Remaining design gaps

## Example prompt

Use the figma-to-react-implementation skill.

Target:
Home page hero section

Inputs:
- Figma frame screenshot
- docs/DESIGN_SYSTEM.md
- src/pages/HomePage.tsx

Implement only the hero section.

Rules:
- Do not edit backend.
- Do not implement other sections.
- After implementation, provide browser verification checklist.
```

---

# Part 4: Create `express-api-quality-review` skill

## Purpose

This skill reviews Express backend APIs.

Create:

```txt
.agent/skills/express-api-quality-review/SKILL.md
```

Content:

```md
---
name: express-api-quality-review
description: Use this skill when reviewing Express.js route, controller, service, validation, authentication, authorization, response format, and error handling quality for a MERN backend API. Do not use it for frontend UI review or database schema design only.
---

# Express API Quality Review

## Goal

Review Express API implementation for correctness, security, consistency, maintainability, and alignment with the API contract.

## When to use this skill

Use this skill when:
- Reviewing a new API endpoint
- Reviewing backend module structure
- Checking route/controller/service separation
- Checking validation
- Checking auth and role middleware
- Checking response format
- Checking error handling
- Preparing API for frontend integration

## When not to use this skill

Do not use this skill when:
- Only reviewing UI
- Only writing database schema docs
- Only improving README
- Only testing frontend layout
- Only deploying frontend

## Required inputs

Read relevant files:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- Relevant route files
- Relevant controller files
- Relevant service files
- Relevant model files
- Validation files
- Auth/role middleware
- Error handler

## Workflow

1. Read the API contract.
2. Read only relevant backend files.
3. Check route names and HTTP methods.
4. Check controller responsibility.
5. Check service/business logic.
6. Check model usage.
7. Check validation rules.
8. Check authentication and authorization.
9. Check response format.
10. Check error handling.
11. Identify mismatches.
12. Return a review report before editing.

## Quality checklist

- [ ] Endpoint matches API contract
- [ ] Method and route are correct
- [ ] Request body is validated
- [ ] Auth required where needed
- [ ] Admin role checked where needed
- [ ] Controller is not overloaded
- [ ] Service handles business logic
- [ ] Model queries are safe
- [ ] Response format is consistent
- [ ] Errors are handled consistently

## Constraints

- Do not edit files unless explicitly asked.
- Do not remove auth checks.
- Do not remove validation.
- Do not expose secrets.
- Do not modify unrelated modules.
- Do not install packages without approval.
- Do not silently change API contract.

## Output format

Return:
1. API review summary
2. Files reviewed
3. Contract match/mismatch
4. Validation issues
5. Auth/authorization issues
6. Error handling issues
7. Code organization issues
8. Required fixes
9. Optional improvements
10. Final verdict: Ready / Needs revision / Not ready

## Example prompt

Use the express-api-quality-review skill.

Review the food API implementation against docs/API_CONTRACT.md.

Read only:
- docs/API_CONTRACT.md
- server/src/modules/foods/
- server/src/middlewares/

Do not edit files yet.

Return a review report.
```

---

# Part 5: Create `mongodb-schema-review` skill

## Purpose

This skill reviews MongoDB/Mongoose models and schema decisions.

Create:

```txt
.agent/skills/mongodb-schema-review/SKILL.md
```

Content:

```md
---
name: mongodb-schema-review
description: Use this skill when reviewing MongoDB and Mongoose schema design, including collections, fields, validation, references, embedded data, indexes, timestamps, enums, and access patterns. Do not use it for frontend UI review or general README writing.
---

# MongoDB Schema Review

## Goal

Review MongoDB/Mongoose schema design for correctness, validation, access patterns, relationships, and long-term maintainability.

## When to use this skill

Use this skill when:
- Creating or reviewing Mongoose models
- Checking schema alignment with requirements
- Checking order/user/resource relationships
- Deciding embed vs reference
- Checking indexes
- Checking validation and enums
- Checking timestamps
- Reviewing database architecture

## When not to use this skill

Do not use this skill when:
- Only styling frontend
- Only reviewing deployment logs
- Only writing React components
- Only creating README
- Only checking browser layout

## Required inputs

Read:
- docs/DATABASE_SCHEMA.md
- docs/API_CONTRACT.md
- docs/DATABASE_ARCHITECTURE.md
- Relevant Mongoose model files
- Relevant service files if needed

## Workflow

1. Read database schema docs.
2. Identify collections and relationships.
3. Review required fields.
4. Review optional fields.
5. Review validation rules.
6. Review enums/defaults.
7. Review indexes.
8. Review embed vs reference decisions.
9. Check whether API needs are supported.
10. Identify risks and improvements.

## Quality checklist

- [ ] Collections match features
- [ ] Required fields are defined
- [ ] Unique fields are indexed
- [ ] Enum fields are restricted
- [ ] Timestamps enabled where useful
- [ ] Sensitive fields protected
- [ ] Password is hashed outside direct plain storage
- [ ] Order snapshots preserve historical data
- [ ] Access patterns are supported
- [ ] Models align with API contract

## Constraints

- Do not expose database URI.
- Do not remove validation.
- Do not store plain text passwords.
- Do not over-normalize simple MongoDB data.
- Do not add unnecessary complexity.
- Do not edit files unless asked.

## Output format

Return:
1. Schema review summary
2. Files reviewed
3. Model-by-model review
4. Missing fields
5. Validation issues
6. Relationship issues
7. Index suggestions
8. Security concerns
9. Required fixes
10. Final verdict

## Example prompt

Use the mongodb-schema-review skill.

Review:
- docs/DATABASE_SCHEMA.md
- server/src/modules/users/user.model.ts
- server/src/modules/foods/food.model.ts
- server/src/modules/orders/order.model.ts

Do not edit files yet.

Return a schema review report.
```

---

# Part 6: Create `browser-verification` skill

## Purpose

This skill guides browser testing and visual verification.

Create:

```txt
.agent/skills/browser-verification/SKILL.md
```

Content:

```md
---
name: browser-verification
description: Use this skill when verifying a web application in the browser, including layout, responsiveness, navigation, forms, console errors, loading states, empty states, error states, authentication flows, and user/admin flows. Do not use it for backend-only code review.
---

# Browser Verification

## Goal

Verify that the implemented web app works correctly in the browser and produce clear evidence of what works, what is broken, and what should be fixed.

## When to use this skill

Use this skill when:
- A frontend page is implemented
- A full-stack flow is connected
- A UI change needs verification
- A form needs testing
- A protected route needs testing
- A deployment needs smoke testing
- A final project needs browser evidence

## When not to use this skill

Do not use this skill when:
- Only reviewing backend code without running UI
- Only writing API docs
- Only designing database schema
- Only generating README text

## Required inputs

Provide:
- Local or deployed URL
- Target page/route
- Expected behavior
- User role or demo credentials if needed
- Screenshots/design reference if visual QA is needed

## Workflow

1. Open the app URL.
2. Check page loads without crash.
3. Check browser console for errors.
4. Check layout at desktop width.
5. Check layout at mobile width.
6. Test navigation.
7. Test forms.
8. Test loading, empty, error states where possible.
9. Test auth/protected route behavior if relevant.
10. Capture findings.
11. Return pass/fail report before editing.

## Quality checklist

- [ ] Page loads
- [ ] No critical console errors
- [ ] Layout is not broken
- [ ] Mobile view works
- [ ] Navigation works
- [ ] Buttons are clickable
- [ ] Forms show validation
- [ ] Loading state appears
- [ ] Empty/error states handled
- [ ] Auth/role behavior works where relevant

## Constraints

- Do not change files during verification unless asked.
- Do not ignore console errors.
- Do not claim success without checking.
- Do not test only happy path.
- Do not expose credentials in public output.

## Output format

Return:
1. Verification target
2. Environment or URL
3. Pages tested
4. What passed
5. What failed
6. Console errors
7. Responsive issues
8. Screenshots/artifact summary
9. Required fixes
10. Final verdict: Pass / Conditional pass / Fail

## Example prompt

Use the browser-verification skill.

Verify:
- http://localhost:5173/menu
- http://localhost:5173/cart
- http://localhost:5173/login

Check desktop and mobile layout, console errors, buttons, and navigation.

Do not edit files yet.
```

---

# Part 7: Create `test-plan-generator` skill

## Purpose

This skill creates a practical testing plan.

Create:

```txt
.agent/skills/test-plan-generator/SKILL.md
```

Content:

```md
---
name: test-plan-generator
description: Use this skill when creating a practical testing plan for a MERN project, including frontend tests, backend API tests, browser verification, auth tests, role-based access tests, and deployment smoke tests. Do not use it for visual UI implementation only.
---

# Test Plan Generator

## Goal

Create a realistic testing plan that helps junior MERN developers verify key functionality without overcomplicating the project.

## When to use this skill

Use this skill when:
- Preparing testing tasks
- Planning backend API tests
- Planning frontend component tests
- Planning browser verification
- Planning auth and role tests
- Preparing final submission
- Creating QA checklist

## When not to use this skill

Do not use this skill when:
- Only styling a component
- Only writing README
- Only designing Figma UI
- Only creating database schema

## Required inputs

Read:
- docs/PRD.md
- docs/ACCEPTANCE_CRITERIA.md
- docs/API_CONTRACT.md
- docs/PAGE_ROUTE_MAP.md
- docs/AUTHORIZATION_MATRIX.md
- Existing frontend/backend files if available

## Workflow

1. Read requirements and acceptance criteria.
2. Identify critical user flows.
3. Identify backend APIs to test.
4. Identify frontend components/pages to test.
5. Identify auth and authorization tests.
6. Identify browser verification tasks.
7. Identify deployment smoke tests.
8. Prioritize must-have tests.
9. Return a practical test plan.

## Quality checklist

- [ ] Tests match acceptance criteria
- [ ] Critical APIs included
- [ ] Auth tests included
- [ ] Admin role tests included
- [ ] Main user flow tested
- [ ] Browser verification included
- [ ] Deployment smoke test included
- [ ] Test scope is realistic

## Constraints

- Do not create overly complex enterprise test suites.
- Do not ignore auth/role testing.
- Do not remove manual browser verification.
- Do not write test files unless asked.
- Do not claim full coverage without evidence.

## Output format

Return:
1. Testing summary
2. Critical flows
3. Backend API tests
4. Frontend tests
5. Auth/authorization tests
6. Browser verification checklist
7. Deployment smoke tests
8. Priority order
9. Recommended tools
10. Final test checklist

## Example prompt

Use the test-plan-generator skill.

Read:
- docs/ACCEPTANCE_CRITERIA.md
- docs/API_CONTRACT.md
- docs/AUTHORIZATION_MATRIX.md

Create a practical test plan for the project.

Do not write test code yet.
```

---

# Part 8: Create `deployment-readiness-review` skill

## Purpose

This skill checks deployment readiness.

Create:

```txt
.agent/skills/deployment-readiness-review/SKILL.md
```

Content:

```md
---
name: deployment-readiness-review
description: Use this skill when reviewing whether a MERN project is ready for deployment, including environment variables, build commands, frontend/backend URLs, MongoDB Atlas setup, CORS, JWT secrets, deployment platforms, smoke tests, and README updates. Do not use it for early UI design only.
---

# Deployment Readiness Review

## Goal

Review whether the project is ready for frontend, backend, and database deployment.

## When to use this skill

Use this skill when:
- Preparing to deploy frontend
- Preparing to deploy backend
- Checking environment variables
- Checking CORS config
- Checking MongoDB Atlas config
- Checking build/start commands
- Checking production API URLs
- Creating deployment checklist
- Running production smoke test

## When not to use this skill

Do not use this skill when:
- Project has no working local app
- Core features are not implemented
- Only planning UI design
- Only writing user stories
- Only reviewing database schema

## Required inputs

Read:
- README.md
- package.json files
- .env.example files
- frontend API config
- backend server config
- CORS config
- MongoDB connection config
- docs/DEPLOYMENT_PLAN.md if available

## Workflow

1. Check frontend build command.
2. Check backend build/start command.
3. Check required environment variables.
4. Check MongoDB Atlas connection requirements.
5. Check CORS frontend URL.
6. Check JWT secret usage.
7. Check API base URL config.
8. Check deployment platform settings.
9. Create production smoke test checklist.
10. Return readiness report before changes.

## Quality checklist

- [ ] Frontend builds locally
- [ ] Backend starts locally
- [ ] Environment variables documented
- [ ] `.env` not committed
- [ ] `.env.example` exists
- [ ] MongoDB Atlas ready
- [ ] CORS configured
- [ ] API base URL configured
- [ ] JWT secret configured
- [ ] Production smoke test planned
- [ ] README includes deployment notes

## Constraints

- Do not expose secrets.
- Do not commit `.env`.
- Do not change deployment platform without approval.
- Do not skip smoke testing.
- Do not claim deployed success without live verification.

## Output format

Return:
1. Deployment readiness summary
2. Files reviewed
3. Missing environment variables
4. Build/start command issues
5. CORS/API URL issues
6. Database connection risks
7. Security risks
8. Required fixes
9. Smoke test checklist
10. Final verdict: Ready / Needs fixes / Not ready

## Example prompt

Use the deployment-readiness-review skill.

Review:
- client/package.json
- server/package.json
- server/src/config/env.ts
- server/src/app.ts
- client/src/lib/api.ts
- README.md

Do not edit files yet.

Return deployment readiness report.
```

---

# Part 9: Create `portfolio-readme-generator` skill

## Purpose

This skill helps create a strong GitHub README.

Create:

```txt
.agent/skills/portfolio-readme-generator/SKILL.md
```

Content:

```md
---
name: portfolio-readme-generator
description: Use this skill when creating or improving a portfolio-ready README for a MERN or Next.js project, including project summary, features, tech stack, live links, screenshots, demo credentials, setup instructions, environment variables, API overview, testing, deployment, and interview explanation. Do not use it for backend code implementation.
---

# Portfolio README Generator

## Goal

Create a recruiter-friendly and evaluator-friendly README that clearly explains the project, features, stack, setup, deployment, screenshots, and learning outcomes.

## When to use this skill

Use this skill when:
- Preparing final assignment submission
- Improving GitHub project presentation
- Adding live links and screenshots
- Writing setup instructions
- Creating demo credentials section
- Explaining architecture and features
- Preparing for interview discussion

## When not to use this skill

Do not use this skill when:
- Writing backend code
- Fixing API bugs
- Designing database schema only
- Running deployment
- Editing secrets

## Required inputs

Read:
- Project brief
- PRD
- Architecture docs
- Live frontend link
- Backend/API link
- Screenshots
- Demo credentials
- Setup commands
- Environment variable list
- Tech stack
- Known limitations

## Workflow

1. Understand project purpose.
2. Identify target users and roles.
3. Summarize main features.
4. List tech stack.
5. Add live links.
6. Add screenshots section.
7. Add demo credentials safely.
8. Add setup instructions.
9. Add environment variable guide without secrets.
10. Add API overview.
11. Add testing/deployment notes.
12. Add learning/reflection section.

## Quality checklist

- [ ] Project summary is clear
- [ ] Live links included
- [ ] GitHub repo structure explained
- [ ] Features listed
- [ ] Tech stack listed
- [ ] Screenshots included
- [ ] Demo credentials included if safe
- [ ] Setup instructions work
- [ ] Environment variables documented without secrets
- [ ] Known limitations included
- [ ] Interview explanation included

## Constraints

- Do not include real secrets.
- Do not fake live links.
- Do not claim features that are not implemented.
- Do not exaggerate production readiness.
- Do not expose private credentials.
- Do not remove known limitations.

## Output format

Return a complete README with:
1. Project title
2. Summary
3. Live links
4. Demo credentials
5. Features
6. Tech stack
7. Screenshots
8. Folder structure
9. Setup instructions
10. Environment variables
11. API overview
12. Testing
13. Deployment
14. Known limitations
15. What I learned
16. Future improvements

## Example prompt

Use the portfolio-readme-generator skill.

Read:
- docs/PROJECT_BRIEF.md
- docs/PRD.md
- docs/ARCHITECTURE_OVERVIEW.md
- docs/DEPLOYMENT_PLAN.md

Create a professional README.md for the final project.

Do not invent features or fake live links.
```

---

# Part 10: Skill authoring checklist

Create:

```txt
.agent/skills/SKILL_AUTHORING_CHECKLIST.md
```

Content:

```md
# Skill Authoring Checklist

## Skill identity

- [ ] Folder name is short and specific
- [ ] `name` matches the skill purpose
- [ ] `description` is clear
- [ ] Description says when to use the skill
- [ ] Description says when not to use the skill
- [ ] Skill is not too broad

## Instruction quality

- [ ] Goal is clear
- [ ] Required inputs are listed
- [ ] Workflow is step-by-step
- [ ] Quality checklist exists
- [ ] Constraints exist
- [ ] Output format exists
- [ ] Example prompt exists

## Safety

- [ ] Skill does not expose secrets
- [ ] Skill does not encourage destructive commands
- [ ] Skill does not remove validation/auth/tests
- [ ] Skill does not modify unrelated files
- [ ] Skill asks for review before risky edits

## Reusability

- [ ] Skill can be reused in similar projects
- [ ] Skill avoids unnecessary project-specific names
- [ ] Skill uses generic MERN terminology where possible
- [ ] Long references are moved into references/ if needed

## Testing

- [ ] Skill triggers for correct task
- [ ] Skill does not trigger for unrelated task
- [ ] Output follows expected format
- [ ] Output is practical and reviewable
```

---

# Part 11: Skill safety checklist

Create:

```txt
.agent/skills/SKILL_SAFETY_CHECKLIST.md
```

Content:

```md
# Skill Safety Checklist

Before using any skill, check:

## Internal skills

- [ ] I wrote or reviewed the skill myself
- [ ] I understand what the skill does
- [ ] The skill has clear constraints
- [ ] The skill does not expose secrets
- [ ] The skill does not encourage unsafe commands
- [ ] The skill does not remove tests/auth/security

## External/community skills

- [ ] I read the full `SKILL.md`
- [ ] I checked scripts, references, and assets
- [ ] I checked if it asks for network access
- [ ] I checked if it modifies many files
- [ ] I checked if it includes hidden or suspicious instructions
- [ ] I tested it in a safe project first
- [ ] I did not install it blindly
```

---

# Part 12: Skill testing workflow

A skill is not complete until you test it.

Create:

```txt
docs/SKILL_TEST_REPORT.md
```

Use this structure:

```md
# Skill Test Report

## Skill: mern-architecture-review

### Test prompt
-

### Did it trigger correctly?
Yes / No

### Did it follow the output format?
Yes / No

### Was the result useful?
Yes / No

### Did it avoid unrelated changes?
Yes / No

### Issues found
-

### Improvements needed
-

### Rating
Good / Needs improvement / Not ready
```

Repeat for every skill.

---

## Test prompts for each skill

### Test 1: Architecture review

```txt
Use the mern-architecture-review skill.

Read:
- docs/PROJECT_BRIEF.md
- docs/PRD.md
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTHORIZATION_MATRIX.md

Do not edit files.

Return an architecture review report.
```

### Test 2: React UI polish

```txt
Use the react-ui-polish skill.

Review:
- client/src/pages/HomePage.tsx
- client/src/components/layout/Navbar.tsx
- docs/UI_SPEC.md

Do not edit files.

Return a UI polish report.
```

### Test 3: Express API quality

```txt
Use the express-api-quality-review skill.

Review:
- docs/API_CONTRACT.md
- server/src/modules/foods/

Do not edit files.

Return an API quality review.
```

### Test 4: MongoDB schema review

```txt
Use the mongodb-schema-review skill.

Review:
- docs/DATABASE_SCHEMA.md
- server/src/modules/users/user.model.ts
- server/src/modules/orders/order.model.ts

Do not edit files.

Return a schema review.
```

### Test 5: Browser verification

```txt
Use the browser-verification skill.

Verify:
- http://localhost:5173/

Check:
1. Page loads
2. Console errors
3. Layout
4. Mobile responsiveness

Do not edit files.
```

---

# Part 13: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 05-module-04-skill-md-mastery.md
2. Antigravity Agent Skills docs
3. Antigravity Skills codelab
4. Google skills GitHub repository
5. Agent Skills specification
6. OpenAI Codex Skills docs
7. GitHub Copilot Agent Skills docs
8. Your own SKILL.md files
9. Your SKILL_TEST_REPORT.md
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for SKILL.md mastery.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. What Agent Skills are
2. What SKILL.md does
3. YAML frontmatter
4. Why description matters
5. Markdown instruction body
6. Required inputs
7. Workflows
8. Constraints
9. Output formats
10. Skill testing
11. Skill safety
12. Common mistakes
13. Practical MERN examples
```

---

## NotebookLM Prompt 2: Skill Review

```txt
Review my SKILL.md files.

Check:
1. Is each skill focused?
2. Is the description specific?
3. Does the skill say when to use and when not to use?
4. Are required inputs clear?
5. Is the workflow practical?
6. Are safety constraints strong?
7. Is the output format reviewable?
8. Are examples useful?
9. Which skills are too broad?
10. Which skills should be improved?

Return a skill improvement checklist.
```

---

## NotebookLM Prompt 3: Skill Testing Plan

```txt
Create a skill testing plan.

For each skill:
1. Test prompt
2. Expected trigger
3. Expected output format
4. What would count as failure
5. Improvement suggestion if weak

Focus on:
- mern-architecture-review
- react-ui-polish
- figma-to-react-implementation
- express-api-quality-review
- mongodb-schema-review
- browser-verification
- test-plan-generator
- deployment-readiness-review
- portfolio-readme-generator
```

---

# Part 14: Required video resources

Watch at least two videos.

Search YouTube:

```txt
Google Antigravity skills SKILL.md tutorial
How to create Agent Skills in Google Antigravity
Antigravity skills tutorial
Agent Skills SKILL.md explanation
```

Recommended video note format:

```md
# Module 4 Video Learning Notes

## Video 1
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### How I will apply this to my project
1.
2.
3.

## Video 2
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### How I will apply this to my project
1.
2.
3.
```

Save as:

```txt
docs/notebooklm/module-04-video-learning-notes.md
```

---

# Part 15: Practice tasks

## Practice Task 1: Create skills folder

Create this structure:

```txt
.agent/
  skills/
    mern-architecture-review/
    react-ui-polish/
    figma-to-react-implementation/
    express-api-quality-review/
    mongodb-schema-review/
    browser-verification/
    test-plan-generator/
    deployment-readiness-review/
    portfolio-readme-generator/
```

---

## Practice Task 2: Create all `SKILL.md` files

Create one `SKILL.md` file inside each skill folder.

Use the templates above.

---

## Practice Task 3: Create skill index

Create:

```txt
.agent/skills/SKILL_INDEX.md
```

Use this structure:

```md
# Skill Index

| Skill | Purpose | When to use |
|---|---|---|
| mern-architecture-review | Review full-stack architecture | Before coding or major refactor |
| react-ui-polish | Review UI quality | After page/component implementation |
| figma-to-react-implementation | Convert design to UI | During Figma-to-code work |
| express-api-quality-review | Review backend APIs | After endpoint implementation |
| mongodb-schema-review | Review models/schema | Before or after model creation |
| browser-verification | Verify UI in browser | After implementation/integration |
| test-plan-generator | Create testing plan | Before QA/testing |
| deployment-readiness-review | Check deployment readiness | Before deployment |
| portfolio-readme-generator | Create README | Before final submission |
```

---

## Practice Task 4: Test three skills

Test at least three skills:

```txt
1. mern-architecture-review
2. express-api-quality-review
3. browser-verification
```

Document results in:

```txt
docs/SKILL_TEST_REPORT.md
```

---

## Practice Task 5: Improve weak skills

After testing, update weak skills.

Common improvements:

- Make description more specific
- Add when-not-to-use section
- Add required inputs
- Add stronger constraints
- Add better output format
- Add example prompt

---

# Required deliverables for this module

Submit:

```txt
1. .agent/skills/mern-architecture-review/SKILL.md
2. .agent/skills/react-ui-polish/SKILL.md
3. .agent/skills/figma-to-react-implementation/SKILL.md
4. .agent/skills/express-api-quality-review/SKILL.md
5. .agent/skills/mongodb-schema-review/SKILL.md
6. .agent/skills/browser-verification/SKILL.md
7. .agent/skills/test-plan-generator/SKILL.md
8. .agent/skills/deployment-readiness-review/SKILL.md
9. .agent/skills/portfolio-readme-generator/SKILL.md
10. .agent/skills/SKILL_INDEX.md
11. .agent/skills/SKILL_AUTHORING_CHECKLIST.md
12. .agent/skills/SKILL_SAFETY_CHECKLIST.md
13. docs/SKILL_TEST_REPORT.md
14. NotebookLM Study Guide screenshot
15. NotebookLM Skill Review screenshot
16. Video learning notes
17. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/05-module-04-skill-md-mastery-reflection.md
```

Use this format:

```md
# Reflection: Module 4 - SKILL.md Mastery

## Skills I created
-

## Which skill was easiest to create
-

## Which skill was hardest to create
-

## What I learned about YAML frontmatter
-

## What I learned about skill descriptions
-

## What I learned about constraints
-

## What I learned from testing skills
-

## Which skill I improved after testing
-

## How these skills will save quota
-

## How I will use skills in the next module
-
```

---

# Quiz

## Multiple choice

**1. What is the most important file inside a skill folder?**

A. `README.txt`  
B. `SKILL.md`  
C. `package-lock.json`  
D. `index.html`  

Correct answer: **B**

---

**2. What are the two major parts of `SKILL.md`?**

A. CSS and HTML  
B. YAML frontmatter and Markdown body  
C. MongoDB and Express  
D. Images and videos  

Correct answer: **B**

---

**3. Why is the description field important?**

A. It helps the agent understand when the skill is relevant  
B. It changes app color  
C. It installs packages automatically  
D. It creates database users  

Correct answer: **A**

---

**4. Which skill name is better?**

A. do-everything  
B. express-api-quality-review  
C. helper  
D. fullstack-master  

Correct answer: **B**

---

**5. What should a skill include?**

A. Goal, inputs, workflow, constraints, output format, examples  
B. Only one sentence  
C. Database password  
D. Random commands  

Correct answer: **A**

---

**6. What should you do before using a third-party skill?**

A. Install blindly  
B. Read the full `SKILL.md`, scripts, references, and assets  
C. Run all scripts immediately  
D. Delete your project  

Correct answer: **B**

---

**7. What makes a skill too broad?**

A. It tries to handle many unrelated tasks  
B. It has clear scope  
C. It has constraints  
D. It has examples  

Correct answer: **A**

---

**8. Why should skills include constraints?**

A. To prevent unsafe or unrelated behavior  
B. To make UI colorful  
C. To expose secrets  
D. To remove tests  

Correct answer: **A**

---

**9. Why should you test a skill?**

A. To confirm it triggers correctly and produces useful output  
B. To avoid reading it  
C. To replace GitHub  
D. To skip verification  

Correct answer: **A**

---

**10. Which skill is best for checking a deployed page in browser?**

A. browser-verification  
B. mongodb-schema-review  
C. portfolio-readme-generator  
D. express-api-quality-review  

Correct answer: **A**

---

## Short-answer questions

1. What is an Agent Skill?
2. What does `SKILL.md` do?
3. Why should skill descriptions be specific?
4. What are YAML frontmatter and Markdown body?
5. What is one skill you created in this module?
6. What is one constraint every coding skill should include?
7. Why should external skills be reviewed carefully?
8. How can skills save Antigravity quota?
9. What should be included in a skill test report?
10. How will you use skills in the next module?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Skills folder | `.agent/skills/` or equivalent skill directory created |
| Number of skills | At least 8 project skills created |
| YAML frontmatter | Every skill has `name` and `description` |
| Description quality | Descriptions are specific and trigger-focused |
| Workflow | Every skill has step-by-step workflow |
| Constraints | Skills include safety constraints |
| Output format | Skills define reviewable outputs |
| Example prompt | Skills include usage example |
| Skill index | Skill index created |
| Safety checklist | Safety checklist created |
| Test report | At least 3 skills tested |
| Improvement | Weak skills improved after testing |
| NotebookLM evidence | Study guide/review screenshots submitted |
| Reflection | Student explains how skills improve workflow |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can create focused SKILL.md files with clear frontmatter, instructions, workflows, constraints, output formats, and examples. I can test whether skills trigger correctly, improve weak skills, and use project skills to make Antigravity more consistent, safer, and more quota-efficient.
```

After completing this file, continue to:

```txt
06-module-05-figma-to-code-workflow.md
```
