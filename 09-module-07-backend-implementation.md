# Module 7: Backend Implementation — Build the Express + MongoDB API with Antigravity

**File Name:** `09-module-07-backend-implementation.md`  
**Module Type:** Core Module  
**Target Learners:** Junior MERN Stack Developers  
**Estimated Time:** 7–10 hours  
**Recommended After:** Module 6: Frontend Implementation  
**Main Goal:** Build a clean backend API using Node.js, Express, TypeScript, MongoDB, Mongoose, JWT authentication, role-based authorization, validation, and consistent error handling.

---

## Module purpose

In Module 6, you built the frontend using mock data.

Now you will build the backend.

This module focuses only on the server side:

```txt
server/
  Node.js + Express + TypeScript + MongoDB + Mongoose
```

The backend will provide real APIs for:

- User registration
- User login
- JWT authentication
- Role-based authorization
- Food/menu CRUD
- Order creation
- User order history
- Admin order management
- Order status update
- Consistent success/error responses

The goal is not to create random Express routes.

The goal is to create a backend that matches your earlier planning documents:

```txt
API_CONTRACT.md
DATABASE_SCHEMA.md
AUTHORIZATION_MATRIX.md
BACKEND_ARCHITECTURE.md
DATA_FLOW.md
ERROR_FLOW.md
```

---

## What you will build in this module

You will build:

| Area | Work |
|---|---|
| Backend setup | Express + TypeScript server |
| Config | Environment variable loading and validation |
| Database | MongoDB Atlas/local MongoDB connection |
| Models | User, Food, Order |
| Auth | Register, login, JWT token generation |
| Security | Password hashing, auth middleware, admin middleware |
| Validation | Zod validation schemas |
| Routes | Auth, foods, orders |
| Controllers | Request/response handling |
| Services | Business logic and database operations |
| Error handling | Global error handler, not found handler |
| Response format | Consistent success/error response |
| Testing | Manual API testing through Postman/Thunder Client |
| Documentation | Backend implementation plan, API test report, security checklist |

---

## Required backend stack

Recommended stack:

```txt
Node.js
Express.js
TypeScript
MongoDB
Mongoose
Zod
JWT
bcrypt
cors
dotenv
```

Recommended dev tools:

```txt
ts-node-dev or tsx
Postman / Thunder Client / Insomnia / Hoppscotch
MongoDB Atlas
MongoDB Compass optional
```

---

## Backend architecture reminder

Use this backend flow:

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

Do not put everything inside route files.

A clean backend is easier to review, test, and explain.

---

## Backend folder structure

Create this structure:

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
        user.types.ts
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
      AppError.ts
      catchAsync.ts
      sendResponse.ts
      generateToken.ts
    types/
      express.d.ts
    constants/
      orderStatus.ts
```

---

## Backend implementation rule

Do not ask Antigravity to build the whole backend at once.

Use this order:

```txt
Backend setup
→ Database connection
→ Utilities/middlewares
→ User model
→ Auth routes
→ Food model/routes
→ Order model/routes
→ Manual API testing
→ Security review
→ Documentation update
```

---

# Part 1: Backend setup

## Create server folder

From project root:

```bash
mkdir server
cd server
npm init -y
```

Install dependencies:

```bash
npm install express cors dotenv mongoose zod bcrypt jsonwebtoken
```

Install dev dependencies:

```bash
npm install -D typescript tsx @types/node @types/express @types/cors @types/bcrypt @types/jsonwebtoken
```

Initialize TypeScript:

```bash
npx tsc --init
```

Recommended `package.json` scripts:

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

---

## Recommended `tsconfig.json`

Use a practical backend TypeScript config:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "rootDir": "src",
    "outDir": "dist",
    "strict": true,
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "skipLibCheck": true
  },
  "include": ["src"]
}
```

If your local setup needs CommonJS instead, keep it consistent across imports and build output.

---

## Create `.env.example`

Create:

```txt
server/.env.example
```

Content:

```env
NODE_ENV=development
PORT=5000
CLIENT_URL=http://localhost:5173
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/localbites
JWT_SECRET=replace_with_long_random_secret
JWT_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=10
```

Create actual `.env` locally:

```txt
server/.env
```

Important:

```txt
Never commit .env to GitHub.
```

Add to root `.gitignore` or server `.gitignore`:

```txt
.env
dist
node_modules
```

---

# Part 2: Environment config

Create:

```txt
server/src/config/env.ts
```

Example:

```ts
import dotenv from "dotenv";
import { z } from "zod";

dotenv.config();

const envSchema = z.object({
  NODE_ENV: z.enum(["development", "production", "test"]).default("development"),
  PORT: z.coerce.number().default(5000),
  CLIENT_URL: z.string().url(),
  MONGODB_URI: z.string().min(1, "MONGODB_URI is required"),
  JWT_SECRET: z.string().min(20, "JWT_SECRET must be at least 20 characters"),
  JWT_EXPIRES_IN: z.string().default("7d"),
  BCRYPT_SALT_ROUNDS: z.coerce.number().default(10),
});

const parsed = envSchema.safeParse(process.env);

if (!parsed.success) {
  console.error("Invalid environment variables", parsed.error.flatten().fieldErrors);
  process.exit(1);
}

export const env = parsed.data;
```

Why this matters:

- Missing env variables fail early.
- JWT secret length is checked.
- Port and salt rounds are coerced into numbers.
- Deployment issues become easier to debug.

---

# Part 3: Database connection

Create:

```txt
server/src/config/db.ts
```

Example:

```ts
import mongoose from "mongoose";
import { env } from "./env";

export async function connectDB() {
  try {
    await mongoose.connect(env.MONGODB_URI);
    console.log("MongoDB connected");
  } catch (error) {
    console.error("MongoDB connection failed", error);
    process.exit(1);
  }
}
```

---

## MongoDB setup checklist

Use MongoDB Atlas or local MongoDB.

For Atlas:

```txt
1. Create cluster
2. Create database user
3. Save username/password safely
4. Add network access
5. Copy connection string
6. Replace username/password/database name
7. Put URI in .env
8. Test connection
```

Common MongoDB mistakes:

| Mistake | Fix |
|---|---|
| Wrong password | Reset DB user password |
| Password special characters not encoded | URL-encode password |
| Network access blocked | Add IP access rule |
| Wrong database name | Check URI |
| Cluster paused | Resume cluster |
| `.env` not loaded | Check dotenv import |

---

# Part 4: Express app setup

Create:

```txt
server/src/app.ts
```

Example:

```ts
import express from "express";
import cors from "cors";
import { env } from "./config/env";
import { authRoutes } from "./modules/auth/auth.routes";
import { foodRoutes } from "./modules/foods/food.routes";
import { orderRoutes } from "./modules/orders/order.routes";
import { notFound } from "./middlewares/notFound";
import { errorHandler } from "./middlewares/errorHandler";

export const app = express();

app.use(
  cors({
    origin: env.CLIENT_URL,
    credentials: true,
  })
);

app.use(express.json());

app.get("/health", (_req, res) => {
  res.status(200).json({
    success: true,
    message: "Server is healthy",
  });
});

app.use("/api/auth", authRoutes);
app.use("/api/foods", foodRoutes);
app.use("/api/orders", orderRoutes);

app.use(notFound);
app.use(errorHandler);
```

Create:

```txt
server/src/server.ts
```

Example:

```ts
import { app } from "./app";
import { connectDB } from "./config/db";
import { env } from "./config/env";

async function bootstrap() {
  await connectDB();

  app.listen(env.PORT, () => {
    console.log(`Server running on port ${env.PORT}`);
  });
}

bootstrap();
```

Run:

```bash
npm run dev
```

Test:

```txt
http://localhost:5000/health
```

Expected response:

```json
{
  "success": true,
  "message": "Server is healthy"
}
```

---

# Part 5: Utility files

## `AppError.ts`

Create:

```txt
server/src/utils/AppError.ts
```

```ts
export class AppError extends Error {
  statusCode: number;
  isOperational: boolean;

  constructor(message: string, statusCode = 500) {
    super(message);
    this.statusCode = statusCode;
    this.isOperational = true;

    Error.captureStackTrace(this, this.constructor);
  }
}
```

---

## `catchAsync.ts`

Create:

```txt
server/src/utils/catchAsync.ts
```

```ts
import type { NextFunction, Request, Response } from "express";

export function catchAsync(
  fn: (req: Request, res: Response, next: NextFunction) => Promise<unknown>
) {
  return (req: Request, res: Response, next: NextFunction) => {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
}
```

---

## `sendResponse.ts`

Create:

```txt
server/src/utils/sendResponse.ts
```

```ts
import type { Response } from "express";

type SendResponseOptions<T> = {
  res: Response;
  statusCode?: number;
  message: string;
  data?: T;
};

export function sendResponse<T>({
  res,
  statusCode = 200,
  message,
  data,
}: SendResponseOptions<T>) {
  return res.status(statusCode).json({
    success: true,
    message,
    data,
  });
}
```

---

## `generateToken.ts`

Create:

```txt
server/src/utils/generateToken.ts
```

```ts
import jwt from "jsonwebtoken";
import { env } from "../config/env";

type TokenPayload = {
  userId: string;
  role: string;
};

export function generateToken(payload: TokenPayload) {
  return jwt.sign(payload, env.JWT_SECRET, {
    expiresIn: env.JWT_EXPIRES_IN,
  });
}
```

If TypeScript complains about `expiresIn`, check your installed jsonwebtoken types and keep the value format consistent.

---

# Part 6: Error handling middleware

Express error-handling middleware must have four arguments:

```txt
err, req, res, next
```

Create:

```txt
server/src/middlewares/notFound.ts
```

```ts
import type { Request, Response } from "express";

export function notFound(req: Request, res: Response) {
  res.status(404).json({
    success: false,
    message: `Route not found: ${req.originalUrl}`,
    errors: [],
  });
}
```

Create:

```txt
server/src/middlewares/errorHandler.ts
```

```ts
import type { ErrorRequestHandler } from "express";
import { env } from "../config/env";
import { AppError } from "../utils/AppError";

export const errorHandler: ErrorRequestHandler = (err, _req, res, _next) => {
  let statusCode = 500;
  let message = "Something went wrong";
  let errors: unknown[] = [];

  if (err instanceof AppError) {
    statusCode = err.statusCode;
    message = err.message;
  } else if (err.name === "ValidationError") {
    statusCode = 400;
    message = "Validation error";
    errors = Object.values(err.errors ?? {}).map((error: any) => error.message);
  } else if (err.name === "CastError") {
    statusCode = 400;
    message = "Invalid ID";
  } else if (err.code === 11000) {
    statusCode = 409;
    message = "Duplicate value";
  } else if (err instanceof Error) {
    message = err.message;
  }

  res.status(statusCode).json({
    success: false,
    message,
    errors,
    stack: env.NODE_ENV === "development" ? err.stack : undefined,
  });
};
```

---

# Part 7: Request validation middleware

Create:

```txt
server/src/middlewares/validateRequest.ts
```

```ts
import type { NextFunction, Request, Response } from "express";
import type { ZodSchema } from "zod";

export function validateRequest(schema: ZodSchema) {
  return (req: Request, _res: Response, next: NextFunction) => {
    const result = schema.safeParse({
      body: req.body,
      params: req.params,
      query: req.query,
    });

    if (!result.success) {
      return next(result.error);
    }

    req.body = result.data.body ?? req.body;
    req.params = result.data.params ?? req.params;
    req.query = result.data.query ?? req.query;

    next();
  };
}
```

Zod validates runtime input. TypeScript types alone do not protect your API from invalid request bodies.

---

# Part 8: User model

Create:

```txt
server/src/modules/users/user.types.ts
```

```ts
export type UserRole = "customer" | "admin";
```

Create:

```txt
server/src/modules/users/user.model.ts
```

```ts
import mongoose, { Schema, type InferSchemaType } from "mongoose";
import bcrypt from "bcrypt";
import { env } from "../../config/env";

const userSchema = new Schema(
  {
    name: {
      type: String,
      required: [true, "Name is required"],
      trim: true,
    },
    email: {
      type: String,
      required: [true, "Email is required"],
      unique: true,
      lowercase: true,
      trim: true,
    },
    password: {
      type: String,
      required: [true, "Password is required"],
      minlength: 6,
      select: false,
    },
    role: {
      type: String,
      enum: ["customer", "admin"],
      default: "customer",
    },
  },
  {
    timestamps: true,
  }
);

userSchema.pre("save", async function (next) {
  if (!this.isModified("password")) return next();

  this.password = await bcrypt.hash(this.password, env.BCRYPT_SALT_ROUNDS);
  next();
});

userSchema.methods.comparePassword = function (candidatePassword: string) {
  return bcrypt.compare(candidatePassword, this.password);
};

export type UserDocument = InferSchemaType<typeof userSchema> & {
  comparePassword(candidatePassword: string): Promise<boolean>;
};

export const User = mongoose.model("User", userSchema);
```

Important:

```txt
Never return password in API response.
```

---

# Part 9: Auth validation

Create:

```txt
server/src/modules/auth/auth.validation.ts
```

