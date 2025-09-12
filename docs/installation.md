---
sidebar_position: 2
---

# Installation

Ready to leave boilerplate behind and build your first Nubie app?  
Great choice. Let’s get you up and running — fast, clean, and frustration-free.

## 1. Clone the Starter Project

Start by cloning the the starter template:

```bash
git clone https://github.com/ronitkrshah/nubie-starter-template.git MyApi --depth=1
```

This gives you a ready-to-use Nubie project with everything preconfigured.

## 2. Install Dependencies

You can also use `yarn` or `pnpm` if preferred.

```bash
cd MyApi
npm install   # or yarn / pnpm install
```

## 3. Run the Server

Compile your TypeScript project and start the server:

```bash
npx tsc && node build/index.js
```

Your API will be live at: `http://localhost:8080/api/v1`
