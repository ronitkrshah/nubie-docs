---
sidebar_position: 2
---

# Routing

Nubie supports clean and expressive routing using decorators.  
No need to wire up routes manually — just annotate your methods and you're done.

You can use the following decorators for HTTP methods:

- `@HttpGet()`
- `@HttpPost()`
- `@HttpPut()`
- `@HttpDelete()`
- `@HttpPatch()`

Each decorator corresponds to its HTTP method and defines the route handler inside your controller class.

Every method must return an Object Literal using `HttpResponse` function or undefined If response handled manually

---

## Get

Used to handle `GET` requests.

```ts
import { ApiController, HttpGet, HttpResponse } from "nubie";

@ApiController()
class ProductController {
  @HttpGet("/")
  public async getAllProductsAsync() {
    return HttpResponse.Ok(["apple", "banana", "carrot"]);
  }
}
```

#### ⚠️ Important Note:

**GET** requests should not contain a request body.
Use query parameters or route params instead.

## Post

Used to handle POST requests — perfect for creating stuff.

```ts
import { ApiController, HttpPost, HttpResponse, Body } from "nubie";

@ApiController()
class ProductController {
  @HttpPost("create")
  public async createProductAsync(
    @Body() product: Record<string, string | number>
  ) {
    return HttpResponse.Created({ id: 1, ...product });
  }
}
```

## Put

Used for updating or replacing resources.

```ts
import { ApiController, HttpPut, HttpResponse, Param, Body } from "nubie";

@ApiController()
class ProductController {
  @HttpPut("add/:id")
  public async updateProductAsync(
    @Param("id") id: string,
    @Body() product: Record<string, string | number>
  ) {
    return HttpResponse.Ok({ id, ...product });
  }
}
```

## Delete

Used to delete resources.

```ts
import { ApiController, HttpDelete, HttpResponse, Param } from "nubie";

@ApiController()
class ProductController {
  @HttpDelete("delete/:id")
  public async deleteProductAsync(@Param("id") id: string) {
    return HttpResponse.NoContent();
  }
}
```

## Patch

Used for partial updates.

```ts
import { ApiController, HttpPatch, HttpResponse, Param, Body } from "nubie";

@ApiController()
class ProductController {
  @HttpPatch("update/:id")
  public async patchProductAsync(
    @Param("id") id: string,
    @Body() partialProduct: any
  ) {
    return HttpResponse.Ok({ id, ...partialProduct });
  }
}
```
