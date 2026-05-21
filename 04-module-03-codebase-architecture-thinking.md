# Module 3: Codebase and Architecture Thinking — Understand the Whole System Before Building

**File Name:** `04-module-03-codebase-architecture-thinking.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 4–6 hours  
**Recommended After:** Module 2: Spec-First Development  
**Main Goal:** Learn how to think about full-stack architecture before asking Antigravity to implement features.

---

## Module purpose

In Module 2, you created the project specifications:

- Project brief
- PRD
- User stories
- Acceptance criteria
- Feature scope
- Page route map
- API contract
- Database schema
- Authorization matrix
- Implementation plan
- Task breakdown
- Risk register

Now you will learn how to think like a full-stack developer before writing implementation code.

This module is about **architecture thinking**.

Architecture thinking means understanding:

- How the frontend is structured
- How the backend is structured
- How the database is structured
- How data moves through the system
- How authentication works
- How authorization works
- How errors flow
- How state is managed
- How folders should be organized
- How one feature connects from UI to database

Most junior developers think only file by file.

Professional developers think in systems.

This module will train you to see the full system.

---

## Why architecture thinking matters with Antigravity

Antigravity can create code quickly.

But if you do not understand the architecture, you may not notice when the agent:

- Creates duplicate logic
- Places files in the wrong folder
- Mixes frontend and backend concerns
- Puts business logic inside UI components
- Skips validation
- Creates insecure authorization
- Creates inconsistent API response formats
- Creates database models that do not match API needs
- Adds unnecessary packages
- Generates code you cannot explain

Your goal is not only to build.

Your goal is to understand what is being built.

---

## Architecture mental model

A MERN app has three main layers:

```txt
Frontend → Backend → Database
```

But a real project has more detail:

```txt
User Action
↓
React Component
↓
Frontend State / Form
↓
API Client
↓
Express Route
↓
Middleware
↓
Controller
↓
Service / Business Logic
↓
Mongoose Model
↓
MongoDB
↓
Response
↓
Frontend UI Update
```

You should be able to explain this flow for every major feature.

---

# Part 1: MERN architecture overview

## Classic MERN architecture

A standard MERN application usually looks like this:

```txt
client/
  React frontend

server/
  Express backend

database/
  MongoDB Atlas
```

The frontend handles:

- Pages
- Components
- Forms
- UI state
- API calls
- Auth token storage
- Loading/error/success states
- Routing

The backend handles:

- API routes
- Authentication
- Authorization
- Validation
- Business rules
- Database interaction
- Error handling
- Secure environment variables

The database stores:

- Users
- Main resources
- Orders/bookings/submissions
- Relationships
- Status fields
- Timestamps

---

## What should not happen

Avoid these architecture mistakes:

| Mistake | Why it is bad |
|---|---|
| Frontend directly connects to MongoDB | Exposes database/security risk |
| Frontend decides admin permission alone | Users can manipulate frontend |
| Backend route contains all logic | Code becomes hard to test and maintain |
| Password stored in plain text | Critical security issue |
| No API response format | Frontend integration becomes messy |
| No error middleware | Errors become inconsistent |
| No folder structure | Project becomes difficult to extend |
| No state plan | React state becomes scattered |

---

# Part 2: Recommended project folder structure

## Root structure

For a clear MERN project, use this structure:

```txt
project-name/
  client/
  server/
  docs/
  README.md
```

Optional:

```txt
project-name/
  client/
  server/
  docs/
  design/
  screenshots/
  README.md
```

---

## Frontend folder structure

Recommended React/Vite/TypeScript structure:

```txt
client/
  src/
    assets/
    components/
      common/
      layout/
      ui/
      food/
      cart/
      auth/
      admin/
    pages/
      public/
      auth/
      customer/
      admin/
    routes/
      AppRoutes.tsx
      ProtectedRoute.tsx
      AdminRoute.tsx
    hooks/
    lib/
      api.ts
      auth.ts
      utils.ts
    services/
      authService.ts
      foodService.ts
      orderService.ts
    context/
      AuthContext.tsx
      CartContext.tsx
    types/
      user.ts
      food.ts
      order.ts
      api.ts
    constants/
    styles/
    App.tsx
    main.tsx
