# Module 8: Full-Stack Integration — Connect React Frontend with Express Backend

**File Name:** `10-module-08-fullstack-integration.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 7–10 hours  
**Recommended After:** Module 6 and Module 7  
**Main Goal:** Replace mock frontend data with real backend APIs, connect authentication, connect protected routes, connect CRUD flows, handle loading/error states, fix CORS/env issues, and verify the complete MERN user/admin flow in the browser.

---

## Module purpose

In Module 6, you built the frontend with mock data.

In Module 7, you built the backend API.

Now you will connect them.

This module is where the project becomes a real full-stack MERN application.

You will connect:

```txt
React frontend
↓
API client
↓
Express backend
↓
MongoDB database
```

You will replace mock data with real API calls.

You will connect:

- Register
- Login
- Logout
- Auth persistence
- Token-based requests
- Public food listing
- Food details
- Cart checkout
- Order placement
- My orders
- Admin food management
- Admin order management
- Admin order status update
- Loading states
- Empty states
- Error states
- Protected routes
- Browser verification

This module is important because full-stack integration is where many beginner projects break.

---

## Why integration is difficult

A frontend can work perfectly with mock data.

A backend can work perfectly in Postman.

But the full app may still fail because of:

- Wrong API base URL
- CORS error
- Missing `Authorization` header
- Token not saved correctly
- Token not sent correctly
- Frontend data shape not matching backend response
- Different field names such as `id` vs `_id`
- Backend returns nested `data`, frontend expects direct array
- Protected route redirects incorrectly
- Admin role not reflected in frontend
- Forms send strings where backend expects numbers
- CORS `credentials` mismatch
- Environment variables not loaded
- Deployed frontend still using localhost API
- Error messages not shown in UI
- Loading states missing

This module teaches you how to fix these problems systematically.

---

## Full-stack integration principle

Use this principle:

```txt
One flow at a time.
One API at a time.
One page at a time.
Verify after every connection.
```

Do not connect the whole app in one prompt.

Bad approach:

```txt
Connect frontend and backend.
```

Better approach:

```txt
Connect only login API first.
Then verify token storage.
Then connect protected route.
Then connect food list.
```

---

## Integration order

Follow this order:

```txt
1. Confirm backend APIs work manually
2. Confirm frontend runs
3. Configure frontend API base URL
4. Configure backend CORS
5. Create API client
6. Connect auth APIs
7. Persist token/user
8. Send Authorization header
9. Replace food mock data
10. Replace order mock data
11. Connect admin food CRUD
12. Connect admin order status
13. Verify protected routes
14. Handle loading/error/empty states
15. Run full browser QA
16. Document bugs and fixes
```

---

## What you will build in this module

You will create or update:

```txt
client/src/lib/api.ts
client/src/services/authService.ts
client/src/services/foodService.ts
client/src/services/orderService.ts
client/src/context/AuthContext.tsx
client/src/context/CartContext.tsx
client/src/pages/auth/LoginPage.tsx
client/src/pages/auth/RegisterPage.tsx
client/src/pages/public/MenuPage.tsx
client/src/pages/public/FoodDetailsPage.tsx
client/src/pages/customer/CheckoutPage.tsx
client/src/pages/customer/MyOrdersPage.tsx
client/src/pages/admin/ManageFoodsPage.tsx
client/src/pages/admin/ManageOrdersPage.tsx
client/.env.example
```

You will also create docs:

```txt
docs/FULLSTACK_INTEGRATION_PLAN.md
docs/API_CLIENT_PLAN.md
docs/AUTH_INTEGRATION_PLAN.md
docs/ENV_AND_CORS_CHECKLIST.md
docs/FULLSTACK_FLOW_TEST_PLAN.md
docs/FULLSTACK_BROWSER_QA_REPORT.md
docs/INTEGRATION_BUG_LOG.md
```

---

# Part 1: Pre-integration checklist

Before connecting frontend and backend, confirm both sides work independently.

## Backend checklist

Run backend:

```bash
cd server
npm run dev
```

Check:

```txt
GET http://localhost:5000/health
```

Expected:

```json
{
  "success": true,
  "message": "Server is healthy"
}
```

Then test these manually through Postman/Thunder Client:

```txt
POST /api/auth/register
POST /api/auth/login
GET /api/foods
POST /api/foods as admin
POST /api/orders as customer
GET /api/orders/my-orders as customer
GET /api/orders as admin
PATCH /api/orders/:id/status as admin
```

Do not integrate frontend until these work.

---

## Frontend checklist

Run frontend:

```bash
cd client
npm run dev
```

Check:

```txt
http://localhost:5173
```

Verify:

```txt
1. Home page loads
2. Menu page loads with mock data
3. Login page loads
4. Cart works with mock data
5. Admin pages render
6. No major console errors
```

---

## Documentation checklist

Confirm these files exist:

```txt
docs/API_CONTRACT.md
docs/DATABASE_SCHEMA.md
docs/AUTHORIZATION_MATRIX.md
docs/FRONTEND_STATE_PLAN.md
docs/BACKEND_API_TEST_REPORT.md
docs/BACKEND_SECURITY_CHECKLIST.md
```

These files will help Antigravity connect the app correctly.

---

# Part 2: Environment variables

## Frontend environment variables

Create:

```txt
client/.env.example
```

Content:

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

Create local:

```txt
client/.env
```

Content:

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

Important:

```txt
Frontend Vite env variables that should be available in browser code must start with VITE_.
Do not put private secrets in frontend env variables.
```

---

## Backend environment variables

Your backend should already have:

```txt
server/.env.example
```

Example:

```env
NODE_ENV=development
PORT=5000
CLIENT_URL=http://localhost:5173
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/localbites
JWT_SECRET=replace_with_long_random_secret
JWT_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=10
```

Important:

```txt
CLIENT_URL must match the frontend origin.
```

For local Vite frontend:

```txt
http://localhost:5173
```

For deployed frontend later:

```txt
https://your-project.vercel.app
```

---

## Why env variables matter

Do not hardcode URLs like this everywhere:

```ts
fetch("http://localhost:5000/api/foods")
```

Instead, use:

```ts
const API_BASE_URL = import.meta.env.VITE_API_BASE_URL;
```

This makes deployment easier.

---

# Part 3: CORS setup

CORS allows your browser frontend to call your backend from a different origin.

During local development:

```txt
Frontend: http://localhost:5173
Backend:  http://localhost:5000
```

These are different origins because the ports are different.

Your Express backend should allow your frontend origin.

Example in `server/src/app.ts`:

```ts
app.use(
  cors({
    origin: env.CLIENT_URL,
    credentials: true,
  })
);
```

If you are only sending JWT in `Authorization` header and not cookies, `credentials` may not be strictly required. However, keep your CORS strategy consistent.

---

## Common CORS errors

| Problem | Cause | Fix |
|---|---|---|
| CORS blocked | Backend did not allow frontend origin | Set `CLIENT_URL=http://localhost:5173` |
| Preflight error | Backend rejects OPTIONS request | Ensure CORS middleware runs before routes |
| Works in Postman but not browser | Postman does not enforce browser CORS | Fix Express CORS config |
| Deployed frontend blocked | Backend still allows only localhost | Update deployed `CLIENT_URL` |
| Credentials error | Credentials mismatch | Align frontend request and backend CORS |

