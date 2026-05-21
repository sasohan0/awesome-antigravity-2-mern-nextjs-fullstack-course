# Module 1: Antigravity 2.0 Setup, Mental Model and Safe Workflow

**File Name:** `02-module-01-antigravity-setup.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 2–3.5 hours  
**Recommended Before:** Starting any coding task with Antigravity  
**Main Goal:** Learn how Antigravity works, set up a safe workflow, and use it without blindly trusting AI-generated work.

---

## Module purpose

This module teaches you how to start using **Google Antigravity 2.0** as a serious development partner.

Before building a full MERN project, you must understand:

- What Antigravity is
- How agentic development is different from normal autocomplete
- How to start a project safely
- How to ask for plans before code
- How to review changed files
- How to avoid wasting free quota
- How to verify work in the browser
- How to document your progress

This module is not about building a large app yet.

This module is about learning the correct workflow.

If you skip this module, you may use Antigravity incorrectly and create messy, broken, unreviewed projects.

---

## What Antigravity is

Antigravity is an agent-first development platform.

Traditional AI coding tools usually help with:

- Autocomplete
- Small code snippets
- Chat-based suggestions
- Explaining errors
- Refactoring selected code

Antigravity is different because it works more like an agentic development environment.

It can help across:

- Editor
- Terminal
- Browser
- Planning
- Implementation
- Verification
- Artifacts
- Multi-step development tasks

But this also means you need to control it properly.

Antigravity can move fast.

Your job is to make sure it moves in the correct direction.

---

## Important mental model

Do not think of Antigravity as:

```txt
A tool that magically builds perfect projects.
```

Think of it as:

```txt
A junior-to-mid level AI development partner that can work fast but still needs clear direction, review, and verification.
```

That means you must:

- Give context
- Define the task
- Limit the scope
- Review the plan
- Review the code
- Test the output
- Stop it when it goes off-track
- Keep documentation updated

---

## Antigravity workflow in one sentence

Use this workflow:

```txt
Context → Plan → Approve → Implement → Review → Verify → Document → Next Task
```

Never jump directly from idea to full implementation.

---

## The 8-step safe workflow

Use this workflow for almost every task.

### Step 1: Give context

Before asking Antigravity to build, give it enough context.

Example:

```txt
I am building a MERN food ordering platform.

Frontend:
React + Vite + TypeScript + Tailwind

Backend:
Node.js + Express + MongoDB + Mongoose

Current task:
Plan the project structure only.

Do not write code yet.
```

---

### Step 2: Ask for a plan first

Never start with:

```txt
Build the whole app.
```

Start with:

```txt
Create a development plan first.
Do not write code yet.
List:
1. Required folders
2. Required files
3. Implementation order
4. Risks
5. Questions before coding
```

---

### Step 3: Review the plan

Before accepting any code, read the plan.

Check:

- Is the stack correct?
- Is the scope too big?
- Are files organized properly?
- Is it adding unnecessary features?
- Is it skipping important setup?
- Is it planning tests?
- Is it planning verification?

If the plan is too broad, ask it to reduce scope.

---

### Step 4: Approve one small task

Do not approve everything.

Approve only one small task.

Good first tasks:

```txt
Create only the frontend folder structure.
```

```txt
Create only the backend server setup.
```

```txt
Create only the Navbar and Hero section.
```

```txt
Create only the User model and auth route plan.
```

---

### Step 5: Review changed files

After Antigravity changes files, check:

- Which files changed?
- Did it touch unrelated files?
- Did it install packages?
- Did it create duplicate logic?
- Did it remove existing code?
- Did it expose secrets?
- Did it add unnecessary complexity?

Ask for a summary:

```txt
Summarize exactly what files you changed and why.
Do not make new changes.
```

---

### Step 6: Run verification

Verification depends on the task.

For frontend:

```txt
npm run dev
Check browser
Check mobile view
Check console errors
```

For backend:

```txt
npm run dev
Check health route
Test API in Postman/Thunder Client
Check MongoDB connection
```

For full-stack:

```txt
Login flow
Protected route
CRUD flow
Loading state
Error state
Admin route
```

---

### Step 7: Document the result

Update markdown files:

```txt
PROJECT_CONTEXT.md
NEXT_STEPS.md
ERROR_LOG.md
DECISIONS.md
```

Example:

```md
## Decision
We will use React + Vite for frontend and Express for backend.

## Why
This helps junior MERN developers understand frontend/backend separation clearly.