```

---

## Frontend folder responsibilities

| Folder | Responsibility |
|---|---|
| `components/common` | Buttons, inputs, cards, loaders, reusable UI |
| `components/layout` | Navbar, footer, sidebar, dashboard layout |
| `components/food` | Food card, food filters, food details sections |
| `components/cart` | Cart item, cart summary, quantity controls |
| `components/auth` | Login/register forms |
| `components/admin` | Admin table, forms, status badges |
| `pages` | Route-level screens |
| `routes` | Route config and protected routes |
| `hooks` | Custom React hooks |
| `lib` | API client, utilities, helper functions |
| `services` | API call functions |
| `context` | Auth/cart/global providers |
| `types` | TypeScript types |
| `constants` | Static values and config |

---

## Backend folder structure

Recommended Express/TypeScript structure:

```txt
server/
  src/
    app.ts
    server.ts
    config/
      env.ts
      db.ts
    modules/
      auth/
        auth.routes.ts
        auth.controller.ts
        auth.service.ts
        auth.validation.ts
      users/
        user.model.ts
        user.routes.ts
        user.controller.ts
        user.service.ts
      foods/
        food.model.ts
        food.routes.ts
        food.controller.ts
        food.service.ts
        food.validation.ts
      orders/
        order.model.ts
        order.routes.ts
        order.controller.ts
        order.service.ts
        order.validation.ts
    middlewares/
      auth.middleware.ts
      role.middleware.ts
      validateRequest.ts
      errorHandler.ts
      notFound.ts
    utils/
      sendResponse.ts
      catchAsync.ts
      AppError.ts
    types/
    constants/
```

---

## Backend folder responsibilities

| Folder/File | Responsibility |
|---|---|
| `app.ts` | Express app setup, middleware, routes |
| `server.ts` | Start server and connect database |
| `config/db.ts` | MongoDB connection |
| `config/env.ts` | Validate environment variables |
| `modules` | Feature-based backend modules |
| `*.routes.ts` | Route definitions |
| `*.controller.ts` | Request/response handling |
| `*.service.ts` | Business logic and database operations |
| `*.model.ts` | Mongoose schema/model |
| `*.validation.ts` | Zod/Joi validation schemas |
| `middlewares` | Auth, role, validation, error handling |
| `utils/sendResponse.ts` | Standard API response helper |
| `utils/catchAsync.ts` | Async error wrapper |
| `utils/AppError.ts` | Custom error class |

---

## Why use feature-based modules?

Instead of this:

```txt
controllers/
routes/
models/
services/
```

You can use:

```txt
modules/
  foods/
  orders/
  auth/
```

This keeps related files together.

For example:

```txt
modules/foods/
  food.model.ts
  food.routes.ts
  food.controller.ts
  food.service.ts
  food.validation.ts
```

This is easier for Antigravity because you can say:

```txt
Work only inside server/src/modules/foods.
```

That reduces unrelated changes.

---

# Part 3: Frontend architecture thinking

React apps should be planned around:

- Pages
- Components
- Props
- State
- Data fetching
- User actions
- UI states

React’s official “Thinking in React” approach recommends breaking the UI into components, describing visual states, and connecting data flow between components.

---

## Frontend architecture questions

Before building a page, ask:

1. What route is this page?
2. Is it public or protected?
3. What data does it need?
4. Where does the data come from?
5. What components make up the page?
6. What state is local?
7. What state is global?
8. What loading state is needed?
9. What error state is needed?
10. What empty state is needed?
11. What user actions happen here?
12. What API calls happen here?

---

## Example: Menu page architecture

Route:

```txt
/menu
```

Purpose:

```txt
Show available food items.
```

Data needed:

```txt
foods
categories
search query
loading state
error state
```

Components:

```txt
MenuPage
FoodFilter
FoodGrid
FoodCard
EmptyState
LoadingSpinner
ErrorMessage
```

User actions:

```txt
Search food
Filter category
Open details
Add to cart
```

API calls:

```txt
GET /foods
GET /foods?search=burger
GET /foods?category=Pizza
```

State:

| State | Location |
|---|---|
| Search query | MenuPage local state |
| Selected category | MenuPage local state |
| Food list | Server state via API/TanStack Query |
| Cart items | Cart context or localStorage |
| Loading/error | Query state |

---

## Component tree example

```txt
MenuPage
  ├── PageHeader
  ├── FoodFilter
  ├── FoodGrid
  │     └── FoodCard
  ├── EmptyState
  └── Pagination optional
