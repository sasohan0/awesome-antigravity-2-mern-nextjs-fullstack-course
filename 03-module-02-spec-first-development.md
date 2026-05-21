# Module 2: Spec-First Development — Plan Before You Code

**File Name:** `03-module-02-spec-first-development.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 3–5 hours  
**Recommended After:** Module 1: Antigravity Setup  
**Main Goal:** Learn how to turn a vague project idea into clear specifications before asking Antigravity to build.

---

## Module purpose

This module teaches you how to plan a MERN project before writing code.

Most junior developers make this mistake:

```txt
They start coding before understanding the project.
```

With Antigravity, this mistake becomes even more dangerous because the agent can create many files quickly.

If your project idea is unclear, Antigravity may create:

- Wrong folder structure
- Wrong database models
- Unnecessary features
- Confusing routes
- Inconsistent naming
- Weak authentication flow
- Broken frontend/backend integration
- Code that is hard to explain in interviews

Spec-first development solves this problem.

In this module, you will create the core planning documents that guide the whole project.

You will learn how to create:

```txt
1. PROJECT_BRIEF.md
2. PRD.md
3. USER_STORIES.md
4. ACCEPTANCE_CRITERIA.md
5. FEATURE_SCOPE.md
6. PAGE_ROUTE_MAP.md
7. API_CONTRACT.md
8. DATABASE_SCHEMA.md
9. AUTHORIZATION_MATRIX.md
10. IMPLEMENTATION_PLAN.md
11. TASK_BREAKDOWN.md
12. RISK_REGISTER.md
```

These files will become the “source of truth” for Antigravity.

---

## What is spec-first development?

Spec-first development means:

```txt
You define what should be built before you start building it.
```

Instead of saying:

```txt
Build a food ordering app.
```

You define:

- Who will use the app
- What problem the app solves
- What pages are needed
- What user roles exist
- What features are in scope
- What features are out of scope
- What database models are needed
- What API endpoints are needed
- What validation rules are needed
- What success looks like
- What should be tested

This makes development faster, safer, and easier to review.

---

## Why spec-first matters when using Antigravity

Antigravity can plan, code, run commands, and verify work. But it still needs clear direction.

If you give vague instructions, you may get vague or overbuilt results.

Spec-first files help Antigravity understand:

| Spec file | Why it helps Antigravity |
|---|---|
| `PROJECT_BRIEF.md` | Gives the project summary and goal |
| `PRD.md` | Explains product requirements |
| `USER_STORIES.md` | Shows what users need to do |
| `ACCEPTANCE_CRITERIA.md` | Defines when a feature is complete |
| `PAGE_ROUTE_MAP.md` | Prevents frontend route confusion |
| `API_CONTRACT.md` | Aligns frontend and backend |
| `DATABASE_SCHEMA.md` | Guides models and relations |
| `AUTHORIZATION_MATRIX.md` | Clarifies permissions |
| `IMPLEMENTATION_PLAN.md` | Defines build order |
| `TASK_BREAKDOWN.md` | Converts big work into small tasks |
| `RISK_REGISTER.md` | Identifies blockers before they become problems |

These files save quota because you do not need to repeat the same context in every prompt.

---

## The main idea

Before asking Antigravity to build, create this chain:

```txt
Idea → Project Brief → PRD → User Stories → Acceptance Criteria → Routes → API Contract → Database Schema → Tasks → Implementation
```

If any step is missing, the build becomes risky.

---

## Example project idea

For this module, we will use this example:

```txt
LocalBites — A local food ordering platform where customers can browse food items, add items to cart, place orders, and admins can manage food items and orders.
```

You can also choose another project idea:

- Event booking app
- Course marketplace
- Expense tracker
- Real estate listing app
- Fitness appointment booking app
- Service marketplace
- Job application tracker

Use one project idea consistently throughout this module.

---

# Part 1: Project Brief

## What is a project brief?

A project brief is a short document that explains the project at a high level.

It answers:

- What are we building?
- Who is it for?
- What problem does it solve?
- What are the core features?
- What is out of scope?
- What is the final deliverable?

---

## `PROJECT_BRIEF.md` template

Create:

```txt
docs/PROJECT_BRIEF.md
```

Use this structure:

```md
# Project Brief

## Project name
LocalBites

## One-line summary
A local food ordering platform where customers can browse food items, place orders, and admins can manage menu items and orders.

## Problem
Small local restaurants need a simple online ordering platform where customers can view food items and place orders without calling manually.

## Target users
1. Customers
2. Admin/Restaurant manager

## Main user goals
- Customers can browse food items
- Customers can add food items to cart
- Customers can place orders
- Customers can view their orders
- Admin can add, update, and delete food items
- Admin can view and update order status

## Core features
1. Public food listing
2. Food details
3. Cart
4. Checkout/order placement
5. Authentication
6. User order history
7. Admin food management
8. Admin order management