---

# Part 4: API response shape

Your backend response format should look like this:

```json
{
  "success": true,
  "message": "Foods retrieved successfully",
  "data": []
}
```

Your frontend must read:

```ts
response.data.data
```

if using Axios, or:

```ts
const json = await response.json();
return json.data;
```

if using `fetch`.

Many integration bugs happen because the frontend expects:

```ts
foods
```

but the backend returns:

```ts
{
  success,
  message,
  data: foods
}
```

Be careful.

---

# Part 5: Create API client

You can use either `fetch` or Axios.

For this bootcamp, use a simple `fetch` wrapper first. It is enough for junior MERN projects and avoids extra dependency.

Create:

```txt
client/src/lib/api.ts
```

```ts
import type { ApiResponse } from "../types/api";

const API_BASE_URL = import.meta.env.VITE_API_BASE_URL;

if (!API_BASE_URL) {
  throw new Error("VITE_API_BASE_URL is not defined");
}

type ApiRequestOptions = RequestInit & {
  token?: string | null;
};

export async function apiRequest<T>(
  endpoint: string,
  options: ApiRequestOptions = {}
): Promise<T> {
  const { token, headers, ...rest } = options;

  const response = await fetch(`${API_BASE_URL}${endpoint}`, {
    ...rest,
    headers: {
      "Content-Type": "application/json",
      ...(token ? { Authorization: `Bearer ${token}` } : {}),
      ...headers,
    },
  });

  const json = (await response.json()) as ApiResponse<T>;

  if (!response.ok || !json.success) {
    throw new Error(json.message || "API request failed");
  }

  return json.data;
}
```

---

## API client rules

The API client should:

- Use base URL from env
- Add `Content-Type`
- Add `Authorization` header if token exists
- Parse backend response
- Throw readable errors
- Return only `data`
- Avoid duplicating fetch logic everywhere

---

# Part 6: Update frontend API types

Create/update:

```txt
client/src/types/api.ts
```

```ts
export type ApiResponse<T> = {
  success: boolean;
  message: string;
  data: T;
};

export type ApiError = {
  success: false;
  message: string;
  errors?: unknown[];
};
```

Create/update:

```txt
client/src/types/auth.ts
```

```ts
import type { User } from "./user";

export type AuthResponse = {
  user: User;
  token: string;
};

export type LoginInput = {
  email: string;
  password: string;
};

export type RegisterInput = {
  name: string;
  email: string;
  password: string;
};
```

---

# Part 7: Auth service

Create:

```txt
client/src/services/authService.ts
```

```ts
import { apiRequest } from "../lib/api";
import type { AuthResponse, LoginInput, RegisterInput } from "../types/auth";

export function registerUser(input: RegisterInput) {
  return apiRequest<AuthResponse>("/auth/register", {
    method: "POST",
    body: JSON.stringify(input),
  });
}

export function loginUser(input: LoginInput) {
  return apiRequest<AuthResponse>("/auth/login", {
    method: "POST",
    body: JSON.stringify(input),
  });
}
```

---

# Part 8: Update AuthContext for real auth

Replace mock auth with real auth storage.

Create/update:

```txt
client/src/context/AuthContext.tsx
```

Example:

```tsx
import {
  createContext,
  useContext,
  useMemo,
  useState,
  type ReactNode,
} from "react";
import { loginUser, registerUser } from "../services/authService";
import type { AuthResponse, LoginInput, RegisterInput } from "../types/auth";
import type { User } from "../types/user";

const AUTH_STORAGE_KEY = "localbites_auth";

type AuthState = {
  user: User;
  token: string;
};

type AuthContextValue = {
  user: User | null;
  token: string | null;
  isAuthenticated: boolean;
  isAdmin: boolean;
  register: (input: RegisterInput) => Promise<AuthResponse>;
  login: (input: LoginInput) => Promise<AuthResponse>;
  logout: () => void;
};

const AuthContext = createContext<AuthContextValue | null>(null);

function loadInitialAuth(): AuthState | null {
  try {
    const stored = localStorage.getItem(AUTH_STORAGE_KEY);
    return stored ? (JSON.parse(stored) as AuthState) : null;
  } catch {
    return null;
  }
}

export function AuthProvider({ children }: { children: ReactNode }) {
  const [auth, setAuth] = useState<AuthState | null>(loadInitialAuth);

  const saveAuth = (nextAuth: AuthState) => {
    setAuth(nextAuth);
    localStorage.setItem(AUTH_STORAGE_KEY, JSON.stringify(nextAuth));
  };

  const register = async (input: RegisterInput) => {
    const result = await registerUser(input);
    saveAuth(result);
    return result;
  };

  const login = async (input: LoginInput) => {
    const result = await loginUser(input);
    saveAuth(result);
    return result;
  };

  const logout = () => {
    setAuth(null);
    localStorage.removeItem(AUTH_STORAGE_KEY);
  };

  const value = useMemo<AuthContextValue>(
    () => ({
      user: auth?.user ?? null,
      token: auth?.token ?? null,
      isAuthenticated: Boolean(auth?.token),
      isAdmin: auth?.user.role === "admin",
      register,
      login,
      logout,
    }),
    [auth]
  );

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}

export function useAuth() {
  const context = useContext(AuthContext);

  if (!context) {
    throw new Error("useAuth must be used inside AuthProvider");
  }

  return context;
}
```