```

---

## Frontend state categories

Not all state is the same.

| State type | Example | Where to manage |
|---|---|---|
| Local UI state | Modal open/closed | Component state |
| Form state | Login form input | React Hook Form or local state |
| Global client state | Cart items | Context/Zustand/localStorage |
| Server state | Food list, orders | TanStack Query |
| Auth state | Current user/token | Auth context |
| URL state | Search/filter query | URL params/search params |

---

## Frontend architecture document

Create:

```txt
docs/FRONTEND_ARCHITECTURE.md
```

Use this template:

```md
# Frontend Architecture

## Stack
- React
- TypeScript
- Tailwind CSS
- React Router
- TanStack Query optional
- Context API for auth/cart

## Route groups

### Public routes
-

### Auth routes
-

### Customer protected routes
-

### Admin protected routes
-

## Component groups

### Layout components
-

### Shared UI components
-

### Feature components
-

## State plan

| State | Type | Where managed |
|---|---|---|
| Auth user | Global | AuthContext |
| Cart | Global/localStorage | CartContext |
| Food list | Server | TanStack Query/API service |
| Search/filter | Local/URL | Page state or URL |
| Forms | Form state | React Hook Form/local state |

## API service plan

| Service file | Purpose |
|---|---|
| authService.ts | login/register/me |
| foodService.ts | food list/details/admin CRUD |
| orderService.ts | order placement/history/admin updates |

## UI states required
- Loading
- Error
- Empty
- Success
- Unauthorized
- Not found
```

---

# Part 4: Backend architecture thinking

Backend architecture should separate responsibilities.

A common Express flow:

```txt
Route → Middleware → Controller → Service → Model → Database
```

---

## Route

Defines the URL and HTTP method.

Example:

```txt
POST /api/orders
```

Route should not contain heavy business logic.

---

## Middleware

Runs before controller.

Examples:

- Authentication middleware
- Role middleware
- Validation middleware
- Error middleware
- CORS middleware
- JSON parser

Express middleware is central to request processing. Error-handling middleware in Express uses four arguments: `err`, `req`, `res`, and `next`.

---

## Controller

Handles request and response.

Controller should:

- Read request
- Call service
- Send response
- Pass errors to error handler

Controller should not contain too much business logic.

---

## Service

Contains business logic.

Service should:

- Query database
- Apply business rules
- Create/update/delete documents
- Return data to controller

---

## Model

Defines database schema.

Mongoose model should include:

- Fields
- Types
- Required rules
- Defaults
- Enums
- Indexes
- Timestamps

---

## Backend flow example: Create order

```txt
POST /api/orders
↓
authMiddleware checks token
↓
validateRequest checks body
↓
orderController.createOrder
↓
orderService.createOrder
↓
Order model creates document
↓
MongoDB saves order
↓
sendResponse returns success
```

---

## Backend architecture document

Create:

```txt
docs/BACKEND_ARCHITECTURE.md
```

Use this template:

```md
# Backend Architecture

## Stack
- Node.js
- Express.js
- TypeScript
- MongoDB
- Mongoose
- JWT
- Zod/Joi validation

## Request flow

```txt
Request
→ Route
→ Middleware
→ Controller
→ Service
→ Model
→ MongoDB
→ Response
```

## Module structure

```txt
modules/
  auth/
  users/
  foods/
  orders/
```

## Middleware plan

| Middleware | Purpose |
|---|---|
| authMiddleware | Verify JWT |
| roleMiddleware | Check role |
| validateRequest | Validate request body |
| errorHandler | Handle errors consistently |
| notFound | Handle unknown routes |

## Response format

Success:

```json
{
  "success": true,
  "message": "Success message",
  "data": {}
}
```

Error:

```json
{
  "success": false,
  "message": "Error message",
  "errors": []
}
```

