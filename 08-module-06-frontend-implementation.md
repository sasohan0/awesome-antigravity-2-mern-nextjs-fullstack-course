# Module 6: Frontend Implementation — Build the React/Tailwind UI with Antigravity

**File Name:** `08-module-06-frontend-implementation.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 6–9 hours  
**Recommended After:** Module 5 / Bonus Module 5.5  
**Main Goal:** Build the frontend foundation of a MERN project using React, TypeScript, Tailwind CSS, routing, reusable components, mock data, UI states, and Antigravity-assisted implementation.

---

## Module purpose

In the previous modules, you prepared the project properly:

- You learned the Antigravity workflow.
- You learned NotebookLM learning workflow.
- You created project specs.
- You created architecture docs.
- You created `SKILL.md` files.
- You learned Figma-to-code workflow.
- You optionally practiced UI replication.

Now you will start building the actual frontend.

This module focuses only on the frontend.

You will build:

```txt
client/
  React + TypeScript + Tailwind frontend
```

You will not build the backend in this module.

You will use mock data first so that you can design and test the frontend without waiting for APIs.

Backend integration will happen later.

---

## Why frontend-first with mock data?

Many junior developers try to build frontend and backend at the same time.

That often creates confusion:

- UI is incomplete.
- Backend routes are incomplete.
- API response format changes.
- Students do not know whether the bug is frontend or backend.
- Antigravity changes too many files at once.

Frontend-first with mock data helps you:

- Build pages faster.
- Validate design and layout.
- Create reusable components.
- Understand required data shapes.
- Prepare API integration later.
- Keep scope controlled.
- Use Antigravity safely.

The rule for this module:

```txt
Build the frontend shell and screens first using mock data.
Do not connect real APIs yet.
```

---

## What you will build in this module

Using the example project **LocalBites**, you will build:

| Area | Pages/components |
|---|---|
| Layout | Navbar, Footer, PageContainer, DashboardLayout |
| Public pages | Home, Menu, Food Details |
| Auth pages | Login, Register |
| Customer pages | Cart, Checkout, My Orders |
| Admin pages | Admin Dashboard, Manage Foods, Manage Orders |
| Shared UI | Button, Card, Badge, Input, Select, Modal optional |
| UI states | Loading, Empty, Error, Unauthorized, Not Found |
| Data | Mock foods, mock users, mock orders |
| Routing | Public routes, protected routes, admin routes |
| State | Auth context, cart context/localStorage |
| Docs | Frontend implementation notes and browser QA |

This module does **not** require backend APIs yet.

---

## Expected frontend stack

Recommended stack:

```txt
React
Vite
TypeScript
Tailwind CSS
React Router
Context API
Optional: TanStack Query later
Optional: React Hook Form later
Optional: Zod later
```

For beginners, keep it simple.

Do not install too many packages at once.

---

## Frontend implementation principle

Use this principle:

```txt
Design docs → Mock data → Components → Pages → Routes → State → UI states → Browser verification
```

Do not jump directly into a full page.

---

# Part 1: Frontend setup

## Create frontend app

From the project root:

```bash
npm create vite@latest client
```

Choose:

```txt
React
TypeScript
```

Then:

```bash
cd client
npm install
npm run dev
```

Expected local URL:

```txt
http://localhost:5173
```

---

## Install Tailwind CSS

Use the current Tailwind + Vite workflow.

Install:

```bash
npm install tailwindcss @tailwindcss/vite
```

Update `vite.config.ts`:

```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

Update your main CSS file:

```css
@import "tailwindcss";
```

Run:

```bash
npm run dev
```

Test Tailwind:

```tsx
<h1 className="text-4xl font-bold text-blue-600">
  Tailwind is working
</h1>
```

---

## Install React Router

```bash
npm install react-router
```

If your project needs DOM router utilities and the current package setup requires it, follow the latest React Router docs.

For this module, routing goal is simple:

```txt
/           Home
/menu       Menu
/menu/:id   Food Details
/login      Login
/register   Register
/cart       Cart
/checkout   Checkout
/my-orders  My Orders
/admin      Admin Dashboard
/admin/foods Manage Foods
/admin/orders Manage Orders
```

---

## Recommended frontend folder structure

Create this structure:

```txt
client/
  src/
    assets/
    components/
      common/
      layout/
      food/
      cart/
      auth/
      admin/
      states/
    pages/
      public/
      auth/
      customer/
      admin/
    routes/
      AppRoutes.tsx
      ProtectedRoute.tsx
      AdminRoute.tsx
    data/
      mockFoods.ts
      mockOrders.ts
      mockUsers.ts
    context/
      AuthContext.tsx
      CartContext.tsx
    hooks/
    lib/
      formatCurrency.ts
      cn.ts
    services/
      mockAuthService.ts
      mockFoodService.ts
      mockOrderService.ts
    types/
      user.ts
      food.ts
      order.ts
      api.ts
    styles/
    App.tsx
    main.tsx
```

This structure keeps the code readable.

---

# Part 2: Frontend types

Before building components, define types.

Create:

```txt
client/src/types/food.ts
```

```ts
export type FoodCategory =
  | "Burger"
  | "Pizza"
  | "Rice"
  | "Dessert"
  | "Drink";

export type Food = {
  id: string;
  name: string;
  description: string;
  price: number;
  category: FoodCategory;
  image: string;
  isAvailable: boolean;
  rating?: number;
};
```

Create:

```txt
client/src/types/user.ts
```

```ts
export type UserRole = "customer" | "admin";

export type User = {
  id: string;
  name: string;
  email: string;
  role: UserRole;
};
```

Create:

```txt
client/src/types/order.ts
```

```ts
export type OrderStatus =
  | "pending"
  | "confirmed"
  | "preparing"
  | "delivered"
  | "cancelled";

export type OrderItem = {
  foodId: string;
  name: string;
  price: number;
  quantity: number;
};

export type Order = {
  id: string;
  userId: string;
  items: OrderItem[];
  totalPrice: number;
  deliveryAddress: string;
  phone: string;
  status: OrderStatus;
  createdAt: string;
};
```