---

## Token storage note

For this beginner MERN project, localStorage is simple and common.

But understand the tradeoff:

```txt
localStorage is easy but vulnerable if your app has XSS vulnerabilities.
```

For advanced production apps, teams may use HTTP-only cookies, stronger CSRF/XSS controls, token rotation, or managed auth providers.

For this bootcamp:

```txt
Use localStorage carefully.
Do not store secrets other than the auth token.
Do not expose private keys in frontend.
```

---

# Part 9: Connect login page

Update:

```txt
client/src/pages/auth/LoginPage.tsx
```

Required behavior:

- Email/password input
- Submit calls `login`
- Show loading state
- Show error state
- Redirect after success
- Optional demo credential notes

Example flow:

```txt
User submits login form
→ login service calls POST /auth/login
→ backend returns user/token
→ AuthContext saves user/token
→ user redirected to /menu or previous route
```

Antigravity prompt:

```txt
Connect LoginPage to real auth API.

Read:
- client/src/context/AuthContext.tsx
- client/src/services/authService.ts
- client/src/pages/auth/LoginPage.tsx

Rules:
- Use existing common Input/Button/ErrorState components.
- Show loading state while submitting.
- Show API error message.
- Save auth through AuthContext login().
- Redirect to /menu after success.
- Do not edit backend.
- Do not change register page yet.
```

---

# Part 10: Connect register page

Update:

```txt
client/src/pages/auth/RegisterPage.tsx
```

Required behavior:

- Name/email/password input
- Basic frontend validation
- Submit calls `register`
- Show loading state
- Show error state
- Redirect after success

Antigravity prompt:

```txt
Connect RegisterPage to real auth API.

Rules:
- Use AuthContext register().
- Show loading and error states.
- Redirect to /menu after registration.
- Do not edit backend.
- Do not change login page.
```

---

# Part 11: Update route guards

Update:

```txt
client/src/routes/ProtectedRoute.tsx
client/src/routes/AdminRoute.tsx
```

Protected route should check:

```txt
isAuthenticated
```

Admin route should check:

```txt
isAuthenticated + isAdmin
```

Example:

```tsx
import { Navigate, Outlet, useLocation } from "react-router";
import { useAuth } from "../context/AuthContext";

export function ProtectedRoute() {
  const { isAuthenticated } = useAuth();
  const location = useLocation();

  if (!isAuthenticated) {
    return <Navigate to="/login" state={{ from: location }} replace />;
  }

  return <Outlet />;
}
```

Admin route:

```tsx
import { Navigate, Outlet } from "react-router";
import { useAuth } from "../context/AuthContext";

export function AdminRoute() {
  const { isAuthenticated, isAdmin } = useAuth();

  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }

  if (!isAdmin) {
    return <Navigate to="/unauthorized" replace />;
  }

  return <Outlet />;
}
```

---

# Part 12: Food service

Create:

```txt
client/src/services/foodService.ts
```

```ts
import { apiRequest } from "../lib/api";
import type { Food } from "../types/food";

export type FoodQuery = {
  search?: string;
  category?: string;
  minPrice?: string;
  maxPrice?: string;
};

function buildQueryString(query: FoodQuery) {
  const params = new URLSearchParams();

  Object.entries(query).forEach(([key, value]) => {
    if (value) params.set(key, value);
  });

  const queryString = params.toString();

  return queryString ? `?${queryString}` : "";
}

export function getFoods(query: FoodQuery = {}) {
  return apiRequest<Food[]>(`/foods${buildQueryString(query)}`);
}

export function getFoodById(id: string) {
  return apiRequest<Food>(`/foods/${id}`);
}

export function createFood(input: Omit<Food, "id">, token: string) {
  return apiRequest<Food>("/foods", {
    method: "POST",
    token,
    body: JSON.stringify(input),
  });
}

export function updateFood(id: string, input: Partial<Food>, token: string) {
  return apiRequest<Food>(`/foods/${id}`, {
    method: "PATCH",
    token,
    body: JSON.stringify(input),
  });
}

export function deleteFood(id: string, token: string) {
  return apiRequest<null>(`/foods/${id}`, {
    method: "DELETE",
    token,
  });
}
```

---

## MongoDB `_id` vs frontend `id`

Your backend may return:

```json
{
  "_id": "mongoId",
  "name": "Burger"
}
```

Your frontend type may expect:

```ts
id: string
```

You have two options:

### Option 1: Use `_id` in frontend types

```ts
export type Food = {
  _id: string;
  name: string;
  ...
}
```

### Option 2: Normalize API response

```ts
function normalizeFood(food: BackendFood): Food {
  return {
    id: food._id,
    name: food.name,
    ...
  };
}
```

For beginners, using `_id` directly is acceptable if you are consistent.

But do not mix randomly.

Pick one approach and document it in:

```txt
docs/API_DATA_SHAPE_DECISIONS.md
```

---

# Part 13: Connect menu page

Update:

```txt
client/src/pages/public/MenuPage.tsx
```

Required behavior:

- Fetch foods from backend
- Show loading state
- Show error state
- Show empty state
- Search/filter calls backend or filters locally
- Add to cart uses real food data

Antigravity prompt:

```txt
Connect MenuPage to real food API.

Read:
- client/src/services/foodService.ts
- client/src/pages/public/MenuPage.tsx
- client/src/components/food/FoodCard.tsx
- client/src/components/states/

Rules:
- Replace mockFoods with getFoods().
- Add loading state.
- Add error state.
- Add empty state.
- Keep add-to-cart behavior.
- Do not edit backend.
- Do not connect admin food page yet.
```

---

# Part 14: Connect food details page

Update:

```txt
client/src/pages/public/FoodDetailsPage.tsx
```

Required behavior:

- Read `id` from URL
- Fetch food by ID
- Show loading
- Show error/not found
- Add to cart

Antigravity prompt:

```txt
Connect FoodDetailsPage to real food details API.

Rules:
- Use getFoodById(id).
- Show loading state.
- Show error/not-found state.
- Keep add-to-cart.
- Do not edit backend.
```

---

# Part 15: Order service

Create:

```txt
client/src/services/orderService.ts
```