## Out of scope for first version
- Payment gateway
- Delivery tracking map
- Multiple restaurants
- Coupon system
- Real-time chat
- Mobile app

## Tech stack
Frontend:
React, TypeScript, Tailwind CSS

Backend:
Node.js, Express.js, MongoDB, Mongoose

Auth:
JWT-based authentication

Deployment:
Frontend on Vercel
Backend on Render
Database on MongoDB Atlas

## Final deliverables
- GitHub repository
- Live frontend link
- Live backend/API link
- README.md
- Screenshots
- Demo credentials
- Documentation files
```

---

# Part 2: PRD

## What is a PRD?

PRD means **Product Requirements Document**.

A PRD explains what the product should do and why.

A good PRD helps developers avoid random feature decisions.

---

## What a PRD should include

Your `PRD.md` should include:

```txt
1. Product overview
2. Goals
3. Non-goals
4. User roles
5. Core features
6. Functional requirements
7. Non-functional requirements
8. User flows
9. Success criteria
10. Assumptions
11. Risks
```

---

## `PRD.md` template

Create:

```txt
docs/PRD.md
```

Use this structure:

```md
# Product Requirements Document

## Product name
LocalBites

## Product overview
LocalBites is a MERN-based food ordering platform for local restaurants. Customers can browse menu items, add them to cart, place orders, and view order history. Admins can manage food items and update order status.

## Product goals
1. Allow customers to browse food items easily.
2. Allow customers to place orders.
3. Allow admins to manage food items.
4. Allow admins to manage order statuses.
5. Provide a responsive and clean UI.
6. Build a portfolio-ready MERN project.

## Non-goals
The first version will not include:
- Online payment
- Real-time delivery tracking
- Multiple restaurant onboarding
- Coupon engine
- Push notifications
- Mobile app

## User roles

### Customer
Can browse food, add to cart, place orders, and view order history.

### Admin
Can manage food items and orders.

## Functional requirements

### Public food browsing
- Users can see a list of available food items.
- Users can filter/search food items.
- Users can open a food details page.

### Cart
- Users can add food items to cart.
- Users can update quantity.
- Users can remove items.
- Users can see total price.

### Authentication
- Users can register.
- Users can log in.
- JWT token is stored securely on frontend.
- Protected routes require login.

### Order placement
- Logged-in users can place orders.
- Order includes selected items, total price, delivery information, and status.
- User can view order history.

### Admin food management
- Admin can add food.
- Admin can update food.
- Admin can delete food.
- Admin can view all foods.

### Admin order management
- Admin can view all orders.
- Admin can update order status.

## Non-functional requirements
- App must be responsive.
- API responses should be consistent.
- Protected routes must be secured.
- Error messages should be user-friendly.
- Code should be organized and readable.
- Project should be deployable.

## Success criteria
The project is successful when:
1. A customer can register and log in.
2. A customer can browse food items.
3. A customer can place an order.
4. A customer can view order history.
5. Admin can manage food items.
6. Admin can update order status.
7. App is deployed.
8. README explains setup and features.
```

---

# Part 3: User Stories

## What is a user story?

A user story describes what a user wants to do and why.

The standard format is:

```txt
As a [type of user],
I want to [do something],
so that [benefit].
```

User stories help you think from the user's perspective, not just from the developer's perspective.

---

## User story rules

Good user stories should be:

- Small
- Clear
- Testable
- User-focused
- Connected to acceptance criteria

Avoid vague stories like:

```txt
As a user, I want a nice app.
```

Write specific stories like:

```txt
As a customer, I want to add food items to my cart, so that I can prepare my order before checkout.
```

---

## `USER_STORIES.md` template

Create:

```txt
docs/USER_STORIES.md
```

Use this structure:

```md
# User Stories

## Customer stories

### Story 1: Browse food items
As a customer, I want to browse available food items, so that I can choose what I want to order.

### Story 2: Search food items
As a customer, I want to search or filter food items, so that I can find my preferred food quickly.

### Story 3: View food details
As a customer, I want to view food details, so that I can understand price, description, and category before ordering.

### Story 4: Add food to cart
As a customer, I want to add food items to my cart, so that I can prepare my order.

### Story 5: Update cart
As a customer, I want to update quantity or remove items from cart, so that I can control my order.

### Story 6: Place order
As a logged-in customer, I want to place an order, so that the restaurant can process my request.

### Story 7: View order history
As a logged-in customer, I want to view my previous orders, so that I can track my order history.

## Admin stories

### Story 8: Add food item
As an admin, I want to add new food items, so that customers can order them.

### Story 9: Update food item
As an admin, I want to update food details, so that menu information stays accurate.

### Story 10: Delete food item
As an admin, I want to delete unavailable food items, so that customers do not order them.

