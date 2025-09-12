---
sidebar_position: 9
---

# Error Handling

Nubie provides a flexible mechanism for handling application errors through the `setErrorHandler()` method.  
This allows you to define a **custom error handler** or rely on Nubie’s **default error response format**.

---

## Default Error Response

If no custom error handler is configured, Nubie automatically returns a standardized JSON error response:

```json
{
  "message": "Internal Server Error",
  "timestamp": "2025-09-12T18:45:16.813Z",
  "path": "/api/v1/cars/all",
  "method": "GET"
}
```

### Fields:

- **message** – A human-readable error message.
- **timestamp** – ISO 8601 timestamp of when the error occurred.
- **path** – The request path that triggered the error.
- **method** – The HTTP method of the request.

### Parametres

| Parameter               | Type     | Required | Description                                                                                                   |
| ----------------------- | -------- | -------- | ------------------------------------------------------------------------------------------------------------- |
| errorHandler            | Function | No       | Custom error handling function. Receives the error, request, response, and next function.                     |
| useDefaultErrorResponse | boolean  | No       | If true, applies Nubie’s default error response format even when a custom handler is used. Defaults to false. |