## Error handling strategy
- Use async error wrapper
- Use custom AppError
- Use global error handler
- Hide stack trace in production
- Return consistent errors
```

---

# Part 5: Database architecture thinking

MongoDB is flexible, but flexible does not mean random.

MongoDB’s official data modeling guidance emphasizes designing based on application data access patterns.

That means you should ask:

- What data is accessed together?
- What queries will happen often?
- What fields are required?
- What data should be embedded?
- What data should be referenced?
- What indexes are needed?
- What should remain stable even if related data changes later?

---

## Example: Order item snapshot

If a customer orders a burger for 250 BDT, and later the admin changes the burger price to 300 BDT, the old order should still show 250 BDT.

So in the order, store a snapshot:

```ts
items: [
  {
    foodId: ObjectId,
    name: "Chicken Burger",
    price: 250,
    quantity: 2
  }
]
```

Do not rely only on current food price.

This is architecture thinking.

---

## Database architecture document

Create:

```txt
docs/DATABASE_ARCHITECTURE.md
```

Use this template:

```md
# Database Architecture

## Collections
1. users
2. foods
3. orders

## Access patterns

| User action | Collection/query needed |
|---|---|
| Browse foods | foods.find({ isAvailable: true }) |
| Search food | foods.find({ name/category filter }) |
| Place order | orders.create |
| View my orders | orders.find({ user }) |
| Admin view all orders | orders.find() |
| Admin update status | orders.findByIdAndUpdate |

## Embed vs reference decisions

| Data | Decision | Reason |
|---|---|---|
| Order → user | Reference | User account exists separately |
| Order → items | Embed snapshot | Preserve price/name at order time |
| Food → createdBy | Reference | Track admin creator |

## Index plan

| Collection | Field | Reason |
|---|---|---|
| users | email | unique login lookup |
| foods | category | filtering |
| foods | name | search |
| orders | user | my orders |
| orders | status | admin filtering |
| orders | createdAt | sorting |
```

---

# Part 6: Authentication architecture

Authentication answers:

```txt
Who is the user?
```

A JWT-based auth flow usually looks like this:

```txt
User submits email/password
↓
Backend validates credentials
↓
Backend signs JWT
↓
Frontend stores token
↓
Frontend sends token in Authorization header
↓
Backend verifies token
↓
Backend attaches user to request
```

---

## Auth flow document

Create:

```txt
docs/AUTH_FLOW.md
```

Use this template:

```md
# Authentication Flow

## Register flow

```txt
User fills register form
→ Frontend validates basic input
→ POST /api/auth/register
→ Backend validates input
→ Backend hashes password
→ Backend saves user
→ Backend returns token/user
→ Frontend stores token
→ User redirected
```

## Login flow

```txt
User fills login form
→ POST /api/auth/login
→ Backend checks email/password
→ Backend returns token/user
→ Frontend stores token
→ User redirected
```

## Protected request flow

```txt
Frontend sends Authorization: Bearer token
→ authMiddleware verifies token
→ Backend loads user
→ Controller runs
→ Response returned
```

## Logout flow

```txt
User clicks logout
→ Frontend removes token/user
→ Redirect to login/home
```

## Security rules
- Never store plain text password
- Hash password before saving
- Do not trust frontend role
- Verify token on backend
- Check role from database
```

---

# Part 7: Authorization architecture

Authorization answers:

```txt
What is the user allowed to do?
```

This is different from login.

A user may be logged in but still not allowed to access admin routes.

OWASP guidance is clear that access control must be enforced in trusted server-side code or serverless APIs, not only in frontend UI.

---

## Authorization flow example

```txt
Request to PATCH /api/orders/:id/status
↓
authMiddleware checks valid token
↓
roleMiddleware checks user.role === "admin"
↓
Controller updates order status
```

If a customer tries the same endpoint, backend should return:

```txt
403 Forbidden
```

---

## Authorization architecture document

Create:

```txt
docs/AUTHORIZATION_ARCHITECTURE.md
```

Use this template:

```md
# Authorization Architecture

## Roles

| Role | Description |
|---|---|
| visitor | Not logged in |
| customer | Logged-in normal user |
| admin | Admin/restaurant manager |

## Rule
Frontend can hide UI, but backend must enforce access.

## Protected route types

| Route type | Example | Check |
|---|---|---|
| Public | GET /foods | No token |
| Authenticated | POST /orders | Valid token |
| Owner-only | GET /orders/my-orders | Valid token + own user ID |
| Admin-only | POST /foods | Valid token + admin role |