## Date
25 May
```

---

### Step 8: Move to the next small task

Only after verification should you move to the next task.

---

## Required project context files

Create these files before building:

```txt
PROJECT_CONTEXT.md
LEARNING_PLAN.md
NEXT_STEPS.md
ERROR_LOG.md
DECISIONS.md
```

### `PROJECT_CONTEXT.md`

Use this file to explain the project.

It should include:

```md
# Project Context

## Project name
-

## Project type
-

## Tech stack
-

## User roles
-

## Main features
-

## Current status
-

## Important decisions
-

## What Antigravity should know
-
```

### `LEARNING_PLAN.md`

Use this file to track your course learning.

```md
# Learning Plan

## My goal
-

## My weak areas
-

## Modules to complete
-

## Daily schedule
-

## Proof I need to submit
-
```

### `NEXT_STEPS.md`

Use this file to guide the next small tasks.

```md
# Next Steps

## Current module
-

## Current task
-

## Next 3 actions
1.
2.
3.

## Blockers
-

## What to ask Antigravity next
-
```

### `ERROR_LOG.md`

Use this file to document errors.

```md
# Error Log

## Error
-

## Where it happened
-

## Cause
-

## Fix
-

## What I learned
-
```

### `DECISIONS.md`

Use this file to document technical decisions.

```md
# Decisions

## Decision
-

## Options considered
-

## Why this option
-

## Risks
-

## Date
-
```

---

## Installation and setup checklist

Before using Antigravity seriously, confirm:

```txt
1. Antigravity is installed
2. You can open a project folder
3. You can create/edit files
4. Terminal is accessible
5. Browser verification works
6. You can see changed files
7. You can review artifacts
8. You can stop or redirect the agent
9. Git is working
10. Your project is connected to GitHub
```

---

## First safe Antigravity prompt

Use this as your first prompt:

```txt
I am starting the Antigravity 2.0 MERN Bootcamp.

Create a project learning workspace.

Create these files:
1. PROJECT_CONTEXT.md
2. LEARNING_PLAN.md
3. NEXT_STEPS.md
4. ERROR_LOG.md
5. DECISIONS.md

Rules:
- Do not create app code yet.
- Do not install packages.
- Keep the files beginner-friendly.
- Add sections for module progress, blockers, decisions, and next actions.
- After creating the files, summarize what each file is for.
```

---

## Second safe Antigravity prompt

After the files are created, ask:

```txt
Review the workspace files you created.

Tell me:
1. What each file is for
2. How I should update them during the course
3. What file I should update before asking you to code
4. What mistakes I should avoid

Do not edit files yet.
```

---

## Third safe Antigravity prompt

Ask for a learning plan:

```txt
Read LEARNING_PLAN.md and PROJECT_CONTEXT.md.

Create a 7-day Eid learning plan for the Antigravity 2.0 MERN Bootcamp.

Rules:
- Do not create app code.
- Include daily learning goals.
- Include practice tasks.
- Include evidence to submit.
- Include time estimates.
- Include backup plan if I fall behind.
```

---

## How to use Antigravity for planning

Planning prompts are the safest prompts.

Use them often.

Example:

```txt
Create an implementation plan for a MERN food ordering project.

Include:
1. Folder structure
2. Frontend pages
3. Backend routes
4. Database models
5. Auth flow
6. Admin flow
7. Testing plan
8. Deployment plan

Do not write code yet.
```

Another example:

```txt
Before implementing the cart feature, create a plan.

Include:
1. Required components
2. State management approach
3. Data structure
4. Edge cases
5. Files to modify
6. Verification checklist

Do not write code yet.
```

---

## How to use Antigravity for code generation

Only use code generation after planning.

Good code generation prompt:

```txt
Implement only the Navbar component.

Use:
- React
- TypeScript
- Tailwind CSS

Requirements:
- Responsive layout
- Logo area
- Navigation links
- Login button
- Mobile menu placeholder

Rules:
- Modify only files related to Navbar.
- Do not create backend files.
- Do not install packages.
- After implementation, explain changed files.
```

---

## How to use Antigravity for debugging

Bad debugging prompt:

```txt
Fix this.
```

Good debugging prompt:

```txt
I am getting this error:

[paste error]

Context:
- File:
- Command I ran:
- What I expected:
- What happened:

Task:
Explain the cause first.
Then suggest the smallest safe fix.
Do not modify files until I approve.
```

---

## How to use Antigravity for browser verification

After frontend implementation, ask:

```txt
Open the app in the browser and verify the current page.

