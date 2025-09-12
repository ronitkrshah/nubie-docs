---
sidebar_position: 3
---

# Validation & Parameters

Nubie provides built‑in support for request validation using **DTOs** (Data Transfer Objects).  
It integrates seamlessly with the popular [`class-validator`](https://github.com/typestack/class-validator) and [`class-transformer`](https://github.com/typestack/class-transformer) libraries to ensure incoming data is validated and transformed before reaching your business logic.

---

## Request Body Validation

### Setup

Install the required dependencies:

```bash
npm install class-validator class-transformer
```

Nubie automatically hooks into these libraries — no additional configuration is required.

### Basic Usage

To validate a request body, define a DTO class and annotate its properties with class-validator decorators.

```ts
import { IsEmail, IsString, MinLength } from "class-validator";

export class RegisterRequest {
  @IsEmail()
  email: string;

  @IsString()
  @MinLength(6)
  password: string;
}
```

Use the DTO in your controller with the `@BodyValidation()` decorator:

```ts
import {
  ApiController,
  HttpPost,
  Body,
  HttpResponse,
  BodyValidation,
} from "nubie";
import { RegisterRequest } from "./RegisterRequest";

@ApiController()
class AuthController {
  @HttpPost("register")
  @BodyValidation(RegisterRequest)
  public async registerUserAsync(@Body() user: RegisterRequest) {
    // The 'user' object is validated and transformed before this point
    return HttpResponse.Created({ message: "User registered successfully." });
  }
}
```

## Query Parameters

Use the `@Query()` decorator to extract and optionally validate query string parameters.

```ts
import { ApiController, HttpGet, HttpResponse, Query, QueryType } from "nubie";

@ApiController()
class UsersController {
  @HttpGet("all")
  public async getUsersAsync(
    @Query("search", QueryType.Required) search: string,
    @Query("role") role?: string
  ) {
    return HttpResponse.Ok([{ id: 1, username: "ExampleUser" }]);
  }
}
```

> Notes: `QueryType.Required` enforces that the parameter must be present. Omit the second argument for optional parameters.

## Route Parameters

Use the `@Param()` decorator to extract values from dynamic segments in the route path.

```ts
import { ApiController, HttpGet, HttpResponse, Param } from "nubie";

@ApiController()
class UsersController {
  @HttpGet("find/:id")
  public async getUserByIdAsync(@Param("id") id: string) {
    return HttpResponse.Ok({ id });
  }
}
```

```js
// Example Request
GET /api/v1/users/find/42 → { "id": "42" } -->
```

## Validation Failure Response

If validation fails, Nubie automatically returns:

- HTTP Status: 400 Bad Request
- Response Body: JSON object containing detailed validation errors

This eliminates the need to manually implement validation checks in your controllers.
