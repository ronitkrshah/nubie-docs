---
sidebar_position: 6
---

# Request & Response Decorators

Nubie equips you with expressive decorators to tap into the HTTP request lifecycle with ease — from accessing headers to enforcing required ones, we’ve got you covered.

---

## Parameter-Level Decorators

These decorators inject helpful request components directly into your route handlers.

### `@Req()`

Injects the raw request object (`req`) from the underlying HTTP framework.

```ts
@HttpPost("/login")
async loginAsync(@Req() req) {
  console.log(req.body);
}
```

### `@Res()`

Injects the raw response object (`res`). Useful for manually crafting responses.

```ts
@HttpPost("/custom")
async sendCustomAsync(@Res() res) {
  res.status(200).send("Manual response sent!");
  // ⛔ Important: Don't return anything from this method if you send response manually.
}
```

> 🧠 Nubie handles response dispatching for you unless you go manual. If you send a response using `res`, **do not return anything** from your handler method — doing so may result in unexpected behavior.

### `@Headers()`

Injects the complete headers from the incoming request.

```ts
@HttpGet("/debug")
async logHeadersAsync(@Headers() headers) {
  console.log("Headers:", headers);
}
```

---

## Method-Level Header Enforcement

### `@Header("x-custom-key")`

Use this to declare that a specific header **must** be present in the incoming request. If it’s missing, Nubie throws a descriptive error automatically.

```ts
@HttpGet("/secure")
@Header("x-api-key")
async secureRouteAsync(@Req() req) {
  // Will only run if x-api-key is present
}
```

> 🔒 Great for enforcing things like auth tokens, custom headers, or tracing IDs.
