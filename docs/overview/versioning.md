---
sidebar_position: 4
---

# Versioning

Nubie gives you two handy decorators to manage versioning in your app: `@ApiVersion()` and `@RouteVersion()`. Each takes a number as input (the version), but they behave very differently. Default Version is `1`

---

## ApiVersion

Applies a version globally to **all routes** within the controller.

```ts
@ApiVersion(2)
class AuthController {
  // All routes here are treated as v2
}
```

Think of it as setting the theme for the whole room — every route inside the controller will wear that version badge.

---

## RouteVersion

Applies versioning to a **specific route**, giving you fine-grained control.

```ts
class AuthController {
  @RouteVersion(3)
  @Get("/login")
  loginUser(req, res) {
    // This route is versioned as v3
  }
}
```

Perfect when you want to bump just one route to a newer version without affecting the rest of the controller.

---

## Behavior Summary

| Decorator         | Applies To        | Version Scope            |
| ----------------- | ----------------- | ------------------------ |
| `@ApiVersion()`   | Entire controller | All routes in the class  |
| `@RouteVersion()` | Single route      | Only the decorated route |

---

## Good to Know

- If both decorators are used, `@RouteVersion()` **overrides** `@ApiVersion()` for that specific route.
- You can version routes however you want — Nubie doesn’t judge your versioning scheme. It just follows your lead.
