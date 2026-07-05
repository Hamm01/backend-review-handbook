# 01 What is Node.js

> **Node.js is an open-source JavaScript runtime built on Google's V8 JavaScript engine that enables JavaScript to execute outside of a web browser, allowing developers to build scalable server-side applications, command-line tools, automation scripts, APIs, and distributed systems using JavaScript.**

---

# Overview

Before Node.js was introduced, JavaScript had only one purpose: **running inside a web browser**.

Browsers such as Chrome, Firefox, Safari, and Edge execute JavaScript to make web pages interactive. JavaScript could manipulate HTML, respond to user events, validate forms, update the DOM, make AJAX requests, and perform animations.

However, JavaScript had one major limitation:

> **It could not directly interact with the operating system.**

For example, browser JavaScript cannot:

- Read files from your computer
- Create folders
- Open TCP sockets
- Listen on HTTP ports
- Access system processes
- Create web servers
- Communicate directly with databases

These restrictions exist for security reasons. Imagine opening a website that could immediately delete files from your computer—that would be catastrophic.

Node.js solves this problem.

Instead of executing JavaScript inside a browser, Node.js executes JavaScript inside its own runtime environment and provides additional APIs that allow JavaScript to interact with the operating system.

Those APIs include modules such as:

- `fs` → File System
- `path` → File and directory paths
- `http` → HTTP Server
- `https` → Secure HTTP Server
- `net` → TCP Networking
- `crypto` → Cryptography
- `stream` → Data Streaming
- `os` → Operating System Information
- `child_process` → Execute system processes
- `worker_threads` → Multithreading

These APIs are **not part of JavaScript itself.**

They are APIs provided by the Node.js runtime.

Think of Node.js as an environment that gives JavaScript additional superpowers.

---

# Why this exists

Understanding _why_ Node.js exists is far more important than memorizing its APIs.

Let's travel back before Node.js existed.

Around 2008, backend development primarily relied on technologies such as:

- PHP
- Java Servlets
- ASP.NET
- Ruby on Rails
- Python (Django)

Most web servers followed a request-per-thread model.

A simplified flow looked like this:

```
Client Request

        │

        ▼

Create Thread

        │

        ▼

Read File

        │

        ▼

Query Database

        │

        ▼

Return Response

        │

        ▼

Destroy Thread
```

Creating and managing thousands of operating system threads consumes memory and CPU resources.

Now imagine 20,000 users simultaneously requesting data from a server.

Thousands of threads would need to be created.

Most of those threads would spend their time waiting for slow operations like:

- Database queries
- Reading files
- Network requests
- External APIs

During that waiting time, the CPU is mostly idle.

Ryan Dahl, the creator of Node.js, asked a simple question:

> "Why should an entire thread wait while the operating system reads a file or waits for the database?"

Instead of blocking a thread, Node.js delegates slow operations to the operating system and continues processing other work.

That idea became the foundation of Node.js.

Instead of:

```
Thread

↓

Wait

↓

Wait

↓

Wait

↓

Continue
```

Node.js prefers:

```
Execute

↓

Delegate Slow Work

↓

Continue Processing

↓

Receive Result Later
```

This architecture makes Node.js particularly efficient for I/O-intensive applications.

Examples include:

- REST APIs
- GraphQL Servers
- Chat Applications
- Real-time Dashboards
- File Upload Services
- Notification Systems
- Payment Gateways
- Backend APIs
- Microservices

Notice something important.

Node.js is **not** necessarily faster at computation.

It is faster at **handling many simultaneous I/O operations efficiently.**

---

# Where it's used in projects

Today, Node.js powers thousands of production systems ranging from startups to global technology companies.

Common project types include:

## REST APIs

```
Mobile App

      │

      ▼

Node.js API

      │

      ▼

PostgreSQL
```

This is probably the most common use case.

Examples:

- User Authentication
- Product APIs
- Payment APIs
- Blogging Platforms
- Inventory Systems

---

## Real-Time Applications

```
Users

    │

WebSocket

    │

Node.js

    │

Broadcast

    │

All Connected Clients
```

Examples:

- Chat Applications
- Multiplayer Games
- Live Notifications
- Live Auctions
- Stock Market Dashboards

---

## File Processing

```
Upload

    │

Node.js

    │

Resize Image

    │

Save

    │

Cloud Storage
```

Examples:

- Image Optimization
- Video Compression
- PDF Generation
- CSV Processing
- Backup Systems

---

## Command-Line Tools

Many developer tools are built with Node.js.

Examples include:

- Vite
- ESLint
- Prettier
- TypeScript Compiler
- npm
- pnpm
- Turborepo

When you execute:

```bash
npm install
```

or

```bash
npx prisma migrate dev
```

you are executing Node.js programs.

---

## Backend for Frontend (BFF)

A common architecture is:

```
React

      │

Node.js

      │

Authentication

      │

Database

      │

Third-party APIs
```

Node.js acts as the communication layer between frontend applications and backend services.

---

## Automation Scripts

Examples include:

- Sending Emails
- Processing CSV Files
- Migrating Databases
- Scheduled Jobs
- File Backups
- Report Generation

---

## Microservices

```
Authentication Service

Product Service

Order Service

Notification Service

Payment Service
```

Each service may independently run on Node.js.

---

# Installation

Node.js is distributed through official installers for Windows, macOS, and Linux.

Installing Node.js automatically installs:

- Node Runtime
- npm (Node Package Manager)

Verify the installation:

```bash
node --version
```

Example:

```bash
v24.4.1
```

Verify npm:

```bash
npm --version
```

You should also verify that Node is available in your system PATH:

```bash
where node
```

On Linux/macOS:

```bash
which node
```

Professional developers often use **Node Version Manager (nvm)** to manage multiple Node.js versions for different projects.

For example:

```
Project A

Node 22

Project B

Node 24
```

Using a version manager avoids conflicts between projects.

---

# Syntax

The Node.js runtime executes JavaScript files.

Example:

```ts
console.log('Hello Node.js')
```

Run the file:

```bash
node index.js
```

Or, when using TypeScript:

```bash
tsx src/index.ts
```

Node.js simply loads the file, executes it using the V8 JavaScript engine, and exits when there is no more work remaining in the Event Loop.

Unlike browser JavaScript, there is no HTML page involved.

Node.js starts execution from the file you specify.

---

# TypeScript Examples

Modern backend development almost always uses TypeScript.

Example:

```ts
function greet(name: string): string {
  return `Hello ${name}`
}

console.log(greet('Himanish'))
```

TypeScript adds static type checking during development, reducing runtime errors and improving maintainability for large codebases.

Node.js itself executes JavaScript, so TypeScript is transpiled (or executed through tools like `tsx`) before running.

---

# ES Module Example

Modern Node.js projects prefer ES Modules.

Example:

```ts
import fs from 'node:fs/promises'

const content = await fs.readFile('notes.txt', 'utf-8')

console.log(content)
```

Notice the import syntax:

```ts
import fs from 'node:fs/promises'
```

This replaces the older CommonJS syntax:

```js
const fs = require('fs')
```

Throughout this handbook, all examples will use:

- ES Modules
- TypeScript
- Modern Node.js
- Async/Await
- Latest LTS practices

---