Create:

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

---

## Why types matter

Types help Antigravity and developers understand:

- What data a component expects
- What mock data should contain
- What API integration will need later
- What props should be passed
- What errors TypeScript should catch

Do not skip types.

---

# Part 3: Mock data

Create:

```txt
client/src/data/mockFoods.ts
```

Example:

```ts
import type { Food } from "../types/food";

export const mockFoods: Food[] = [
  {
    id: "food-1",
    name: "Classic Chicken Burger",
    description: "Grilled chicken patty with fresh lettuce, tomato, and house sauce.",
    price: 250,
    category: "Burger",
    image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd",
    isAvailable: true,
    rating: 4.7,
  },
  {
    id: "food-2",
    name: "Cheese Pizza",
    description: "Crispy crust pizza with mozzarella cheese and rich tomato sauce.",
    price: 520,
    category: "Pizza",
    image: "https://images.unsplash.com/photo-1513104890138-7c749659a591",
    isAvailable: true,
    rating: 4.6,
  },
  {
    id: "food-3",
    name: "Chicken Biryani",
    description: "Aromatic rice with tender chicken and traditional spices.",
    price: 320,
    category: "Rice",
    image: "https://images.unsplash.com/photo-1563379091339-03246963d51a",
    isAvailable: true,
    rating: 4.8,
  },
];
```

Create:

```txt
client/src/data/mockOrders.ts
```

Example:

```ts
import type { Order } from "../types/order";

export const mockOrders: Order[] = [
  {
    id: "order-1",
    userId: "user-1",
    items: [
      {
        foodId: "food-1",
        name: "Classic Chicken Burger",
        price: 250,
        quantity: 2,
      },
    ],
    totalPrice: 500,
    deliveryAddress: "Dhaka, Bangladesh",
    phone: "01700000000",
    status: "pending",
    createdAt: new Date().toISOString(),
  },
];
```

---

## Mock data rules

Mock data should match your future API response shape.

Do not create random frontend-only data that backend cannot support later.

Ask:

```txt
Will this mock data shape match API_CONTRACT.md and DATABASE_SCHEMA.md?
```

If not, update the docs or mock data.

---

# Part 4: Shared utility functions

Create:

```txt
client/src/lib/formatCurrency.ts
```

```ts
export function formatCurrency(amount: number): string {
  return `৳${amount.toLocaleString("en-BD")}`;
}
```

Create:

```txt
client/src/lib/cn.ts
```

```ts
export function cn(...classes: Array<string | false | null | undefined>) {
  return classes.filter(Boolean).join(" ");
}
```

These small utilities keep components clean.

---

# Part 5: Common UI components

Create reusable components first.

## Button component

Create:

```txt
client/src/components/common/Button.tsx
```

Example:

```tsx
import type { ButtonHTMLAttributes, ReactNode } from "react";
import { cn } from "../../lib/cn";

type ButtonVariant = "primary" | "secondary" | "ghost" | "danger";

type ButtonProps = ButtonHTMLAttributes<HTMLButtonElement> & {
  children: ReactNode;
  variant?: ButtonVariant;
};

const variantClasses: Record<ButtonVariant, string> = {
  primary: "bg-orange-500 text-white hover:bg-orange-600",
  secondary: "bg-gray-900 text-white hover:bg-gray-800",
  ghost: "bg-transparent text-gray-700 hover:bg-gray-100",
  danger: "bg-red-500 text-white hover:bg-red-600",
};

export function Button({
  children,
  variant = "primary",
  className,
  ...props
}: ButtonProps) {
  return (
    <button
      className={cn(
        "inline-flex items-center justify-center rounded-xl px-4 py-2 text-sm font-semibold transition disabled:cursor-not-allowed disabled:opacity-60",
        variantClasses[variant],
        className
      )}
      {...props}
    >
      {children}
    </button>
  );
}
```

---

## Card component

Create:

```txt
client/src/components/common/Card.tsx
```

```tsx
import type { ReactNode } from "react";
import { cn } from "../../lib/cn";

type CardProps = {
  children: ReactNode;
  className?: string;
};

export function Card({ children, className }: CardProps) {
  return (
    <div
      className={cn(
        "rounded-2xl border border-gray-200 bg-white p-5 shadow-sm",
        className
      )}
    >
      {children}
    </div>
  );
}
```

---

## Badge component

Create:

```txt
client/src/components/common/Badge.tsx
```

```tsx
import type { ReactNode } from "react";
import { cn } from "../../lib/cn";

type BadgeProps = {
  children: ReactNode;
  className?: string;
};

export function Badge({ children, className }: BadgeProps) {
  return (
    <span
      className={cn(
        "inline-flex rounded-full bg-orange-50 px-3 py-1 text-xs font-semibold text-orange-600",
        className
      )}
    >
      {children}
    </span>
  );
}
```

---

## Input component

Create:

```txt
client/src/components/common/Input.tsx
```

```tsx
import type { InputHTMLAttributes } from "react";
import { cn } from "../../lib/cn";

type InputProps = InputHTMLAttributes<HTMLInputElement> & {
  label?: string;
  error?: string;
};

export function Input({ label, error, className, id, ...props }: InputProps) {
  return (
    <label className="block">
      {label && (
        <span className="mb-1 block text-sm font-medium text-gray-700">
          {label}
        </span>
      )}
      <input
        id={id}
        className={cn(
          "w-full rounded-xl border border-gray-300 px-4 py-2 outline-none transition focus:border-orange-500 focus:ring-2 focus:ring-orange-100",
          error && "border-red-500 focus:border-red-500 focus:ring-red-100",
          className
        )}
        {...props}
      />
      {error && <span className="mt-1 block text-sm text-red-600">{error}</span>}
    </label>
  );
}
```

---

# Part 6: UI state components

Every professional app needs UI states.

Create:

```txt
client/src/components/states/LoadingState.tsx
```

```tsx
export function LoadingState({ message = "Loading..." }: { message?: string }) {
  return (
    <div className="flex min-h-40 items-center justify-center rounded-2xl border border-dashed border-gray-300 p-8 text-gray-500">
      {message}
    </div>
  );
}
```