## Backend authorization flow

```txt
Request
→ authMiddleware
→ roleMiddleware or ownership check
→ controller
→ response
```

## Frontend authorization flow

```txt
AuthContext reads user
→ ProtectedRoute checks login
→ AdminRoute checks role for UI
→ Backend still verifies permission
```

## Important security rules
- Never trust role from request body
- Never rely only on hidden frontend buttons
- Check permission on backend
- Deny by default
- Log unauthorized attempts if possible
```

---

# Part 8: Data flow architecture

Data flow explains how information moves.

Example: customer places order.

```txt
Customer clicks Place Order
↓
Checkout form validates input
↓
Frontend sends POST /orders
↓
Backend checks JWT
↓
Backend validates body
↓
Backend creates order
↓
MongoDB stores order
↓
Backend returns success response
↓
Frontend clears cart
↓
Frontend redirects to My Orders
```

---

## Data flow document

Create:

```txt
docs/DATA_FLOW.md
```

Use this template:

```md
# Data Flow

## Flow 1: Browse food

```txt
User opens /menu
→ MenuPage loads
→ foodService.getFoods()
→ GET /api/foods
→ Backend queries foods
→ Response returns food list
→ FoodGrid renders cards
```

## Flow 2: Add to cart

```txt
User clicks Add to Cart
→ CartContext receives item
→ If item exists, increase quantity
→ If item does not exist, add item
→ Cart persists to localStorage optional
→ Cart badge updates
```

## Flow 3: Place order

```txt
User submits checkout
→ Frontend validates form
→ POST /api/orders with token
→ Backend verifies token
→ Backend validates body
→ Order service creates order
→ Cart clears
→ User redirected to My Orders
```

## Flow 4: Admin updates order status

```txt
Admin opens orders page
→ GET /api/orders
→ Backend checks admin role
→ Orders displayed
→ Admin changes status
→ PATCH /api/orders/:id/status
→ Backend updates order
→ UI refreshes order list
```
```

---

# Part 9: Error flow architecture

Errors should be planned.

Common error types:

| Error type | Example |
|---|---|
| Validation error | Missing email/password |
| Authentication error | Missing or invalid token |
| Authorization error | Customer accessing admin route |
| Not found error | Food item does not exist |
| Conflict error | Email already registered |
| Server error | Database connection fails |
| Network error | Frontend cannot reach backend |

---

## Error flow document

Create:

```txt
docs/ERROR_FLOW.md
```

Use this template:

```md
# Error Flow

## Backend error format

```json
{
  "success": false,
  "message": "Error message",
  "errors": []
}
```

## Frontend error handling

| Error | UI behavior |
|---|---|
| 400 validation | Show form field/general error |
| 401 unauthenticated | Redirect to login or show login message |
| 403 unauthorized | Show access denied |
| 404 not found | Show not found page/state |
| 409 conflict | Show duplicate/email exists message |
| 500 server error | Show generic server error |

## Error handling rules
- Do not expose stack trace to user
- Show readable messages
- Log useful details during development
- Use consistent API error shape
- Test error states manually
```

---

# Part 10: Architecture decision records

Professional teams document important decisions.

Create:

```txt
docs/ARCHITECTURE_DECISIONS.md
```

Use this structure:

```md
# Architecture Decisions

## Decision 1: Use separate client and server folders

### Decision
The app will use separate `client/` and `server/` folders.

### Why
This helps junior developers understand frontend/backend separation clearly.

### Alternatives considered
- Next.js full-stack app
- Single folder Express serving React build

### Risks
- Requires separate deployment setup
- Requires CORS configuration

### Date
-

---

## Decision 2: Use feature-based backend modules

### Decision
Backend will use `modules/auth`, `modules/foods`, and `modules/orders`.

### Why
Keeps route, controller, service, model, and validation close together.

### Risks
Students must understand module boundaries.

### Date
-

---

## Decision 3: Use order item snapshot

### Decision
Order items will store foodId, name, price, and quantity.

### Why
Order history should preserve item name and price at order time.

### Risks
Food data may be duplicated inside order.

