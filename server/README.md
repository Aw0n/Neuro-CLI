<div align="center">

# ⚡ Neuro-CLI - Server & CLI

### Express.js API Server with Orbit CLI Tool

[![Express](https://img.shields.io/badge/Express-5.1-000000?style=for-the-badge&logo=express)](https://expressjs.com/)
[![Node.js](https://img.shields.io/badge/Node.js-Latest-339933?style=for-the-badge&logo=node.js)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Latest-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Prisma](https://img.shields.io/badge/Prisma-6.18-2D3748?style=for-the-badge&logo=prisma)](https://www.prisma.io/)
[![Google AI](https://img.shields.io/badge/Google_AI-SDK-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev/)

[Overview](#-overview) • [Installation](#-installation) • [API Documentation](#-api-documentation) • [CLI Usage](#-orbit-cli)

</div>

---

## 📋 Overview

The **Neuro-CLI Server** is a comprehensive backend solution that provides:

- 🔌 **RESTful API** - Express.js server for web client communication
- 🖥️ **Orbit CLI** - Command-line interface for terminal-based AI interactions
- 🔐 **Authentication** - Better-Auth with device flow support
- 💾 **Database** - PostgreSQL with Prisma ORM
- 🤖 **AI Integration** - Google AI SDK for conversational AI
- 📡 **CORS Support** - Cross-origin requests enabled

## 🏗️ Server Architecture

```mermaid
graph TB
    subgraph "CLI Application"
        CLI_MAIN[🖥️ main.js<br/>CLI Entry Point]
        CLI_COMMANDS[📋 Commands]
        CLI_CHAT[💬 Chat Service]
        CLI_AI[🤖 AI Service]
    end

    subgraph "Express Server"
        EXPRESS[⚡ Express App<br/>Port 3005]
        AUTH_ROUTES[🔐 /api/auth/*]
        SESSION_ROUTES[👤 /api/me]
        DEVICE_ROUTES[📱 /device]
    end

    subgraph "Services & Libraries"
        BETTER_AUTH[🔐 Better-Auth]
        GOOGLE_AI[🤖 Google AI SDK]
        PRISMA_CLIENT[📊 Prisma Client]
    end

    subgraph "Data Layer"
        DATABASE[(🗄️ PostgreSQL)]
    end

    CLI_MAIN --> CLI_COMMANDS
    CLI_COMMANDS --> CLI_CHAT
    CLI_CHAT --> CLI_AI

    CLI_AI --> GOOGLE_AI
    CLI_COMMANDS --> BETTER_AUTH
    CLI_AI --> PRISMA_CLIENT

    EXPRESS --> AUTH_ROUTES
    EXPRESS --> SESSION_ROUTES
    EXPRESS --> DEVICE_ROUTES

    AUTH_ROUTES --> BETTER_AUTH
    SESSION_ROUTES --> BETTER_AUTH

    BETTER_AUTH --> PRISMA_CLIENT
    PRISMA_CLIENT --> DATABASE

    style CLI_MAIN fill:#4CAF50,stroke:#2E7D32,stroke-width:3px,color:#fff
    style EXPRESS fill:#FF9800,stroke:#E65100,stroke-width:3px,color:#fff
    style BETTER_AUTH fill:#9C27B0,stroke:#6A1B9A,stroke-width:3px,color:#fff
    style GOOGLE_AI fill:#F44336,stroke:#C62828,stroke-width:3px,color:#fff
    style DATABASE fill:#607D8B,stroke:#37474F,stroke-width:3px,color:#fff
```

## 🛠️ Technology Stack

### Core Technologies

| Technology      | Version    | Purpose                |
| --------------- | ---------- | ---------------------- |
| **Express**     | 5.1.0      | Web server framework   |
| **Node.js**     | ES Modules | JavaScript runtime     |
| **Prisma**      | 6.18.0     | Database ORM           |
| **PostgreSQL**  | Latest     | Relational database    |
| **Better-Auth** | 1.3.34     | Authentication library |

### AI & ML

| Package            | Purpose                           |
| ------------------ | --------------------------------- |
| **@ai-sdk/google** | Google AI provider integration    |
| **ai**             | Vercel AI SDK for AI interactions |

### CLI Tools

| Package            | Purpose                            |
| ------------------ | ---------------------------------- |
| **commander**      | CLI framework and argument parsing |
| **@clack/prompts** | Beautiful CLI prompts              |
| **inquirer**       | Interactive command-line prompts   |
| **chalk**          | Terminal string styling            |
| **figlet**         | ASCII art text generation          |
| **boxen**          | Terminal boxes                     |
| **ora**            | Terminal spinners                  |
| **yocto-spinner**  | Lightweight spinner alternative    |

### Utilities

| Package             | Purpose                         |
| ------------------- | ------------------------------- |
| **cors**            | Cross-Origin Resource Sharing   |
| **dotenv**          | Environment variable management |
| **marked**          | Markdown parser                 |
| **marked-terminal** | Terminal markdown rendering     |
| **node-fetch**      | HTTP client                     |
| **open**            | Open URLs in browser            |
| **zod**             | Schema validation               |

## 📁 Project Structure

```
server/
├── src/
│   ├── cli/                      # Orbit CLI Application
│   │   ├── main.js              # CLI entry point
│   │   ├── ai/                  # AI service layer
│   │   │   └── google-service.js
│   │   ├── chat/                # Chat implementations
│   │   │   ├── chat-with-ai.js         # Basic chat mode
│   │   │   ├── chat-with-ai-tool.js    # Tool mode
│   │   │   └── chat-with-ai-agent.js   # Agent mode
│   │   └── commands/            # CLI command definitions
│   │       ├── auth/
│   │       │   └── login.js     # login, logout, whoami
│   │       └── ai/
│   │           └── wakeUp.js    # AI chat command
│   │
│   ├── config/                  # Configuration files
│   │   └── ...
│   │
│   ├── lib/                     # Shared libraries
│   │   ├── auth.js             # Better-Auth configuration
│   │   └── ...
│   │
│   ├── services/                # Business logic services
│   │   └── ...
│   │
│   └── index.js                 # Express server entry point
│
├── prisma/
│   ├── schema.prisma           # Database schema
│   └── migrations/             # Database migrations
│
├── .env                        # Environment variables (create from .env.example)
├── .env.example               # Environment template
├── package.json               # Dependencies and scripts
└── README.md                  # This file
```

## 🚀 Installation

### Prerequisites

| Requirement | Version        | Download                                      |
| ----------- | -------------- | --------------------------------------------- |
| Node.js     | 18.x or higher | [nodejs.org](https://nodejs.org/)             |
| PostgreSQL  | 14.x or higher | [postgresql.org](https://www.postgresql.org/) |
| npm         | 9.x or higher  | Included with Node.js                         |

### Setup Steps

1. **Navigate to Server Directory**

   ```bash
   cd server
   ```

2. **Install Dependencies**

   ```bash
   npm install
   ```

3. **Configure Environment Variables**

   ```bash
   cp .env.example .env
   ```

   Edit `.env` with your configuration (see [Environment Variables](#-environment-variables))

4. **Setup Database**

   ```bash
   # Generate Prisma Client
   npx prisma generate

   # Push schema to database
   npx prisma db push

   # (Optional) Open Prisma Studio
   npx prisma studio
   ```

5. **Start Development Server**

   ```bash
   npm run dev
   ```

   Server will run on `http://localhost:3005`

## ⚙️ Configuration

### Environment Variables

Create a `.env` file in the server directory with the following variables:

| Variable             | Description                    | Example                                               | Required              |
| -------------------- | ------------------------------ | ----------------------------------------------------- | --------------------- |
| `DATABASE_URL`       | PostgreSQL connection string   | `postgresql://user:password@localhost:5432/neuro_cli` | ✅ Yes                |
| `BETTER_AUTH_SECRET` | Secret key for auth encryption | `your-secret-key-min-32-chars`                        | ✅ Yes                |
| `BETTER_AUTH_URL`    | Base URL for auth service      | `http://localhost:3005`                               | ✅ Yes                |
| `GOOGLE_AI_API_KEY`  | Google AI API key              | `your-google-ai-api-key`                              | ✅ Yes                |
| `PORT`               | Server port                    | `3005`                                                | ❌ No (default: 3005) |

**Example `.env` file:**

```env
# Database Configuration
DATABASE_URL="postgresql://postgres:password@localhost:5432/neuro_cli"

# Better-Auth Configuration
BETTER_AUTH_SECRET="your-super-secret-key-must-be-at-least-32-characters-long"
BETTER_AUTH_URL="http://localhost:3005"

# Google AI Configuration
GOOGLE_AI_API_KEY="your-google-ai-api-key-here"

# Server Configuration
PORT=3005
```

> [!CAUTION]
> Never commit your `.env` file to version control. The `.env.example` file should only contain template/placeholder values.

### Database Configuration

1. **Create PostgreSQL Database**

   ```bash
   # Using psql
   createdb neuro_cli

   # Or using PostgreSQL CLI
   psql -U postgres
   CREATE DATABASE neuro_cli;
   ```

2. **Update DATABASE_URL**

   ```env
   DATABASE_URL="postgresql://USERNAME:PASSWORD@HOST:PORT/DATABASE"
   ```

3. **Run Migrations**
   ```bash
   npx prisma db push
   ```

## 🔌 API Documentation

### Base URL

```
http://localhost:3005
```

### Endpoints

| Endpoint                | Method | Description                                   | Authentication |
| ----------------------- | ------ | --------------------------------------------- | -------------- |
| `/api/auth/*`           | ALL    | Better-Auth endpoints (login, register, etc.) | Public         |
| `/api/me`               | GET    | Get current session via Bearer token          | Required       |
| `/api/me/:access_token` | GET    | Get session by token (deprecated)             | Public         |
| `/device`               | GET    | Redirect to device code entry page            | Public         |

### API Endpoint Details

#### 1. Authentication Endpoints

**Better-Auth routes** - All auth operations

```http
POST /api/auth/sign-in/email
POST /api/auth/sign-up/email
POST /api/auth/device-code
POST /api/auth/device-code/verify
GET  /api/auth/session
...and more
```

These endpoints are handled by Better-Auth. See [Better-Auth Documentation](https://www.better-auth.com/docs) for complete API reference.

---

#### 2. Get Current Session

**Endpoint:** `GET /api/me`

**Description:** Retrieve current user session using Bearer token authentication

**Headers:**

```http
Authorization: Bearer <access_token>
```

**Response (Success - 200):**

```json
{
  "user": {
    "id": "user_123",
    "name": "John Doe",
    "email": "john@example.com",
    "image": "https://...",
    "emailVerified": true,
    "createdAt": "2024-01-20T10:00:00.000Z",
    "updatedAt": "2024-01-20T10:00:00.000Z"
  },
  "session": {
    "id": "session_123",
    "expiresAt": "2024-02-20T10:00:00.000Z",
    "token": "...",
    "userId": "user_123"
  }
}
```

**Response (Error - 401):**

```json
{
  "error": "No active session"
}
```

---

#### 3. Get Session by Token (Deprecated)

**Endpoint:** `GET /api/me/:access_token`

**Description:** Retrieve session using URL parameter (use Bearer token method instead)

**Parameters:**

- `access_token` (path) - The access token

**Response:** Same as `/api/me`

> [!WARNING]
> This endpoint is deprecated. Use the Bearer token approach with `/api/me` instead for better security.

---

#### 4. Device Code Redirect

**Endpoint:** `GET /device`

**Description:** Redirect to web client device code entry page

**Query Parameters:**

- `user_code` (required) - The device user code

**Example:**

```http
GET /device?user_code=ABCD-1234
```

**Response:** 302 Redirect to `http://localhost:3000/device?user_code=ABCD-1234`

## 🖥️ Orbit CLI

### Overview

**Orbit CLI** is a terminal-based interface for AI interactions with beautiful prompts and real-time responses.

### Installation

The CLI is available through npm scripts:

```bash
# From server directory
npm run cli -- <command> [options]
```

Or install globally:

```bash
# Make CLI available globally
npm link

# Now use from anywhere
orbit <command> [options]
```

### Available Commands

| Command  | Description                  | Usage                   |
| -------- | ---------------------------- | ----------------------- |
| `login`  | Authenticate via device flow | `npm run cli -- login`  |
| `logout` | End current session          | `npm run cli -- logout` |
| `whoami` | Display current user info    | `npm run cli -- whoami` |
| `wakeUp` | Start AI chat session        | `npm run cli -- wakeUp` |

### Command Details

#### Login Command

Authenticate using device flow:

```bash
npm run cli -- login
```

**Flow:**

1. Displays device code and verification URL
2. Opens browser automatically (or manually navigate)
3. Enter code in web interface
4. Approve authentication
5. CLI receives access token
6. Session stored locally

---

#### Logout Command

End current session:

```bash
npm run cli -- logout
```

Clears stored authentication tokens.

---

#### Whoami Command

Display current user information:

```bash
npm run cli -- whoami
```

**Output:**

```
📋 Current User Information
━━━━━━━━━━━━━━━━━━━━━━━━
Name:  John Doe
Email: john@example.com
ID:    user_123
```

---

#### WakeUp Command

Start interactive AI chat:

```bash
npm run cli -- wakeUp
```

**Features:**

- 💬 **Chat Mode** - Standard conversational AI
- 🔧 **Tool Mode** - AI with function calling capabilities
- 🤖 **Agent Mode** - Autonomous AI agent

**Interactive Flow:**

1. Select conversation mode
2. Enter your query
3. Receive AI response (rendered as markdown)
4. Continue conversation or exit

### CLI Features

```mermaid
graph LR
    START[🚀 Start Orbit CLI] --> AUTH{Authenticated?}
    AUTH -->|No| LOGIN[🔐 Run Login]
    AUTH -->|Yes| COMMANDS[📋 Available Commands]

    LOGIN --> DEVICE[📱 Get Device Code]
    DEVICE --> BROWSER[🌐 Open Browser]
    BROWSER --> APPROVE[✅ Approve]
    APPROVE --> TOKEN[🎫 Store Token]
    TOKEN --> COMMANDS

    COMMANDS --> CHAT[💬 WakeUp - Chat]
    COMMANDS --> INFO[👤 Whoami]
    COMMANDS --> EXIT[🚪 Logout]

    CHAT --> MODE{Select Mode}
    MODE --> CHAT_MODE[💭 Chat Mode]
    MODE --> TOOL_MODE[🔧 Tool Mode]
    MODE --> AGENT_MODE[🤖 Agent Mode]

    style START fill:#4CAF50,stroke:#2E7D32,stroke-width:2px,color:#fff
    style LOGIN fill:#FF9800,stroke:#E65100,stroke-width:2px,color:#fff
    style APPROVE fill:#9C27B0,stroke:#6A1B9A,stroke-width:2px,color:#fff
    style CHAT fill:#2196F3,stroke:#1565C0,stroke-width:2px,color:#fff
```

### Example Usage

```bash
# Complete workflow
$ npm run cli -- login
   ___       _     _ _      ____ _     ___
  / _ \ _ __| |__ (_) |_   / ___| |   |_ _|
 | | | | '__| '_ \| | __| | |   | |    | |
 | |_| | |  | |_) | | |_  | |___| |___ | |
  \___/|_|  |_.__/|_|\__|  \____|_____|___|

A Cli based AI tool

🔐 Device Code: ABCD-1234
🌐 Opening browser for authentication...
✅ Authentication successful!

$ npm run cli -- whoami
📋 Current User Information
Name:  John Doe
Email: john@example.com

$ npm run cli -- wakeUp
💬 Select conversation mode:
  [x] Chat
  [ ] Tool
  [ ] Agent

🤖 Enter your message: What is the weather like?
💭 AI: I don't have access to real-time weather data...

$ npm run cli -- logout
👋 Logged out successfully
```

## 💾 Database Schema

### Schema Overview

```mermaid
erDiagram
    User ||--o{ Session : has
    User ||--o{ Account : has
    User ||--o{ Conversation : has
    Conversation ||--o{ Message : contains

    User {
        string id PK
        string name
        string email UK
        boolean emailVerified
        string image
        datetime createdAt
        datetime updatedAt
    }

    Session {
        string id PK
        string token UK
        datetime expiresAt
        string userId FK
        string ipAddress
        string userAgent
        datetime createdAt
        datetime updatedAt
    }

    Account {
        string id PK
        string accountId
        string providerId
        string userId FK
        string accessToken
        string refreshToken
        string idToken
        datetime accessTokenExpiresAt
        datetime refreshTokenExpiresAt
        string scope
        string password
        datetime createdAt
        datetime updatedAt
    }

    Conversation {
        string id PK
        string userId FK
        string title
        string mode
        datetime createdAt
        datetime updatedAt
    }

    Message {
        string id PK
        string conversationId FK
        string role
        string content
        datetime createdAt
    }

    DeviceCode {
        string id PK
        string deviceCode
        string userCode
        string userId
        datetime expiresAt
        string status
        datetime lastPolledAt
        int pollingInterval
        string clientId
        string scope
    }

    Verification {
        string id PK
        string identifier
        string value
        datetime expiresAt
        datetime createdAt
        datetime updatedAt
    }
```

### Table Descriptions

| Table            | Purpose                  | Key Fields                      |
| ---------------- | ------------------------ | ------------------------------- |
| **user**         | User accounts            | id, email, name                 |
| **session**      | Active user sessions     | token, expiresAt, userId        |
| **account**      | OAuth provider accounts  | providerId, accessToken, userId |
| **conversation** | AI conversation threads  | mode (chat/tool/agent), userId  |
| **message**      | Individual messages      | role, content, conversationId   |
| **deviceCode**   | Device flow codes        | userCode, deviceCode, status    |
| **verification** | Email/phone verification | identifier, value, expiresAt    |

### Conversation Modes

| Mode    | Description                             |
| ------- | --------------------------------------- |
| `chat`  | Standard conversational AI interaction  |
| `tool`  | AI with function calling capabilities   |
| `agent` | Autonomous AI agent with task execution |

### Message Roles

| Role        | Description                      |
| ----------- | -------------------------------- |
| `user`      | Messages from the user           |
| `assistant` | AI-generated responses           |
| `system`    | System messages and instructions |
| `tool`      | Tool call results                |

## 💻 Development

### Available Scripts

| Command       | Description                                          |
| ------------- | ---------------------------------------------------- |
| `npm run dev` | Start development server with nodemon (auto-restart) |
| `npm run cli` | Run Orbit CLI tool                                   |

### Development Workflow

1. **Start Development Server**

   ```bash
   npm run dev
   ```

   - Automatically restarts on file changes
   - Uses nodemon for hot reloading

2. **Test CLI Commands**

   ```bash
   npm run cli -- <command>
   ```

3. **Database Management**

   ```bash
   # Generate Prisma Client after schema changes
   npx prisma generate

   # Apply schema changes to database
   npx prisma db push

   # View/edit data in browser
   npx prisma studio

   # Create migration
   npx prisma migrate dev --name migration_name
   ```

4. **View Database**
   ```bash
   # Open Prisma Studio on http://localhost:5555
   npx prisma studio
   ```

## 🔧 Troubleshooting

### Common Issues

| Issue                           | Solution                                                      |
| ------------------------------- | ------------------------------------------------------------- |
| **Port 3005 already in use**    | Change `PORT` in `.env` or kill process: `npx kill-port 3005` |
| **Database connection failed**  | Verify PostgreSQL is running and `DATABASE_URL` is correct    |
| **Prisma client not generated** | Run `npx prisma generate`                                     |
| **Auth errors**                 | Check `BETTER_AUTH_SECRET` is at least 32 characters          |
| **AI not responding**           | Verify `GOOGLE_AI_API_KEY` is valid                           |
| **CLI command not found**       | Run from server directory with `npm run cli -- <command>`     |

### Debug Mode

```bash
# Enable verbose logging
DEBUG=* npm run dev

# Debug Prisma queries
DEBUG="prisma:*" npm run dev
```

## 🔗 Related Documentation

- [Root README](../README.md) - Project overview
- [Client README](../client/README.md) - Frontend documentation
- [Better-Auth Docs](https://www.better-auth.com/docs) - Authentication
- [Prisma Docs](https://www.prisma.io/docs) - Database ORM
- [Google AI SDK](https://ai.google.dev/docs) - AI integration

## 👨‍💻 Author

**Mausam Kar**

- Portfolio: [mausam04.vercel.app](https://mausam04.vercel.app)

---

<div align="center">

**[⬆ Back to Top](#-neuro-cli---server--cli)**

Built with Express.js, Prisma, and Google AI SDK

</div>