Create:

```txt
client/src/components/states/EmptyState.tsx
```

```tsx
type EmptyStateProps = {
  title: string;
  message: string;
};

export function EmptyState({ title, message }: EmptyStateProps) {
  return (
    <div className="rounded-2xl border border-dashed border-gray-300 p-8 text-center">
      <h3 className="text-lg font-semibold text-gray-900">{title}</h3>
      <p className="mt-2 text-sm text-gray-500">{message}</p>
    </div>
  );
}
```

Create:

```txt
client/src/components/states/ErrorState.tsx
```

```tsx
type ErrorStateProps = {
  title?: string;
  message: string;
};

export function ErrorState({
  title = "Something went wrong",
  message,
}: ErrorStateProps) {
  return (
    <div className="rounded-2xl border border-red-200 bg-red-50 p-6 text-red-700">
      <h3 className="font-semibold">{title}</h3>
      <p className="mt-1 text-sm">{message}</p>
    </div>
  );
}
```

---

# Part 7: Layout components

## Navbar

Create:

```txt
client/src/components/layout/Navbar.tsx
```

Navbar requirements:

- Logo/brand
- Home link
- Menu link
- Cart link
- Login/logout area
- Admin link only for admin user
- Mobile-friendly layout

Simple structure:

```tsx
import { Link, NavLink } from "react-router";
import { Button } from "../common/Button";
import { useAuth } from "../../context/AuthContext";
import { useCart } from "../../context/CartContext";

const navLinkClass = ({ isActive }: { isActive: boolean }) =>
  isActive
    ? "text-orange-600 font-semibold"
    : "text-gray-600 hover:text-orange-600";

export function Navbar() {
  const { user, logout } = useAuth();
  const { totalItems } = useCart();

  return (
    <header className="sticky top-0 z-50 border-b border-gray-200 bg-white/90 backdrop-blur">
      <div className="mx-auto flex h-16 max-w-6xl items-center justify-between px-4">
        <Link to="/" className="text-xl font-bold text-gray-900">
          LocalBites
        </Link>

        <nav className="hidden items-center gap-6 md:flex">
          <NavLink to="/" className={navLinkClass}>Home</NavLink>
          <NavLink to="/menu" className={navLinkClass}>Menu</NavLink>
          <NavLink to="/cart" className={navLinkClass}>
            Cart ({totalItems})
          </NavLink>
          {user?.role === "admin" && (
            <NavLink to="/admin" className={navLinkClass}>Admin</NavLink>
          )}
        </nav>

        <div className="flex items-center gap-3">
          {user ? (
            <Button variant="ghost" onClick={logout}>Logout</Button>
          ) : (
            <Link to="/login">
              <Button>Login</Button>
            </Link>
          )}
        </div>
      </div>
    </header>
  );
}
```

---

## Footer

Create:

```txt
client/src/components/layout/Footer.tsx
```

```tsx
export function Footer() {
  return (
    <footer className="border-t border-gray-200 bg-gray-50">
      <div className="mx-auto max-w-6xl px-4 py-8 text-sm text-gray-500">
        <p>© {new Date().getFullYear()} LocalBites. Built for MERN practice.</p>
      </div>
    </footer>
  );
}
```

---

## Main layout

Create:

```txt
client/src/components/layout/MainLayout.tsx
```

```tsx
import { Outlet } from "react-router";
import { Navbar } from "./Navbar";
import { Footer } from "./Footer";

export function MainLayout() {
  return (
    <div className="min-h-screen bg-white text-gray-900">
      <Navbar />
      <main>
        <Outlet />
      </main>
      <Footer />
    </div>
  );
}
```

---

## Dashboard layout

Create:

```txt
client/src/components/layout/DashboardLayout.tsx
```

```tsx
import { NavLink, Outlet } from "react-router";

const linkClass = ({ isActive }: { isActive: boolean }) =>
  isActive
    ? "rounded-xl bg-orange-500 px-4 py-2 font-semibold text-white"
    : "rounded-xl px-4 py-2 text-gray-600 hover:bg-gray-100";

export function DashboardLayout() {
  return (
    <div className="mx-auto grid min-h-[70vh] max-w-6xl gap-6 px-4 py-8 md:grid-cols-[240px_1fr]">
      <aside className="rounded-2xl border border-gray-200 bg-white p-4 shadow-sm">
        <nav className="flex flex-col gap-2">
          <NavLink to="/admin" end className={linkClass}>Overview</NavLink>
          <NavLink to="/admin/foods" className={linkClass}>Foods</NavLink>
          <NavLink to="/admin/orders" className={linkClass}>Orders</NavLink>
        </nav>
      </aside>

      <section>
        <Outlet />
      </section>
    </div>
  );
}
```

---

# Part 8: Auth context

Create:

```txt
client/src/context/AuthContext.tsx
```

Basic mock version:

```tsx
import {
  createContext,
  useContext,
  useMemo,
  useState,
  type ReactNode,
} from "react";
import type { User } from "../types/user";

type AuthContextValue = {
  user: User | null;
  loginAsCustomer: () => void;
  loginAsAdmin: () => void;
  logout: () => void;
};

const AuthContext = createContext<AuthContextValue | null>(null);

const customerUser: User = {
  id: "user-1",
  name: "Customer User",
  email: "customer@example.com",
  role: "customer",
};

const adminUser: User = {
  id: "admin-1",
  name: "Admin User",
  email: "admin@example.com",
  role: "admin",
};

export function AuthProvider({ children }: { children: ReactNode }) {
  const [user, setUser] = useState<User | null>(customerUser);

  const value = useMemo<AuthContextValue>(
    () => ({
      user,
      loginAsCustomer: () => setUser(customerUser),
      loginAsAdmin: () => setUser(adminUser),
      logout: () => setUser(null),
    }),
    [user]
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

This is mock auth.

Real JWT auth will be added later.

---

# Part 9: Cart context

Create:

```txt
client/src/context/CartContext.tsx
```

Basic version:

```tsx
import {
  createContext,
  useContext,
  useMemo,
  useState,
  type ReactNode,
} from "react";
import type { Food } from "../types/food";