```ts
import { apiRequest } from "../lib/api";
import type { Order, OrderStatus } from "../types/order";
import type { CartItem } from "../context/CartContext";

export type CreateOrderInput = {
  items: CartItem[];
  deliveryAddress: string;
  phone: string;
  totalPrice: number;
};

export function createOrder(input: CreateOrderInput, token: string) {
  return apiRequest<Order>("/orders", {
    method: "POST",
    token,
    body: JSON.stringify(input),
  });
}

export function getMyOrders(token: string) {
  return apiRequest<Order[]>("/orders/my-orders", {
    token,
  });
}

export function getAllOrders(token: string) {
  return apiRequest<Order[]>("/orders", {
    token,
  });
}

export function updateOrderStatus(
  orderId: string,
  status: OrderStatus,
  token: string
) {
  return apiRequest<Order>(`/orders/${orderId}/status`, {
    method: "PATCH",
    token,
    body: JSON.stringify({ status }),
  });
}
```

---

# Part 16: Connect checkout page

Update:

```txt
client/src/pages/customer/CheckoutPage.tsx
```

Required behavior:

- Require login
- Require cart items
- Collect delivery address and phone
- Send order API request
- Send token
- Show loading
- Show success
- Clear cart after success
- Redirect to `/my-orders` or show success link

Antigravity prompt:

```txt
Connect CheckoutPage to real create order API.

Read:
- client/src/context/AuthContext.tsx
- client/src/context/CartContext.tsx
- client/src/services/orderService.ts
- client/src/pages/customer/CheckoutPage.tsx

Rules:
- If no token, redirect to login.
- If cart is empty, show empty state.
- Submit delivery address and phone.
- Use cart items and totalPrice.
- Show loading while submitting.
- Show API error message.
- Clear cart after successful order.
- Redirect or link to /my-orders after success.
- Do not edit backend.
```

---

## Important order data warning

Your backend expects item fields:

```txt
foodId
name
quantity
price
```

Your frontend cart item must match this.

If frontend sends:

```txt
id
title
qty
```

backend validation will fail.

Update cart item shape if needed.

---

# Part 17: Connect My Orders page

Update:

```txt
client/src/pages/customer/MyOrdersPage.tsx
```

Required behavior:

- Fetch logged-in user's orders
- Send token
- Show loading
- Show error
- Show empty state
- Show status badge

Antigravity prompt:

```txt
Connect MyOrdersPage to real API.

Rules:
- Use getMyOrders(token).
- Show loading, error, and empty states.
- Display order status, items, total price, and date.
- Do not edit backend.
```

---

# Part 18: Connect admin food management

Update:

```txt
client/src/pages/admin/ManageFoodsPage.tsx
```

Required behavior:

- Fetch all foods
- Create food as admin
- Update food as admin
- Delete food as admin
- Send admin token
- Show loading/error
- Refresh list after mutation
- Show form validation basics

Antigravity prompt:

```txt
Connect ManageFoodsPage to real admin food APIs.

Read:
- client/src/services/foodService.ts
- client/src/context/AuthContext.tsx
- client/src/pages/admin/ManageFoodsPage.tsx

Rules:
- Use token from AuthContext.
- Fetch foods from backend.
- Create food using POST /foods.
- Update food using PATCH /foods/:id.
- Delete food using DELETE /foods/:id.
- Show loading and error states.
- Refresh list after successful mutation.
- Do not edit backend.
- Keep UI simple and reliable.
```

---

## Admin form warning

HTML inputs return strings.

Backend expects `price` as number.

Convert:

```ts
price: Number(form.price)
```

If you send `"250"` instead of `250`, Zod may reject it.

---

# Part 19: Connect admin order management

Update:

```txt
client/src/pages/admin/ManageOrdersPage.tsx
```

Required behavior:

- Fetch all orders as admin
- Send token
- Show loading/error
- Display order rows
- Update order status
- Refresh after update
- Show 403 error if not admin

Antigravity prompt:

```txt
Connect ManageOrdersPage to real admin order APIs.

Rules:
- Use getAllOrders(token).
- Use updateOrderStatus(orderId, status, token).
- Show loading, error, empty states.
- Display customer/user info if backend returns it.
- Refresh list after status update.
- Do not edit backend.
```

---

# Part 20: Optional TanStack Query upgrade

You can connect APIs using `useEffect` and `useState`.

That is acceptable for beginners.

But for stronger frontend architecture, you can use TanStack Query.

TanStack Query is useful for:

- Server state
- Caching
- Loading state
- Error state
- Refetching
- Mutations
- Invalidating data after create/update/delete

Install:

```bash
cd client
npm install @tanstack/react-query
```

Create provider in `App.tsx` or `main.tsx`:

```tsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient();

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <AuthProvider>
        <CartProvider>
          <AppRoutes />
        </CartProvider>
      </AuthProvider>
    </QueryClientProvider>
  );
}
```

Example query:

```tsx
const { data: foods = [], isLoading, error } = useQuery({
  queryKey: ["foods", search, category],
  queryFn: () => getFoods({ search, category }),
});
```

Example mutation:

```tsx
const queryClient = useQueryClient();

const createFoodMutation = useMutation({
  mutationFn: (input: CreateFoodInput) => createFood(input, token),
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ["foods"] });
  },
});
```

Optional rule:

```txt
Use TanStack Query if you can understand it.
Use useEffect/useState if you are still struggling.
```

Do not add complexity you cannot explain.

---

# Part 21: Full-stack flow tests

Test the app as a real user.

## Flow 1: Register

```txt
1. Open /register
2. Create new account
3. Confirm redirect/login state
4. Confirm token saved
5. Confirm navbar changes
```

Expected:

```txt
User registered and logged in.
```

---

## Flow 2: Login

```txt
1. Logout
2. Open /login
3. Login with existing account
4. Confirm redirect
5. Confirm protected route access
```

Expected:

```txt
User can login and access protected pages.
```

---

## Flow 3: Browse food

```txt
1. Open /menu
2. Confirm food loads from backend
3. Open food details page
4. Add item to cart
```

Expected:

```txt
Foods are loaded from MongoDB via Express API.
```

---

## Flow 4: Place order

```txt
1. Add item to cart
2. Open /checkout
3. Enter address and phone
4. Submit order
5. Confirm success
6. Open /my-orders
```

Expected:

```txt
Order is created in MongoDB and visible in My Orders.
```

---

## Flow 5: Admin food management

```txt
1. Login as admin
2. Open /admin/foods
3. Create a food item
4. Confirm it appears in menu
5. Update item
6. Delete item if needed
```

