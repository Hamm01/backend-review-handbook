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

Node.js Runtime

│

├── File System APIs
│ ├── readFile()
│ ├── writeFile()
│ ├── mkdir()
│ └── createReadStream()
│
├── Networking APIs
│ ├── createServer()
│ ├── Socket
│ └── HTTP
│
├── Cryptography
│ ├── randomBytes()
│ ├── createHash()
│ └── createHmac()
│
├── Process APIs
│ ├── process.env
│ ├── process.cwd()
│ └── process.exit()
│
└── OS APIs
├── cpus()
├── hostname()
└── platform()

---

# Performance Notes

Writing correct code is only the first step.

A production backend must also be **fast**, **efficient**, and **scalable**.

Node.js became popular not because JavaScript is faster than Java or Go, but because its runtime efficiently handles thousands of concurrent I/O operations.

Understanding where Node.js performs well—and where it does not—is essential for designing reliable systems.

---

## Node.js Excels at I/O-Bound Workloads

An I/O-bound application spends most of its time waiting for external resources.

Examples include:

- Reading files
- Writing files
- Database queries
- Calling external APIs
- Sending emails
- Uploading images
- Downloading files
- Waiting for user input

Typical request flow:

```
Client

↓

Express

↓

Database Query

↓

Waiting...

↓

Database Returns Result

↓

Response
```

Notice that while waiting for the database, the CPU is mostly idle.

Instead of blocking the entire application, Node.js allows other requests to continue executing.

This is why Node.js can efficiently serve thousands of simultaneous users.

---

## Node.js Is Not Ideal for CPU-Bound Workloads

CPU-bound tasks continuously use the processor for calculations.

Examples include:

- Video encoding
- Image rendering
- Machine Learning
- Cryptocurrency mining
- Scientific simulations
- Large mathematical computations

Imagine this code:

```ts
function calculate() {
  while (true) {}
}

calculate()
```

Although this example is unrealistic, it demonstrates an important concept.

Because JavaScript executes on the main thread, an infinite computation prevents Node.js from processing any other requests.

Every incoming request waits until the computation finishes.

This is known as **blocking the Event Loop**.

When CPU-intensive work is unavoidable, common solutions include:

- Worker Threads
- Child Processes
- Separate Microservices
- Dedicated Compute Servers
- Job Queues

We'll explore each of these later in the handbook.

---

## Prefer Asynchronous APIs

Node.js usually provides both synchronous and asynchronous versions of many APIs.

Example:

```ts
readFileSync()
```

vs.

```ts
await readFile()
```

The synchronous version blocks execution.

The asynchronous version allows Node.js to continue handling other tasks while the operating system performs the work.

For backend servers, asynchronous APIs should almost always be preferred.

---

## Streams Reduce Memory Usage

Consider reading a 5 GB log file.

Option 1:

```
Entire File

↓

Memory

↓

Process
```

Memory usage:

```
≈ 5 GB RAM
```

Option 2:

```
64 KB

↓

Process

↓

64 KB

↓

Process

↓

64 KB

↓

Process
```

Memory usage:

```
≈ Few Kilobytes
```

This difference becomes significant when hundreds of users upload files simultaneously.

Streams are one of the biggest reasons Node.js performs well for file-processing workloads.

---

## Avoid Blocking the Event Loop

The Event Loop is the heart of every Node.js application.

Blocking it means blocking **every connected client**.

Examples of operations that can block the Event Loop:

- Large JSON parsing
- Heavy loops
- Synchronous filesystem operations
- Compression
- Encryption
- Huge object cloning

A senior engineer constantly asks:

> "Will this operation prevent other requests from executing?"

If the answer is yes, another architecture should be considered.

---

# Security Considerations

Security begins long before deployment.

Many vulnerabilities appear because developers misuse the runtime rather than because Node.js itself is insecure.

---

## Never Trust Client Input

Everything arriving from the client should be considered untrusted.

Examples include:

- Query Parameters
- Request Body
- Headers
- Uploaded Files
- Cookies

Always validate incoming data before using it.

Later chapters will introduce:

- Zod
- express-validator
- Schema Validation
- DTO Validation

---

## Never Store Secrets in Source Code

Avoid code like this:

```ts
const JWT_SECRET = 'mysecret'
```

Instead:

```ts
const JWT_SECRET = process.env.JWT_SECRET
```

Store sensitive values inside environment variables.

Examples include:

- Database Passwords
- API Keys
- JWT Secrets
- OAuth Credentials
- Cloud Storage Keys

---

## Keep Dependencies Updated

A backend application often depends on hundreds of packages.

Each dependency may contain security vulnerabilities.

Regularly update packages and review security advisories.

Useful command:

```bash
npm audit
```

We'll discuss dependency management later in the handbook.

---

## Principle of Least Privilege