export type CartItem = {
  foodId: string;
  name: string;
  price: number;
  quantity: number;
};

type CartContextValue = {
  items: CartItem[];
  totalItems: number;
  totalPrice: number;
  addToCart: (food: Food) => void;
  removeFromCart: (foodId: string) => void;
  updateQuantity: (foodId: string, quantity: number) => void;
  clearCart: () => void;
};

const CartContext = createContext<CartContextValue | null>(null);

export function CartProvider({ children }: { children: ReactNode }) {
  const [items, setItems] = useState<CartItem[]>([]);

  const addToCart = (food: Food) => {
    setItems((current) => {
      const existing = current.find((item) => item.foodId === food.id);

      if (existing) {
        return current.map((item) =>
          item.foodId === food.id
            ? { ...item, quantity: item.quantity + 1 }
            : item
        );
      }

      return [
        ...current,
        {
          foodId: food.id,
          name: food.name,
          price: food.price,
          quantity: 1,
        },
      ];
    });
  };

  const removeFromCart = (foodId: string) => {
    setItems((current) => current.filter((item) => item.foodId !== foodId));
  };

  const updateQuantity = (foodId: string, quantity: number) => {
    if (quantity <= 0) {
      removeFromCart(foodId);
      return;
    }

    setItems((current) =>
      current.map((item) =>
        item.foodId === foodId ? { ...item, quantity } : item
      )
    );
  };

  const clearCart = () => setItems([]);

  const totalItems = items.reduce((sum, item) => sum + item.quantity, 0);
  const totalPrice = items.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );

  const value = useMemo<CartContextValue>(
    () => ({
      items,
      totalItems,
      totalPrice,
      addToCart,
      removeFromCart,
      updateQuantity,
      clearCart,
    }),
    [items, totalItems, totalPrice]
  );

  return <CartContext.Provider value={value}>{children}</CartContext.Provider>;
}

export function useCart() {
  const context = useContext(CartContext);

  if (!context) {
    throw new Error("useCart must be used inside CartProvider");
  }

  return context;
}
```

Later, you can persist cart to localStorage.

---

# Part 10: Route guards

## Protected route

Create:

```txt
client/src/routes/ProtectedRoute.tsx
```

```tsx
import { Navigate, Outlet, useLocation } from "react-router";
import { useAuth } from "../context/AuthContext";

export function ProtectedRoute() {
  const { user } = useAuth();
  const location = useLocation();

  if (!user) {
    return <Navigate to="/login" state={{ from: location }} replace />;
  }

  return <Outlet />;
}
```

## Admin route

Create:

```txt
client/src/routes/AdminRoute.tsx
```

```tsx
import { Navigate, Outlet } from "react-router";
import { useAuth } from "../context/AuthContext";

export function AdminRoute() {
  const { user } = useAuth();

  if (!user) {
    return <Navigate to="/login" replace />;
  }

  if (user.role !== "admin") {
    return <Navigate to="/unauthorized" replace />;
  }

  return <Outlet />;
}
```

Important:

```txt
Frontend route guards are for UI protection only.
Backend must still enforce security later.
```

---

# Part 11: App routes

Create:

```txt
client/src/routes/AppRoutes.tsx
```

```tsx
import { createBrowserRouter, RouterProvider } from "react-router";
import { MainLayout } from "../components/layout/MainLayout";
import { DashboardLayout } from "../components/layout/DashboardLayout";
import { ProtectedRoute } from "./ProtectedRoute";
import { AdminRoute } from "./AdminRoute";

import { HomePage } from "../pages/public/HomePage";
import { MenuPage } from "../pages/public/MenuPage";
import { FoodDetailsPage } from "../pages/public/FoodDetailsPage";
import { LoginPage } from "../pages/auth/LoginPage";
import { RegisterPage } from "../pages/auth/RegisterPage";
import { CartPage } from "../pages/customer/CartPage";
import { CheckoutPage } from "../pages/customer/CheckoutPage";
import { MyOrdersPage } from "../pages/customer/MyOrdersPage";
import { AdminOverviewPage } from "../pages/admin/AdminOverviewPage";
import { ManageFoodsPage } from "../pages/admin/ManageFoodsPage";
import { ManageOrdersPage } from "../pages/admin/ManageOrdersPage";
import { UnauthorizedPage } from "../pages/public/UnauthorizedPage";
import { NotFoundPage } from "../pages/public/NotFoundPage";

const router = createBrowserRouter([
  {
    element: <MainLayout />,
    children: [
      { path: "/", element: <HomePage /> },
      { path: "/menu", element: <MenuPage /> },
      { path: "/menu/:id", element: <FoodDetailsPage /> },
      { path: "/login", element: <LoginPage /> },
      { path: "/register", element: <RegisterPage /> },
      { path: "/unauthorized", element: <UnauthorizedPage /> },
      {
        element: <ProtectedRoute />,
        children: [
          { path: "/cart", element: <CartPage /> },
          { path: "/checkout", element: <CheckoutPage /> },
          { path: "/my-orders", element: <MyOrdersPage /> },
        ],
      },
      {
        element: <AdminRoute />,
        children: [
          {
            path: "/admin",
            element: <DashboardLayout />,
            children: [
              { index: true, element: <AdminOverviewPage /> },
              { path: "foods", element: <ManageFoodsPage /> },
              { path: "orders", element: <ManageOrdersPage /> },
            ],
          },
        ],
      },
      { path: "*", element: <NotFoundPage /> },
    ],
  },
]);

export function AppRoutes() {
  return <RouterProvider router={router} />;
}
```

---

## App provider setup

Update:

```txt
client/src/App.tsx
```

```tsx
import { AppRoutes } from "./routes/AppRoutes";
import { AuthProvider } from "./context/AuthContext";
import { CartProvider } from "./context/CartContext";

