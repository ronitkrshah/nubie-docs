---
sidebar_position: 3
---

# Basic Usage

Once your Nubie project is installed and running, you can start building your first API endpoint. Delete all files from `src` directory to start from fresh.

## Step 1: Initialize Nubie

In `src/index.ts`, make sure you have the following setup:

```ts
import { Nubie } from "nubie";

Nubie.createApp().runAsync();
```

This bootstraps the Nubie framework, loads your controllers, and starts the Express server.

## Step 2: Create a Controller

Inside `src/controllers`, create a new file called `HelloController.ts`:

```ts
import { ApiController, HttpGet, HttpResponse } from "nubie";

@ApiController()
class HelloController {
  @HttpGet("/")
  public async sayHelloAsync() {
    return HttpResponse.Ok({ message: "Hello from Nubie!" });
  }
}
```

**Note**: You may have noticed that we didn’t export the `HelloController` class. This is intentional. Nubie automatically scans the `controllers` directory and registers all valid controller classes based on naming conventions. As long as your class name ends with `Controller` and is placed in the correct folder, Nubie will detect and wire it into the application without requiring manual imports or exports. This keeps your codebase clean and focused on logic, not setup.

## Step 3: Run The Server

```bash
npm run dev
```

## Step 4: Visit

```
http://localhost:8080/api/v1/hello
```

You’ll see:

```json
{
  "message": "Hello from Nubie!"
}
```