Expected:

```txt
Admin can manage foods.
```

---

## Flow 6: Admin order management

```txt
1. Login as admin
2. Open /admin/orders
3. View all orders
4. Change status
5. Confirm updated status appears
```

Expected:

```txt
Admin can manage order statuses.
```

---

## Flow 7: Authorization failure

```txt
1. Login as normal customer
2. Try /admin/orders
3. Try admin API with customer token through API client/Postman
```

Expected:

```txt
Frontend redirects to unauthorized.
Backend returns 403.
```

---

# Part 22: Integration documentation files

Create:

```txt
docs/FULLSTACK_INTEGRATION_PLAN.md
```

Template:

```md
# Full-Stack Integration Plan

## Goal
Connect React frontend with Express backend and replace mock data with real APIs.

## Integration order
1. Configure frontend API URL
2. Configure backend CORS
3. Create API client
4. Connect auth APIs
5. Persist token/user
6. Send Authorization header
7. Connect foods
8. Connect orders
9. Connect admin food CRUD
10. Connect admin order status
11. Test full user/admin flows
12. Fix integration bugs

## Rules
- Connect one API at a time.
- Verify every flow in browser.
- Do not change backend contract randomly.
- Update docs when data shape changes.
```

---

Create:

```txt
docs/API_CLIENT_PLAN.md
```

Template:

```md
# API Client Plan

## Base URL
Frontend uses:

```txt
VITE_API_BASE_URL
```

## API client responsibilities
- Read base URL from env
- Add Content-Type header
- Add Authorization header when token exists
- Parse backend response
- Throw readable errors
- Return response data only

## Services
| Service | APIs |
|---|---|
| authService | register/login |
| foodService | list/details/create/update/delete |
| orderService | create/my-orders/all-orders/update-status |
```

---

Create:

```txt
docs/AUTH_INTEGRATION_PLAN.md
```

Template:

```md
# Auth Integration Plan

## Register
Register form → POST /auth/register → Save user/token → Redirect

## Login
Login form → POST /auth/login → Save user/token → Redirect

## Persistence
Auth state is stored in localStorage for this beginner project.

## Logout
Remove auth state from localStorage.

## Protected requests
Send:

```txt
Authorization: Bearer <token>
```

## Route guards
- ProtectedRoute checks login
- AdminRoute checks login + admin role

## Security note
Backend must still enforce all auth and role checks.
```

---

Create:

```txt
docs/ENV_AND_CORS_CHECKLIST.md
```

Template:

```md
# Env and CORS Checklist

## Frontend
- [ ] `client/.env` exists
- [ ] `VITE_API_BASE_URL=http://localhost:5000/api`
- [ ] Frontend restarted after env change
- [ ] No private secrets in frontend env

## Backend
- [ ] `server/.env` exists
- [ ] `CLIENT_URL=http://localhost:5173`
- [ ] `MONGODB_URI` works
- [ ] `JWT_SECRET` configured
- [ ] Backend restarted after env change

## CORS
- [ ] CORS middleware runs before routes
- [ ] Origin matches frontend URL
- [ ] Browser requests are not blocked
- [ ] Deployed frontend URL added later
```

---

Create:

```txt
docs/FULLSTACK_FLOW_TEST_PLAN.md
```

Template:

```md
# Full-Stack Flow Test Plan

| Flow | User role | Expected result | Status |
|---|---|---|---|
| Register | Visitor | Account created and logged in | Pending |
| Login | Visitor | Token saved and route access works | Pending |
| Browse food | Visitor/customer | Foods load from backend | Pending |
| Food details | Visitor/customer | Single food loads from backend | Pending |
| Add to cart | Customer | Cart updates | Pending |
| Checkout | Customer | Order created in backend | Pending |
| My orders | Customer | Own orders display | Pending |
| Admin foods | Admin | Create/update/delete food works | Pending |
| Admin orders | Admin | All orders display | Pending |
| Update status | Admin | Order status updates | Pending |
| Admin access denied | Customer | Unauthorized/403 | Pending |
```

---

Create:

```txt
docs/FULLSTACK_BROWSER_QA_REPORT.md
```

Template:

```md
# Full-Stack Browser QA Report

## Local URLs
Frontend:
-

Backend:
-

## Test accounts

Customer:
-

Admin:
-

## Flows tested

### Register
Status:
Notes:

### Login
Status:
Notes:

### Browse foods
Status:
Notes:

### Place order
Status:
Notes:

### My orders
Status:
Notes:

### Admin food management
Status:
Notes:

### Admin order management
Status:
Notes:

### Authorization
Status:
Notes:

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

Create:

```txt
docs/INTEGRATION_BUG_LOG.md
```

Template:

```md
# Integration Bug Log

| Bug | Where | Cause | Fix | Status |
|---|---|---|---|---|
| CORS blocked | Browser | CLIENT_URL mismatch | Updated backend env | Fixed |
| Token missing | Checkout | Auth header not sent | Added token in apiRequest | Fixed |
| Food list blank | MenuPage | Response nested in data | Returned json.data | Fixed |
| Price validation failed | Admin form | Price sent as string | Converted to Number | Fixed |
```

---

Create:

```txt
docs/API_DATA_SHAPE_DECISIONS.md
```

Template:

```md
# API Data Shape Decisions

## ID field decision

Backend returns MongoDB `_id`.

Frontend will use:
- `_id` directly
or
- normalized `id`

Decision:
-

Reason:
-

## Response format

Backend response:

```json
{
  "success": true,
  "message": "Message",
  "data": {}
}
```

Frontend API client returns only:

```txt
data
```

## Date fields

Backend returns:
- createdAt
- updatedAt

Frontend will format dates in UI using:
-

## Known differences
-
```

---

# Part 23: Antigravity prompts for this module

## Prompt 1: Create integration docs

```txt
I am doing Module 8: Full-Stack Integration.

Create these docs:
1. docs/FULLSTACK_INTEGRATION_PLAN.md
2. docs/API_CLIENT_PLAN.md
3. docs/AUTH_INTEGRATION_PLAN.md
4. docs/ENV_AND_CORS_CHECKLIST.md
5. docs/FULLSTACK_FLOW_TEST_PLAN.md
6. docs/FULLSTACK_BROWSER_QA_REPORT.md
7. docs/INTEGRATION_BUG_LOG.md
8. docs/API_DATA_SHAPE_DECISIONS.md

Rules:
- Do not change code yet.
- Use my existing React frontend and Express backend architecture.
- Keep instructions practical for a junior MERN developer.
```

