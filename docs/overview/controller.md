---
sidebar_position: 1
---

# ApiController

The `@ApiController()` decorator tells Nubie:

> "This class contains API routes. Treat it like a controller."

No manual router setup. No `express.Router()`.  
Just decorate your class and Nubie takes care of the rest.

---

## What is a Controller?

A **controller** is a class that groups related API endpoints together.  
In Nubie, each controller maps to a base route (e.g., `/users`, `/auth`) and contains handler methods for various HTTP verbs like `GET`, `POST`, `PUT`, and `DELETE`.

Think of it as a clean, structured way to organize your routes — instead of scattering them across your app.

Behind the scenes, Nubie:

1. **Scans your `controllers` directory** during app startup.
2. **Finds classes decorated with `@ApiController()`**, whether or not they are exported.
3. **Derives the route prefix** from the class name or custom value (e.g., `UsersController` → `/users`).
4. **Registers decorated methods** (like `@HttpGet()`, `@HttpPost()`, etc.) as route handlers.
5. **Attaches middleware and metadata** like validation, authentication, and DI based on additional decorators.

No registration, no boilerplate, no `app.get()` anywhere in your code.

---

## Basic Example

```ts
import { ApiController, HttpGet, HttpResponse } from "nubie";

@ApiController()
class UsersController {
  @HttpGet("hello")
  public async sayHiAsync() {
    return HttpResponse.Ok({ message: "Hello from Nubie" });
  }
}
```

### What happens here?

- Nubie sees `@ApiController()` and recognizes this class as a route group.
- It detects `UsersController` → `/users` (by convention).
- It registers the method `sayHiAsync()` to handle `GET /users/hello`.

---

## With Route Parameters

```ts
import { ApiController, HttpGet, HttpResponse, Param } from "nubie";

@ApiController()
class UsersController {
  @HttpGet("hello/:name")
  public async sayHiWithNameAsync(@Param("name") name: string) {
    return HttpResponse.Ok({ message: `Hi ${name}, welcome to Nubie!` });
  }
}
```

This maps to:

```bash
GET /api/v1/users/hello/:name
```

Nubie extracts the `name` parameter automatically and injects it into your method using `@Param()`.

---

## Custom Routes

You can override the default route prefix by passing a value to `@ApiController()`:

```ts
@ApiController("accounts")
class AuthController { ... }
```

This would result in:

```bash
GET /api/v1/accounts/...
```

Instead of `/auth`, based on the class name.

---

## Configuration Defaults

Unless overridden, Nubie:

- Uses the **class name (without `Controller`)** as the route prefix.
- Loads all controllers from the `controllers/` directory.
- Automatically maps and registers methods based on decorators.

---

## Naming Conventions (Required)

To keep things consistent and avoid confusion, Nubie enforces two simple naming rules:

### ✅ Controller Class Names

- Must end with `Controller`
- Examples: `UsersController`, `AuthController`, `OrdersController`
- ❌ `User`, `Login`, `API` → will throw an error and stop the app

### ✅ Route Handler Methods

- Must be `async`
- Must end with `Async`
- Examples: `getUserAsync`, `loginAsync`, `deletePostAsync`
- Ensures predictable behavior and helps Nubie auto-map your methods safely

---

## Summary

The `@ApiController()` decorator:

- Marks a class as a controller that contains routes
- Automatically wires up route handlers defined via decorators
- Follows clean naming conventions to keep your app maintainable
- Removes the need for manual registration, file imports, or Express setup

> In short: You focus on writing logic. Nubie handles the boring parts.
