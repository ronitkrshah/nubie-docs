---
sidebar_position: 8
---

# Dependency Injection

> _💡 Don’t understand Dependency Injection (DI) or Inversion of Control (IoC)? Totally fine. You can skip this doc and Nubie will still love you._

Nubie gives you straightforward access to DI using [tsyringe](https://github.com/microsoft/tsyringe) under the hood.

## Registering Services

```ts
NubieContainer.addSingleton("IAuthService", GithubAuthService);
// NubieContainer.addTransient("IAuthService", GithubAuthService);

/** Injection */
@ApiController()
class LoginController {
  private readonly _authService: IAuthService;

  constructor(@Inject("IAuthService") authService: IAuthService) {
    this._authService = authService;
  }
}
```

👆 That’s it. Nubie slides the right service into your class when it spins it up. No new, no fuss, just that crisp DI goodness.