```ts
import { z } from "zod";

export const registerSchema = z.object({
  body: z.object({
    name: z.string().min(2, "Name must be at least 2 characters"),
    email: z.string().email("Invalid email address"),
    password: z.string().min(6, "Password must be at least 6 characters"),
  }),
});

export const loginSchema = z.object({
  body: z.object({
    email: z.string().email("Invalid email address"),
    password: z.string().min(1, "Password is required"),
  }),
});
```

---

# Part 10: Auth service

Create:

```txt
server/src/modules/auth/auth.service.ts
```

```ts
import { AppError } from "../../utils/AppError";
import { generateToken } from "../../utils/generateToken";
import { User } from "../users/user.model";

type RegisterInput = {
  name: string;
  email: string;
  password: string;
};

type LoginInput = {
  email: string;
  password: string;
};

function sanitizeUser(user: any) {
  return {
    id: user._id.toString(),
    name: user.name,
    email: user.email,
    role: user.role,
  };
}

export async function registerUser(input: RegisterInput) {
  const existingUser = await User.findOne({ email: input.email });

  if (existingUser) {
    throw new AppError("Email is already registered", 409);
  }

  const user = await User.create(input);

  const token = generateToken({
    userId: user._id.toString(),
    role: user.role,
  });

  return {
    user: sanitizeUser(user),
    token,
  };
}

export async function loginUser(input: LoginInput) {
  const user = await User.findOne({ email: input.email }).select("+password");

  if (!user) {
    throw new AppError("Invalid email or password", 401);
  }

  const isPasswordValid = await user.comparePassword(input.password);

  if (!isPasswordValid) {
    throw new AppError("Invalid email or password", 401);
  }

  const token = generateToken({
    userId: user._id.toString(),
    role: user.role,
  });

  return {
    user: sanitizeUser(user),
    token,
  };
}
```

---

# Part 11: Auth controller and routes

Create:

```txt
server/src/modules/auth/auth.controller.ts
```

```ts
import { catchAsync } from "../../utils/catchAsync";
import { sendResponse } from "../../utils/sendResponse";
import { loginUser, registerUser } from "./auth.service";

export const register = catchAsync(async (req, res) => {
  const result = await registerUser(req.body);

  sendResponse({
    res,
    statusCode: 201,
    message: "Registration successful",
    data: result,
  });
});

export const login = catchAsync(async (req, res) => {
  const result = await loginUser(req.body);

  sendResponse({
    res,
    message: "Login successful",
    data: result,
  });
});
```

Create:

```txt
server/src/modules/auth/auth.routes.ts
```

```ts
import { Router } from "express";
import { validateRequest } from "../../middlewares/validateRequest";
import { login, register } from "./auth.controller";
import { loginSchema, registerSchema } from "./auth.validation";

export const authRoutes = Router();

authRoutes.post("/register", validateRequest(registerSchema), register);
authRoutes.post("/login", validateRequest(loginSchema), login);
```

Test:

```txt
POST /api/auth/register
POST /api/auth/login
```

---

# Part 12: Extend Express request type

Create:

```txt
server/src/types/express.d.ts
```

```ts
import type { UserRole } from "../modules/users/user.types";

declare global {
  namespace Express {
    interface Request {
      user?: {
        userId: string;
        role: UserRole;
      };
    }
  }
}

export {};
```

Make sure `tsconfig.json` includes `src`.

---

# Part 13: Auth middleware

Create:

```txt
server/src/middlewares/auth.middleware.ts
```

```ts
import type { NextFunction, Request, Response } from "express";
import jwt from "jsonwebtoken";
import { env } from "../config/env";
import { AppError } from "../utils/AppError";

type JwtPayload = {
  userId: string;
  role: "customer" | "admin";
};

export function authMiddleware(
  req: Request,
  _res: Response,
  next: NextFunction
) {
  const authHeader = req.headers.authorization;

  if (!authHeader?.startsWith("Bearer ")) {
    return next(new AppError("Authentication required", 401));
  }

  const token = authHeader.split(" ")[1];

  try {
    const decoded = jwt.verify(token, env.JWT_SECRET) as JwtPayload;

    req.user = {
      userId: decoded.userId,
      role: decoded.role,
    };

    next();
  } catch {
    next(new AppError("Invalid or expired token", 401));
  }
}
```

---

# Part 14: Role middleware

Create:

```txt
server/src/middlewares/role.middleware.ts
```

```ts
import type { NextFunction, Request, Response } from "express";
import type { UserRole } from "../modules/users/user.types";
import { AppError } from "../utils/AppError";

export function requireRole(...allowedRoles: UserRole[]) {
  return (req: Request, _res: Response, next: NextFunction) => {
    if (!req.user) {
      return next(new AppError("Authentication required", 401));
    }

    if (!allowedRoles.includes(req.user.role)) {
      return next(new AppError("You are not allowed to perform this action", 403));
    }

    next();
  };
}
```

Important:

```txt
Frontend admin routes are not enough.
Backend must enforce admin permissions.
```

---

# Part 15: Food model

Create:

```txt
server/src/modules/foods/food.model.ts
```

```ts
import mongoose, { Schema, type InferSchemaType } from "mongoose";

const foodSchema = new Schema(
  {
    name: {
      type: String,
      required: [true, "Food name is required"],
      trim: true,
    },
    description: {
      type: String,
      required: [true, "Description is required"],
      trim: true,
    },
    price: {
      type: Number,
      required: [true, "Price is required"],
      min: [0, "Price cannot be negative"],
    },
    category: {
      type: String,
      required: [true, "Category is required"],
      enum: ["Burger", "Pizza", "Rice", "Dessert", "Drink"],
    },
    image: {
      type: String,
      required: [true, "Image is required"],
    },
    isAvailable: {
      type: Boolean,
      default: true,
    },
    createdBy: {
      type: Schema.Types.ObjectId,
      ref: "User",
    },
  },
  {
    timestamps: true,
  }
);

foodSchema.index({ name: "text", description: "text" });
foodSchema.index({ category: 1 });
foodSchema.index({ isAvailable: 1 });

export type FoodDocument = InferSchemaType<typeof foodSchema>;

export const Food = mongoose.model("Food", foodSchema);
```

---

# Part 16: Food validation

Create:

```txt
server/src/modules/foods/food.validation.ts
```

```ts
import { z } from "zod";

const categoryEnum = z.enum(["Burger", "Pizza", "Rice", "Dessert", "Drink"]);

export const createFoodSchema = z.object({
  body: z.object({
    name: z.string().min(2),
    description: z.string().min(5),
    price: z.number().nonnegative(),
    category: categoryEnum,
    image: z.string().url(),
    isAvailable: z.boolean().optional(),
  }),
});

export const updateFoodSchema = z.object({
  body: z.object({
    name: z.string().min(2).optional(),
    description: z.string().min(5).optional(),
    price: z.number().nonnegative().optional(),
    category: categoryEnum.optional(),
    image: z.string().url().optional(),
    isAvailable: z.boolean().optional(),
  }),
});

export const foodIdParamSchema = z.object({
  params: z.object({
    id: z.string().min(1),
  }),
});
```

