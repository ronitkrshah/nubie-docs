---
sidebar_position: 1
---

# Welcome to Nubie

**Nubie is a TypeScript WebAPI framework for nubs, gawds, and curious devs in-between.**  
Built on Express. Inspired by .NET WebAPI. Powered by decorators, zero boilerplate, and the idea that backend code should just make sense.

---

## Why Nubie?

Let’s face it — setting up backend APIs with raw Express can feel like an endless checklist:

- Writing boilerplate routes by hand.
- Parsing inputs manually.
- Wiring up dependencies without a clear pattern.
- Cobbling together middleware.
- Repeating `app.get(...)` until you forget why you started.

Nubie was created to remove that pain.

### A Weekend Experiment

“What if we could write APIs like we do in .NET — but in TypeScript — and actually enjoy it?”

That idea sparked a minimal, decorator-driven, opinionated framework that handles routing, validation, dependency injection, and more without draining your will to live.

---

## What is Nubie?

Nubie is a WebAPI framework built for beginners and seasoned developers alike. It gets you from a blank editor to a working API in record time, with code that’s readable, scalable, and even entertaining to write.

It layers on Express, so you retain all of its power, while providing a modern, intuitive API through decorators such as `@ApiController`, `@HttpPost`, `@Query`, and `@Inject`.

Here’s a simple example:

```ts
@ApiController()
class UsersController {
  private readonly _userService: IUserService;

  public constructor(@Inject("IUserService") userService: IUserService) {
    this._userService = userService;
  }

  @HttpGet("/")
  public async getAllUsersAsync() {
    return HttpResponse.Ok(this.userService.getAll());
  }

  @HttpPost("/")
  @BodyValidation(CreateUserDto)
  public async createUserAsync(@Body() userDto: CreateUserDto) {
    return HttpResponse.Created(this.userService.create(userDto));
  }
}
```

This code is clear, concise, and free of unnecessary wiring.

### What the Code Does

- `@ApiController()` marks the class as an API controller.
- `@Inject("IUserService")` injects a user service implementation.
- `@HttpGet("/")` and `@HttpPost("/")` define GET and POST endpoints on the same route.
- `@BodyValidation(CreateUserDto)` enforces that incoming payloads match the expected format.
- Service methods return structured HTTP responses via `HttpResponse`.

### Final Endpoint Structure

By convention, Nubie uses `v1` as the global route prefix and derives the base path from the controller name.

UsersController → `/users`

```
[GET] http://localhost:4321/api/v1/users
[POST] http://localhost:4321/api/v1/users
```

Your route decorators operate relative to this base, with no extra configuration necessary.

---

## Key Features

- Decorator-driven routing, validation, and input parsing.
- Built-in Auth & Roles – Lock routes behind `@Roles('admin')` and trust JWTs.
- Automatic request validation that stops invalid data before it reaches your logic.
- Simple dependency injection via `@Inject()`.
- Zero boilerplate: skip manual middleware setup and response formatting.
- Plug-and-play Express compatibility — use any Express middleware under the hood.

Made with care by [RKS](https://github.com/ronitkrshah)
