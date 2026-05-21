# Module 9: Testing, Browser Verification and QA — Prove the App Works Before Deployment

**File Name:** `11-module-09-testing-browser-verification-qa.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 6–9 hours  
**Recommended After:** Module 8: Full-Stack Integration  
**Main Goal:** Learn how to verify a full-stack MERN app with manual QA, browser checks, API tests, component tests, E2E tests, accessibility/performance checks, bug reports, and Antigravity-assisted debugging.

---

## Module purpose

In Module 8, you connected the frontend with the backend.

Now you must prove that the app works.

A project is not complete just because:

```txt
The code runs.
The homepage opens.
Antigravity says it is done.
```

A real project needs verification.

This module teaches you how to test and verify your MERN app before deployment.

You will learn how to check:

- Frontend routes
- Backend APIs
- Authentication
- Authorization
- Customer flows
- Admin flows
- Form validation
- Loading states
- Empty states
- Error states
- Mobile responsiveness
- Console errors
- Network errors
- CORS errors
- API response issues
- Accessibility basics
- Performance basics
- End-to-end flows
- Bug documentation
- Regression checks

The goal is simple:

```txt
Do not ship unverified AI-generated code.
```

---

## Why this module matters

AI-assisted development can produce code quickly.

But speed without verification creates fragile projects.

Common AI-generated project problems:

- UI looks fine but buttons do not work.
- Backend route exists but returns wrong response shape.
- Login works once but breaks after refresh.
- Admin pages are visible to normal users.
- Mobile layout breaks.
- Forms accept invalid data.
- Errors are not shown to users.
- API errors appear only in console.
- Checkout works with mock data but fails with backend.
- Deployment fails because env variables are missing.
- README claims features that do not actually work.

Testing prevents these problems.

---

## Testing mindset

Testing is not only writing automated test files.

Testing means:

```txt
Checking whether the system behaves correctly under expected and unexpected conditions.
```

In this course, testing has five layers:

| Layer | Purpose |
|---|---|
| Manual browser QA | Confirm the app works like a user would use it |
| API testing | Confirm backend endpoints work correctly |
| Component testing | Confirm important UI components behave correctly |
| E2E testing | Confirm complete user/admin flows work in the browser |
| Quality audits | Check accessibility, performance, SEO, and best practices |

You do not need enterprise-level test coverage.

But you must verify the critical flows.

---

## Minimum testing expectation

For this bootcamp, every student must complete:

```txt
1. Manual browser QA
2. API test report
3. Auth/authorization tests
4. Full-stack flow tests
5. Mobile responsiveness checks
6. Console/network error checks
7. Bug log
8. Fix verification report
```

Automated tests are strongly recommended, but manual QA is mandatory.

---

## Recommended testing stack

For this project, use:

```txt
Manual browser testing
Chrome DevTools
Postman / Thunder Client / Insomnia / Hoppscotch
Vitest
React Testing Library
Playwright
Lighthouse
```

Recommended usage:

| Tool | Use |
|---|---|
| Chrome DevTools | Console, Network, responsive view, localStorage |
| Postman/Thunder Client | API testing |
| Vitest | Unit/component test runner |
| React Testing Library | Test React components like users interact with them |
| Playwright | End-to-end browser flow testing |
| Lighthouse | Performance/accessibility/SEO/best practices check |
| Antigravity Browser Agent | Assisted browser verification and bug investigation |

---

## Testing principle for junior developers

Use this order:

```txt
Manual QA first
→ API testing
→ Component testing
→ E2E testing
→ Lighthouse/accessibility checks
→ Bug fixes
→ Regression test
```

Do not start with complicated automated tests if basic flows are broken.

---

# Part 1: Create testing documentation files

Before testing, create these files:

```txt
docs/TESTING_STRATEGY.md
docs/QA_CHECKLIST.md
docs/API_TEST_REPORT.md
docs/BROWSER_TEST_REPORT.md
docs/AUTHORIZATION_TEST_REPORT.md
docs/BUG_REPORT_TEMPLATE.md
docs/BUG_LOG.md
docs/REGRESSION_TEST_CHECKLIST.md
docs/LIGHTHOUSE_REPORT.md
docs/FINAL_QA_SIGNOFF.md
```

These files make your QA process visible and professional.

---

## `TESTING_STRATEGY.md`

Create:

```txt
docs/TESTING_STRATEGY.md
```

Template:

```md
# Testing Strategy

## Goal
Verify that the MERN application works correctly before deployment.

## Testing layers

| Layer | Tool | Purpose |
|---|---|---|
| Manual QA | Browser + DevTools | Verify main flows manually |
| API testing | Postman/Thunder Client | Verify backend endpoints |
| Component testing | Vitest + React Testing Library | Verify important UI components |
| E2E testing | Playwright | Verify complete browser flows |
| Quality audit | Lighthouse | Check performance/accessibility/SEO/best practices |

## Critical flows
1. Register
2. Login
3. Browse food/items/resources
4. Add to cart or select resource
5. Checkout/order/booking/submission
6. View own history
7. Admin create/update/delete resource
8. Admin manage orders/status
9. Unauthorized user blocked from admin routes
10. Logout

## Testing rules
- Test one flow at a time.
- Record bugs immediately.
- Fix critical bugs before adding features.
- Retest after every fix.
- Do not claim a feature works without evidence.
```

---

## `QA_CHECKLIST.md`

Create:

```txt
docs/QA_CHECKLIST.md
```

Template:

```md
# QA Checklist

## Setup
- [ ] Frontend runs locally
- [ ] Backend runs locally
- [ ] MongoDB connection works
- [ ] Frontend env variables are set
- [ ] Backend env variables are set
- [ ] CORS works
- [ ] No secrets are committed