---

# Part 17: Food service

Create:

```txt
server/src/modules/foods/food.service.ts
```

```ts
import { AppError } from "../../utils/AppError";
import { Food } from "./food.model";

type FoodQuery = {
  search?: string;
  category?: string;
  minPrice?: string;
  maxPrice?: string;
};

export async function getFoods(query: FoodQuery) {
  const filter: Record<string, unknown> = {};

  if (query.search) {
    filter.$text = { $search: query.search };
  }

  if (query.category) {
    filter.category = query.category;
  }

  if (query.minPrice || query.maxPrice) {
    filter.price = {};
    if (query.minPrice) (filter.price as any).$gte = Number(query.minPrice);
    if (query.maxPrice) (filter.price as any).$lte = Number(query.maxPrice);
  }

  return Food.find(filter).sort({ createdAt: -1 });
}

export async function getFoodById(id: string) {
  const food = await Food.findById(id);

  if (!food) {
    throw new AppError("Food item not found", 404);
  }

  return food;
}

export async function createFood(data: unknown, adminId: string) {
  return Food.create({
    ...(data as Record<string, unknown>),
    createdBy: adminId,
  });
}

export async function updateFood(id: string, data: unknown) {
  const food = await Food.findByIdAndUpdate(id, data, {
    new: true,
    runValidators: true,
  });

  if (!food) {
    throw new AppError("Food item not found", 404);
  }

  return food;
}

export async function deleteFood(id: string) {
  const food = await Food.findByIdAndDelete(id);

  if (!food) {
    throw new AppError("Food item not found", 404);
  }

  return food;
}
```

---

# Part 18: Food controller and routes

Create:

```txt
server/src/modules/foods/food.controller.ts
```

```ts
import { catchAsync } from "../../utils/catchAsync";
import { sendResponse } from "../../utils/sendResponse";
import {
  createFood,
  deleteFood,
  getFoodById,
  getFoods,
  updateFood,
} from "./food.service";

export const listFoods = catchAsync(async (req, res) => {
  const foods = await getFoods(req.query);

  sendResponse({
    res,
    message: "Foods retrieved successfully",
    data: foods,
  });
});

export const getSingleFood = catchAsync(async (req, res) => {
  const food = await getFoodById(req.params.id);

  sendResponse({
    res,
    message: "Food retrieved successfully",
    data: food,
  });
});

export const createNewFood = catchAsync(async (req, res) => {
  const food = await createFood(req.body, req.user!.userId);

  sendResponse({
    res,
    statusCode: 201,
    message: "Food created successfully",
    data: food,
  });
});

export const updateExistingFood = catchAsync(async (req, res) => {
  const food = await updateFood(req.params.id, req.body);

  sendResponse({
    res,
    message: "Food updated successfully",
    data: food,
  });
});

export const removeFood = catchAsync(async (req, res) => {
  await deleteFood(req.params.id);

  sendResponse({
    res,
    message: "Food deleted successfully",
    data: null,
  });
});
```

Create:

```txt
server/src/modules/foods/food.routes.ts
```

```ts
import { Router } from "express";
import { authMiddleware } from "../../middlewares/auth.middleware";
import { requireRole } from "../../middlewares/role.middleware";
import { validateRequest } from "../../middlewares/validateRequest";
import {
  createNewFood,
  getSingleFood,
  listFoods,
  removeFood,
  updateExistingFood,
} from "./food.controller";
import {
  createFoodSchema,
  foodIdParamSchema,
  updateFoodSchema,
} from "./food.validation";

export const foodRoutes = Router();

foodRoutes.get("/", listFoods);
foodRoutes.get("/:id", validateRequest(foodIdParamSchema), getSingleFood);

foodRoutes.post(
  "/",
  authMiddleware,
  requireRole("admin"),
  validateRequest(createFoodSchema),
  createNewFood
);

foodRoutes.patch(
  "/:id",
  authMiddleware,
  requireRole("admin"),
  validateRequest(foodIdParamSchema),
  validateRequest(updateFoodSchema),
  updateExistingFood
);

foodRoutes.delete(
  "/:id",
  authMiddleware,
  requireRole("admin"),
  validateRequest(foodIdParamSchema),
  removeFood
);
```

---

# Part 19: Order constants

Create:

```txt
server/src/constants/orderStatus.ts
```

```ts
export const ORDER_STATUSES = [
  "pending",
  "confirmed",
  "preparing",
  "delivered",
  "cancelled",
] as const;

export type OrderStatus = (typeof ORDER_STATUSES)[number];
```

---

# Part 20: Order model

Create:

```txt
server/src/modules/orders/order.model.ts
```

```ts
import mongoose, { Schema, type InferSchemaType } from "mongoose";
import { ORDER_STATUSES } from "../../constants/orderStatus";

const orderItemSchema = new Schema(
  {
    foodId: {
      type: Schema.Types.ObjectId,
      ref: "Food",
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    quantity: {
      type: Number,
      required: true,
      min: 1,
    },
    price: {
      type: Number,
      required: true,
      min: 0,
    },
  },
  { _id: false }
);

const orderSchema = new Schema(
  {
    user: {
      type: Schema.Types.ObjectId,
      ref: "User",
      required: true,
      index: true,
    },
    items: {
      type: [orderItemSchema],
      validate: {
        validator(items: unknown[]) {
          return items.length > 0;
        },
        message: "Order must contain at least one item",
      },
    },
    deliveryAddress: {
      type: String,
      required: true,
      trim: true,
    },
    phone: {
      type: String,
      required: true,
      trim: true,
    },
    totalPrice: {
      type: Number,
      required: true,
      min: 0,
    },
    status: {
      type: String,
      enum: ORDER_STATUSES,
      default: "pending",
      index: true,
    },
  },
  {
    timestamps: true,
  }
);

orderSchema.index({ createdAt: -1 });

export type OrderDocument = InferSchemaType<typeof orderSchema>;

export const Order = mongoose.model("Order", orderSchema);
```

---

# Part 21: Order validation

Create:

```txt
server/src/modules/orders/order.validation.ts
```

```ts
import { z } from "zod";
import { ORDER_STATUSES } from "../../constants/orderStatus";

export const createOrderSchema = z.object({
  body: z.object({
    items: z
      .array(
        z.object({
          foodId: z.string().min(1),
          name: z.string().min(1),
          quantity: z.number().int().positive(),
          price: z.number().nonnegative(),
        })
      )
      .min(1),
    deliveryAddress: z.string().min(5),
    phone: z.string().min(6),
    totalPrice: z.number().nonnegative(),
  }),
});

export const updateOrderStatusSchema = z.object({
  body: z.object({
    status: z.enum(ORDER_STATUSES),
  }),
});

export const orderIdParamSchema = z.object({
  params: z.object({
    id: z.string().min(1),
  }),
});
```