### Date
-
```

---

# Part 11: Antigravity prompts for this module

## Prompt 1: Create architecture docs

```txt
I am doing Module 3: Codebase and Architecture Thinking.

Read these files:
- docs/PROJECT_BRIEF.md
- docs/PRD.md
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTHORIZATION_MATRIX.md

Create these files:
1. docs/ARCHITECTURE_OVERVIEW.md
2. docs/FRONTEND_ARCHITECTURE.md
3. docs/BACKEND_ARCHITECTURE.md
4. docs/DATABASE_ARCHITECTURE.md
5. docs/AUTH_FLOW.md
6. docs/AUTHORIZATION_ARCHITECTURE.md
7. docs/DATA_FLOW.md
8. docs/ERROR_FLOW.md
9. docs/ARCHITECTURE_DECISIONS.md

Rules:
- Do not create app code.
- Do not install packages.
- Keep the architecture realistic for junior MERN developers.
- Use React, TypeScript, Tailwind, Express, MongoDB, Mongoose, JWT.
- Include user and admin roles.
- After creating files, summarize what each file is for.
```

---

## Prompt 2: Review architecture consistency

```txt
Review the architecture documents.

Check:
1. Does frontend architecture match page route map?
2. Does backend architecture match API contract?
3. Does database architecture match the required features?
4. Does auth flow match authorization rules?
5. Does data flow explain key user actions?
6. Does error flow handle common errors?
7. Are decisions clear and realistic?

Do not edit files yet.

Return:
- Strong parts
- Missing parts
- Inconsistencies
- Required fixes before coding
```

---

## Prompt 3: Improve only data flow

```txt
Read only:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/DATA_FLOW.md

Improve DATA_FLOW.md.

Add clear flows for:
1. Register
2. Login
3. Browse food
4. Add to cart
5. Place order
6. View my orders
7. Admin create food
8. Admin update order status

Do not edit other files.
```

---

## Prompt 4: Create architecture explanation for interview

```txt
Read all architecture docs.

Create docs/INTERVIEW_ARCHITECTURE_EXPLANATION.md.

Include:
1. 30-second project architecture explanation
2. 1-minute project architecture explanation
3. Frontend architecture explanation
4. Backend architecture explanation
5. Database architecture explanation
6. Auth and authorization explanation
7. Data flow explanation for placing an order
8. Biggest architecture decision and why
```

---

# Part 12: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 04-module-03-codebase-architecture-thinking.md
2. PROJECT_BRIEF.md
3. PRD.md
4. API_CONTRACT.md
5. DATABASE_SCHEMA.md
6. AUTHORIZATION_MATRIX.md
7. React Thinking in React docs
8. Express middleware docs
9. MongoDB data modeling docs
10. OWASP access control docs
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for MERN codebase and architecture thinking.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. What architecture thinking means
2. MERN frontend/backend/database responsibilities
3. Recommended folder structure
4. Frontend component and state architecture
5. Backend route-controller-service-model flow
6. MongoDB data modeling decisions
7. Auth flow
8. Authorization flow
9. Data flow
10. Error flow
11. Common mistakes
12. Practice checklist
```

---

## NotebookLM Prompt 2: Architecture Review

```txt
Review my architecture docs.

Check:
1. Are folder structures clear?
2. Are frontend and backend responsibilities separated?
3. Are data flows clear?
4. Is auth flow secure?
5. Is authorization enforced server-side?
6. Are database decisions aligned with access patterns?
7. Are errors handled consistently?
8. What should I fix before coding?

Return:
- Strong parts
- Missing parts
- Risks
- Fix checklist
```

---

## NotebookLM Prompt 3: Interview Explanation

```txt
Help me explain my MERN architecture in an interview.

Create:
1. A 30-second explanation
2. A 1-minute explanation
3. A technical explanation
4. A simple non-technical explanation
5. One example data flow
6. One security decision
7. One database design decision
```

---

# Part 13: Required video resources

Watch at least two videos.

Search YouTube:

```txt
MERN stack architecture explained
React component architecture and state management
Express route controller service architecture
MongoDB schema design best practices
JWT authentication authorization MERN stack
```

Recommended video note format:

```md
# Module 3 Video Learning Notes

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
docs/notebooklm/module-03-video-learning-notes.md
```