## Browser
- [ ] Home page loads
- [ ] Menu/resource page loads
- [ ] Details page loads
- [ ] Login page loads
- [ ] Register page loads
- [ ] Cart/checkout or main user flow works
- [ ] My orders/history page works
- [ ] Admin dashboard loads
- [ ] 404 page works
- [ ] Unauthorized page works

## Auth
- [ ] Register works
- [ ] Login works
- [ ] Logout works
- [ ] Refresh keeps/clears expected auth state
- [ ] Invalid credentials show error
- [ ] Protected route blocks visitor
- [ ] Admin route blocks customer

## UI states
- [ ] Loading states appear
- [ ] Empty states appear
- [ ] Error states appear
- [ ] Success feedback appears
- [ ] Form validation appears

## Mobile
- [ ] Navbar works on mobile
- [ ] Cards stack correctly
- [ ] Forms fit screen
- [ ] Tables are usable or scrollable
- [ ] No horizontal overflow

## Technical
- [ ] No major console errors
- [ ] No failed network requests in normal flow
- [ ] API errors show readable messages
- [ ] Build passes
- [ ] README matches implemented features
```

---

## `BUG_REPORT_TEMPLATE.md`

Create:

```txt
docs/BUG_REPORT_TEMPLATE.md
```

Template:

```md
# Bug Report Template

## Bug title
-

## Severity
Critical / High / Medium / Low

## Area
Frontend / Backend / Full-stack / Deployment / UI / Auth / Admin / Mobile

## Environment
Local / Deployed

## Steps to reproduce
1.
2.
3.

## Expected result
-

## Actual result
-

## Screenshot or evidence
-

## Console error
-

## Network error
-

## Suspected cause
-

## Fix applied
-

## Retest result
Pass / Fail

## Status
Open / Fixed / Won't fix
```

---

## `BUG_LOG.md`

Create:

```txt
docs/BUG_LOG.md
```

Template:

```md
# Bug Log

| ID | Bug | Severity | Area | Cause | Fix | Status |
|---|---|---|---|---|---|---|
| BUG-001 | Login error not shown | Medium | Frontend/Auth | Error not rendered | Added ErrorState | Fixed |
| BUG-002 | Customer can open admin link | High | Authorization | Route guard missing role check | Updated AdminRoute | Fixed |
| BUG-003 | Price validation fails | High | Full-stack | Input sent string | Converted price to number | Fixed |
```

---

## `FINAL_QA_SIGNOFF.md`

Create:

```txt
docs/FINAL_QA_SIGNOFF.md
```

Template:

```md
# Final QA Signoff

## Project name
-

## QA date
-

## Tested by
-

## Local URLs
Frontend:
Backend:

## Deployed URLs
Frontend:
Backend:

## Summary
-

## Critical flows tested
- [ ] Register
- [ ] Login
- [ ] Browse resource
- [ ] Details page
- [ ] Cart/checkout/order flow
- [ ] User history
- [ ] Admin resource management
- [ ] Admin status management
- [ ] Authorization failure
- [ ] Logout

## Open bugs
-

## Known limitations
-

## Final verdict
Pass / Conditional Pass / Fail

## Notes before deployment
-
```

---

# Part 2: Manual browser QA

Manual browser QA means using the app like a real user.

Use:

```txt
Chrome
Chrome DevTools
Responsive device toolbar
Console tab
Network tab
Application tab
```

---

## Browser QA checklist

Create:

```txt
docs/BROWSER_TEST_REPORT.md
```

Template:

```md
# Browser Test Report

## Environment
Local / Deployed

Frontend URL:
Backend URL:

## Browser
Chrome / Firefox / Edge

## Test account

Customer:
Admin:

## Page tests

| Page/Route | Expected | Result | Notes |
|---|---|---|---|
| / | Home loads | Pass/Fail |  |
| /menu | Items load | Pass/Fail |  |
| /menu/:id | Details load | Pass/Fail |  |
| /login | Login page loads | Pass/Fail |  |
| /register | Register page loads | Pass/Fail |  |
| /cart | Cart works | Pass/Fail |  |
| /checkout | Checkout works | Pass/Fail |  |
| /my-orders | User orders show | Pass/Fail |  |
| /admin | Admin dashboard loads | Pass/Fail |  |
| /admin/foods | Admin food management works | Pass/Fail |  |
| /admin/orders | Admin order management works | Pass/Fail |  |
| /unauthorized | Unauthorized page loads | Pass/Fail |  |
| random route | 404 page loads | Pass/Fail |  |

## Console errors
-

## Network errors
-

## Mobile issues
-

## Bugs created
-