---

# Part 22: Order service

Create:

```txt
server/src/modules/orders/order.service.ts
```

```ts
import { AppError } from "../../utils/AppError";
import { Order } from "./order.model";

type CreateOrderInput = {
  items: {
    foodId: string;
    name: string;
    quantity: number;
    price: number;
  }[];
  deliveryAddress: string;
  phone: string;
  totalPrice: number;
};

export async function createOrder(input: CreateOrderInput, userId: string) {
  return Order.create({
    ...input,
    user: userId,
    status: "pending",
  });
}

export async function getMyOrders(userId: string) {
  return Order.find({ user: userId }).sort({ createdAt: -1 });
}

export async function getAllOrders() {
  return Order.find()
    .populate("user", "name email")
    .sort({ createdAt: -1 });
}

export async function updateOrderStatus(id: string, status: string) {
  const order = await Order.findByIdAndUpdate(
    id,
    { status },
    {
      new: true,
      runValidators: true,
    }
  );

  if (!order) {
    throw new AppError("Order not found", 404);
  }

  return order;
}
```

---

# Part 23: Order controller and routes

Create:

```txt
server/src/modules/orders/order.controller.ts
```

```ts
import { catchAsync } from "../../utils/catchAsync";
import { sendResponse } from "../../utils/sendResponse";
import {
  createOrder,
  getAllOrders,
  getMyOrders,
  updateOrderStatus,
} from "./order.service";

export const createNewOrder = catchAsync(async (req, res) => {
  const order = await createOrder(req.body, req.user!.userId);

  sendResponse({
    res,
    statusCode: 201,
    message: "Order placed successfully",
    data: order,
  });
});

export const listMyOrders = catchAsync(async (req, res) => {
  const orders = await getMyOrders(req.user!.userId);

  sendResponse({
    res,
    message: "My orders retrieved successfully",
    data: orders,
  });
});

export const listAllOrders = catchAsync(async (_req, res) => {
  const orders = await getAllOrders();

  sendResponse({
    res,
    message: "Orders retrieved successfully",
    data: orders,
  });
});

export const changeOrderStatus = catchAsync(async (req, res) => {
  const order = await updateOrderStatus(req.params.id, req.body.status);

  sendResponse({
    res,
    message: "Order status updated successfully",
    data: order,
  });
});
```

Create:

```txt
server/src/modules/orders/order.routes.ts
```

```ts
import { Router } from "express";
import { authMiddleware } from "../../middlewares/auth.middleware";
import { requireRole } from "../../middlewares/role.middleware";
import { validateRequest } from "../../middlewares/validateRequest";
import {
  changeOrderStatus,
  createNewOrder,
  listAllOrders,
  listMyOrders,
} from "./order.controller";
import {
  createOrderSchema,
  orderIdParamSchema,
  updateOrderStatusSchema,
} from "./order.validation";

export const orderRoutes = Router();

orderRoutes.use(authMiddleware);

orderRoutes.post("/", validateRequest(createOrderSchema), createNewOrder);
orderRoutes.get("/my-orders", listMyOrders);

orderRoutes.get("/", requireRole("admin"), listAllOrders);

orderRoutes.patch(
  "/:id/status",
  requireRole("admin"),
  validateRequest(orderIdParamSchema),
  validateRequest(updateOrderStatusSchema),
  changeOrderStatus
);
```

---

# Part 24: Backend API testing checklist

Use Postman, Thunder Client, Insomnia, or Hoppscotch.

## Health check

```txt
GET /health
```

Expected:

```json
{
  "success": true,
  "message": "Server is healthy"
}
```

---

## Register

```txt
POST /api/auth/register
```

Body:

```json
{
  "name": "Admin User",
  "email": "admin@example.com",
  "password": "password123"
}
```

Expected:

```txt
201 Created
Token returned
Password not returned
```

---

## Login

```txt
POST /api/auth/login
```

Body:

```json
{
  "email": "admin@example.com",
  "password": "password123"
}
```

Expected:

```txt
200 OK
Token returned
```

---

## Create admin user

For the first admin, you may temporarily update the role in MongoDB Atlas/Compass manually:

```txt
role: "admin"
```

Do not create insecure public admin registration in production.

---

## Create food as admin

```txt
POST /api/foods
Authorization: Bearer <admin_token>
```

Body:

```json
{
  "name": "Classic Chicken Burger",
  "description": "Grilled chicken patty with fresh vegetables and house sauce.",
  "price": 250,
  "category": "Burger",
  "image": "https://images.unsplash.com/photo-1568901346375-23c9450c58cd",
  "isAvailable": true
}
```

Expected:

```txt
201 Created
Food created
```

---

## Get foods

```txt
GET /api/foods
```

Expected:

```txt
200 OK
Array of foods
```

---

## Create order as customer

```txt
POST /api/orders
Authorization: Bearer <customer_token>
```

Body:

```json
{
  "items": [
    {
      "foodId": "replace_with_food_id",
      "name": "Classic Chicken Burger",
      "quantity": 2,
      "price": 250
    }
  ],
  "deliveryAddress": "Dhaka, Bangladesh",
  "phone": "01700000000",
  "totalPrice": 500
}
```

Expected:

```txt
201 Created
Order created with pending status
```

---

## Get my orders

```txt
GET /api/orders/my-orders
Authorization: Bearer <customer_token>
```

Expected:

```txt
200 OK
Only current user's orders
```

---

## Admin get all orders

```txt
GET /api/orders
Authorization: Bearer <admin_token>
```

Expected:

```txt
200 OK
All orders
```

Customer token should return:

```txt
403 Forbidden
```

---

## Admin update order status

```txt
PATCH /api/orders/:id/status
Authorization: Bearer <admin_token>
```

Body:

```json
{
  "status": "preparing"
}
```

Expected:

```txt
200 OK
Order status updated
```

---

# Part 25: Backend documentation files

Create these docs:

```txt
docs/BACKEND_IMPLEMENTATION_PLAN.md
docs/BACKEND_MODULE_MAP.md
docs/BACKEND_ENV_CHECKLIST.md
docs/BACKEND_API_TEST_PLAN.md
docs/BACKEND_API_TEST_REPORT.md
docs/BACKEND_SECURITY_CHECKLIST.md
docs/BACKEND_ERROR_REPORT.md
```

---

## `BACKEND_IMPLEMENTATION_PLAN.md`