Check:
1. Layout
2. Responsiveness
3. Console errors
4. Broken links
5. Button visibility
6. Mobile view

Return:
- What works
- What is broken
- Screenshot/artifact summary
- Fix recommendations

Do not edit files yet.
```

---

## How to use Antigravity for code review

After changes, ask:

```txt
Review the changes you made.

Check:
1. Scope
2. File changes
3. Code quality
4. TypeScript issues
5. Security risks
6. Missing states
7. Testing needs
8. Unrelated changes

Do not edit files yet.
Return a review report.
```

---

## What not to do

Avoid these prompts:

```txt
Build the full app in one go.
```

```txt
Fix all problems.
```

```txt
Make it professional.
```

```txt
Add everything needed.
```

```txt
You decide everything.
```

```txt
Delete anything unnecessary.
```

These prompts are risky because they are too broad.

They can cause:

- Wasted quota
- Wrong architecture
- Broken code
- Unrelated file changes
- Hidden bugs
- Poor understanding
- Weak interview explanation

---

## Safe prompt formula

Use this formula:

```txt
Context:
[What project/module/task is this?]

Goal:
[What exactly should be done?]

Scope:
[What files/folders can be touched?]

Rules:
[What should not happen?]

Output:
[What should Antigravity return?]

Verification:
[How should success be checked?]
```

Example:

```txt
Context:
I am building the frontend for a MERN food ordering app.

Goal:
Create only the MenuCard component.

Scope:
You may edit only:
- src/components/MenuCard.tsx
- src/types/food.ts

Rules:
- Do not edit routing.
- Do not create backend files.
- Do not install packages.

Output:
After editing, explain the props, changed files, and usage example.

Verification:
Tell me how to render and check this component.
```

---

## Free-plan quota strategy

If you have limited quota, use this strategy.

### 1. Write context in files

Instead of repeating project details every time, save them in:

```txt
PROJECT_CONTEXT.md
API_CONTRACT.md
DATABASE_SCHEMA.md
DESIGN_SYSTEM.md
NEXT_STEPS.md
```

Then prompt:

```txt
Read PROJECT_CONTEXT.md and NEXT_STEPS.md.
Continue from the current task.
```

### 2. Ask for plans before implementation

Planning is cheaper than fixing bad implementation later.

### 3. Work by file or feature

Do not ask Antigravity to scan the whole repo unless necessary.

### 4. Use NotebookLM for studying

Do not use Antigravity quota to explain long documentation when NotebookLM can help.

### 5. Save reusable prompts

Create:

```txt
PROMPT_LIBRARY.md
```

### 6. Use `SKILL.md` later

In Module 4, you will learn how to create reusable skills so you do not need to repeat the same instructions again and again.

---

## Required official resources

Add these to NotebookLM:

| Resource | Link |
|---|---|
| Google Antigravity official site | https://antigravity.google/ |
| Google Antigravity docs | https://antigravity.google/docs/home |
| Getting Started with Google Antigravity codelab | https://codelabs.developers.google.com/getting-started-google-antigravity |
| Building with Google Antigravity codelab | https://codelabs.developers.google.com/building-with-google-antigravity |
| Google developer blog: Build with Antigravity | https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/ |
| Antigravity Artifacts docs | https://antigravity.google/docs/artifacts |

---

## Required video resources

Watch at least two videos:

### Video 1: Official/basic Antigravity walkthrough

Search YouTube:

```txt
Learn the basics of Google Antigravity
```

Watch for:

- Editor view
- Agent Manager
- Browser
- Terminal usage
- How agents plan
- How to review output

### Video 2: Practical Antigravity app-building workflow

Search YouTube:

```txt
Building with Google Antigravity full stack app
```

Watch for:

- How prompts are structured
- How tasks are broken down
- How browser verification is used
- How the developer reviews agent output

### Video learning task

Create:

```txt
docs/VIDEO_LEARNING_NOTES.md
```

Use this format:

```md
# Module 1 Video Learning Notes

## Video 1
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### 3 things I will apply
1.
2.
3.

### 2 mistakes I will avoid
1.
2.

## Video 2
Title:
Link:

### 5 lessons learned
1.
2.
3.
4.
5.

### 3 things I will apply
1.
2.
3.

### 2 mistakes I will avoid
1.
2.
```

---

## NotebookLM workflow for this module

Create or open your notebook:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add sources:

```txt
1. 00-introduction.md
2. 01-utilize-notebooklm.md
3. 02-module-01-antigravity-setup.md
4. Antigravity official docs
5. Antigravity getting started codelab
6. Antigravity building codelab
7. Selected video links
```

Then use these prompts.

### Prompt 1: Study guide

```txt
Create a beginner-friendly study guide for Antigravity 2.0 setup and safe workflow.