export default function App() {
  return (
    <AuthProvider>
      <CartProvider>
        <AppRoutes />
      </CartProvider>
    </AuthProvider>
  );
}
```

---

# Part 12: Public pages

## Home page

Create:

```txt
client/src/pages/public/HomePage.tsx
```

Requirements:

- Hero section
- CTA to menu
- Featured foods
- How it works
- Responsive layout

Antigravity prompt:

```txt
Read:
- docs/DESIGN_SYSTEM.md
- docs/UI_SPEC.md
- docs/COMPONENT_MAP.md

Implement only HomePage with:
1. Hero section
2. CTA buttons
3. Featured food cards using mockFoods
4. How it works section

Rules:
- Use React + TypeScript + Tailwind.
- Do not edit backend.
- Do not create real API calls.
- Use mock data only.
- Keep components reusable.
```

---

## Menu page

Create:

```txt
client/src/pages/public/MenuPage.tsx
```

Requirements:

- Search input
- Category filter
- Food grid
- Empty state
- Add to cart button
- Details link

Possible component breakdown:

```txt
MenuPage
  ├── MenuHeader
  ├── FoodFilters
  ├── FoodGrid
  │     └── FoodCard
  └── EmptyState
```

---

## Food card

Create:

```txt
client/src/components/food/FoodCard.tsx
```

Requirements:

- Image
- Name
- Description
- Price
- Category badge
- Rating optional
- Add to cart
- View details

---

## Food details page

Create:

```txt
client/src/pages/public/FoodDetailsPage.tsx
```

Requirements:

- Read food ID from route params
- Find food from mockFoods
- Show not found if missing
- Add to cart button
- Back to menu link

---

# Part 13: Auth pages

## Login page

Create:

```txt
client/src/pages/auth/LoginPage.tsx
```

Since this module uses mock auth, login page can include:

- Email input
- Password input
- Login as Customer button
- Login as Admin button
- Link to register

Important note:

```txt
This is mock auth only.
Real JWT login will be added after backend implementation.
```

---

## Register page

Create:

```txt
client/src/pages/auth/RegisterPage.tsx
```

Requirements:

- Name input
- Email input
- Password input
- Confirm password input
- Register button
- Link to login
- Mock success message or redirect

---

# Part 14: Customer pages

## Cart page

Create:

```txt
client/src/pages/customer/CartPage.tsx
```

Requirements:

- Show cart items
- Increase quantity
- Decrease quantity
- Remove item
- Show total price
- Continue shopping link
- Checkout button
- Empty cart state

---

## Checkout page

Create:

```txt
client/src/pages/customer/CheckoutPage.tsx
```

Requirements:

- Delivery address
- Phone number
- Order summary
- Place order button
- Empty cart protection
- Mock success state
- Clear cart after order optional

---

## My Orders page

Create:

```txt
client/src/pages/customer/MyOrdersPage.tsx
```

Requirements:

- Show mock orders for current user
- Show status badge
- Show order items
- Empty state if no orders

---

# Part 15: Admin pages

## Admin overview

Create:

```txt
client/src/pages/admin/AdminOverviewPage.tsx
```

Requirements:

- Dashboard cards
- Total foods
- Total orders
- Pending orders
- Revenue mock calculation

---

## Manage foods

Create:

```txt
client/src/pages/admin/ManageFoodsPage.tsx
```

Requirements:

- Food table
- Add food form/modal optional
- Edit/delete buttons as mock UI
- Availability badge
- Search/filter optional

No real backend mutation yet.

Use mock UI.

---

## Manage orders

Create:

```txt
client/src/pages/admin/ManageOrdersPage.tsx
```

Requirements:

- Order table
- Status badge
- Customer/user ID
- Total price
- Change status dropdown as mock UI
- Empty state

---

# Part 16: Unauthorized and Not Found pages

Create:

```txt
client/src/pages/public/UnauthorizedPage.tsx
```

```tsx
import { Link } from "react-router";
import { Button } from "../../components/common/Button";

export function UnauthorizedPage() {
  return (
    <section className="mx-auto max-w-3xl px-4 py-24 text-center">
      <h1 className="text-3xl font-bold text-gray-900">Access denied</h1>
      <p className="mt-3 text-gray-600">
        You do not have permission to access this page.
      </p>
      <Link to="/" className="mt-6 inline-block">
        <Button>Go home</Button>
      </Link>
    </section>
  );
}
```

Create:

```txt
client/src/pages/public/NotFoundPage.tsx
```

```tsx
import { Link } from "react-router";
import { Button } from "../../components/common/Button";

export function NotFoundPage() {
  return (
    <section className="mx-auto max-w-3xl px-4 py-24 text-center">
      <h1 className="text-3xl font-bold text-gray-900">Page not found</h1>
      <p className="mt-3 text-gray-600">
        The page you are looking for does not exist.
      </p>
      <Link to="/" className="mt-6 inline-block">
        <Button>Go home</Button>
      </Link>
    </section>
  );
}
```

---

# Part 17: Frontend documentation files

Create these docs:

```txt
docs/FRONTEND_IMPLEMENTATION_PLAN.md
docs/FRONTEND_COMPONENT_TREE.md
docs/MOCK_DATA_PLAN.md
docs/FRONTEND_STATE_PLAN.md
docs/FRONTEND_ROUTE_TEST_PLAN.md
docs/FRONTEND_BROWSER_QA_REPORT.md
```

---

## `FRONTEND_IMPLEMENTATION_PLAN.md`

Template:

```md
# Frontend Implementation Plan

## Stack
- React
- Vite
- TypeScript
- Tailwind CSS
- React Router

## Implementation order
1. Setup Vite + React + TypeScript
2. Install/configure Tailwind
3. Create folder structure
4. Create types
5. Create mock data
6. Create common components
7. Create layout
8. Create contexts
9. Create routes
10. Create public pages
11. Create auth pages
12. Create customer pages
13. Create admin pages
14. Add UI states
15. Run browser verification

## Rules
- Use mock data only
- No real API integration yet
- Do not create backend files
- Keep components reusable
- Verify every route
```

---

## `FRONTEND_COMPONENT_TREE.md`

Template:

```md
# Frontend Component Tree

