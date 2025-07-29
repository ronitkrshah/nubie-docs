---
sidebar_position: 1
---

# ApiController

The `@ApiController()` decorator tells Nubie:

> "Hey, this class contains routes you should care about."

That’s it. No manual router setup. No express boilerplate.  
Just decorate a class, and Nubie takes over.

---

## Basic Example

```ts
import { ApiController, HttpGet, HttpResponse } from "nubie";

@ApiController()
class UsersController {
  @HttpGet("hello")
  public async sayHiAsync() {
    return HttpResponse.Ok({ message: "Hello from Nubie 👋" });
  }
}
```

In this example:

- The class is decorated with `@ApiController()`
- The method is decorated with `@HttpGet("hello")`
- This will automatically expose: GET `/hello`

No app.get(), no express.Router() — just clean structure.

---

## What Does @ApiController() Mean?

It means:

- All routes inside this class will start with `users`
- You can define as many methods as you want with decorators like @HttpGet(), @HttpPost(), etc.
- Nubie will register them automatically no need to call or register the controllers. If you defined a class another file.
  No need to export the class. Nubie take care of this automatically

Think of it like grouping related routes in one place.

## With Route Params

```ts
import { ApiController, HttpGet, HttpResponse, Param } from "nubie";

@ApiController()
class UsersController {
  @HttpGet("hello")
  public async sayHiAsync() {
    return HttpResponse.Ok({ message: "Hello from Nubie 👋" });
  }

  @HttpGet("hello/:name")
  public async sayHiWithNameAsync(@Param("name") name: string) {
    return HttpResponse.Ok({ message: `Hi ${name}, welcome to Nubie!` });
  }
}
```

## Options

You can pass your custom route to `@ApiController("my-route")`  
Custom route is optional. By default it uses your class name as Route

> Example: UsersController -> /users

## Run

This will result in the route:

```bash
[GET] http://localhost:4321/api/v1/users/hello
[GET] http://localhost:4321/api/v1/users/hello/:name
```

## Naming Conventions

Nubie follows simple, enforced naming conventions to keep everything clean:

### Controller Naming

All controller classes must end with Controller

> Example: `UsersController`, `AuthController`, `ProductsController`

If you name a controller User or Login, Nubie will raise an Error and stop running

### Method Naming

- All route handler methods must be an `AsyncFunction`
- Method names must end with `Async` suffix  
  Example: `getUserAsync`, `createOrderAsync`, `loginAsync`
  This ensures consistency across your app and helps Nubie auto-register routes with less guesswork.