Audience:
Junior MERN stack developers.

Output:
1. What Antigravity is
2. How agentic development differs from normal AI coding
3. Key parts of Antigravity
4. Safe workflow
5. Quota-smart workflow
6. Common mistakes
7. Good prompt examples
8. Practice task checklist
9. 10 quiz questions with answers
```

### Prompt 2: Mind map

```txt
Create a mind map for Antigravity safe development workflow.

Center:
Antigravity 2.0 for MERN Developers

Branches:
1. Setup
2. Agent Manager
3. Editor
4. Terminal
5. Browser verification
6. Artifacts
7. Planning prompts
8. Code review
9. Quota management
10. GitHub evidence
```

### Prompt 3: Flashcards

```txt
Create flashcards for this module.

Terms:
- Agentic development
- Agent Manager
- Editor view
- Browser verification
- Artifact
- Prompt scope
- Project context
- Small task workflow
- Code review
- Quota-smart workflow
```

### Prompt 4: Practice checklist

```txt
Create a checklist for completing Module 1.

Include:
1. Setup tasks
2. NotebookLM tasks
3. Antigravity tasks
4. Files to create
5. Screenshots to submit
6. Common mistakes to avoid
7. Reflection questions
```

---

## Practice Task 1: Create project learning workspace

Ask Antigravity:

```txt
I am starting the Antigravity 2.0 MERN Bootcamp.

Create a project learning workspace.

Create these files:
1. PROJECT_CONTEXT.md
2. LEARNING_PLAN.md
3. NEXT_STEPS.md
4. ERROR_LOG.md
5. DECISIONS.md

Rules:
- Do not create app code yet.
- Do not install packages.
- Keep the files beginner-friendly.
- Add sections for module progress, blockers, decisions, and next actions.
- After creating the files, summarize what each file is for.
```

Expected output:

```txt
PROJECT_CONTEXT.md
LEARNING_PLAN.md
NEXT_STEPS.md
ERROR_LOG.md
DECISIONS.md
```

---

## Practice Task 2: Review the workspace

Ask Antigravity:

```txt
Review the workspace files you created.

Tell me:
1. What each file is for
2. How I should update them during the course
3. What file I should update before asking you to code
4. What mistakes I should avoid

Do not edit files yet.
```

---

## Practice Task 3: Create a prompt library

Ask Antigravity:

```txt
Create PROMPT_LIBRARY.md for this course.

Include prompt templates for:
1. Planning
2. Code generation
3. Debugging
4. Browser verification
5. Code review
6. Documentation update
7. Quota-saving workflow

Rules:
- Do not create app code.
- Keep the prompts reusable.
- Each prompt should include context, goal, scope, rules, output, and verification.
```

---

## Practice Task 4: Create a safety checklist

Ask Antigravity:

```txt
Create ANTIGRAVITY_SAFETY_CHECKLIST.md.

Include:
1. Before starting a task
2. Before allowing file edits
3. Before running terminal commands
4. Before accepting generated code
5. Before pushing to GitHub
6. Before deployment

Keep it practical for junior MERN developers.
```

---

## Practice Task 5: Create the first project plan

Choose a simple project idea, such as:

```txt
Food ordering app
Event booking app
Course marketplace
Expense tracker
Real estate listing app
```

Then ask Antigravity:

```txt
I am practicing Antigravity planning.

Project idea:
[Write your project idea]

Create a high-level MERN project plan.

Include:
1. Project summary
2. User roles
3. Main features
4. Frontend pages
5. Backend APIs
6. Database models
7. Authentication needs
8. Admin/dashboard needs
9. Testing needs
10. Deployment needs

Rules:
- Do not write code.
- Keep it realistic for a junior developer.
- Mention what should be built first.
```

Save the result as:

```txt
docs/PRACTICE_PROJECT_PLAN.md
```

---

## Practice Task 6: Create a browser verification checklist

Ask Antigravity:

```txt
Create BROWSER_VERIFICATION_CHECKLIST.md for MERN frontend work.

