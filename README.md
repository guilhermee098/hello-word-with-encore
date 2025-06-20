# Hello World with Encore.ts

> A beginner-friendly template demonstrating REST API development with Encore.ts framework

[![License: MPL 2.0](https://img.shields.io/badge/License-MPL_2.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.2.2-blue.svg)](https://www.typescriptlang.org/)
[![Encore](https://img.shields.io/badge/Encore-1.47.3-purple.svg)](https://encore.dev/)
[![Issues](https://img.shields.io/github/issues/guilherme098/hello-word-with-encore)](https://github.com/guilherme098/hello-word-with-encore/issues)

## Table of Contents

- [Project Overview](#project-overview)
- [Getting Started](#getting-started)
- [Usage & Examples](#usage--examples)
- [Architecture & Design](#architecture--design)
- [API Reference](#api-reference)
- [Testing](#testing)
- [Contributing](#contributing)
- [Roadmap & License](#roadmap--license)

## Project Overview

**Hello World with Encore.ts** is a minimal REST API starter project designed to help developers learn the fundamentals of building backend services with [Encore.ts](https://encore.dev/). This template demonstrates core concepts including service creation, API endpoints, and local development workflows.

### Goals

- Provide a simple entry point for Encore.ts beginners
- Demonstrate best practices for TypeScript-based backend development
- Showcase Encore's developer experience and tooling

### Target Audience

- Developers new to Encore.ts framework
- TypeScript developers exploring backend development
- Students learning modern API development patterns

### Core Features

- ✅ Single REST API endpoint with path parameters
- ✅ TypeScript-first development with strict type checking
- ✅ Built-in development dashboard and tracing
- ✅ Unit testing with Vitest
- ✅ One-command deployment to cloud platforms
- ✅ Automatic API documentation generation

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js)
- **Encore CLI** - Install using one of the methods below:

```bash
# macOS
brew install encoredev/tap/encore

# Linux
curl -L https://encore.dev/install.sh | bash

# Windows (PowerShell)
iwr https://encore.dev/install.ps1 | iex
```

### Installation & Setup

1. **Create a new project from this template:**

   ```bash
   encore app create my-hello-app --example=ts/hello-world
   cd my-hello-app
   ```

2. **Or clone this repository:**

   ```bash
   git clone https://github.com/guilherme098/hello-word-with-encore.git
   cd hello-word-with-encore
   npm install
   ```

3. **Start the development server:**

   ```bash
   encore run
   ```

4. **Verify the installation:**

   ```bash
   curl http://localhost:4000/hello/World
   ```

   Expected response:

   ```json
   { "message": "Hello World!" }
   ```

### Quick Start Example

Once your server is running, you can interact with the API:

```bash
# Basic greeting
curl http://localhost:4000/hello/Alice
# Response: {"message": "Hello Alice!"}

# Try different names
curl http://localhost:4000/hello/Developer
# Response: {"message": "Hello Developer!"}
```

Access the development dashboard at [http://localhost:9400](http://localhost:9400) to explore:

- API documentation
- Request traces and performance metrics
- Service architecture visualization

## Usage & Examples

### Common Workflows

**1. Making API Calls**

```bash
# Using curl
curl http://localhost:4000/hello/YourName

# Using JavaScript fetch
const response = await fetch('http://localhost:4000/hello/YourName');
const data = await response.json();
console.log(data.message); // "Hello YourName!"
```

**2. Running Tests**

```bash
# Run all tests
encore test

# Run tests with coverage
npm test
```

**3. Building for Production**

```bash
# Create Docker image
encore build docker my-app

# Deploy to Encore Cloud
git add .
git commit -m "Deploy to cloud"
git push encore
```

### Configuration Options

The project uses standard Encore.ts configuration:

**encore.app** - Main app configuration:

```json
{
  "id": "",
  "lang": "typescript"
}
```

**tsconfig.json** - TypeScript settings with strict mode enabled and ES2022 target.

## Architecture & Design

### High-Level Architecture

```
┌─────────────────┐    HTTP GET     ┌──────────────────┐
│   HTTP Client   │ ─────────────► │   Encore.ts      │
│                 │                │   Runtime        │
└─────────────────┘                └──────────────────┘
                                            │
                                            ▼
                                   ┌──────────────────┐
                                   │  Hello Service   │
                                   │                  │
                                   │  GET /hello/:name│
                                   └──────────────────┘
```

### Key Components

1. **Service Definition** (`hello/encore.service.ts`)

   - Defines the "hello" microservice
   - Establishes service boundaries

2. **API Endpoint** (`hello/hello.ts`)

   - Implements the GET `/hello/:name` endpoint
   - Handles request/response logic with type safety

3. **Test Suite** (`hello/hello.test.ts`)
   - Unit tests for API functionality
   - Demonstrates testing patterns

### Data Flow

1. HTTP request received at `/hello/:name`
2. Encore router extracts `name` parameter
3. Handler function processes request
4. Response formatted as JSON with greeting message
5. HTTP response sent to client

## API Reference

### Endpoints

#### GET /hello/:name

Returns a personalized greeting message.

**Parameters:**

- `name` (string, required) - Name to include in greeting

**Request:**

```http
GET /hello/World HTTP/1.1
Host: localhost:4000
```

**Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "message": "Hello World!"
}
```

**Example Usage:**

```bash
curl http://localhost:4000/hello/Alice
```

## Testing

### Running Tests

```bash
# Run all tests
encore test

# Run tests in watch mode
npm test

# Run with verbose output
npm test -- --reporter=verbose
```

### Test Structure

The project includes unit tests using Vitest:

```typescript
// hello/hello.test.ts
import { describe, expect, test } from "vitest";
import { get } from "./hello";

describe("get", () => {
  test("should combine string with parameter value", async () => {
    const resp = await get({ name: "world" });
    expect(resp.message).toBe("Hello world!");
  });
});
```

### Writing Additional Tests

To add more tests, create `.test.ts` files in your service directories. Encore automatically discovers and runs them.

## Contributing

We welcome contributions to improve this learning template!

### Code Style Guidelines

- Follow TypeScript best practices
- Use meaningful variable and function names
- Add JSDoc comments for public APIs
- Maintain consistent indentation (2 spaces)

### Development Workflow

1. **Fork the repository**
2. **Create a feature branch:**
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes and add tests**
4. **Run the test suite:**
   ```bash
   encore test
   ```
5. **Commit your changes:**
   ```bash
   git commit -m "Add: your feature description"
   ```
6. **Push to your fork and submit a pull request**

### Reporting Issues

- Use the [GitHub issue tracker](https://github.com/guilherme098/hello-word-with-encore/issues)
- Provide clear reproduction steps
- Include error messages and environment details

## Roadmap & License

### Current Status

This project is a stable learning template suitable for Encore.ts beginners.

### Future Considerations

While this template focuses on simplicity, developers can extend it with:

- Database integration
- Authentication systems
- Additional API endpoints
- Middleware implementation

### License

This project is licensed under the Mozilla Public License 2.0 - see the [LICENSE](LICENSE) file for details.

---

**Ready to build something amazing?** 🚀

- 📚 [Encore.ts Documentation](https://encore.dev/docs/ts)
- 💬 [Community Discord](https://encore.dev/discord)
- 🐛 [Report Issues](https://github.com/guilherme098/hello-word-with-encore/issues)
- ⭐ [Star this repo](https://github.com/guilherme098/hello-word-with-encore) if it helped you learn!