## Main app

```txt
App
  └── AuthProvider
      └── CartProvider
          └── AppRoutes
              └── MainLayout
                  ├── Navbar
                  ├── Outlet
                  └── Footer
```

## Public pages

```txt
HomePage
  ├── HeroSection
  ├── FeaturedFoods
  │     └── FoodCard
  └── HowItWorksSection

MenuPage
  ├── FoodFilters
  ├── FoodGrid
  │     └── FoodCard
  └── EmptyState
```

## Customer pages

```txt
CartPage
  ├── CartItem
  ├── CartSummary
  └── EmptyState

CheckoutPage
  ├── CheckoutForm
  └── OrderSummary
```

## Admin pages

```txt
DashboardLayout
  ├── Sidebar
  └── Outlet

ManageFoodsPage
  ├── FoodForm
  └── FoodTable

ManageOrdersPage
  └── OrderTable
```
```

---

## `MOCK_DATA_PLAN.md`

Template:

```md
# Mock Data Plan

## Purpose
Use mock data to build frontend before backend integration.

## Mock data files

| File | Purpose |
|---|---|
| src/data/mockFoods.ts | Food/menu data |
| src/data/mockOrders.ts | Order data |
| src/data/mockUsers.ts | User/auth data |

## Rules
- Mock data should match future API shape.
- Do not create UI-only data that backend cannot return.
- Keep IDs consistent.
- Include enough data for empty, normal, and admin states.
```

---

## `FRONTEND_STATE_PLAN.md`

Template:

```md
# Frontend State Plan

| State | Type | Owner |
|---|---|---|
| Current user | Global client state | AuthContext |
| Cart items | Global client state | CartContext/localStorage |
| Menu search | Local page state | MenuPage |
| Category filter | Local page state | MenuPage |
| Checkout form | Form/page state | CheckoutPage |
| Mock orders | Mock data/page state | MyOrdersPage/AdminOrdersPage |
| Loading/error | UI state | Page/component level |

## Later API integration
Server state such as foods and orders may move to TanStack Query in Module 8.
```

---

## `FRONTEND_ROUTE_TEST_PLAN.md`

Template:

```md
# Frontend Route Test Plan

| Route | Expected result | Status |
|---|---|---|
| `/` | Home page loads | Pending |
| `/menu` | Food grid loads | Pending |
| `/menu/:id` | Food details loads | Pending |
| `/cart` | Protected cart page loads for logged-in user | Pending |
| `/checkout` | Protected checkout page loads | Pending |
| `/my-orders` | Protected order history loads | Pending |
| `/admin` | Admin only overview loads | Pending |
| `/admin/foods` | Admin food management loads | Pending |
| `/admin/orders` | Admin order management loads | Pending |
| `/unauthorized` | Unauthorized page loads | Pending |
| random route | Not found page loads | Pending |
```

---

## `FRONTEND_BROWSER_QA_REPORT.md`

Template:

```md
# Frontend Browser QA Report

## Browser URL
-

## Routes tested
-

## Desktop test

### What works
-

### Issues
-

## Mobile test

### What works
-

### Issues
-

## Console errors
-

## Broken links
-

## UI state checks
- Loading:
- Empty:
- Error:
- Unauthorized:
- Not found:

## Critical fixes
-

## Final verdict
Pass / Conditional pass / Fail
```

---

# Part 18: Antigravity prompts for this module

## Prompt 1: Create frontend docs

```txt
I am doing Module 6: Frontend Implementation.

Create these docs:
1. docs/FRONTEND_IMPLEMENTATION_PLAN.md
2. docs/FRONTEND_COMPONENT_TREE.md
3. docs/MOCK_DATA_PLAN.md
4. docs/FRONTEND_STATE_PLAN.md
5. docs/FRONTEND_ROUTE_TEST_PLAN.md
6. docs/FRONTEND_BROWSER_QA_REPORT.md

Rules:
- Do not create app code yet.
- Use React, Vite, TypeScript, Tailwind, React Router.
- Use mock data first.
- Keep it practical for a junior MERN developer.
```

---

## Prompt 2: Create frontend folder structure

```txt
Read:
- docs/FRONTEND_IMPLEMENTATION_PLAN.md
- docs/FRONTEND_COMPONENT_TREE.md

Task:
Create only the frontend folder structure and placeholder files.

Rules:
- Work only inside client/src.
- Do not implement full page logic yet.
- Do not edit backend.
- Do not install packages.
- After creating files, summarize the folder structure.
```

---

## Prompt 3: Create types and mock data

```txt
Read:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/MOCK_DATA_PLAN.md

Task:
Create TypeScript types and mock data.

Files:
- src/types/food.ts
- src/types/user.ts
- src/types/order.ts
- src/types/api.ts
- src/data/mockFoods.ts
- src/data/mockOrders.ts
- src/data/mockUsers.ts

Rules:
- Match API contract and database schema.
- Do not create real API calls.
- Do not edit backend.
```

---

## Prompt 4: Create common components

```txt
Create reusable common UI components.

Files:
- src/components/common/Button.tsx
- src/components/common/Card.tsx
- src/components/common/Badge.tsx
- src/components/common/Input.tsx
- src/components/states/LoadingState.tsx
- src/components/states/EmptyState.tsx
- src/components/states/ErrorState.tsx

Rules:
- Use React + TypeScript + Tailwind.
- Keep components simple and reusable.
- Do not create pages yet.
- Do not edit backend.
```

---

## Prompt 5: Create layout and routes

```txt
Create layout and routing.

Files:
- src/components/layout/Navbar.tsx
- src/components/layout/Footer.tsx
- src/components/layout/MainLayout.tsx
- src/components/layout/DashboardLayout.tsx
- src/routes/AppRoutes.tsx
- src/routes/ProtectedRoute.tsx
- src/routes/AdminRoute.tsx

Rules:
- Use React Router.
- Use mock AuthContext and CartContext if needed.
- Do not connect backend APIs.
- Do not edit backend.
```

---

## Prompt 6: Implement public pages

```txt
Implement only public pages.