## Final verdict
Pass / Conditional pass / Fail
```

---

## How to inspect browser issues

### Console tab

Check for:

```txt
TypeError
ReferenceError
Cannot read properties of undefined
Failed to fetch
Warning about keys
React Router errors
```

### Network tab

Check for:

```txt
401 Unauthorized
403 Forbidden
404 Not Found
500 Server Error
CORS error
Wrong API URL
Missing request body
Invalid response
```

### Application tab

Check:

```txt
localStorage auth token
cart data if stored
cookies if used
```

### Responsive toolbar

Check:

```txt
Mobile width: 375px
Tablet width: 768px
Desktop width: 1440px
```

---

## Manual QA flows

### Flow 1: Register

Steps:

```txt
1. Open /register
2. Enter name, email, password
3. Submit
4. Confirm success or redirect
5. Check localStorage/token if applicable
6. Check navbar user state
```

Expected:

```txt
New user account created and user is logged in or redirected correctly.
```

---

### Flow 2: Login

Steps:

```txt
1. Open /login
2. Enter valid email/password
3. Submit
4. Confirm redirect
5. Refresh page
6. Confirm auth persistence works as designed
```

Expected:

```txt
User stays logged in after refresh if localStorage auth persistence is implemented.
```

---

### Flow 3: Invalid login

Steps:

```txt
1. Open /login
2. Enter wrong password
3. Submit
```

Expected:

```txt
Readable error message appears.
App does not crash.
```

---

### Flow 4: Browse items

Steps:

```txt
1. Open /menu
2. Confirm list loads from backend
3. Use search/filter if available
4. Open details page
```

Expected:

```txt
Items load correctly and details page works.
```

---

### Flow 5: Cart and checkout

Steps:

```txt
1. Add item to cart
2. Open cart
3. Update quantity
4. Remove item
5. Add again
6. Go to checkout
7. Enter address/phone
8. Place order
```

Expected:

```txt
Order is created and cart is cleared or success message appears.
```

---

### Flow 6: My orders

Steps:

```txt
1. Login as customer
2. Place order
3. Open /my-orders
```

Expected:

```txt
Only current user's orders appear.
```

---

### Flow 7: Admin food management

Steps:

```txt
1. Login as admin
2. Open /admin/foods
3. Create food
4. Confirm it appears in menu
5. Update food
6. Delete food if needed
```

Expected:

```txt
Admin can manage foods.
```

---

### Flow 8: Admin order management

Steps:

```txt
1. Login as admin
2. Open /admin/orders
3. View all orders
4. Change order status
5. Confirm status updates
```

Expected:

```txt
Admin can update order status.
```

---

### Flow 9: Authorization failure

Steps:

```txt
1. Login as customer
2. Try to open /admin
3. Try admin API in Postman with customer token
```

Expected:

```txt
Frontend blocks route.
Backend returns 403.
```

---

# Part 3: API testing

API testing verifies the backend independently.

Use:

```txt
Postman
Thunder Client
Insomnia
Hoppscotch
```

Create:

```txt
docs/API_TEST_REPORT.md
```

Template:

```md
# API Test Report

## Tool used
Postman / Thunder Client / Insomnia / Hoppscotch

## Base URL
http://localhost:5000

## Auth tokens
Customer token: Stored privately, not pasted publicly
Admin token: Stored privately, not pasted publicly

## Test results

| API | Method | Access | Expected | Result | Notes |
|---|---|---|---|---|---|
| /health | GET | Public | 200 | Pass/Fail |  |
| /api/auth/register | POST | Public | 201 | Pass/Fail |  |
| /api/auth/login | POST | Public | 200 | Pass/Fail |  |
| /api/foods | GET | Public | 200 | Pass/Fail |  |
| /api/foods/:id | GET | Public | 200/404 | Pass/Fail |  |
| /api/foods | POST | Admin | 201 | Pass/Fail |  |
| /api/foods/:id | PATCH | Admin | 200 | Pass/Fail |  |
| /api/foods/:id | DELETE | Admin | 200 | Pass/Fail |  |
| /api/orders | POST | Customer | 201 | Pass/Fail |  |
| /api/orders/my-orders | GET | Customer | 200 | Pass/Fail |  |
| /api/orders | GET | Admin | 200 | Pass/Fail |  |
| /api/orders/:id/status | PATCH | Admin | 200 | Pass/Fail |  |

## Negative tests

| Test | Expected | Result |
|---|---|---|
| Login wrong password | 401 | Pass/Fail |
| Create food without token | 401 | Pass/Fail |
| Create food as customer | 403 | Pass/Fail |
| Invalid order body | 400 | Pass/Fail |
| Unknown route | 404 | Pass/Fail |

## Bugs found
-

## Final verdict
Pass / Conditional pass / Fail
```

---

## API testing rules

Do not only test happy paths.

Test:

```txt
Valid request
Invalid request
Missing token
Invalid token
Wrong role
Missing required field
Invalid ID
Duplicate email
Unknown route
```

---

# Part 4: Auth and authorization testing

Authentication and authorization bugs are serious.

Create:

```txt
docs/AUTHORIZATION_TEST_REPORT.md
```

Template:

```md
# Authorization Test Report

## Roles tested
- Visitor
- Customer
- Admin

## Frontend route tests

| Route | Visitor | Customer | Admin |
|---|---|---|---|
| /menu | Allow | Allow | Allow |
| /checkout | Redirect login | Allow | Allow |
| /my-orders | Redirect login | Allow | Allow |
| /admin | Redirect login | Block/Unauthorized | Allow |
| /admin/foods | Redirect login | Block/Unauthorized | Allow |
| /admin/orders | Redirect login | Block/Unauthorized | Allow |

## Backend API tests

| API | Visitor | Customer | Admin |
|---|---|---|---|
| GET /api/foods | Allow | Allow | Allow |
| POST /api/foods | 401 | 403 | Allow |
| PATCH /api/foods/:id | 401 | 403 | Allow |
| DELETE /api/foods/:id | 401 | 403 | Allow |
| POST /api/orders | 401 | Allow | Allow |
| GET /api/orders/my-orders | 401 | Allow | Allow |
| GET /api/orders | 401 | 403 | Allow |
| PATCH /api/orders/:id/status | 401 | 403 | Allow |

## Issues found
-

## Final verdict
Pass / Conditional pass / Fail
```

---

## Important security rule

Frontend route protection is not enough.

Always test backend directly with Postman/Thunder Client.

If a customer can call admin API directly and get data, the app is insecure.

---

# Part 5: Component testing with Vitest + React Testing Library

Component tests verify important UI behavior.

You do not need to test everything.

Test critical reusable components and pages.

Recommended examples:

```txt
Button renders and handles click
Input shows error
EmptyState displays message
FoodCard shows food and Add to Cart button
LoginPage shows validation or error
Cart item quantity updates
```

---

## Install testing dependencies

From `client/`:

```bash
npm install -D vitest jsdom @testing-library/react @testing-library/jest-dom @testing-library/user-event
```

Add scripts to `client/package.json`:

```json
{
  "scripts": {
    "test": "vitest",
    "test:ui": "vitest --ui",
    "test:run": "vitest run"
  }
}
```

---

## Configure Vitest

If your Vite config supports Vitest config directly, update:

```txt
client/vite.config.ts
```

Example:

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
  test: {
    environment: "jsdom",
    setupFiles: "./src/test/setup.ts",
    globals: true,
  },
});
```

