---
sidebar_position: 3
---

# Configuration

Nubie supports basic configurations to customize your app behavior.  
All settings are defined in the `Nubie.json` file located at the root of your project.

## Options

- **port**: `number` (default: `4321`)  
  Specifies the host port for running your application.

- **defaultApiVersion**: `number` (default: `1`)  
  Indicates the default API version used for routing.

- **controllersDirectory**: `string` (default: `controllers`)  
  Directory where controller files are stored. Auto importing controller without exporting files

- **buildDir**: `string` (default: `dist`)  
  Directory containing compiled output (e.g., TypeScript build).

- **jwtSeceretKey**: `string` (default: `undefined`)  
  Secret key used for JWT authentication. Must be provided for auth features.

```json
{
  "port": 4321,
  "defaultApiVersion": 1,
  "controllersDirectory": "controllers",
  "buildDir": "dist",
  "jwtSeceretKey": "your-secret-key-here"
}
```