Template:

```md
# Backend Implementation Plan

## Stack
- Node.js
- Express
- TypeScript
- MongoDB
- Mongoose
- Zod
- JWT
- bcrypt

## Implementation order
1. Setup server
2. Configure env variables
3. Connect MongoDB
4. Create utilities
5. Create global middleware
6. Create User model
7. Create auth routes
8. Create auth/role middleware
9. Create Food model/routes
10. Create Order model/routes
11. Test APIs manually
12. Create backend security checklist
13. Prepare for frontend integration
```

---

## `BACKEND_MODULE_MAP.md`

Template:

```md
# Backend Module Map

| Module | Files | Purpose |
|---|---|---|
| auth | routes/controller/service/validation | Register/login |
| users | model/types | User schema and role |
| foods | model/routes/controller/service/validation | Food CRUD |
| orders | model/routes/controller/service/validation | Order flow |
| middlewares | auth/role/validate/error | Shared request handling |
| utils | AppError/catchAsync/sendResponse/token | Shared helpers |
```

---

## `BACKEND_ENV_CHECKLIST.md`

Template:

```md
# Backend Environment Checklist

- [ ] `.env` exists locally
- [ ] `.env` is not committed
- [ ] `.env.example` exists
- [ ] PORT configured
- [ ] CLIENT_URL configured
- [ ] MONGODB_URI configured
- [ ] JWT_SECRET configured and long enough
- [ ] JWT_EXPIRES_IN configured
- [ ] BCRYPT_SALT_ROUNDS configured
- [ ] MongoDB Atlas IP access configured
- [ ] Database user exists
```

---

## `BACKEND_API_TEST_PLAN.md`

Template:

```md
# Backend API Test Plan

| API | Method | Access | Test case |
|---|---|---|---|
| /health | GET | Public | Server health |
| /api/auth/register | POST | Public | Register user |
| /api/auth/login | POST | Public | Login user |
| /api/foods | GET | Public | List foods |
| /api/foods/:id | GET | Public | Get food details |
| /api/foods | POST | Admin | Create food |
| /api/foods/:id | PATCH | Admin | Update food |
| /api/foods/:id | DELETE | Admin | Delete food |
| /api/orders | POST | Customer/Admin | Create order |
| /api/orders/my-orders | GET | Customer/Admin | Get own orders |
| /api/orders | GET | Admin | Get all orders |
| /api/orders/:id/status | PATCH | Admin | Update order status |
```

---

## `BACKEND_API_TEST_REPORT.md`

Template:

```md
# Backend API Test Report

## Test tool
Postman / Thunder Client / Insomnia / Hoppscotch

## Base URL
http://localhost:5000

## Results

| API | Status | Notes |
|---|---|---|
| GET /health | Pass/Fail |  |
| POST /api/auth/register | Pass/Fail |  |
| POST /api/auth/login | Pass/Fail |  |
| GET /api/foods | Pass/Fail |  |
| POST /api/foods admin | Pass/Fail |  |
| POST /api/foods customer forbidden | Pass/Fail |  |
| POST /api/orders | Pass/Fail |  |
| GET /api/orders/my-orders | Pass/Fail |  |
| GET /api/orders admin | Pass/Fail |  |
| PATCH /api/orders/:id/status admin | Pass/Fail |  |

## Bugs found
-

## Fixes applied
-

## Final verdict
Pass / Conditional pass / Fail
```

---

## `BACKEND_SECURITY_CHECKLIST.md`

Template:

```md
# Backend Security Checklist

## Secrets
- [ ] `.env` not committed
- [ ] JWT secret is long and private
- [ ] MongoDB URI is private
- [ ] `.env.example` has placeholders only

## Authentication
- [ ] Passwords are hashed
- [ ] Password is not returned in API response
- [ ] JWT is signed with secret
- [ ] Invalid token returns 401
- [ ] Missing token returns 401

## Authorization
- [ ] Admin routes require admin role
- [ ] Customer cannot access admin routes
- [ ] Users can access only own orders
- [ ] Backend enforces authorization

## Validation
- [ ] Request body validation exists
- [ ] Invalid data returns 400
- [ ] Object ID errors handled
- [ ] Duplicate email handled

## Errors
- [ ] Global error handler exists
- [ ] Not found handler exists
- [ ] Production stack trace hidden
- [ ] Error response format is consistent
```

---

# Part 26: Antigravity prompts for this module

## Prompt 1: Create backend docs

```txt
I am doing Module 7: Backend Implementation.

Create these docs:
1. docs/BACKEND_IMPLEMENTATION_PLAN.md
2. docs/BACKEND_MODULE_MAP.md
3. docs/BACKEND_ENV_CHECKLIST.md
4. docs/BACKEND_API_TEST_PLAN.md
5. docs/BACKEND_API_TEST_REPORT.md
6. docs/BACKEND_SECURITY_CHECKLIST.md
7. docs/BACKEND_ERROR_REPORT.md

Rules:
- Do not create backend code yet.
- Use Express, TypeScript, MongoDB, Mongoose, Zod, JWT, bcrypt.
- Align with docs/API_CONTRACT.md and docs/DATABASE_SCHEMA.md.
```

---

## Prompt 2: Setup backend foundation only

```txt
Read:
- docs/BACKEND_IMPLEMENTATION_PLAN.md
- docs/BACKEND_MODULE_MAP.md

Task:
Create only the backend foundation.

Allowed:
- server/package.json scripts
- tsconfig.json
- src/app.ts
- src/server.ts
- src/config/env.ts
- src/config/db.ts
- .env.example

Rules:
- Do not create auth/food/order modules yet.
- Do not edit frontend.
- Do not hardcode secrets.
- Do not commit .env.
- After implementation, explain how to test /health.
```

---

## Prompt 3: Create utilities and middlewares

```txt
Create only shared utilities and middlewares.

Files:
- src/utils/AppError.ts
- src/utils/catchAsync.ts
- src/utils/sendResponse.ts
- src/utils/generateToken.ts
- src/middlewares/validateRequest.ts
- src/middlewares/errorHandler.ts
- src/middlewares/notFound.ts

Rules:
- Do not create feature modules yet.
- Keep response format consistent with API_CONTRACT.md.
- Do not edit frontend.
```

---

## Prompt 4: Create auth module

```txt
Read:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTH_FLOW.md
- docs/AUTHORIZATION_MATRIX.md

Create auth module:
- users/user.model.ts
- users/user.types.ts
- auth/auth.validation.ts
- auth/auth.service.ts
- auth/auth.controller.ts
- auth/auth.routes.ts
- middlewares/auth.middleware.ts
- middlewares/role.middleware.ts
- types/express.d.ts

Rules:
- Hash passwords with bcrypt.
- Do not return password.
- Use JWT.
- Do not create public admin registration.
- Do not edit frontend.
```

