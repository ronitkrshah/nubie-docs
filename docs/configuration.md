---
sidebar_position: 3
---

# Configuration

Nubie supports simple, centralized configuration through a `Nubie.json` file at the root of your project.  
Use it to control your app’s behavior without diving into code.

## Available Options

- **port**: `number` (default: `4321`)  
  The port your application will listen on when the server starts.

- **defaultApiVersion**: `number` (default: `1`)  
  Sets the default API version for route prefixing. Useful for versioned APIs like `/api/v1`.

- **controllersDirectory**: `string` (default: `"controllers"`)  
  Folder where your controller files are located. Nubie will auto-discover and register them — no need to manually import anything.

- **buildDir**: `string` (default: `"dist"`)  
  Directory where your compiled (built) project lives. Nubie uses this path to load runtime files.

- **jwtSecretKey**: `string` (default: `undefined`)  
  Secret key used to verify and sign JWT tokens. Required if you’re using auth decorators like `@Roles()`.

## Example `Nubie.json`

```json
{
  "port": 4321,
  "defaultApiVersion": 1,
  "controllersDirectory": "controllers",
  "buildDir": "dist",
  "jwtSecretKey": "your-secret-key-here"
}
```

> All fields are optional. Nubie will fall back to safe defaults if you leave something out.