---

## Prompt 2: Review readiness before integration

```txt
Review whether the project is ready for full-stack integration.

Read:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/FRONTEND_STATE_PLAN.md
- docs/BACKEND_API_TEST_REPORT.md
- docs/BACKEND_SECURITY_CHECKLIST.md

Check:
1. Backend APIs tested?
2. Frontend pages ready?
3. API data shape clear?
4. Auth flow clear?
5. Env variables ready?
6. CORS ready?
7. What should be connected first?

Do not edit files.

Return a readiness report.
```

---

## Prompt 3: Create API client only

```txt
Create only the frontend API client.

Files:
- client/src/lib/api.ts
- client/src/types/api.ts
- client/.env.example

Rules:
- Use VITE_API_BASE_URL.
- Add Authorization header when token is provided.
- Parse backend success/error response.
- Return only response data.
- Do not connect pages yet.
- Do not edit backend.
```

---

## Prompt 4: Connect auth only

```txt
Connect only authentication.

Files:
- client/src/services/authService.ts
- client/src/types/auth.ts
- client/src/context/AuthContext.tsx
- client/src/pages/auth/LoginPage.tsx
- client/src/pages/auth/RegisterPage.tsx
- client/src/routes/ProtectedRoute.tsx
- client/src/routes/AdminRoute.tsx

Rules:
- Use real backend register/login APIs.
- Store user/token in localStorage.
- Send no fake/mock login after this.
- Show loading and error states.
- Do not connect foods/orders yet.
- Do not edit backend unless there is a confirmed backend bug.
```

---

## Prompt 5: Connect food APIs only

```txt
Connect only food APIs.

Files:
- client/src/services/foodService.ts
- client/src/pages/public/MenuPage.tsx
- client/src/pages/public/FoodDetailsPage.tsx
- client/src/components/food/FoodCard.tsx

Rules:
- Replace mock foods with backend GET /foods.
- Connect GET /foods/:id.
- Show loading, error, empty states.
- Keep cart behavior working.
- Do not connect admin food CRUD yet.
- Do not edit backend.
```

---

## Prompt 6: Connect order APIs only

```txt
Connect only customer order APIs.

Files:
- client/src/services/orderService.ts
- client/src/pages/customer/CheckoutPage.tsx
- client/src/pages/customer/MyOrdersPage.tsx
- client/src/context/CartContext.tsx if needed

Rules:
- Send Authorization header with token.
- Create order from cart items.
- Show loading/error/success.
- Clear cart after success.
- Fetch my orders from backend.
- Do not connect admin order page yet.
- Do not edit backend unless confirmed bug.
```

---

## Prompt 7: Connect admin APIs only

```txt
Connect only admin APIs.

Files:
- client/src/pages/admin/ManageFoodsPage.tsx
- client/src/pages/admin/ManageOrdersPage.tsx
- client/src/services/foodService.ts
- client/src/services/orderService.ts

Rules:
- Use admin token from AuthContext.
- Connect create/update/delete food.
- Connect get all orders.
- Connect update order status.
- Show 403/unauthorized errors clearly.
- Refresh data after mutation.
- Do not rewrite unrelated frontend pages.
```

---

## Prompt 8: Browser verification

```txt
Use browser verification for full-stack integration.

Test:
1. Register
2. Login
3. Browse foods
4. Food details
5. Add to cart
6. Checkout/order placement
7. My orders
8. Admin food CRUD
9. Admin order status update
10. Customer denied from admin routes

Check:
- Console errors
- Network errors
- CORS errors
- Loading states
- Error states
- Empty states
- Responsive layout

Create or update docs/FULLSTACK_BROWSER_QA_REPORT.md.

Do not edit files yet.
```

---

## Prompt 9: Fix only integration bugs

```txt
Read docs/FULLSTACK_BROWSER_QA_REPORT.md and docs/INTEGRATION_BUG_LOG.md.

Fix only critical integration bugs.

Rules:
- Do not add new features.
- Do not rewrite working pages.
- Do not change API contract unless required and documented.
- Do not remove auth or role checks.
- Keep fixes minimal.
- After fixing, update bug log.
```

---

# Part 24: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 10-module-08-fullstack-integration.md
2. Vite env variables docs
3. Express CORS middleware docs
4. TanStack Query overview docs if using it
5. React Router docs
6. Your API_CONTRACT.md
7. Your BACKEND_API_TEST_REPORT.md
8. Your FRONTEND_STATE_PLAN.md
9. Your FULLSTACK_BROWSER_QA_REPORT.md
10. Your INTEGRATION_BUG_LOG.md
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for full-stack MERN integration.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. What full-stack integration means
2. Why frontend mock data must be replaced carefully
3. API base URL setup
4. Vite env variables
5. Express CORS setup
6. API client design
7. Auth token storage and Authorization header
8. Connecting food APIs
9. Connecting order APIs
10. Connecting admin APIs
11. Loading/error/empty states
12. Browser QA
13. Common integration bugs
14. Practice checklist
```

---

## NotebookLM Prompt 2: Integration Bug Diagnosis

```txt
Review my integration bug log and browser QA report.

Classify bugs into:
1. Env/config bugs
2. CORS bugs
3. Auth/token bugs
4. API response shape bugs
5. Data type bugs
6. Route/protected route bugs
7. Backend bugs
8. Frontend UI state bugs

For each bug:
- Explain likely cause
- Suggest safest fix
- Tell what to verify after fixing
```

---

## NotebookLM Prompt 3: Full-Stack Flow Explanation

```txt
Help me explain my full-stack integration in an interview.

Create:
1. 30-second explanation
2. 1-minute explanation
3. Technical explanation
4. Login flow explanation
5. Food list flow explanation
6. Order placement flow explanation
7. Admin order status flow explanation
8. One integration bug and how I fixed it
```

---

## NotebookLM Prompt 4: Final QA Checklist

```txt
Create a final full-stack QA checklist.