### Story 11: View all orders
As an admin, I want to view all customer orders, so that I can manage restaurant operations.

### Story 12: Update order status
As an admin, I want to update order status, so that customers know the progress of their orders.
```

---

# Part 4: Acceptance Criteria

## What are acceptance criteria?

Acceptance criteria define when a feature is complete.

They remove confusion.

Instead of saying:

```txt
Cart should work.
```

Write:

```txt
Given a customer is viewing a food item,
When they click Add to Cart,
Then the item appears in the cart with correct quantity and price.
```

---

## Acceptance criteria format

Use this format:

```txt
Given [context]
When [action]
Then [expected result]
```

This is useful because it is clear and testable.

---

## `ACCEPTANCE_CRITERIA.md` template

Create:

```txt
docs/ACCEPTANCE_CRITERIA.md
```

Use this structure:

```md
# Acceptance Criteria

## Feature: Browse food items

### Criteria 1
Given a visitor opens the menu page,
When food items exist,
Then the page displays food cards with name, image, price, category, and action button.

### Criteria 2
Given no food items exist,
When the visitor opens the menu page,
Then the page displays an empty state message.

## Feature: Add to cart

### Criteria 1
Given a customer sees a food item,
When the customer clicks Add to Cart,
Then the item is added to the cart.

### Criteria 2
Given a food item already exists in the cart,
When the customer clicks Add to Cart again,
Then the quantity increases instead of creating a duplicate item.

## Feature: Place order

### Criteria 1
Given a logged-in customer has items in cart,
When the customer submits checkout information,
Then an order is created with correct items, total price, user ID, and pending status.

### Criteria 2
Given a visitor is not logged in,
When they try to place an order,
Then they are redirected to login or shown an authentication message.

## Feature: Admin food management

### Criteria 1
Given an admin is logged in,
When the admin submits valid food data,
Then a new food item is created.

### Criteria 2
Given a non-admin user tries to access food management,
When they visit the admin route,
Then access is denied.

## Feature: Admin order management

### Criteria 1
Given an admin is logged in,
When the admin opens the order dashboard,
Then all orders are displayed.

### Criteria 2
Given an admin updates order status,
When the update is successful,
Then the order status changes and the UI reflects the update.
```

---

# Part 5: Feature Scope

## Why feature scope matters

A final project fails when the scope becomes too large.

Antigravity may suggest too many features.

You must define:

- Must-have
- Should-have
- Nice-to-have
- Out of scope

---

## `FEATURE_SCOPE.md` template

Create:

```txt
docs/FEATURE_SCOPE.md
```

Use this structure:

```md
# Feature Scope

## Must-have features
These features are required for the first version.

1. Public food listing
2. Food details page
3. Cart
4. User registration/login
5. Order placement
6. User order history
7. Admin food CRUD
8. Admin order status update
9. Responsive UI
10. Deployment

## Should-have features
These features are useful but not mandatory.

1. Search/filter
2. Category filter
3. Order status badge
4. Toast notifications
5. Dashboard summary cards

## Nice-to-have features
These can be added after the main project works.

1. Dark mode
2. Charts
3. Reviews
4. Favorite items
5. Email notification

## Out of scope
These should not be built in the first version.

1. Payment gateway
2. Real-time tracking
3. Multiple restaurant onboarding
4. Delivery rider app
5. Push notifications
6. AI recommendation system
```

---

# Part 6: Page Route Map

## Why page route map matters

Frontend routing becomes messy if you do not plan pages first.

Before coding React routes, define:

- Public pages
- Auth pages
- Protected user pages
- Admin pages
- Error pages

---

## `PAGE_ROUTE_MAP.md` template

Create:

```txt
docs/PAGE_ROUTE_MAP.md
```

Use this structure:

```md
# Page Route Map

## Public routes

| Route | Page | Purpose |
|---|---|---|
| `/` | Home | Landing page |
| `/menu` | Menu page | Show all food items |
| `/menu/:id` | Food details | Show single food item |
| `/login` | Login | User login |
| `/register` | Register | User registration |

## Protected customer routes

| Route | Page | Purpose |
|---|---|---|
| `/cart` | Cart | View and update cart |
| `/checkout` | Checkout | Place order |
| `/my-orders` | My Orders | View order history |
| `/profile` | Profile | View/update user profile |

## Protected admin routes

| Route | Page | Purpose |
|---|---|---|
| `/admin` | Admin Dashboard | Admin overview |
| `/admin/foods` | Manage Foods | Add/update/delete food |
| `/admin/orders` | Manage Orders | View and update orders |
| `/admin/users` | Manage Users | Optional user management |

## Error routes