If TypeScript complains about `test` in Vite config, install the right types or create a separate `vitest.config.ts`.

Create:

```txt
client/src/test/setup.ts
```

```ts
import "@testing-library/jest-dom";
```

---

## Example: Button test

Create:

```txt
client/src/components/common/Button.test.tsx
```

```tsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { describe, expect, it, vi } from "vitest";
import { Button } from "./Button";

describe("Button", () => {
  it("renders children and handles click", async () => {
    const user = userEvent.setup();
    const onClick = vi.fn();

    render(<Button onClick={onClick}>Save</Button>);

    await user.click(screen.getByRole("button", { name: /save/i }));

    expect(onClick).toHaveBeenCalledTimes(1);
  });
});
```

---

## Example: EmptyState test

Create:

```txt
client/src/components/states/EmptyState.test.tsx
```

```tsx
import { render, screen } from "@testing-library/react";
import { describe, expect, it } from "vitest";
import { EmptyState } from "./EmptyState";

describe("EmptyState", () => {
  it("shows title and message", () => {
    render(
      <EmptyState
        title="No items found"
        message="Try changing your filters."
      />
    );

    expect(screen.getByText(/no items found/i)).toBeInTheDocument();
    expect(screen.getByText(/try changing your filters/i)).toBeInTheDocument();
  });
});
```

---

## Component testing rule

Testing Library’s philosophy is:

```txt
Test the app the way users interact with it.
```

Prefer:

```ts
screen.getByRole("button", { name: /login/i })
```

Avoid:

```ts
container.querySelector(".btn-primary")
```

User-facing tests are more useful and less brittle.

---

# Part 6: End-to-end testing with Playwright

E2E tests verify complete flows in a real browser.

Playwright is useful for:

- Login flow
- Browse food flow
- Checkout/order flow
- Admin management flow
- Authorization flow

---

## Install Playwright

From project root or `client/` depending on your setup:

```bash
npm init playwright@latest
```

Recommended:

```txt
TypeScript: yes
Tests folder: tests
GitHub Actions: optional
Install browsers: yes
```

If setting up inside `client/`, run from `client/`.

---

## Basic Playwright test

Create:

```txt
client/tests/home.spec.ts
```

Example:

```ts
import { test, expect } from "@playwright/test";

test("home page loads", async ({ page }) => {
  await page.goto("/");

  await expect(page.getByRole("heading", { name: /localbites/i })).toBeVisible();
});
```

Update:

```txt
client/playwright.config.ts
```

Example local config:

```ts
import { defineConfig, devices } from "@playwright/test";

export default defineConfig({
  testDir: "./tests",
  use: {
    baseURL: "http://localhost:5173",
    trace: "on-first-retry",
  },
  projects: [
    {
      name: "chromium",
      use: { ...devices["Desktop Chrome"] },
    },
  ],
  webServer: {
    command: "npm run dev",
    url: "http://localhost:5173",
    reuseExistingServer: true,
  },
});
```

Run:

```bash
npx playwright test
```

Open report:

```bash
npx playwright show-report
```

---

## E2E test examples

### Login page loads

```ts
import { test, expect } from "@playwright/test";

test("login page loads", async ({ page }) => {
  await page.goto("/login");

  await expect(page.getByRole("heading", { name: /login/i })).toBeVisible();
  await expect(page.getByLabel(/email/i)).toBeVisible();
  await expect(page.getByLabel(/password/i)).toBeVisible();
});
```

---

### Menu page loads items

```ts
import { test, expect } from "@playwright/test";

test("menu page shows food items", async ({ page }) => {
  await page.goto("/menu");

  await expect(page.getByRole("heading", { name: /menu/i })).toBeVisible();
  await expect(page.getByText(/burger|pizza|rice/i)).toBeVisible();
});
```

---

### Unauthorized admin route blocks customer

```ts
import { test, expect } from "@playwright/test";

test("visitor cannot access admin page", async ({ page }) => {
  await page.goto("/admin");

  await expect(page).toHaveURL(/login|unauthorized/);
});
```

---

## E2E test warning

E2E tests are powerful but require stable test data.

For beginner projects, first complete manual QA.

Then automate the most important flows.

Recommended first E2E tests:

```txt
1. Home page loads
2. Menu page loads
3. Login page loads
4. Protected route redirects visitor
5. Unknown route shows 404
```

Advanced E2E tests:

```txt
1. Register and login
2. Create order
3. Admin updates order
4. Customer denied admin access
```

---

# Part 7: Antigravity browser verification

Antigravity can help with browser-based verification if browser tools are available.

Use it carefully.

Do not ask:

```txt
Check everything.
```

Ask:

```txt
Verify these exact routes and flows. Do not edit files yet.
```

---

## Browser verification prompt

```txt
Use browser verification.

Local URLs:
Frontend: http://localhost:5173
Backend: http://localhost:5000

Verify these flows:
1. Home page loads
2. Menu page loads
3. Food details works
4. Login page works
5. Protected route redirects visitor
6. Admin route blocks customer
7. Cart/checkout flow works
8. My orders page works

Check:
- Console errors
- Network errors
- Layout issues
- Mobile responsiveness
- Loading/empty/error states

Do not edit files yet.

Create docs/BROWSER_TEST_REPORT.md and docs/BUG_LOG.md updates.
```

---

## Antigravity bug investigation prompt

```txt
Investigate this bug.

Bug:
[Paste bug title]

Evidence:
[Paste screenshot/console/network error]

Files likely involved:
[List files]

Rules:
- Explain likely cause first.
- Do not edit files yet.
- Suggest smallest safe fix.
- Mention how to retest after fixing.
```

---

## Antigravity fix prompt