Include:
1. Frontend routes
2. Backend APIs
3. Auth flows
4. User flows
5. Admin flows
6. Authorization failure cases
7. Network tab checks
8. Console checks
9. Mobile checks
10. Documentation checks
```

---

# Part 25: Required official/resource links

Add these to NotebookLM or your module notes:

| Resource | Link | Why it matters |
|---|---|---|
| Vite Env Variables and Modes | https://vite.dev/guide/env-and-mode | Explains `import.meta.env` and `VITE_` client exposure |
| Express CORS middleware | https://expressjs.com/en/resources/middleware/cors.html | Explains CORS configuration in Express |
| MDN CORS Guide | https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS | Explains browser CORS behavior and preflight requests |
| TanStack Query React Overview | https://tanstack.com/query/latest/docs/framework/react/overview | Explains server-state management for React |
| React Router Docs | https://reactrouter.com/ | Routing reference |
| Fetch API MDN | https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API | Native browser fetch reference |
| localStorage MDN | https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage | Browser storage reference |
| OWASP Access Control | https://owasp.org/www-community/Access_Control | Access control/security reference |

---

# Part 26: Required video resources

Watch at least two videos.

Search YouTube:

```txt
MERN stack frontend backend integration tutorial
React Express MongoDB JWT full stack authentication tutorial
React fetch API authorization bearer token tutorial
CORS error React Express fix tutorial
TanStack Query CRUD React tutorial
MERN admin dashboard CRUD tutorial
```

Recommended video types:

| Video type | Why |
|---|---|
| MERN full-stack integration | Shows frontend/backend connection |
| JWT auth with React + Express | Helps login/token flow |
| CORS React Express | Helps common browser errors |
| TanStack Query CRUD | Helps server state and mutations |
| MERN admin dashboard | Helps admin flows |

---

## Video learning notes

Create:

```txt
docs/notebooklm/module-08-video-learning-notes.md
```

Use this format:

```md
# Module 8 Video Learning Notes

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

# Part 27: Practice tasks

## Practice Task 1: Confirm backend APIs

Run backend and complete:

```txt
docs/BACKEND_API_TEST_REPORT.md
```

Do not continue if backend APIs fail.

---

## Practice Task 2: Configure env and CORS

Create/update:

```txt
client/.env
client/.env.example
server/.env
docs/ENV_AND_CORS_CHECKLIST.md
```

Restart both servers after env changes.

---

## Practice Task 3: Create API client

Create:

```txt
client/src/lib/api.ts
client/src/types/api.ts
```

Test with one API first:

```txt
GET /foods
```

---

## Practice Task 4: Connect auth

Connect:

```txt
register
login
logout
token persistence
protected route
admin route
```

Verify:

```txt
1. Register works
2. Login works
3. Logout works
4. Refresh keeps user logged in
5. Protected route blocks visitor
6. Admin route blocks customer
```

---

## Practice Task 5: Connect food pages

Connect:

```txt
MenuPage
FoodDetailsPage
```

Verify:

```txt
Foods are coming from MongoDB, not mock data.
```

---

## Practice Task 6: Connect customer order flow

Connect:

```txt
CheckoutPage
MyOrdersPage
```

Verify:

```txt
Order is created and visible in My Orders.
```

---

## Practice Task 7: Connect admin flow

Connect:

```txt
ManageFoodsPage
ManageOrdersPage
```

Verify:

```txt
Admin can manage food and order status.
Customer cannot.
```

---

## Practice Task 8: Run browser QA

Complete:

```txt
docs/FULLSTACK_BROWSER_QA_REPORT.md
```

Include:

```txt
1. Desktop screenshots
2. Mobile screenshots
3. Network tab evidence
4. Console error notes
5. Bugs found
6. Fixes applied
```

---

## Practice Task 9: Create integration bug log

Complete:

```txt
docs/INTEGRATION_BUG_LOG.md
```

Record at least 3 issues, even if they are minor.

Example:

```txt
Loading state missing
Error message unclear
Price sent as string
Token not sent
CORS origin mismatch
```

---

## Practice Task 10: Final cleanup

Before finishing:

```txt
1. Remove unused mock data from connected pages
2. Keep mock data only where intentionally used
3. Remove console.logs
4. Check env examples
5. Check no secrets committed
6. Update README integration notes
```

---

# Part 28: Common integration bugs and fixes

## Bug 1: CORS blocked by browser

Symptom:

```txt
Access to fetch at ... has been blocked by CORS policy
```

Fix:

```txt
1. Check server CLIENT_URL
2. Check frontend URL exactly
3. Restart backend
4. Ensure cors middleware runs before routes
```

---

## Bug 2: VITE_API_BASE_URL undefined

Symptom:

```txt
VITE_API_BASE_URL is not defined
```

Fix:

```txt
1. Create client/.env
2. Add VITE_API_BASE_URL=http://localhost:5000/api
3. Restart frontend dev server
4. Check spelling
```

---

## Bug 3: 401 Authentication required

Cause:

```txt
Token missing or Authorization header not sent.
```

Fix:

```txt
Check apiRequest token option.
Check AuthContext token.
Check localStorage.
```

---

## Bug 4: 403 Forbidden

Cause:

```txt
User is logged in but not admin.
```

Fix:

```txt
Check user role.
Check admin account in database.
Check backend requireRole("admin").
```

---

## Bug 5: Food list blank

Cause:

```txt
Frontend expects array but backend returns { success, message, data }.
```

Fix:

```txt
API client should return json.data.
```

---

## Bug 6: Zod validation fails on price

Cause:

```txt
HTML input gives string.
Backend expects number.
```

Fix:

```ts
price: Number(form.price)
```

---

## Bug 7: Order validation fails

Cause:

```txt
Cart item shape does not match backend schema.
```

Fix:

```txt
Ensure items contain foodId, name, quantity, price.
```

---

## Bug 8: Refresh logs user out

Cause:

```txt
AuthContext not loading localStorage initially.
```

Fix:

```txt
Create loadInitialAuth() and initialize state from localStorage.
```

---

## Bug 9: Deployed frontend calls localhost

Cause:

```txt
VITE_API_BASE_URL in production still points to localhost.
```

Fix:

```txt
Set production frontend env variable to deployed backend API URL.
Rebuild/redeploy frontend.
```

---

## Bug 10: Backend deployed but frontend blocked

Cause:

```txt
Backend CLIENT_URL still points to localhost.
```

Fix:

```txt
Set backend CLIENT_URL to deployed frontend URL.
Redeploy backend.
```