| Route | Page | Purpose |
|---|---|---|
| `*` | Not Found | Handle unknown routes |
| `/unauthorized` | Unauthorized | Show access denied |
```

---

# Part 7: API Contract

## What is an API contract?

An API contract defines how frontend and backend communicate.

It should explain:

- Endpoint
- Method
- Access level
- Request body
- Response body
- Error response
- Validation rules

This prevents frontend/backend mismatch.

---

## API contract rules

Each endpoint should include:

```txt
1. Method
2. URL
3. Description
4. Access
5. Request body
6. Success response
7. Error response
8. Validation rules
```

---

## `API_CONTRACT.md` template

Create:

```txt
docs/API_CONTRACT.md
```

Use this structure:

```md
# API Contract

Base URL:

```txt
http://localhost:5000/api
```

## Auth APIs

### Register user

Method:

```txt
POST /auth/register
```

Access:

```txt
Public
```

Request body:

```json
{
  "name": "Sohan",
  "email": "sohan@example.com",
  "password": "password123"
}
```

Success response:

```json
{
  "success": true,
  "message": "Registration successful",
  "data": {
    "user": {
      "id": "userId",
      "name": "Sohan",
      "email": "sohan@example.com",
      "role": "customer"
    },
    "token": "jwt_token"
  }
}
```

Validation:
- Name is required
- Email is required and must be valid
- Password must be at least 6 characters

---

### Login user

Method:

```txt
POST /auth/login
```

Access:

```txt
Public
```

Request body:

```json
{
  "email": "sohan@example.com",
  "password": "password123"
}
```

Success response:

```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "user": {
      "id": "userId",
      "name": "Sohan",
      "email": "sohan@example.com",
      "role": "customer"
    },
    "token": "jwt_token"
  }
}
```

---

## Food APIs

### Get all foods

Method:

```txt
GET /foods
```

Access:

```txt
Public
```

Query params:

```txt
search
category
minPrice
maxPrice
```

Success response:

```json
{
  "success": true,
  "data": [
    {
      "id": "foodId",
      "name": "Chicken Burger",
      "description": "Juicy grilled chicken burger",
      "price": 250,
      "category": "Burger",
      "image": "image-url",
      "isAvailable": true
    }
  ]
}
```

---

### Get single food

Method:

```txt
GET /foods/:id
```

Access:

```txt
Public
```

Success response:

```json
{
  "success": true,
  "data": {
    "id": "foodId",
    "name": "Chicken Burger",
    "description": "Juicy grilled chicken burger",
    "price": 250,
    "category": "Burger",
    "image": "image-url",
    "isAvailable": true
  }
}
```

---

### Create food

Method:

```txt
POST /foods
```

Access:

```txt
Admin only
```

Headers:

```txt
Authorization: Bearer <token>
```

Request body:

```json
{
  "name": "Chicken Burger",
  "description": "Juicy grilled chicken burger",
  "price": 250,
  "category": "Burger",
  "image": "image-url",
  "isAvailable": true
}
```

---

### Update food

Method:

```txt
PATCH /foods/:id
```

Access:

```txt
Admin only
```

---

### Delete food

Method:

```txt
DELETE /foods/:id
```

Access:

```txt
Admin only
```

---

## Order APIs

### Create order

Method:

```txt
POST /orders
```

Access:

```txt
Logged-in customer
```

Request body:

```json
{
  "items": [
    {
      "foodId": "foodId",
      "name": "Chicken Burger",
      "quantity": 2,
      "price": 250
    }
  ],
  "deliveryAddress": "Dhaka, Bangladesh",
  "phone": "01700000000",
  "totalPrice": 500
}
```

Success response:

```json
{
  "success": true,
  "message": "Order placed successfully",
  "data": {
    "id": "orderId",
    "status": "pending",
    "totalPrice": 500
  }
}
```

---

### Get my orders

Method:

```txt
GET /orders/my-orders
```

Access:

```txt
Logged-in customer
```

---

### Get all orders

Method:

```txt
GET /orders
```

Access:

```txt
Admin only
```

---

### Update order status

Method:

```txt
PATCH /orders/:id/status
```

Access:

```txt
Admin only
```

Request body:

```json
{
  "status": "preparing"
}
```

Allowed statuses:

```txt
pending
confirmed
preparing
delivered
cancelled
```

---

## Standard error response

```json
{
  "success": false,
  "message": "Error message",
  "errors": []
}
```
```

---

# Part 8: Database Schema

## Why database schema planning matters

MongoDB is flexible, but that does not mean you should design randomly.

You need to know:

- What collections exist
- What fields are required
- What fields are optional
- What relationships exist
- What should be referenced
- What should be embedded
- What indexes may be useful

---

## `DATABASE_SCHEMA.md` template

Create:

```txt
docs/DATABASE_SCHEMA.md
```

Use this structure:

```md
# Database Schema

## Collections

1. users
2. foods
3. orders

---

## User model