```txt
Fix only this bug:

[Bug title]

Allowed files:
[List exact files]

Rules:
- Do not add new features.
- Do not rewrite unrelated code.
- Do not remove validation/auth/security.
- After fixing, update docs/BUG_LOG.md with cause, fix, and retest result.
```

---

# Part 8: Lighthouse and quality audit

Lighthouse helps check:

- Performance
- Accessibility
- Best Practices
- SEO

Run Lighthouse in Chrome DevTools:

```txt
1. Open the app page
2. Open DevTools
3. Go to Lighthouse panel
4. Select categories
5. Generate report
6. Save screenshot or PDF
```

Create:

```txt
docs/LIGHTHOUSE_REPORT.md
```

Template:

```md
# Lighthouse Report

## Page tested
-

## Environment
Local / Deployed

## Scores

| Category | Score |
|---|---:|
| Performance |  |
| Accessibility |  |
| Best Practices |  |
| SEO |  |

## Major issues
-

## Fixes applied
-

## Remaining limitations
-

## Final note
-
```

---

## Lighthouse expectations for this bootcamp

Minimum:

```txt
Run Lighthouse on Home page and one important app page.
```

Recommended:

```txt
Run Lighthouse on:
1. Home
2. Menu
3. Login
4. Admin dashboard
```

Do not obsess over perfect 100 scores.

Focus on major issues:

- Missing alt text
- Low contrast
- Huge images
- Buttons without accessible labels
- Layout shift
- Console errors
- Poor mobile performance

---

# Part 9: Accessibility basics

Accessibility is not optional.

Check:

```txt
1. Buttons have visible text or aria-label
2. Inputs have labels
3. Links are understandable
4. Color contrast is readable
5. Keyboard navigation works
6. Focus outline is visible
7. Images have alt text
8. Error messages are visible
9. Form fields show validation messages
10. Page headings are meaningful
```

Create:

```txt
docs/ACCESSIBILITY_CHECKLIST.md
```

Template:

```md
# Accessibility Checklist

## Forms
- [ ] Every input has a label
- [ ] Error messages are visible
- [ ] Required fields are clear

## Buttons and links
- [ ] Buttons have readable names
- [ ] Icon-only buttons have aria-label
- [ ] Links describe destination

## Keyboard
- [ ] User can tab through page
- [ ] Focus is visible
- [ ] Modal/dropdown does not trap user incorrectly

## Images
- [ ] Informative images have alt text
- [ ] Decorative images use empty alt if appropriate

## Layout
- [ ] Text contrast is readable
- [ ] Mobile layout is usable
- [ ] No important content hidden off-screen

## Result
Pass / Conditional pass / Fail
```

---

# Part 10: Regression testing

Regression testing means:

```txt
After fixing a bug, check that old working features still work.
```

Example:

If you fix checkout, retest:

```txt
1. Add to cart
2. Update quantity
3. Checkout
4. My orders
5. Admin orders
```

Create:

```txt
docs/REGRESSION_TEST_CHECKLIST.md
```

Template:

```md
# Regression Test Checklist

## After auth fix
- [ ] Register
- [ ] Login
- [ ] Logout
- [ ] Refresh page
- [ ] Protected route
- [ ] Admin route

## After food API fix
- [ ] Menu page
- [ ] Food details
- [ ] Add to cart
- [ ] Admin food list
- [ ] Admin create/update/delete

## After order fix
- [ ] Checkout
- [ ] My orders
- [ ] Admin orders
- [ ] Status update

## After UI fix
- [ ] Desktop layout
- [ ] Mobile layout
- [ ] Console errors
- [ ] Main buttons still work

## After deployment/env fix
- [ ] Frontend live URL
- [ ] Backend live URL
- [ ] CORS
- [ ] Login
- [ ] Main API calls
```

---

# Part 11: Test data plan

Testing needs predictable data.

Create:

```txt
docs/TEST_DATA_PLAN.md
```

Template:

```md
# Test Data Plan

## Test users

### Customer
Email:
Password:

### Admin
Email:
Password:

## Test foods/items

| Name | Category | Price | Purpose |
|---|---|---:|---|
| Classic Burger | Burger | 250 | Normal order test |
| Cheese Pizza | Pizza | 520 | Details page test |
| Test Delete Item | Burger | 100 | Delete test |

## Test order scenarios

| Scenario | Purpose |
|---|---|
| Single item order | Basic checkout |
| Multiple item order | Cart total check |
| Empty cart checkout | Empty/protection check |
| Invalid phone/address | Validation check |
| Admin status update | Admin flow check |

## Cleanup plan
- Delete test-only food items after testing.
- Keep one or two sample items for demo.
- Do not use real customer data.
```

---

# Part 12: Common bugs and fixes

## Bug 1: Page crashes with undefined data

Symptom:

```txt
Cannot read properties of undefined
```

Cause:

```txt
Data is loading or API response shape changed.
```

Fix:

```txt
Add loading state.
Add optional chaining carefully.
Normalize response shape.
```

---

## Bug 2: Button does nothing

Cause:

```txt
onClick not connected
disabled state always true
form submit prevented incorrectly
button type missing
```

Fix:

```txt
Check event handler.
Check button type.
Check console.
Check state conditions.
```

---

## Bug 3: Form submits but API fails

Cause:

```txt
Wrong payload shape
String instead of number
Missing token
Wrong endpoint
```

Fix:

```txt
Compare payload with API_CONTRACT.md.
Check Network tab request body.
```

---

## Bug 4: Admin page visible to customer

Cause:

```txt
Frontend route guard missing role check
Navbar shows admin link incorrectly
Backend route not protected
```

Fix:

```txt
Fix AdminRoute.
Hide admin link for customer.
Test backend with customer token.
```

---

## Bug 5: Mobile layout horizontal scroll

Cause:

```txt
Fixed width element
Large table
Long text
Image too wide
```

Fix:

```txt
Use max-w-full.
Use overflow-x-auto for tables.
Use responsive grid.
```

---

## Bug 6: E2E tests flaky

Cause:

```txt
Hard waits
Unstable selectors
Async loading not handled
```

Fix:

```txt
Use Playwright locators.
Use web-first assertions.
Avoid arbitrary timeouts.
```

---

# Part 13: Antigravity prompts for this module

## Prompt 1: Create testing docs

```txt
I am doing Module 9: Testing, Browser Verification and QA.

Create these docs:
1. docs/TESTING_STRATEGY.md
2. docs/QA_CHECKLIST.md
3. docs/API_TEST_REPORT.md
4. docs/BROWSER_TEST_REPORT.md
5. docs/AUTHORIZATION_TEST_REPORT.md
6. docs/BUG_REPORT_TEMPLATE.md
7. docs/BUG_LOG.md
8. docs/REGRESSION_TEST_CHECKLIST.md
9. docs/LIGHTHOUSE_REPORT.md
10. docs/FINAL_QA_SIGNOFF.md
11. docs/ACCESSIBILITY_CHECKLIST.md
12. docs/TEST_DATA_PLAN.md

Rules:
- Do not change app code yet.
- Keep the docs practical for a junior MERN developer.
- Include manual browser QA, API testing, component testing, E2E testing, accessibility, and regression testing.
```

---

## Prompt 2: Manual browser QA

```txt
Use browser verification.

Frontend URL:
http://localhost:5173

Backend URL:
http://localhost:5000

Test these flows:
1. Register
2. Login
3. Invalid login
4. Browse menu/resources
5. Details page
6. Add to cart
7. Checkout/order
8. My orders/history
9. Admin food/resource management
10. Admin order/status management
11. Customer blocked from admin
12. Unknown route shows 404

Check:
- Console errors
- Network errors
- Loading states
- Empty states
- Error states
- Mobile layout

Do not edit files yet.

Update:
- docs/BROWSER_TEST_REPORT.md
- docs/BUG_LOG.md
```

---

## Prompt 3: API test checklist

```txt
Create a step-by-step API testing checklist based on docs/API_CONTRACT.md.

Include:
1. Happy path tests
2. Negative tests
3. Auth tests
4. Admin role tests
5. Invalid data tests
6. Missing token tests
7. Expected status codes
8. Expected response shape

Save/update docs/API_TEST_REPORT.md.

Do not edit backend code.
```

---

## Prompt 4: Setup Vitest tests

```txt
Set up Vitest and React Testing Library for the frontend.

Rules:
- Work only inside client/.
- Add test scripts.
- Add test setup file.
- Create example tests for Button and EmptyState.
- Do not rewrite app code.
- Explain how to run tests.
```

---

## Prompt 5: Setup Playwright tests

```txt
Set up Playwright for E2E tests.

Rules:
- Work only inside client/ unless project root is more appropriate.
- Add Playwright config.
- Add tests for:
  1. Home page loads
  2. Login page loads
  3. Menu page loads
  4. Protected route redirects visitor
  5. Unknown route shows 404
- Do not change app code unless required for testability.
- Explain how to run tests and open report.
```

---

## Prompt 6: Investigate bug

```txt
Investigate this bug.

Bug:
[Paste bug]

Evidence:
[Paste screenshot/console/network error]

Rules:
- Explain likely cause first.
- Do not edit files yet.
- Identify exact files likely involved.
- Suggest smallest safe fix.
- Provide retest steps.
```

---

## Prompt 7: Fix only one bug

```txt
Fix only this bug:
[Bug title]

Allowed files:
[List files]

Rules:
- Do not add new features.
- Do not rewrite unrelated code.
- Do not remove validation/auth/security.
- Do not ignore tests.
- After fixing, update docs/BUG_LOG.md and docs/REGRESSION_TEST_CHECKLIST.md.
```

---

## Prompt 8: Final QA signoff

```txt
Review:
- docs/QA_CHECKLIST.md
- docs/API_TEST_REPORT.md
- docs/BROWSER_TEST_REPORT.md
- docs/AUTHORIZATION_TEST_REPORT.md
- docs/BUG_LOG.md
- docs/LIGHTHOUSE_REPORT.md
- docs/ACCESSIBILITY_CHECKLIST.md

Create docs/FINAL_QA_SIGNOFF.md.

Include:
1. What passed
2. What failed
3. Critical bugs fixed
4. Open issues
5. Known limitations
6. Whether the project is ready for deployment

Do not edit app code.
```

---

# Part 14: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 11-module-09-testing-browser-verification-qa.md
2. Playwright docs
3. Playwright best practices docs
4. Vitest docs
5. React Testing Library docs
6. Testing Library guiding principles
7. Lighthouse docs
8. Chrome DevTools Recorder docs optional
9. Your API_TEST_REPORT.md
10. Your BROWSER_TEST_REPORT.md
11. Your BUG_LOG.md
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for MERN testing and QA.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. Why testing matters after AI-assisted coding
2. Manual browser QA
3. API testing
4. Auth and authorization testing
5. Component testing with Vitest and React Testing Library
6. E2E testing with Playwright
7. Lighthouse and accessibility checks
8. Bug reports
9. Regression testing
10. Common testing mistakes
11. Practice checklist
```

---

## NotebookLM Prompt 2: Bug Review

```txt
Review my BUG_LOG.md and BROWSER_TEST_REPORT.md.

Classify bugs by:
1. Frontend state
2. API integration
3. Auth
4. Authorization
5. Backend validation
6. UI responsiveness
7. Accessibility
8. Performance
9. Deployment readiness

For each bug:
- Explain likely cause
- Suggest fix priority
- Suggest retest steps
```

---

## NotebookLM Prompt 3: Interview Explanation

```txt
Help me explain my testing process in an interview.