---

# Part 29: Quality bar

Minimum passing standard:

```txt
1. Register/login works with backend.
2. Token persists after refresh.
3. Foods load from backend.
4. Food details load from backend.
5. Cart can create real order.
6. My orders shows backend orders.
7. Admin can create/update/delete food.
8. Admin can view/update orders.
9. Customer cannot access admin routes.
10. Full browser QA report completed.
```

Strong standard:

```txt
1. Loading/error/empty states exist on all connected pages.
2. Network errors are user-friendly.
3. API services are cleanly separated.
4. Response data shape decisions are documented.
5. Integration bug log shows clear learning.
6. No major console errors.
7. Mobile layout still works after integration.
```

Advanced standard:

```txt
1. TanStack Query used for server state.
2. Mutations invalidate relevant queries.
3. API errors are normalized.
4. Token expiration is handled.
5. Admin forms have better validation.
6. Optimistic UI used only where safe.
```

---

# Required deliverables for this module

Submit:

```txt
1. client/.env.example
2. server/.env.example
3. client/src/lib/api.ts
4. client/src/services/authService.ts
5. client/src/services/foodService.ts
6. client/src/services/orderService.ts
7. Updated AuthContext
8. Connected LoginPage
9. Connected RegisterPage
10. Connected MenuPage
11. Connected FoodDetailsPage
12. Connected CheckoutPage
13. Connected MyOrdersPage
14. Connected ManageFoodsPage
15. Connected ManageOrdersPage
16. Updated route guards
17. FULLSTACK_INTEGRATION_PLAN.md
18. API_CLIENT_PLAN.md
19. AUTH_INTEGRATION_PLAN.md
20. ENV_AND_CORS_CHECKLIST.md
21. FULLSTACK_FLOW_TEST_PLAN.md
22. FULLSTACK_BROWSER_QA_REPORT.md
23. INTEGRATION_BUG_LOG.md
24. API_DATA_SHAPE_DECISIONS.md
25. Desktop screenshots
26. Mobile screenshots
27. Network tab screenshots
28. NotebookLM Study Guide screenshot
29. NotebookLM bug diagnosis screenshot
30. Video learning notes
31. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/10-module-08-fullstack-integration-reflection.md
```

Use this format:

```md
# Reflection: Module 8 - Full-Stack Integration

## What I connected
-

## APIs I connected
-

## Pages I updated
-

## What I learned about API clients
-

## What I learned about auth tokens
-

## What I learned about CORS
-

## What I learned about env variables
-

## What integration bugs I faced
-

## How I fixed them
-

## What Antigravity helped with
-

## What I had to fix manually
-

## What I will improve before testing/deployment
-
```

---

# Quiz

## Multiple choice

**1. What is the safest integration approach?**

A. Connect the whole app at once  
B. Connect one flow/API at a time and verify after each step  
C. Skip backend testing  
D. Remove auth  

Correct answer: **B**

---

**2. What should frontend Vite env variables start with?**

A. `SECRET_`  
B. `VITE_`  
C. `PRIVATE_`  
D. `MONGO_`  

Correct answer: **B**

---

**3. What causes many CORS errors during local development?**

A. Frontend and backend running on different origins  
B. Tailwind classes  
C. README file  
D. MongoDB collection name  

Correct answer: **A**

---

**4. What should the API client do with the auth token?**

A. Send it in `Authorization: Bearer <token>` when needed  
B. Print it publicly  
C. Store it in CSS  
D. Send it as food price  

Correct answer: **A**

---

**5. Why might a food list appear blank after connection?**

A. Frontend expects direct array but backend returns nested response data  
B. Navbar is blue  
C. Button has border radius  
D. Footer exists  

Correct answer: **A**

---

**6. What should happen when a customer accesses admin APIs?**

A. Backend should return 403 Forbidden  
B. Backend should allow access  
C. Frontend should expose all data  
D. Password should be returned  

Correct answer: **A**

---

**7. Why can price validation fail?**

A. HTML input sends string but backend expects number  
B. MongoDB does not store numbers  
C. React cannot show prices  
D. Tailwind blocks prices  

Correct answer: **A**

---

**8. What should you do after changing `.env` in Vite?**

A. Restart the frontend dev server  
B. Delete React  
C. Reinstall MongoDB  
D. Ignore it  

Correct answer: **A**

---

**9. What should `FULLSTACK_BROWSER_QA_REPORT.md` include?**

A. Tested flows, console/network errors, CORS issues, bugs, fixes, verdict  
B. Only project title  
C. Only GitHub username  
D. Only color palette  

Correct answer: **A**

---

**10. What should be avoided during integration bug fixing?**

A. Adding random new features while fixing critical bugs  
B. Checking network tab  
C. Checking console errors  
D. Updating bug log  

Correct answer: **A**

---

## Short-answer questions

1. What is full-stack integration?
2. Why should backend APIs be tested before frontend integration?
3. What is the purpose of `VITE_API_BASE_URL`?
4. What is CORS?
5. Why do we need an API client?
6. How is the JWT token sent to protected APIs?
7. What is one common API response shape bug?
8. What is one common auth integration bug?
9. What full-stack flows did you test?
10. What integration bug did you fix and what did you learn?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Backend readiness | Backend APIs tested manually |
| Frontend readiness | Frontend pages work before integration |
| Env setup | Frontend/backend env configured |
| CORS | Browser can call backend without CORS block |
| API client | Central API client exists |
| Auth service | Register/login connected |
| Auth persistence | Token/user persist after refresh |
| Route guards | Protected/admin routes work |
| Food APIs | Menu/details connected to backend |
| Order APIs | Checkout/my-orders connected |
| Admin food | Admin create/update/delete connected |
| Admin orders | Admin all orders/status update connected |
| Authorization | Customer blocked from admin flow |
| UI states | Loading/error/empty states exist |
| Bug log | Integration bugs documented |
| Browser QA | Full user/admin flows verified |
| NotebookLM evidence | Study guide and bug diagnosis submitted |
| Reflection | Student explains integration clearly |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can connect a React frontend with an Express/MongoDB backend using a central API client, environment variables, CORS configuration, JWT authentication, protected routes, real food/order/admin APIs, loading/error/empty states, and full browser verification.
```

After completing this file, continue to:

```txt
11-module-09-testing-browser-verification-qa.md
```