```ts
type User = {
  _id: ObjectId;
  name: string;
  email: string;
  password: string;
  role: "customer" | "admin";
  createdAt: Date;
  updatedAt: Date;
}
```

Validation:
- name required
- email required and unique
- password required and hashed
- role default: customer

Indexes:
- email unique index

---

## Food model

```ts
type Food = {
  _id: ObjectId;
  name: string;
  description: string;
  price: number;
  category: string;
  image: string;
  isAvailable: boolean;
  createdBy: ObjectId;
  createdAt: Date;
  updatedAt: Date;
}
```

Validation:
- name required
- price required and must be positive
- category required
- isAvailable default true

Indexes:
- category index
- name text index optional

---

## Order model

```ts
type Order = {
  _id: ObjectId;
  user: ObjectId;
  items: {
    foodId: ObjectId;
    name: string;
    quantity: number;
    price: number;
  }[];
  deliveryAddress: string;
  phone: string;
  totalPrice: number;
  status: "pending" | "confirmed" | "preparing" | "delivered" | "cancelled";
  createdAt: Date;
  updatedAt: Date;
}
```

Validation:
- user required
- items required and must not be empty
- deliveryAddress required
- phone required
- totalPrice required
- status default: pending

Indexes:
- user index
- status index
- createdAt index

---

## Relationship decisions

| Relationship | Decision | Reason |
|---|---|---|
| Order → User | Reference user ID | User data may change, orders should connect to account |
| Order → Food | Store foodId + snapshot name/price | Price/name at order time should remain stable |
| Food → CreatedBy | Reference admin ID | Track who created item |
```

---

# Part 9: Authorization Matrix

## Why authorization matrix matters

Authentication means:

```txt
Who are you?
```

Authorization means:

```txt
What are you allowed to do?
```

You must define both.

---

## `AUTHORIZATION_MATRIX.md` template

Create:

```txt
docs/AUTHORIZATION_MATRIX.md
```

Use this structure:

```md
# Authorization Matrix

## Roles

| Role | Description |
|---|---|
| Visitor | Not logged in |
| Customer | Logged-in normal user |
| Admin | Logged-in admin user |

## Access rules

| Feature/API | Visitor | Customer | Admin |
|---|---:|---:|---:|
| View home page | ✅ | ✅ | ✅ |
| View food list | ✅ | ✅ | ✅ |
| View food details | ✅ | ✅ | ✅ |
| Add to cart | ✅ local only | ✅ | ✅ |
| Place order | ❌ | ✅ | ✅ |
| View own orders | ❌ | ✅ | ✅ |
| View all orders | ❌ | ❌ | ✅ |
| Create food | ❌ | ❌ | ✅ |
| Update food | ❌ | ❌ | ✅ |
| Delete food | ❌ | ❌ | ✅ |
| Update order status | ❌ | ❌ | ✅ |

## Backend security rules

1. Protected routes must check JWT token.
2. Admin routes must check user role from database.
3. Frontend role checks are not enough.
4. Users can only access their own orders.
5. Admin can access all orders.
6. Never trust role sent from frontend request body.
```

---

# Part 10: Implementation Plan

## Why implementation order matters

Do not build randomly.

Use an order that reduces risk.

Recommended order:

```txt
Planning → Frontend shell → Backend foundation → Auth → Main resource → Orders → Admin → Integration → Testing → Deployment
```

---

## `IMPLEMENTATION_PLAN.md` template

Create:

```txt
docs/IMPLEMENTATION_PLAN.md
```

Use this structure:

```md
# Implementation Plan

## Phase 1: Planning
- Project brief
- PRD
- User stories
- Acceptance criteria
- API contract
- Database schema
- Authorization matrix

## Phase 2: Frontend foundation
- Setup React + Vite + TypeScript
- Setup Tailwind CSS
- Create layout
- Create routes
- Create shared components
- Create mock data

## Phase 3: Frontend pages with mock data
- Home page
- Menu page
- Food details page
- Cart page
- Login/register pages
- My orders page
- Admin dashboard pages

## Phase 4: Backend foundation
- Setup Express + TypeScript
- Setup MongoDB connection
- Setup error middleware
- Setup env config
- Setup health route

## Phase 5: Auth backend
- User model
- Register route
- Login route
- JWT middleware
- Role middleware

## Phase 6: Food backend
- Food model
- Food routes
- Food controller/service
- Admin create/update/delete
- Public list/details

## Phase 7: Order backend
- Order model
- Create order
- My orders
- Admin all orders
- Update status

## Phase 8: Full-stack integration
- API client
- Auth context
- Protected routes
- Replace mock data
- Connect cart/order flow
- Connect admin flow

## Phase 9: Testing and QA
- Backend API tests
- Frontend component tests
- Browser verification
- Bug fixes
- Lighthouse check