---

## Prompt 5: Create food module

```txt
Read:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTHORIZATION_MATRIX.md

Create foods module:
- food.model.ts
- food.validation.ts
- food.service.ts
- food.controller.ts
- food.routes.ts

Rules:
- Public users can list/view foods.
- Only admin can create/update/delete foods.
- Validate request body.
- Use consistent responses.
- Do not edit frontend.
```

---

## Prompt 6: Create order module

```txt
Read:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTHORIZATION_MATRIX.md
- docs/DATA_FLOW.md

Create orders module:
- order.model.ts
- order.validation.ts
- order.service.ts
- order.controller.ts
- order.routes.ts
- constants/orderStatus.ts

Rules:
- Logged-in users can create orders and view own orders.
- Admin can view all orders and update status.
- Store item snapshot with foodId, name, price, quantity.
- Validate request body.
- Do not edit frontend.
```

---

## Prompt 7: API review

```txt
Use the express-api-quality-review skill.

Review backend API implementation against:
- docs/API_CONTRACT.md
- docs/DATABASE_SCHEMA.md
- docs/AUTHORIZATION_MATRIX.md

Check:
1. Route names
2. HTTP methods
3. Request validation
4. Response format
5. Auth middleware
6. Admin role checks
7. Error handling
8. Security risks

Do not edit files yet.

Return a review report.
```

---

## Prompt 8: Security review

```txt
Review backend security.

Check:
1. Password hashing
2. Password response hiding
3. JWT secret usage
4. Missing token handling
5. Invalid token handling
6. Admin route protection
7. User order ownership
8. .env safety
9. CORS config
10. Error stack exposure

Do not edit files yet.

Create docs/BACKEND_SECURITY_REVIEW.md.
```

---

## Prompt 9: API testing guide

```txt
Create a step-by-step Postman/Thunder Client API testing guide.

Include:
1. Health check
2. Register
3. Login
4. Save token
5. Create food as admin
6. Try create food as customer and expect 403
7. Get foods
8. Create order as customer
9. Get my orders
10. Get all orders as admin
11. Update order status as admin
12. Common errors and fixes

Save as docs/API_TESTING_GUIDE.md.
```

---

# Part 27: NotebookLM workflow for this module

Create or open:

```txt
Antigravity 2.0 MERN Bootcamp
```

Add these sources:

```txt
1. 09-module-07-backend-implementation.md
2. Express routing/middleware/error-handling docs
3. Mongoose schema/model/validation docs
4. Zod docs
5. jsonwebtoken docs
6. bcrypt docs
7. MongoDB Atlas docs
8. Your API contract
9. Your database schema
10. Your authorization matrix
11. Your backend API test report
```

---

## NotebookLM Prompt 1: Study Guide

```txt
Create a beginner-friendly study guide for backend implementation.

Audience:
Junior MERN developers using Antigravity.

Explain:
1. Express backend architecture
2. Route-controller-service-model flow
3. TypeScript backend setup
4. Environment variables
5. MongoDB/Mongoose connection
6. User model and password hashing
7. JWT authentication
8. Role-based authorization
9. Zod validation
10. Food API
11. Order API
12. Error handling
13. API testing
14. Common mistakes
15. Practice checklist
```

---

## NotebookLM Prompt 2: Backend Review

```txt
Review my backend plan and implementation notes.

Check:
1. Does backend match API_CONTRACT.md?
2. Does database model match DATABASE_SCHEMA.md?
3. Are auth and roles safe?
4. Are API responses consistent?
5. Are validation and error handling included?
6. What should I test first?
7. What is risky before frontend integration?

Return:
- Strong parts
- Missing parts
- Security risks
- API testing checklist
- Fix recommendations
```

---

## NotebookLM Prompt 3: Interview Explanation

```txt
Help me explain my backend architecture in an interview.

Create:
1. 30-second explanation
2. 1-minute explanation
3. Technical explanation
4. Auth flow explanation
5. Authorization explanation
6. API structure explanation
7. Error handling explanation
8. One challenge and how I solved it
```

---

## NotebookLM Prompt 4: Error Debugging Helper

```txt
Create a backend debugging checklist.

Include fixes for:
1. Server not starting
2. TypeScript import errors
3. MongoDB connection failure
4. Invalid JWT
5. Missing Authorization header
6. 403 admin access
7. Zod validation error
8. Mongoose validation error
9. CORS error
10. Duplicate email error
```

---

# Part 28: Required video resources

Watch at least two videos.

Search YouTube:

```txt
Express TypeScript MongoDB REST API tutorial
MERN JWT authentication bcrypt tutorial
Express middleware error handling tutorial
Mongoose schema validation tutorial
Zod Express validation tutorial
Role based authorization Express JWT tutorial
```

Recommended video types:

| Video type | Why |
|---|---|
| Express + TypeScript API tutorial | Helps backend setup |
| Mongoose model/schema tutorial | Helps database models |
| JWT + bcrypt auth tutorial | Helps authentication |
| Role-based authorization tutorial | Helps admin/customer permissions |
| Zod validation tutorial | Helps request validation |
| Postman API testing tutorial | Helps manual API verification |

---

## Video learning notes

Create:

```txt
docs/notebooklm/module-07-video-learning-notes.md
```

Use this format:

```md
# Module 7 Video Learning Notes

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

# Part 29: Practice tasks

## Practice Task 1: Setup backend

Create Express + TypeScript backend and confirm:

```txt
GET /health
```

works.

---

## Practice Task 2: Connect MongoDB

Connect MongoDB and verify server starts without DB error.

Document MongoDB setup in:

```txt
docs/BACKEND_ENV_CHECKLIST.md
```

---

## Practice Task 3: Create utilities and middlewares

Create:

```txt
AppError
catchAsync
sendResponse
generateToken
validateRequest
errorHandler
notFound
```

---

## Practice Task 4: Build auth

Build:

```txt
User model
Register API
Login API
JWT generation
Auth middleware
Role middleware
```

Test register/login manually.

---

## Practice Task 5: Build food APIs

Build:

```txt
GET /api/foods
GET /api/foods/:id
POST /api/foods admin
PATCH /api/foods/:id admin
DELETE /api/foods/:id admin
```

Test admin vs customer access.

---

## Practice Task 6: Build order APIs

Build:

```txt
POST /api/orders
GET /api/orders/my-orders
GET /api/orders admin
PATCH /api/orders/:id/status admin
```

Test ownership and role access.

---

## Practice Task 7: Create API testing guide

Create:

```txt
docs/API_TESTING_GUIDE.md
```

---

## Practice Task 8: Complete API test report

Complete:

```txt
docs/BACKEND_API_TEST_REPORT.md
```

Include screenshots if required by mentor.

---

## Practice Task 9: Security review

Complete:

```txt
docs/BACKEND_SECURITY_REVIEW.md
```

---

## Practice Task 10: Fix critical backend issues

Fix:

- Server crash
- MongoDB connection
- Invalid imports
- Missing env variables
- Password returned in response
- Missing auth
- Missing admin role checks
- Validation errors
- Inconsistent response format

Do not add new features during bug fixing.

---

# Part 30: Common mistakes

## Mistake 1: Building backend without API contract

Do not build random routes.

Use:

```txt
docs/API_CONTRACT.md
```

---

## Mistake 2: Returning password

Never return password in register/login/me responses.

---

## Mistake 3: Trusting frontend role

Do not trust:

```json
{
  "role": "admin"
}
```

from frontend request body.

Backend must decide permission.

---

## Mistake 4: No validation

Every important POST/PATCH route should validate input.

---

## Mistake 5: No global error handler

Without global error handling, API errors become inconsistent and difficult to debug.

---

## Mistake 6: No admin protection

Admin routes must use:

```txt
authMiddleware
requireRole("admin")
```

---

## Mistake 7: Storing plain text password

Always hash password before saving.

---

## Mistake 8: Committing `.env`

Never push secrets to GitHub.

---

## Mistake 9: Frontend integration too early

Test backend APIs manually before connecting frontend.

---

# Required deliverables for this module

Submit:

```txt
1. server/ backend project
2. server/.env.example
3. src/app.ts
4. src/server.ts
5. src/config/env.ts
6. src/config/db.ts
7. User model
8. Auth routes/controller/service/validation
9. Auth middleware
10. Role middleware
11. Food model/routes/controller/service/validation
12. Order model/routes/controller/service/validation
13. Global error handler
14. Not found handler
15. Request validation middleware
16. BACKEND_IMPLEMENTATION_PLAN.md
17. BACKEND_MODULE_MAP.md
18. BACKEND_ENV_CHECKLIST.md
19. BACKEND_API_TEST_PLAN.md
20. BACKEND_API_TEST_REPORT.md
21. BACKEND_SECURITY_CHECKLIST.md
22. BACKEND_SECURITY_REVIEW.md
23. API_TESTING_GUIDE.md
24. API testing screenshots
25. NotebookLM Study Guide screenshot
26. NotebookLM backend review screenshot
27. Video learning notes
28. Reflection file
```

---

# Reflection template

Create:

```txt
docs/reflections/09-module-07-backend-implementation-reflection.md
```

Use this format:

```md
# Reflection: Module 7 - Backend Implementation

## What I built
-

## APIs I completed
-

## Models I created
-

## What I learned about Express architecture
-

## What I learned about MongoDB/Mongoose
-

## What I learned about JWT authentication
-

## What I learned about authorization
-

## What I learned about validation
-

## What I learned about error handling
-

## API testing issues I found
-

## What Antigravity helped with
-

## What I had to fix manually
-

## What I will prepare before full-stack integration
-
```

---

# Quiz

## Multiple choice

**1. What is the recommended backend request flow?**

A. Route → Middleware → Controller → Service → Model → Database  
B. CSS → Button → Footer → Logo  
C. Browser → MongoDB directly  
D. README → GitHub → YouTube  

Correct answer: **A**

---

**2. Why should passwords be hashed?**

A. To prevent storing plain text passwords  
B. To make UI colorful  
C. To improve Tailwind  
D. To avoid creating users  

Correct answer: **A**

---

**3. What does JWT help with?**

A. Authenticating requests with a signed token  
B. Styling cards  
C. Creating Figma files  
D. Hosting MongoDB  

Correct answer: **A**

---

**4. What should admin routes use?**

A. authMiddleware and requireRole("admin")  
B. Only hidden frontend buttons  
C. No security  
D. CSS classes  

Correct answer: **A**

---

**5. What is Zod used for in this module?**

A. Runtime request validation  
B. Image optimization only  
C. GitHub deployment  
D. Password hashing  

Correct answer: **A**

---

**6. What should `.env.example` contain?**

A. Placeholder environment variable names without real secrets  
B. Real database password  
C. Real JWT secret  
D. Private access token  

Correct answer: **A**

---

**7. Why should API responses be consistent?**

A. Frontend integration and debugging become easier  
B. It makes backend slower  
C. It removes need for routes  
D. It replaces database schema  

Correct answer: **A**

---

**8. What is the purpose of a global error handler?**

A. Return consistent error responses and avoid uncaught failures  
B. Hide all bugs forever  
C. Change UI colors  
D. Generate mock data  

Correct answer: **A**

---

**9. What should happen when a customer tries to access admin order list?**

A. 403 Forbidden  
B. 200 OK with all orders  
C. Server exposes all data  
D. Password is returned  

Correct answer: **A**

---

**10. What should you do before frontend integration?**

A. Test backend APIs manually  
B. Delete API contract  
C. Skip auth testing  
D. Push `.env` to GitHub  

Correct answer: **A**

---

## Short-answer questions

1. What files are needed for a clean Express module?
2. Why should backend match `API_CONTRACT.md`?
3. What is the difference between authentication and authorization?
4. Why should backend enforce admin permission?
5. What is the purpose of request validation?
6. What should be stored in `.env`?
7. Why should `.env` never be committed?
8. What APIs did you test manually?
9. What is one backend bug you fixed?
10. What must be ready before Module 8 integration?

---

# Mentor evaluation checklist

| Criteria | Pass condition |
|---|---|
| Backend setup | Express + TypeScript server runs |
| Health route | `/health` works |
| Env config | `.env.example` exists and env validation works |
| MongoDB | Database connection works |
| Utilities | AppError/catchAsync/sendResponse/token utility created |
| Error handling | Global error and not-found handlers exist |
| Validation | Zod validation exists for POST/PATCH routes |
| User model | User schema with hashed password |
| Auth API | Register/login work and return token |
| Auth middleware | Protected routes require valid token |
| Role middleware | Admin routes require admin role |
| Food API | Public list/details and admin CRUD work |
| Order API | Create/my-orders/admin/status update work |
| Security | Password not returned, secrets not committed |
| API testing | Test report completed |
| NotebookLM evidence | Study guide and backend review submitted |
| Reflection | Student explains backend flow clearly |

---

# Completion standard

You complete this module only when you can confidently say:

```txt
I can build an Express + TypeScript + MongoDB backend with structured modules, Mongoose models, Zod validation, JWT authentication, role-based authorization, consistent responses, global error handling, and manual API testing before connecting the frontend.
```

After completing this file, continue to:

```txt
10-module-08-fullstack-integration.md
```
