---
sidebar_position: 1
---

# Welcome to Nubie

**Nubie is a TypeScript WebAPI framework for noobs, gawds, and everyone in between.**  
Built on Express. Inspired by .NET WebAPI. Fueled by decorators, chill vibes, and zero boilerplate.

## 🤔 What is Nubie?

Nubie is what happens when you’re tired of writing the same routing code, fighting middleware, and repeating:

```ts
app.get('/thing', (req, res) => { ... });
```

Over.
And over.
And over again.

With Nubie, you just write a class, sprinkle in some decorators like `@ApiController`, `@HttpGet`, or `@Body`, and _boom_, your API is live.
It handles routing, validation, file uploads, DI, and JWT — with **almost no config**.

---

## ✨ What Makes It Nubie (™️)?

- **🧩 Decorator-Driven** – Define your routes, params, headers, and even uploads with clean annotations.
- **🔐 Auth, Built-in** – Just add `@Roles('admeme')` to protect routes. No more trusting `Bearer banana`.
- **📦 Validation, Outta the Box** – Auto-reject nonsense like `age: "potato"`.
- **💉 Dependency Injection** – Use `@Inject()` to wire up services like a true backend dev.
- **🧼 Minimal Setup** – No `app.use`, no `app.listen`, no stress. Just `createServer()` and go.

---

## 🧠 Who is it for?

- 🐣 **Backend beginners** who want to feel like API wizards.
- 👩‍🔧 **Experienced devs** who want speed and structure without the ceremony.
- 👻 Anyone who thinks writing Express routers over and over again is a form of spiritual punishment.

---

> Made with love (and a little chaos) by [RKS](https://github.com/ronitkrshah)

---