## Phase 10: Deployment
- MongoDB Atlas
- Backend deployment
- Frontend deployment
- Env variables
- Production smoke test
- README update
```

---

# Part 11: Task Breakdown

## Why task breakdown matters

Antigravity works best with small tasks.

Instead of:

```txt
Build the backend.
```

Use:

```txt
Create only the User model and validation schema.
```

---

## `TASK_BREAKDOWN.md` template

Create:

```txt
docs/TASK_BREAKDOWN.md
```

Use this structure:

```md
# Task Breakdown

## Planning tasks

- [ ] Create PROJECT_BRIEF.md
- [ ] Create PRD.md
- [ ] Create USER_STORIES.md
- [ ] Create ACCEPTANCE_CRITERIA.md
- [ ] Create FEATURE_SCOPE.md
- [ ] Create PAGE_ROUTE_MAP.md
- [ ] Create API_CONTRACT.md
- [ ] Create DATABASE_SCHEMA.md
- [ ] Create AUTHORIZATION_MATRIX.md
- [ ] Create IMPLEMENTATION_PLAN.md
- [ ] Create RISK_REGISTER.md

## Frontend tasks

- [ ] Setup React + Vite + TypeScript
- [ ] Setup Tailwind CSS
- [ ] Create route structure
- [ ] Create layout components
- [ ] Create Home page
- [ ] Create Menu page
- [ ] Create Food details page
- [ ] Create Cart page
- [ ] Create Auth pages
- [ ] Create My Orders page
- [ ] Create Admin pages

## Backend tasks

- [ ] Setup Express + TypeScript
- [ ] Setup MongoDB connection
- [ ] Setup env config
- [ ] Setup error middleware
- [ ] Create User model
- [ ] Create auth routes
- [ ] Create JWT middleware
- [ ] Create role middleware
- [ ] Create Food model/routes
- [ ] Create Order model/routes

## Integration tasks

- [ ] Create API client
- [ ] Connect auth
- [ ] Connect food list
- [ ] Connect food details
- [ ] Connect cart checkout
- [ ] Connect my orders
- [ ] Connect admin food management
- [ ] Connect admin order status

## Testing tasks

- [ ] Test auth APIs
- [ ] Test food APIs
- [ ] Test order APIs
- [ ] Test protected routes
- [ ] Test admin authorization
- [ ] Test frontend flows
- [ ] Test deployment
```

---

# Part 12: Risk Register

## Why risk register matters

A risk register helps you prepare for predictable problems.

---

## `RISK_REGISTER.md` template

Create:

```txt
docs/RISK_REGISTER.md
```

Use this structure:

```md
# Risk Register

| Risk | Impact | Probability | Prevention | Fix |
|---|---|---|---|---|
| Scope becomes too large | High | High | Define out-of-scope features | Cut nice-to-have features |
| Auth becomes confusing | High | Medium | Plan auth flow early | Simplify roles |
| API mismatch | High | Medium | Create API contract first | Update frontend/backend together |
| MongoDB schema changes late | Medium | Medium | Create schema early | Add migration/manual update notes |
| Deployment env vars missing | High | Medium | Create env checklist | Recheck Vercel/Render variables |
| Antigravity changes unrelated files | Medium | Medium | Use scoped prompts | Ask it to revert/explain changes |
| Styling not matching Figma | Medium | High | Create design system | Do visual QA |
| Student runs out of time | High | High | Build must-have first | Drop nice-to-have features |
```

---

# Antigravity prompts for this module

## Prompt 1: Create all planning docs

```txt
I am doing Module 2: Spec-First Development.

Project idea:
[Write your project idea]

Create these files inside docs/:
1. PROJECT_BRIEF.md
2. PRD.md
3. USER_STORIES.md
4. ACCEPTANCE_CRITERIA.md
5. FEATURE_SCOPE.md
6. PAGE_ROUTE_MAP.md
7. API_CONTRACT.md
8. DATABASE_SCHEMA.md
9. AUTHORIZATION_MATRIX.md
10. IMPLEMENTATION_PLAN.md
11. TASK_BREAKDOWN.md
12. RISK_REGISTER.md

Rules:
- Do not create app code.
- Do not install packages.
- Keep the scope realistic for a junior MERN developer.
- Use React, TypeScript, Tailwind, Express, MongoDB, Mongoose, JWT.
- Include user and admin roles.
- Include must-have, should-have, nice-to-have, and out-of-scope features.
- After creating the files, summarize what each file is for.
```

---

## Prompt 2: Review the planning docs

```txt
Review all files inside docs/.

Check:
1. Is the project scope realistic?
2. Are user roles clear?
3. Are features clear?
4. Are acceptance criteria testable?
5. Are API endpoints consistent?
6. Are database schemas aligned with APIs?
7. Are authorization rules clear?
8. Are tasks small enough for Antigravity?

Do not edit files yet.