---

# Part 14: Practice tasks

## Practice Task 1: Create architecture docs

Use Antigravity Prompt 1.

Expected files:

```txt
docs/
  ARCHITECTURE_OVERVIEW.md
  FRONTEND_ARCHITECTURE.md
  BACKEND_ARCHITECTURE.md
  DATABASE_ARCHITECTURE.md
  AUTH_FLOW.md
  AUTHORIZATION_ARCHITECTURE.md
  DATA_FLOW.md
  ERROR_FLOW.md
  ARCHITECTURE_DECISIONS.md
```

---

## Practice Task 2: Draw the system flow

Create:

```txt
docs/SYSTEM_FLOW.md
```

Use this format:

```md
# System Flow

## Full-stack request lifecycle

```txt
User action
→ React component
→ API service
→ Express route
→ Middleware
→ Controller
→ Service
→ Mongoose model
→ MongoDB
→ Response
→ UI update
```

## Example: Place order

```txt
Click checkout
→ CheckoutPage
→ orderService.createOrder
→ POST /api/orders
→ authMiddleware
→ validateRequest
→ orderController
→ orderService
→ Order model
→ MongoDB
→ success response
→ cart clears
→ redirect to my orders
```
```

---

## Practice Task 3: Create folder tree proposal

Create:

```txt
docs/FOLDER_TREE_PROPOSAL.md
```

Include:

```txt
client/
server/
docs/
```

Then include detailed frontend and backend trees.

---

## Practice Task 4: Create state ownership map

Create:

```txt
docs/STATE_OWNERSHIP_MAP.md
```

Use this format:

```md
# State Ownership Map

| State | Owner | Why |
|---|---|---|
| Auth user | AuthContext | Needed globally |
| Cart items | CartContext/localStorage | Needed across pages |
| Food list | TanStack Query/API service | Server state |
| Search query | MenuPage or URL | Page-specific |
| Checkout form | CheckoutPage/form library | Form-specific |
| Admin order list | TanStack Query/API service | Server state |
```

---

## Practice Task 5: Create API-to-UI map

Create:

```txt
docs/API_TO_UI_MAP.md
```

Use this format:

```md
# API to UI Map

| API endpoint | Frontend page/component | User action |
|---|---|---|
| GET /foods | MenuPage/FoodGrid | Browse foods |
| GET /foods/:id | FoodDetailsPage | View details |
| POST /auth/login | LoginPage | Login |
| POST /orders | CheckoutPage | Place order |
| GET /orders/my-orders | MyOrdersPage | View my orders |
| GET /orders | AdminOrdersPage | Admin views orders |
| PATCH /orders/:id/status | AdminOrdersPage | Admin updates status |
```

---

## Practice Task 6: Create security boundary map

Create:

```txt
docs/SECURITY_BOUNDARY_MAP.md
```

Use this format:

```md
# Security Boundary Map

## Public
- Home page
- Menu page
- Food details page
- Register
- Login
- GET /foods
- GET /foods/:id

## Customer protected
- Cart checkout
- My orders
- POST /orders
- GET /orders/my-orders

## Admin protected
- Admin dashboard
- Food management
- Order management
- POST /foods
- PATCH /foods/:id
- DELETE /foods/:id
- GET /orders
- PATCH /orders/:id/status

## Rule
Frontend may hide restricted UI, but backend must enforce all access rules.
```

---

# Required deliverables for this module

Submit:

```txt
1. ARCHITECTURE_OVERVIEW.md
2. FRONTEND_ARCHITECTURE.md
3. BACKEND_ARCHITECTURE.md
4. DATABASE_ARCHITECTURE.md
5. AUTH_FLOW.md
6. AUTHORIZATION_ARCHITECTURE.md
7. DATA_FLOW.md
8. ERROR_FLOW.md
9. ARCHITECTURE_DECISIONS.md
10. SYSTEM_FLOW.md
11. FOLDER_TREE_PROPOSAL.md
12. STATE_OWNERSHIP_MAP.md
13. API_TO_UI_MAP.md
14. SECURITY_BOUNDARY_MAP.md
15. INTERVIEW_ARCHITECTURE_EXPLANATION.md
16. NotebookLM Study Guide screenshot
17. NotebookLM architecture review screenshot
18. Video learning notes
19. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/04-module-03-codebase-architecture-thinking-reflection.md
```