Create:
1. 30-second answer
2. 1-minute answer
3. Technical testing explanation
4. Manual QA explanation
5. API testing explanation
6. Component/E2E testing explanation
7. One real bug and how I fixed it
8. What I learned about quality assurance
```

---

## NotebookLM Prompt 4: Final QA Checklist

```txt
Create a final QA checklist before deployment.

Include:
1. Frontend routes
2. Backend APIs
3. Auth flows
4. Admin flows
5. Browser console
6. Network requests
7. Mobile layout
8. Accessibility
9. Lighthouse
10. Regression
11. Documentation
12. README accuracy
```

---

# Part 15: Required official/resource links

Add these to NotebookLM or module notes:

| Resource | Link | Why it matters |
|---|---|---|
| Playwright official docs | https://playwright.dev/ | E2E testing framework |
| Playwright best practices | https://playwright.dev/docs/best-practices | Locators, auto-waiting, resilient tests |
| Playwright locator assertions | https://playwright.dev/docs/api/class-locatorassertions | Web-first assertions |
| Vitest guide | https://vitest.dev/guide/ | Test runner setup and usage |
| React Testing Library intro | https://testing-library.com/docs/react-testing-library/intro/ | React component testing |
| Testing Library guiding principles | https://testing-library.com/docs/guiding-principles/ | User-centered test philosophy |
| Lighthouse overview | https://developer.chrome.com/docs/lighthouse/overview | Page quality auditing |
| Lighthouse in DevTools | https://developer.chrome.com/docs/devtools/lighthouse | Lighthouse panel and user-flow modes |
| Chrome DevTools Recorder | https://developer.chrome.com/docs/devtools/recorder/reference | Record/replay user flows |

---

# Part 16: Required video resources

Watch at least two videos.

Search YouTube:

```txt
Vitest React Testing Library tutorial Vite
Playwright end to end testing React tutorial
MERN app testing Playwright tutorial
Postman API testing MERN tutorial
Chrome DevTools Network Console debugging tutorial
Lighthouse accessibility performance audit tutorial
React Testing Library user event tutorial
```

Recommended video types:

| Video type | Why |
|---|---|
| Vitest + React Testing Library | Component test setup |
| Playwright E2E | Browser flow automation |
| Postman API testing | Backend validation |
| Chrome DevTools debugging | Console/network issue diagnosis |
| Lighthouse audit | Performance/accessibility check |

---

## Video learning notes

Create:

```txt
docs/notebooklm/module-09-video-learning-notes.md
```

Use this format:

```md
# Module 9 Video Learning Notes

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

## Practice Task 1: Create testing docs

Create all testing documentation files listed in this module.

---

## Practice Task 2: Run manual browser QA

Test all critical pages and flows manually.

Complete:

```txt
docs/BROWSER_TEST_REPORT.md
docs/BUG_LOG.md
```

---

## Practice Task 3: Run API tests

Use Postman/Thunder Client/Insomnia/Hoppscotch.

Complete:

```txt
docs/API_TEST_REPORT.md
```

Test both happy and negative cases.

---

## Practice Task 4: Run authorization tests

Complete:

```txt
docs/AUTHORIZATION_TEST_REPORT.md
```

Confirm:

```txt
Visitor blocked
Customer blocked from admin
Admin allowed
Backend returns 401/403 correctly
```

---

## Practice Task 5: Add component tests

Set up Vitest + React Testing Library.

Add at least 2 tests:

```txt
Button test
EmptyState test
```

Recommended extra:

```txt
Input test
FoodCard test
Cart item test
```

---

## Practice Task 6: Add E2E tests

Set up Playwright.

Add at least 3 tests:

```txt
Home page loads
Login page loads
Protected route redirects visitor
```

Recommended extra:

```txt
Menu page loads
Unknown route shows 404
Customer cannot access admin
```

---

## Practice Task 7: Run Lighthouse

Run Lighthouse on:

```txt
Home page
Menu/resource page
```

Complete:

```txt
docs/LIGHTHOUSE_REPORT.md
```

---

## Practice Task 8: Accessibility checklist

Complete:

```txt
docs/ACCESSIBILITY_CHECKLIST.md
```

Fix critical accessibility issues.

---

## Practice Task 9: Fix critical bugs

Fix only critical and high-priority bugs first.

After each fix:

```txt
1. Update BUG_LOG.md
2. Retest flow
3. Update REGRESSION_TEST_CHECKLIST.md
```

---

## Practice Task 10: Final QA signoff

Complete:

```txt
docs/FINAL_QA_SIGNOFF.md
```

Do not proceed to deployment if critical bugs remain open.

---

# Part 18: Common testing mistakes

## Mistake 1: Testing only happy path

Do not test only successful login/order/admin flow.

Test invalid cases too.

---

## Mistake 2: Ignoring browser console

A page can look correct but still have serious console errors.

---

## Mistake 3: Ignoring network tab

Network tab shows the truth of API calls:

```txt
URL
method
status code
request payload
response payload
headers
```

---

## Mistake 4: Testing admin only from frontend

Always test admin APIs directly with customer token.

---

## Mistake 5: No mobile testing

A project is not portfolio-ready if mobile layout is broken.

---

## Mistake 6: Writing brittle E2E tests

Avoid selecting elements by random class names.

Prefer:

```ts
page.getByRole("button", { name: /login/i })
page.getByLabel(/email/i)
```

---

## Mistake 7: Fixing bugs without retesting

Every bug fix needs regression testing.

---

## Mistake 8: Claiming unsupported features

If README says “admin can update orders,” test it.

If it does not work, do not claim it.

---

# Part 19: Quality bar

Minimum passing standard:

```txt
1. Manual browser QA completed.
2. API test report completed.
3. Authorization test report completed.
4. Bug log contains issues and fixes.
5. Critical bugs fixed.
6. At least two component tests added.
7. At least three E2E tests added.
8. Lighthouse run on at least one page.
9. Accessibility checklist completed.
10. Final QA signoff completed.
```