Return:
- Strong parts
- Missing parts
- Risky parts
- Recommended fixes
```

---

## Prompt 3: Improve only the API contract

```txt
Read only docs/API_CONTRACT.md and docs/DATABASE_SCHEMA.md.

Improve API_CONTRACT.md.

Rules:
- Do not edit other files.
- Ensure every endpoint has method, route, access, request body, response body, validation, and error cases.
- Ensure endpoint names match the database schema.
- Keep it beginner-friendly.
```

---

## Prompt 4: Convert plan into Antigravity tasks

```txt
Read docs/IMPLEMENTATION_PLAN.md and docs/TASK_BREAKDOWN.md.

Convert the implementation plan into small Antigravity-ready tasks.

Each task should include:
1. Task name
2. Goal
3. Files to create/edit
4. Prompt to use
5. Verification step
6. Risk level

Do not write code.
```

---

# NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 03-module-02-spec-first-development.md
2. PROJECT_BRIEF.md
3. PRD.md
4. USER_STORIES.md
5. ACCEPTANCE_CRITERIA.md
6. API_CONTRACT.md
7. DATABASE_SCHEMA.md
8. AUTHORIZATION_MATRIX.md
9. OpenAPI official specification link
10. MongoDB data modeling docs
11. User story / acceptance criteria resource
```

Then use these prompts.

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for spec-first MERN development.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. What spec-first development is
2. Why planning before coding matters
3. What a PRD is
4. What user stories are
5. What acceptance criteria are
6. What an API contract is
7. What a database schema is
8. How these documents guide Antigravity
9. Common mistakes
10. Practice checklist

Include examples from the sources.
```

---

## NotebookLM Prompt 2: Planning Review

```txt
Review my planning documents.

Check:
1. Project scope
2. User roles
3. Features
4. Acceptance criteria
5. Page routes
6. API endpoints
7. Database schema
8. Authorization matrix
9. Implementation order
10. Risks

Return:
- What is strong
- What is unclear
- What is missing
- What I should fix before coding
```

---

## NotebookLM Prompt 3: Interview Explanation

```txt
Help me explain spec-first development in an interview.

Create:
1. A simple explanation
2. A 30-second answer
3. A 1-minute answer
4. An example from my project
5. Mistakes I avoided by planning first
```

---

# Required video resources

Watch at least two videos.

Search YouTube:

```txt
how to write user stories and acceptance criteria
API contract first development OpenAPI tutorial
MongoDB schema design best practices
MERN project planning before coding
```

Recommended video note format:

```md
# Module 2 Video Learning Notes

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
docs/notebooklm/module-02-video-learning-notes.md
```

---

# Practice Task 1: Create all planning documents

Use Antigravity Prompt 1 and create all 12 planning documents.

Do not write app code yet.

Expected folder:

```txt
docs/
  PROJECT_BRIEF.md
  PRD.md
  USER_STORIES.md
  ACCEPTANCE_CRITERIA.md
  FEATURE_SCOPE.md
  PAGE_ROUTE_MAP.md
  API_CONTRACT.md
  DATABASE_SCHEMA.md
  AUTHORIZATION_MATRIX.md
  IMPLEMENTATION_PLAN.md
  TASK_BREAKDOWN.md
  RISK_REGISTER.md
```

---

# Practice Task 2: Review and improve the scope

Ask Antigravity to review your planning docs.

Then manually improve:

- Scope
- Out-of-scope list
- User roles
- Acceptance criteria
- API consistency
- Implementation order

---

# Practice Task 3: Create task prompts

Create:

```txt
docs/ANTIGRAVITY_TASK_PROMPTS.md
```

It should include task-specific prompts for:

1. Frontend setup
2. Backend setup
3. Auth backend
4. Food/menu backend
5. Order backend
6. Frontend pages
7. API integration
8. Testing
9. Deployment

---

# Practice Task 4: Create Definition of Done

Create:

```txt
docs/DEFINITION_OF_DONE.md
```

Use this structure:

```md
# Definition of Done

A feature is done only when:

- [ ] Requirement is clear
- [ ] Acceptance criteria are met
- [ ] UI is responsive
- [ ] API works
- [ ] Errors are handled
- [ ] Loading state exists
- [ ] Empty state exists if needed
- [ ] Auth/role checks work if needed
- [ ] Browser verification completed
- [ ] No console errors
- [ ] Code committed to GitHub
- [ ] Documentation updated
```

---

# Practice Task 5: Create implementation sequence

Create:

```txt
docs/BUILD_SEQUENCE.md
```

Use this structure:

```md
# Build Sequence

## Step 1
Frontend setup

## Step 2
Backend setup

## Step 3
Database connection

## Step 4
Auth backend

## Step 5
Frontend auth pages

## Step 6
Main resource backend

## Step 7
Frontend main pages with mock data

## Step 8
API integration

## Step 9
Admin dashboard