Include:
1. Layout checks
2. Responsive checks
3. Navigation checks
4. Form checks
5. Console error checks
6. Loading state checks
7. Empty state checks
8. Error state checks
9. Admin/user flow checks
10. Screenshot evidence checklist
```

---

## Required deliverables for this module

Submit:

```txt
1. Screenshot of Antigravity opened with your project folder
2. PROJECT_CONTEXT.md
3. LEARNING_PLAN.md
4. NEXT_STEPS.md
5. ERROR_LOG.md
6. DECISIONS.md
7. PROMPT_LIBRARY.md
8. ANTIGRAVITY_SAFETY_CHECKLIST.md
9. BROWSER_VERIFICATION_CHECKLIST.md
10. PRACTICE_PROJECT_PLAN.md
11. NotebookLM Study Guide screenshot
12. NotebookLM Mind Map screenshot
13. Video Learning Notes
14. Reflection file
```

---

## Reflection template

Create:

```txt
docs/reflections/02-module-01-antigravity-setup-reflection.md
```

Use this format:

```md
# Reflection: Module 1 - Antigravity Setup

## What I set up
-

## Files I created
-

## What I learned about Antigravity
-

## What I learned about safe prompting
-

## What I learned about quota-saving
-

## What confused me
-

## My best prompt from this module
-

## What I will do differently in the next module
-
```

---

## Quiz

### Multiple choice

**1. What is the safest first step before asking Antigravity to write code?**

A. Ask it to build the full app  
B. Ask it to create a plan first  
C. Ask it to delete unnecessary files  
D. Ask it to deploy immediately  

Correct answer: **B**

---

**2. What is the best mental model for Antigravity?**

A. A magic app builder  
B. A development partner that needs direction, review, and verification  
C. A replacement for GitHub  
D. A database hosting service  

Correct answer: **B**

---

**3. Which prompt is better?**

A. Make the UI professional  
B. Improve only the hero section spacing and mobile layout. Do not change other files.  
C. Fix all bugs  
D. Build everything  

Correct answer: **B**

---

**4. Why should you create `PROJECT_CONTEXT.md`?**

A. To store project context so you do not repeat it in every prompt  
B. To store database password  
C. To replace GitHub  
D. To skip planning  

Correct answer: **A**

---

**5. What should you do after Antigravity changes files?**

A. Push immediately  
B. Review changed files and verify the result  
C. Delete the repo  
D. Ignore the summary  

Correct answer: **B**

---

**6. What is browser verification useful for?**

A. Checking UI, console errors, responsiveness, and flows  
B. Creating MongoDB users  
C. Replacing backend APIs  
D. Avoiding deployment  

Correct answer: **A**

---

**7. What is a quota-smart workflow?**

A. Asking for the whole project at once  
B. Saving context in files and working one task at a time  
C. Repeating the same prompt again and again  
D. Asking Antigravity to read the full repo every time  

Correct answer: **B**

---

**8. What should you avoid putting on GitHub?**

A. README  
B. Source code  
C. Secrets and environment variables  
D. Screenshots  

Correct answer: **C**

---

**9. What should `ERROR_LOG.md` contain?**

A. Errors, causes, fixes, and lessons learned  
B. Only app colors  
C. User passwords  
D. Random thoughts only  

Correct answer: **A**

---

**10. What is the correct workflow?**

A. Context → Plan → Approve → Implement → Review → Verify → Document → Next Task  
B. Build → Pray → Push  
C. Deploy → Plan later  
D. Delete → Rebuild → Ignore  

Correct answer: **A**

---

### Short-answer questions

1. What is Antigravity?
2. Why should you ask for a plan before code?
3. What are the five project context files created in this module?
4. How does `PROJECT_CONTEXT.md` help save quota?
5. What should you check after Antigravity edits files?
6. What is browser verification?
7. What is one bad prompt and one better version?
8. What should be included in `PROMPT_LIBRARY.md`?
9. Why should you document decisions?
10. How will you use Antigravity differently after this module?

---

## Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Antigravity setup | Student can open and use Antigravity with a project folder |
| Context files | Required markdown files created |
| Prompt library | Reusable prompts created |
| Safety checklist | Practical safety checklist created |
| Browser checklist | Browser verification checklist created |
| Planning task | Practice project plan completed |
| NotebookLM evidence | Study guide and mind map submitted |
| Video evidence | Video learning notes submitted |
| Reflection | Student explains safe workflow and quota strategy |

---

## Completion standard

You complete this module only when you can confidently say:

```txt
I can use Antigravity safely by giving context, asking for plans, limiting scope, reviewing changed files, verifying in the browser, documenting progress, and using quota-smart workflows.
```

After completing this file, continue to:

```txt
03-module-02-spec-first-development.md
```
