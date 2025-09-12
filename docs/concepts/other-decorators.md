---
sidebar_position: 6
---

# Other Decorators

Nubie provides a set of decorators to easily access and work with different parts of the HTTP request and response lifecycle.  
These can be applied at the parameter level within your controller methods.

---

## Available Decorators

- **`@BearerToken()`** – Extracts the Bearer token from the `Authorization` header.
- **`@BearerTokenPayload()`** – Retrieves the decoded payload from a Bearer token.
- **`@Body()`** – Injects the parsed request body.
- **`@File()`** – Injects a single uploaded file from a multipart/form-data request.
- **`@Files()`** – Injects multiple uploaded files from a multipart/form-data request.
- **`@Headers()`** – Injects all request headers as an object.
- **`@Ip()`** – Retrieves the client’s IP address.
- **`@Param()`** – Extracts a specific route parameter from the URL path.
- **`@Query()`** – Extracts a specific query string parameter from the URL.
- **`@Req()`** – Injects the raw request object from the underlying HTTP framework.
- **`@Res()`** – Injects the raw response object for manual response handling.

---

## Notes

- Use these decorators to simplify access to request data without manually parsing it.
- When using `@Res()` for manual responses, do not return a value from the method to avoid conflicts with Nubie’s automatic response handling.
- Decorators can be combined in a single method to access multiple request components.

---