Applications should receive only the permissions they actually require.

Examples:

- Read-only database accounts
- Limited cloud permissions
- Restricted filesystem access

Reducing permissions limits damage if an attacker compromises the application.

---

## Sanitize File Uploads

Never assume uploaded files are safe.

Always validate:

- File type
- MIME type
- Extension
- File size

Store uploads outside publicly accessible directories whenever possible.

---

# Production Notes

Production systems differ significantly from tutorial projects.

The following practices are considered standard in modern backend development.

---

## Use Environment Variables

Never hardcode:

- API Keys
- Passwords
- Database URLs
- JWT Secrets

Use:

```
.env
```

or your cloud provider's secret management system.

---

## Log Everything Important

Useful logs include:

- Requests
- Errors
- Authentication
- Payments
- Database failures

Avoid logging sensitive information such as passwords or tokens.

---

## Graceful Shutdown

Servers should close cleanly.

Typical shutdown sequence:

```
Receive SIGTERM

↓

Stop Accepting Requests

↓

Finish Active Requests

↓

Close Database

↓

Close Redis

↓

Exit
```

Improper shutdown can corrupt data or interrupt active users.

---

## Health Checks

Production servers expose endpoints like:

```
GET /health
```

or

```
GET /ready
```

These endpoints help load balancers determine whether an application is healthy.

---

## Monitoring

Applications should expose metrics including:

- CPU Usage
- Memory Usage
- Request Duration
- Error Rate
- Database Latency

Monitoring helps identify issues before users notice them.

---

## Think Like a Senior Engineer

A junior developer might ask:

> "How do I read a file?"

A senior engineer asks:

> "Should I read the whole file into memory?"

---

A junior developer asks:

> "How do I hash passwords?"

A senior engineer asks:

> "What hashing algorithm is appropriate, and what are the security trade-offs?"

---

A junior developer asks:

> "How do I connect to PostgreSQL?"

A senior engineer asks:

> "How many concurrent database connections can this application safely maintain?"

---

A junior developer asks:

> "Can Node.js do this?"

A senior engineer asks:

> "Should Node.js be responsible for doing this?"

Learning APIs makes you productive.

Learning these questions makes you a backend engineer.

---

# Interview Questions

## Junior Level

### Q1. What is Node.js?

### Q2. Is Node.js a programming language?

### Q3. What is V8?

### Q4. Why can't browser JavaScript read local files?

### Q5. What is npm?

### Q6. What is the difference between Node.js and JavaScript?

### Q7. What are built-in modules?

### Q8. Why do we use `process.env`?

### Q9. What is the purpose of the `fs` module?

### Q10. What is the difference between CommonJS and ES Modules?

---

## Mid-Level

### Q1. Why is Node.js suitable for APIs?

### Q2. Explain asynchronous programming.

### Q3. Why should synchronous APIs be avoided in servers?

### Q4. What happens when `readFile()` is called?

### Q5. Explain Streams.

### Q6. What is the Event Loop?

### Q7. Why does Node.js perform well for I/O operations?

### Q8. When should Worker Threads be used?

### Q9. What is libuv?

### Q10. How does Express relate to Node.js?

---

## Senior Level

### Q1.

Design a backend that supports one million concurrent users.

Would Node.js be an appropriate choice?

Explain your reasoning.

---

### Q2.

How would you process 100 GB log files?

Would you use `readFile()` or Streams?

Why?

---

### Q3.

How would you prevent Event Loop blocking during image processing?

---

### Q4.

How would you design graceful shutdown for a production Node.js service?

---

### Q5.

When would you choose Go or Java over Node.js?

Explain the architectural trade-offs.

---

### Q6.

How would you profile a slow Node.js application?

---

### Q7.

How would you detect memory leaks in production?

---

### Q8.

Explain Node.js architecture from JavaScript execution down to the operating system.

---

# Summary

Node.js is not a programming language.

It is not a framework.

It is not a web server.

Node.js is a JavaScript runtime that extends JavaScript with operating system capabilities, allowing developers to build scalable backend applications.

Its greatest strength lies in handling asynchronous, I/O-heavy workloads efficiently.

Node.js achieves this by combining:

- The V8 JavaScript Engine
- The Node.js Runtime
- Built-in APIs
- libuv
- An Event-Driven Architecture

Throughout this handbook, every technology we study—Express, Prisma, Redis, Docker, JWT, Kafka, BullMQ, and many others—will execute inside the Node.js runtime.

Understanding Node.js is therefore the foundation upon which the rest of this handbook is built.

---

# Further Reading

The next recommended chapters are:

1. Event Loop
2. Module System
3. ES Modules
4. package.json
5. npm, pnpm & bun
6. File System (`fs`)
7. Streams
8. Buffer
9. Process
10. Worker Threads

These topics gradually reveal what happens internally when a Node.js application executes.