Use this format:

```md
# Reflection: Module 3 - Codebase and Architecture Thinking

## What architecture docs I created
-

## What I learned about frontend architecture
-

## What I learned about backend architecture
-

## What I learned about database architecture
-

## What I learned about auth flow
-

## What I learned about authorization
-

## What I learned about data flow
-

## What Antigravity helped with
-

## What I had to correct manually
-

## How I will use this architecture before coding
-
```

---

# Quiz

## Multiple choice

**1. What is architecture thinking?**

A. Choosing only colors  
B. Understanding how the full system is structured and connected  
C. Writing random code quickly  
D. Deploying before planning  

Correct answer: **B**

---

**2. What are the three main MERN layers?**

A. React, Express, MongoDB  
B. Photoshop, Excel, Word  
C. HTML, GitHub, YouTube  
D. Browser, mouse, keyboard  

Correct answer: **A**

---

**3. What is the common backend flow?**

A. Route → Middleware → Controller → Service → Model → Database  
B. CSS → Image → Button → Logo  
C. GitHub → Figma → YouTube → Email  
D. Browser → MongoDB directly  

Correct answer: **A**

---

**4. Why should frontend not connect directly to MongoDB?**

A. It exposes security and database risks  
B. It improves security  
C. It removes need for backend  
D. It makes CSS better  

Correct answer: **A**

---

**5. What should enforce admin authorization?**

A. Backend middleware/server-side checks  
B. Hidden frontend buttons only  
C. CSS classes  
D. README text  

Correct answer: **A**

---

**6. What is server state?**

A. Data that comes from backend/API, such as food list or orders  
B. Button hover color  
C. Font size  
D. Static logo only  

Correct answer: **A**

---

**7. Why store order item snapshot?**

A. To preserve name/price at order time  
B. To expose password  
C. To remove order history  
D. To avoid MongoDB  

Correct answer: **A**

---

**8. What is the purpose of `DATA_FLOW.md`?**

A. Explain how data moves through the system  
B. Store UI colors only  
C. Replace backend tests  
D. Delete files  

Correct answer: **A**

---

**9. What is the purpose of `ERROR_FLOW.md`?**

A. Plan consistent handling of validation, auth, not-found, and server errors  
B. Hide all errors forever  
C. Ignore failed requests  
D. Replace API contract  

Correct answer: **A**

---

**10. Why should architecture decisions be documented?**

A. So future changes and interview explanations are easier  
B. To make the repo confusing  
C. To hide project scope  
D. To avoid learning  

Correct answer: **A**

---

## Short-answer questions

1. Explain the MERN request lifecycle.
2. What is the difference between frontend state and server state?
3. Why should backend logic be separated into route, controller, service, and model?
4. What is the purpose of middleware?
5. What should be included in a frontend architecture document?
6. What should be included in a backend architecture document?
7. Why should authorization happen on the backend?
8. What is one important MongoDB data modeling decision in a food ordering app?
9. What is the purpose of architecture decision records?
10. How will architecture docs help you use Antigravity better?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Architecture overview | Full-stack system explained clearly |
| Frontend architecture | Pages, components, state, API services planned |
| Backend architecture | Route/controller/service/model flow planned |
| Database architecture | Access patterns and relationships considered |
| Auth flow | Register/login/protected request flow explained |
| Authorization | Backend permission rules clearly defined |
| Data flow | Key user/admin flows explained |
| Error flow | Common errors and UI responses planned |
| Architecture decisions | Important technical decisions documented |
| Folder tree | Realistic project structure proposed |
| State ownership | State responsibilities mapped |
| API-to-UI map | Endpoints connected to UI features |
| Security boundary | Public/protected/admin boundaries clear |
| NotebookLM evidence | Study guide and review screenshots submitted |
| Reflection | Student explains architecture in own words |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I understand the full MERN architecture of my project, including frontend structure, backend structure, database design, auth flow, authorization rules, data flow, error flow, state ownership, security boundaries, and architecture decisions before asking Antigravity to implement features.
```

After completing this file, continue to:

```txt
05-module-04-skill-md-mastery.md
```