Strong standard:

```txt
1. All critical user/admin flows tested.
2. Negative API tests included.
3. Role-based access tested in frontend and backend.
4. Component tests cover important UI states.
5. Playwright tests cover login/menu/protected routes.
6. Mobile QA screenshots included.
7. Network/console issues documented.
8. Regression checklist completed after fixes.
```

Advanced standard:

```txt
1. Playwright tests cover full order flow.
2. Playwright tests cover admin status update.
3. Test data setup is documented.
4. CI runs tests on GitHub Actions.
5. Lighthouse issues improved.
6. Accessibility issues fixed.
7. QA signoff is production-style.
```

---

# Required deliverables for this module

Submit:

```txt
1. TESTING_STRATEGY.md
2. QA_CHECKLIST.md
3. API_TEST_REPORT.md
4. BROWSER_TEST_REPORT.md
5. AUTHORIZATION_TEST_REPORT.md
6. BUG_REPORT_TEMPLATE.md
7. BUG_LOG.md
8. REGRESSION_TEST_CHECKLIST.md
9. LIGHTHOUSE_REPORT.md
10. ACCESSIBILITY_CHECKLIST.md
11. TEST_DATA_PLAN.md
12. FINAL_QA_SIGNOFF.md
13. At least 2 Vitest/React Testing Library tests
14. At least 3 Playwright tests
15. Test command screenshots
16. Browser QA screenshots
17. Network tab screenshot for one API call
18. Console screenshot showing no major errors or documented errors
19. Lighthouse screenshot/report
20. NotebookLM Study Guide screenshot
21. NotebookLM bug review screenshot
22. Video learning notes
23. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/11-module-09-testing-browser-verification-qa-reflection.md
```

Use this format:

```md
# Reflection: Module 9 - Testing, Browser Verification and QA

## What I tested
-

## Manual browser QA results
-

## API testing results
-

## Authorization testing results
-

## Component tests I wrote
-

## E2E tests I wrote
-

## Lighthouse/accessibility findings
-

## Bugs I found
-

## Bugs I fixed
-

## What Antigravity helped with
-

## What I had to verify manually
-

## What I learned about testing AI-generated code
-

## What I will improve before deployment
-
```

---

# Quiz

## Multiple choice

**1. What is the main goal of testing in this module?**

A. To prove the app behaves correctly before deployment  
B. To make the README longer  
C. To avoid using the browser  
D. To replace backend APIs  

Correct answer: **A**

---

**2. What should you test besides happy paths?**

A. Invalid inputs, missing tokens, wrong roles, errors, and empty states  
B. Only the logo  
C. Only the homepage color  
D. Only GitHub repository name  

Correct answer: **A**

---

**3. What is the purpose of the Network tab?**

A. Inspect API requests, responses, status codes, and payloads  
B. Edit MongoDB schema directly  
C. Create Figma designs  
D. Generate passwords  

Correct answer: **A**

---

**4. Why is backend authorization testing important?**

A. Frontend route hiding is not enough to secure admin APIs  
B. It makes CSS faster  
C. It removes need for login  
D. It replaces MongoDB  

Correct answer: **A**

---

**5. What testing philosophy does Testing Library encourage?**

A. Tests should resemble how users interact with the app  
B. Tests should check only private implementation details  
C. Tests should avoid user interactions  
D. Tests should depend on random class names  

Correct answer: **A**

---

**6. What is Playwright used for?**

A. End-to-end browser flow testing  
B. Database hosting  
C. Password hashing  
D. CSS color extraction only  

Correct answer: **A**

---

**7. What is Lighthouse used for?**

A. Auditing performance, accessibility, SEO, and best practices  
B. Creating JWT tokens  
C. Replacing React Router  
D. Updating MongoDB documents  

Correct answer: **A**

---

**8. What should happen after fixing a bug?**

A. Regression testing  
B. Ignore old flows  
C. Delete the bug log  
D. Skip browser checks  

Correct answer: **A**

---

**9. Which selector style is better for E2E tests?**

A. `getByRole("button", { name: /login/i })`  
B. `.random-div-123`  
C. `nth-child(9)`  
D. Generated CSS hash  

Correct answer: **A**

---

**10. What should `FINAL_QA_SIGNOFF.md` contain?**

A. Tested flows, open bugs, known limitations, final verdict  
B. Only project title  
C. Only npm version  
D. Only color codes  

Correct answer: **A**

---

## Short-answer questions

1. What is the difference between manual QA and automated testing?
2. Why should you test authorization from the backend directly?
3. What should you inspect in the browser console?
4. What should you inspect in the Network tab?
5. What are three negative API tests?
6. What is one component you tested with Vitest?
7. What is one E2E flow you tested with Playwright?
8. What is one Lighthouse issue you found?
9. What is regression testing?
10. What bug did you find and how did you fix it?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Testing strategy | Clear layered testing plan exists |
| Manual QA | Main routes and flows tested |
| API testing | Happy and negative API tests documented |
| Authorization | Visitor/customer/admin access tested |
| Bug log | Bugs documented with cause/fix/status |
| Component tests | At least 2 Vitest/RTL tests exist |
| E2E tests | At least 3 Playwright tests exist |
| Browser checks | Console/network/mobile checked |
| Lighthouse | At least one Lighthouse report created |
| Accessibility | Accessibility checklist completed |
| Regression | Retest checklist completed after fixes |
| Final signoff | Final QA verdict documented |
| NotebookLM evidence | Study guide and bug review screenshots submitted |
| Reflection | Student explains testing process clearly |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can verify a MERN app through manual browser QA, API testing, auth/authorization testing, component tests, E2E tests, accessibility/performance audits, bug logging, regression testing, and final QA signoff before deployment.
```

After completing this file, continue to:

```txt
12-module-10-deployment-production-readiness.md
```
