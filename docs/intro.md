---
sidebar_position: 1
---

# Welcome to Nubie

**Nubie is a small TypeScript WebAPI framework designed to simplify backend development.**  
Built on Express and inspired by the structure of .NET WebAPI, Nubie introduces a clean, decorator-based approach to building APIs with minimal configuration and maximum clarity.

---

## Purpose

Backend development can often feel overwhelming—especially when starting from scratch with raw Express. Nubie was created to reduce that complexity and provide a more intuitive way to build APIs in TypeScript.

Whether you're exploring backend development for the first time or looking for a more structured alternative to manual route handling, Nubie offers a streamlined experience focused on productivity and readability.

## Key Benefits

- **Minimal Setup**: Get started quickly without writing boilerplate code.
- **Declarative Routing**: Define endpoints using decorators like `@HttpGet` and `@HttpPost`.
- **Built-in Validation**: Enforce input structure with DTOs and decorators.
- **Dependency Injection**: Keep your architecture modular and testable.
- **Role-Based Authorization**: Secure routes with `@Roles()` and JWT support.
- **Express Compatibility**: Use existing middleware and tools seamlessly.

## Routing Convention

Nubie uses a default route prefix `(/api/v1)` and derives controller paths from class names:
| Controller Class | Route Path |
|--------------|--------------|
| UsersController | /api/v1/users |
| OrdersController | /api/v1/orders |
| AuthController | /api/v1/auth |

No manual configuration is required. Nubie uses naming conventions to infer routes, ensuring clarity and reducing setup overhead. These are configurable.

## Naming Convention

To maintain consistency and avoid ambiguity, Nubie enforces strict naming conventions for both controllers and their methods.

### Controller Naming

- All controller classes must end with `Controller`.
- The route path is derived by removing the Controller suffix and converting the name to lowercase.

```ts
// Correct
class ProductsController {} → /api/v1/products

// Incorrect
class ProductHandler {} → Not recognized as a controller
```

### Method Naming

- Method names should be descriptive and action-oriented, typically ending with `Async` to indicate asynchronous behavior.
- Nubie does not infer routes from method names; instead, decorators like `@HttpGet()` or `@HttpPost()` define the HTTP verb and path.
- Methods must be an `AsyncFunction`

```ts
@HttpGet("/")
async getAllProductsAsync() { ... }

@HttpPost("/")
async createProductAsync(@Body() dto: CreateProductDto) { ... }

```

## A Weekend Experiment

“What if we could write APIs like we do in .NET — but in TypeScript — and actually enjoy it?”

That idea sparked Nubie: a small, decorator-driven framework that handles routing, validation, and dependency injection with minimal setup. It’s not trying to be enterprise-ready—it’s trying to be developer-friendly.

Made with love by [RKS](https://github.com/ronitkrshah)