## Step 10
Testing

## Step 11
Deployment
```

---

# Required deliverables for this module

Submit:

```txt
1. PROJECT_BRIEF.md
2. PRD.md
3. USER_STORIES.md
4. ACCEPTANCE_CRITERIA.md
5. FEATURE_SCOPE.md
6. PAGE_ROUTE_MAP.md
7. API_CONTRACT.md
8. DATABASE_SCHEMA.md
9. AUTHORIZATION_MATRIX.md
10. IMPLEMENTATION_PLAN.md
11. TASK_BREAKDOWN.md
12. RISK_REGISTER.md
13. ANTIGRAVITY_TASK_PROMPTS.md
14. DEFINITION_OF_DONE.md
15. BUILD_SEQUENCE.md
16. NotebookLM Study Guide screenshot
17. NotebookLM planning review screenshot
18. Video learning notes
19. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/03-module-02-spec-first-development-reflection.md
```

Use this format:

```md
# Reflection: Module 2 - Spec-First Development

## Project idea I selected
-

## Planning documents I created
-

## What I learned about PRD
-

## What I learned about user stories
-

## What I learned about acceptance criteria
-

## What I learned about API contracts
-

## What I learned about database schema planning
-

## What Antigravity helped with
-

## What I had to correct manually
-

## What I will do before coding in the next module
-
```

---

# Quiz

## Multiple choice

**1. What is spec-first development?**

A. Writing code before planning  
B. Defining requirements and structure before coding  
C. Deploying first  
D. Designing only the logo  

Correct answer: **B**

---

**2. What does PRD stand for?**

A. Product Requirements Document  
B. Project React Design  
C. Public Route Definition  
D. Primary Runtime Database  

Correct answer: **A**

---

**3. What is the main purpose of user stories?**

A. To describe features from the user's perspective  
B. To store passwords  
C. To replace backend APIs  
D. To create CSS classes  

Correct answer: **A**

---

**4. Which format is commonly used for user stories?**

A. If/else/code  
B. As a [user], I want [goal], so that [benefit]  
C. Try/catch/finally  
D. Import/export/from  

Correct answer: **B**

---

**5. What do acceptance criteria define?**

A. When a feature is complete and acceptable  
B. Which font to use only  
C. Which laptop to buy  
D. Which repo to delete  

Correct answer: **A**

---

**6. What should an API contract include?**

A. Method, URL, access, request, response, validation, and errors  
B. Only app colors  
C. Only GitHub username  
D. Only screenshots  

Correct answer: **A**

---

**7. Why create `DATABASE_SCHEMA.md` before coding?**

A. To plan collections, fields, relationships, validation, and indexes  
B. To skip backend  
C. To replace MongoDB Atlas  
D. To store secrets  

Correct answer: **A**

---

**8. What should be out of scope for a first junior MERN version?**

A. Must-have CRUD  
B. Basic authentication  
C. Payment gateway and real-time tracking unless required  
D. README  

Correct answer: **C**

---

**9. What is the purpose of an authorization matrix?**

A. Define who can access what  
B. Design only the homepage  
C. Store database password  
D. Replace testing  

Correct answer: **A**

---

**10. Why does task breakdown help Antigravity?**

A. It converts big work into small, clear tasks  
B. It hides requirements  
C. It removes need for review  
D. It deploys automatically  

Correct answer: **A**

---

## Short-answer questions

1. What is spec-first development?
2. Why should you create a PRD before coding?
3. Write one user story for your project.
4. Write one acceptance criterion for that story.
5. What is an API contract?
6. What should be included in a database schema plan?
7. What is the difference between authentication and authorization?
8. Why should some features be marked out of scope?
9. How does task breakdown save Antigravity quota?
10. What planning document will you use most before coding?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Project brief | Clear project summary and target users |
| PRD | Goals, non-goals, roles, features, requirements included |
| User stories | User-focused and testable |
| Acceptance criteria | Clear Given/When/Then style |
| Feature scope | Must-have, should-have, nice-to-have, out-of-scope defined |
| Page route map | Public, protected, admin, error routes planned |
| API contract | Endpoints include method, access, request, response, validation |
| Database schema | Collections, fields, validation, relationships planned |
| Authorization matrix | Role-based access clearly defined |
| Implementation plan | Build order is realistic |
| Task breakdown | Tasks are small enough for Antigravity |
| Risk register | Major risks identified |
| NotebookLM evidence | Study guide and review screenshots submitted |
| Reflection | Student explains planning decisions clearly |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can turn a vague project idea into a clear set of planning documents, including PRD, user stories, acceptance criteria, feature scope, page route map, API contract, database schema, authorization matrix, implementation plan, task breakdown, and risk register before asking Antigravity to write code.
```

After completing this file, continue to:

```txt
04-module-03-codebase-architecture-thinking.md
```
