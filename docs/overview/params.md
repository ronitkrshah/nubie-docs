---
sidebar_position: 3
---

# Validation & Params

No more `"age": "banana"` bugs. Nubie has built-in support for body validation using DTOs (Data Transfer Objects). It uses the popular `class-validator` and `class-transformer` libraries under the hood.

---

## Request Body

### Setup

Run this command to install the required dependencies:

```bash
npm install class-validator class-transformer
```

That’s it. Nubie hooks into them automatically.

---

### Basic Usage

Let’s say you want to validate a request body for creating a user. First, create a DTO (data transfer object) using `class-validator` decorators.

```ts
// contracts/authentication/RegisterRequest.ts
import { IsEmail, IsString, MinLength } from "class-validator";

export class RegisterRequest {
  @IsEmail()
  email: string;

  @IsString()
  @MinLength(6)
  password: string;
}
```

Now use it in your controller with `@BodyValidation()`:

```ts
import {
  ApiController,
  HttpPost,
  Body,
  HttpResponse,
  BodyValidation,
} from "nubie";
import { RegisterRequest } from "../contracts/authentication";

@ApiController()
class AuthController {
  @HttpPost("register")
  @BodyValidation(CreateUserDto)
  public async registerUserAsync(@Body() user: RegisterRequest) {
    // ✅ user is already validated and transformed
    return HttpResponse.Created({ message: "User registered!" });
  }
}
```

---

## Query Params

### Basic Usage

```ts
import {
  ApiController,
  HttpPost,
  Body,
  HttpResponse,
  Query,
  QueryType,
} from "nubie";

@ApiController()
class UsersController {
  @HttpGet("all")
  public async getUsersAsync(
    @Query("search", QuerType.Required) search: string,
    @Query("optional") search?: string
  ) {
    return HttpResponse.Ok([{ id: 1, username: "Meow" }]);
  }
}
```

## Route Params

### Basic Usage

```ts
import { ApiController, HttpPost, Body, HttpResponse, Param } from "nubie";

@ApiController()
class UsersController {
  @HttpGet("find/:id")
  public async getUsersAsync(@Param("id") id: string) {
    return HttpResponse.Ok({ id });
  }
}
```

---

## What Happens If Validation Fails?

If validation fails, Nubie automatically returns:

- HTTP Status: `400 Bad Request`
- A JSON body with detailed validation errors

No need to manually write validation logic — Nubie’s gotchu, noob gawd 😎.