Pages:
- HomePage
- MenuPage
- FoodDetailsPage
- UnauthorizedPage
- NotFoundPage

Rules:
- Use mock data.
- Use reusable components.
- Add loading/empty/error states where useful.
- Do not implement auth pages yet.
- Do not edit backend.
```

---

## Prompt 7: Implement customer pages

```txt
Implement only customer pages.

Pages:
- CartPage
- CheckoutPage
- MyOrdersPage

Rules:
- Use CartContext.
- Use mock orders.
- No real API calls.
- Add empty states.
- Do not edit backend.
```

---

## Prompt 8: Implement admin pages

```txt
Implement only admin pages.

Pages:
- AdminOverviewPage
- ManageFoodsPage
- ManageOrdersPage

Rules:
- Use mock foods and orders.
- Create dashboard cards and tables.
- No real API mutations.
- No backend changes.
```

---

## Prompt 9: Browser verification

```txt
Use browser verification.

Check:
1. All routes
2. Navbar links
3. Cart flow
4. Login/logout mock flow
5. Admin route behavior
6. Mobile layout
7. Console errors
8. Empty states
9. Unauthorized route
10. Not found route

Do not edit files yet.

Create a frontend browser QA report.
```

---

## Prompt 10: Fix only critical frontend issues

```txt
Read docs/FRONTEND_BROWSER_QA_REPORT.md.

Fix only the critical issues.

Rules:
- Do not rewrite the full frontend.
- Do not edit backend.
- Do not create real API calls.
- Do not install packages.
- Keep changes minimal.
- After fixing, summarize changed files.
```

---

# Part 19: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 08-module-06-frontend-implementation.md
2. React Thinking in React docs
3. Vite guide
4. Tailwind Vite installation docs
5. React Router docs
6. TanStack Query overview/docs optional
7. Your frontend architecture docs
8. Your design system docs
9. Your component tree
10. Your browser QA report
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for frontend implementation.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. Why frontend-first with mock data is useful
2. React + Vite + TypeScript setup
3. Tailwind setup
4. Folder structure
5. TypeScript types
6. Mock data
7. Reusable components
8. Layout components
9. React Router routes
10. Auth and cart context
11. Public/customer/admin pages
12. UI states
13. Browser verification
14. Common mistakes
15. Practice checklist
```

---

## NotebookLM Prompt 2: Component Review

```txt
Review my frontend component plan.

Check:
1. Are components reusable?
2. Are pages separated from components?
3. Are common UI components useful?
4. Are UI states included?
5. Are route groups clear?
6. Is state ownership clear?
7. Is mock data aligned with future backend?
8. What should I fix before backend integration?

Return a frontend review checklist.
```

---

## NotebookLM Prompt 3: Route Test Guide

```txt
Create a route-by-route frontend testing guide.

Include:
1. Route
2. What should load
3. User role required
4. What interaction to test
5. What screenshot to capture
6. What common bug may happen
```

---

## NotebookLM Prompt 4: Interview Explanation

```txt
Help me explain my frontend architecture in an interview.

Create:
1. 30-second explanation
2. 1-minute explanation
3. Component architecture explanation
4. State management explanation
5. Routing explanation
6. Mock-data-first explanation
7. What will change during backend integration
```

---

# Part 20: Required video resources

Watch at least two videos.

Search YouTube:

```txt
React Vite TypeScript Tailwind tutorial
React Router protected routes tutorial
React Context API cart tutorial
React dashboard Tailwind tutorial
React frontend architecture components pages services
TanStack Query React tutorial for beginners
```

Recommended video types:

| Video type | Why |
|---|---|
| React + Vite + Tailwind setup | Helps project setup |
| React Router protected routes | Helps auth/admin pages |
| React Context cart example | Helps cart state |
| React dashboard tutorial | Helps admin pages |
| Frontend architecture tutorial | Helps folder structure and separation |

---

## Video learning notes

Create:

```txt
docs/notebooklm/module-06-video-learning-notes.md
```

Use this format:

```md
# Module 6 Video Learning Notes

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

# Part 21: Practice tasks

## Practice Task 1: Setup frontend

Create the Vite + React + TypeScript app inside `client/`.

Install and configure Tailwind.

Submit screenshot of:

```txt
http://localhost:5173
```

---

## Practice Task 2: Create folder structure

Create the recommended folder structure.

Submit screenshot or tree output:

```bash
tree client/src
```

If `tree` is unavailable, use:

```bash
dir client\src
```

---

## Practice Task 3: Create types and mock data

Create:

```txt
types/
data/
```

Submit files:

```txt
food.ts
user.ts
order.ts
api.ts
mockFoods.ts
mockOrders.ts
mockUsers.ts
```

---

## Practice Task 4: Create reusable components

Create:

```txt
Button
Card
Badge
Input
LoadingState
EmptyState
ErrorState
```

Use them in at least one page.

---

## Practice Task 5: Create routes

Create all routes and verify navigation.

Update:

```txt
FRONTEND_ROUTE_TEST_PLAN.md
```

---

## Practice Task 6: Build public pages

Build:

```txt
HomePage
MenuPage
FoodDetailsPage
```

Requirements:

- Responsive
- Uses mock data
- Has food cards
- Has search/filter on menu
- Has details page
- Has add-to-cart button

---

## Practice Task 7: Build auth/customer pages

Build:

```txt
LoginPage
RegisterPage
CartPage
CheckoutPage
MyOrdersPage
```

Requirements:

- Mock login
- Cart flow
- Empty cart state
- Checkout form
- Mock order history

---

## Practice Task 8: Build admin pages

Build:

```txt
AdminOverviewPage
ManageFoodsPage
ManageOrdersPage
```

Requirements:

- Dashboard cards
- Food table
- Order table
- Status badges
- Mock admin interactions

---

## Practice Task 9: Browser QA

Test all routes.

Create:

```txt
docs/FRONTEND_BROWSER_QA_REPORT.md
```

Include desktop and mobile screenshots.

---

## Practice Task 10: Fix critical issues

Fix:

- Broken routes
- Layout crashes
- Missing imports
- TypeScript errors
- Console errors
- Mobile layout issues

Do not add new features during fixes.

---

# Part 22: Common mistakes

## Mistake 1: Connecting backend too early

Do not connect APIs before frontend pages and data shapes are clear.

---

## Mistake 2: Putting everything in one file

Avoid giant files like:

```txt
App.tsx with all pages and all components
```

Use components and pages.

---

## Mistake 3: No UI states

Every list page should consider:

```txt
Loading
Empty
Error
Success
```

Even if mock data does not fail, build the components.

---

## Mistake 4: No protected route thinking

Admin pages should not be visible to normal users.

Mock route guards now.

Backend authorization later.

---

## Mistake 5: Mock data does not match backend

Your mock data should match `API_CONTRACT.md` and `DATABASE_SCHEMA.md`.

---

## Mistake 6: No mobile check

A frontend project is not complete if only desktop works.

---

## Mistake 7: Too many packages

Do not install UI libraries, animation libraries, state libraries, and form libraries all at once.

Keep it manageable.

---

# Required deliverables for this module

Submit:

```txt
1. client/ React project
2. Tailwind configured
3. React Router configured
4. Folder structure screenshot/tree
5. TypeScript types
6. Mock data files
7. Common components
8. Layout components
9. AuthContext
10. CartContext
11. Public pages
12. Auth/customer pages
13. Admin pages
14. Protected route and admin route
15. FRONTEND_IMPLEMENTATION_PLAN.md
16. FRONTEND_COMPONENT_TREE.md
17. MOCK_DATA_PLAN.md
18. FRONTEND_STATE_PLAN.md
19. FRONTEND_ROUTE_TEST_PLAN.md
20. FRONTEND_BROWSER_QA_REPORT.md
21. Desktop screenshots
22. Mobile screenshots
23. NotebookLM Study Guide screenshot
24. NotebookLM component review screenshot
25. Video learning notes
26. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/08-module-06-frontend-implementation-reflection.md
```

Use this format:

```md
# Reflection: Module 6 - Frontend Implementation

## What I built
-

## Pages I completed
-

## Components I created
-

## Mock data I created
-

## What I learned about frontend architecture
-

## What I learned about routing
-

## What I learned about state management
-

## What Antigravity helped with
-

## What I had to fix manually
-

## Browser QA issues I found
-

## What I will prepare before backend implementation
-
```

---

# Quiz

## Multiple choice

**1. Why use mock data before backend integration?**

A. To build and verify frontend without waiting for backend APIs  
B. To avoid building backend forever  
C. To hide requirements  
D. To skip TypeScript  

Correct answer: **A**

---

**2. What should common components contain?**

A. Reusable UI like Button, Card, Badge, Input  
B. Database connection strings  
C. Server routes  
D. Deployment secrets  

Correct answer: **A**

---

**3. What is the purpose of `AuthContext` in this module?**

A. Mock current user/auth state for route behavior  
B. Store MongoDB URI  
C. Replace CSS  
D. Create backend JWT  

Correct answer: **A**

---

**4. What is the purpose of `CartContext`?**

A. Manage cart items, quantities, total items, and total price  
B. Deploy frontend  
C. Store admin password  
D. Replace React Router  

Correct answer: **A**

---

**5. What should frontend route guards do?**

A. Protect UI routes in the frontend, while backend security comes later  
B. Replace backend authorization forever  
C. Store secrets  
D. Delete admin pages  

Correct answer: **A**

---

**6. What should `FRONTEND_BROWSER_QA_REPORT.md` include?**

A. Routes tested, desktop/mobile results, console errors, critical fixes  
B. Only package names  
C. Only database schema  
D. Only GitHub username  

Correct answer: **A**

---

**7. What is a bad frontend implementation practice?**

A. Putting all components and pages in one giant file  
B. Creating reusable components  
C. Using TypeScript types  
D. Testing routes  

Correct answer: **A**

---

**8. What should mock data match?**

A. Future API contract and database schema  
B. Random field names only  
C. Unrelated tutorial data  
D. Browser extension data  

Correct answer: **A**

---

**9. What must be checked before saying frontend is complete?**

A. Browser routes, responsiveness, console errors, UI states  
B. Only homepage title  
C. Only package.json  
D. Only README  

Correct answer: **A**

---

**10. What should you avoid in this module?**

A. Real backend API integration  
B. Mock data  
C. Component reuse  
D. Browser verification  

Correct answer: **A**

---

## Short-answer questions

1. Why is frontend-first with mock data useful?
2. What pages did you build in this module?
3. What are three reusable components you created?
4. What is the difference between public, protected, and admin routes?
5. What state belongs in AuthContext?
6. What state belongs in CartContext?
7. Why should mock data match the API contract?
8. What should be tested in browser QA?
9. What did Antigravity do well in this module?
10. What will change during backend integration?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Frontend setup | React + Vite + TypeScript app runs |
| Tailwind setup | Tailwind classes work |
| Folder structure | Organized by components/pages/routes/context/types/data |
| Types | Food/User/Order/API types exist |
| Mock data | Foods/orders/users mock data exist |
| Common components | Button/Card/Badge/Input/states created |
| Layout | Navbar/Footer/MainLayout/DashboardLayout created |
| Routing | Public/protected/admin routes work |
| Auth context | Mock customer/admin login available |
| Cart context | Add/update/remove/clear cart works |
| Public pages | Home/menu/details pages implemented |
| Customer pages | Cart/checkout/my orders implemented |
| Admin pages | Overview/foods/orders implemented |
| UI states | Loading/empty/error/unauthorized/not found included |
| Browser QA | Desktop/mobile/console checks documented |
| NotebookLM evidence | Study guide and review screenshots submitted |
| Reflection | Student explains frontend choices clearly |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can build a React + TypeScript + Tailwind frontend with reusable components, routes, mock data, auth/cart context, public/customer/admin pages, UI states, and browser verification before connecting the backend.
```

After completing this file, continue to:

```txt
09-module-07-backend-implementation.md
```
