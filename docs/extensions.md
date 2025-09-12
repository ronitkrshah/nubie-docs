---
sidebar_position: 5
---

# Extension Decorators

Nubie provides a robust way to build custom decorators via two abstract classes:

- `MethodExtensionDecorator` — for method-level behaviors (e.g. enforcing headers)
- `ParamExtensionDecorator` — for parameter-level access (e.g. custom param extractors)

These give you full control over request/response handling without diving into middleware manually.

---

## Method-Level Extension: Header Check

Create decorators that run before route handlers and access full Express `req`, `res`, `next`.

### Example: Require Header Key

```ts
import { Request, Response, NextFunction } from "express";
import { MethodExtensionDecorator, NubieError } from "nubie";

class HeaderDecorator extends MethodExtensionDecorator {
  constructor(public readonly key: string) {
    super();
  }

  async executeAsync(
    req: Request,
    res: Response,
    next: NextFunction
  ): Promise<void> {
    if (req.headers[this.key]) return;
    throw new NubieError(
      "MissingRequiredHeader",
      400,
      `${this.key} is missing in request headers`
    );
  }
}

const Header = MethodExtensionDecorator.createDecorator(HeaderDecorator);

export default Header;
```

### Usage

```ts
@HttpGet("/secure-data")
@Header("x-client-id")
async getDataAsync() {

}
```

If the header `x-client-id` is missing, the decorator throws a `400 Bad Request` with a custom error message.

---

## Param-Level Extension: Custom Parameter Access

Build custom parameter decorators that return extracted values — like `req.params`, `req.query`, etc.

### Example: Param Reader

```ts
import { Request, Response, NextFunction } from "express";
import { ParamExtensionDecorator } from "nubie";

class ParamDecorator extends ParamExtensionDecorator {
  constructor(public readonly param: string) {
    super();
  }

  async executeAsync(req: Request): Promise<unknown> {
    return req.params[this.param];
  }
}

const Param = ParamExtensionDecorator.createDecorator(ParamDecorator);

export default Param;
```

### Usage

```ts
@HttpGet("/users/:id")
async getUserAsync(@Param("id") userId: string) {
  console.log("User ID:", userId);
}
```

Automatically extracts the `id` param from the URL and injects it into your handler.
