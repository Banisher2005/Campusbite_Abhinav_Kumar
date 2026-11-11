# CampusBite — AI-Powered Task Management Agent

CampusBite is a hackathon demonstration project showcasing an AI-powered task management agent built using Google's Gemini API, Supabase, and Next.js.

The application allows users to interact with an AI agent using natural language. The agent can understand requests, retrieve information, create tasks, and update task statuses through structured function calling.

## Features

- **AI-Powered Agent:** Interact with Google Gemini using natural language.
- **Function Calling:** Gemini dynamically selects tools based on user requests.
- **Task Management:** Create, retrieve, and complete tasks.
- **Live Database Integration:** Task data is stored and retrieved from Supabase PostgreSQL.
- **Team Passcode Authentication:** Protects the application with a shared team passcode.
- **Tool Execution Visibility:** Displays the tools called by the AI and their execution results.
- **Cloud Deployment:** Hosted using Vercel.

## Technology Stack

| Technology | Purpose |
|---|---|
| Next.js 16 | Full-stack web framework |
| React 19 | User interface |
| TypeScript | Type safety |
| Tailwind CSS 4 | Styling |
| Google Gemini API | AI model and function calling |
| Supabase | PostgreSQL database |
| Zod | Input validation |
| Vercel | Deployment and hosting |

## Project Architecture

```text
campusbite-live/
│
├── app/
│   ├── api/
│   │   ├── agent/
│   │   │   └── route.ts
│   │   ├── health/
│   │   │   └── route.ts
│   │   ├── login/
│   │   │   └── route.ts
│   │   ├── logout/
│   │   │   └── route.ts
│   │   └── tasks/
│   │       └── route.ts
│   │
│   ├── login/
│   ├── globals.css
│   ├── layout.tsx
│   └── page.tsx
│
├── components/
│   ├── AgentChat.tsx
│   └── TaskList.tsx
│
├── lib/
│   ├── agent/
│   │   ├── defineTool.ts
│   │   ├── runAgent.ts
│   │   ├── systemPrompt.ts
│   │   ├── tools.ts
│   │   └── types.ts
│   ├── auth.ts
│   ├── dates.ts
│   ├── env.ts
│   ├── gemini.ts
│   ├── schemas.ts
│   └── supabase.ts
│
├── seed/
│   ├── 00_starter_example.sql
│   └── campusbite.sql
│
├── live-demo/
│   ├── DEMO_SCRIPT.md
│   └── LIVE_BUILD_PROMPTS.md
│
├── .env.example
├── .gitignore
├── package.json
├── tsconfig.json
└── README.md
```

## How the AI Agent Works

The application uses Gemini function calling to interact with the database.

The agent follows this execution flow:

1. The user submits a natural-language request.
2. The request is sent to the Next.js API route.
3. Gemini analyzes the request and selects an appropriate tool.
4. Tool arguments are validated using Zod.
5. The selected function executes against Supabase.
6. The database result is returned to Gemini.
7. Gemini generates a natural-language response.
8. The interface displays the response and tool execution details.

### Available Agent Tools

| Tool | Description |
|---|---|
| `listTasks` | Retrieves tasks and filters them by status |
| `createTask` | Creates a new task |
| `completeTask` | Marks an existing task as completed |

## Getting Started

### Prerequisites

- Node.js 20 or later
- npm
- A Google AI Studio API key
- A Supabase project
- A Vercel account (for deployment)

### 1. Clone the Repository

```bash
git clone https://github.com/Banisher2005/Campusbite_Abhinav_Kumar.git
cd Campusbite_Abhinav_Kumar/campusbite-live
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env.local` file in the `campusbite-live` directory.

Use `.env.example` as your reference.

```env
GEMINI_API_KEY=your_gemini_api_key
GEMINI_MODEL=gemini-3.8-flash

SUPABASE_URL=your_supabase_project_url
SUPABASE_SECRET_KEY=your_supabase_secret_key

APP_PASSCODE=your_team_passcode
```

Replace the placeholder values with your own credentials.

**Important:** Never commit `.env.local` or expose API keys and database secrets in frontend code.

### 4. Configure Supabase

1. Create a project in Supabase.
2. Open the SQL Editor.
3. Execute `seed/00_starter_example.sql`.
4. Execute `seed/campusbite.sql` if required for the demonstration database.
5. Configure the Supabase Project URL and Secret Key in your environment variables.

The application uses Supabase PostgreSQL to store and retrieve task information.

### 5. Run Locally

Start the development server:

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

Enter your configured team passcode to access the application.

### 6. Build for Production

Run the production build:

```bash
npm run build
```

To start the production server locally:

```bash
npm run start
```

## Deployment on Vercel

CampusBite is deployed using Vercel.

1. Import the GitHub repository into Vercel.
2. Configure the project settings.
3. Set the Root Directory to:

```text
campusbite-live
```

4. Select Next.js as the framework.
5. Configure the required environment variables.
6. Deploy the application.

Recommended build settings:

| Setting | Configuration |
|---|---|
| Framework | Next.js |
| Root Directory | `campusbite-live` |
| Build Command | `npm run build` |
| Install Command | `npm install` |
| Output Directory | Default |

### Environment Variables on Vercel

Configure the following variables under Project Settings → Environment Variables:

- `GEMINI_API_KEY`
- `GEMINI_MODEL`
- `SUPABASE_URL`
- `SUPABASE_SECRET_KEY`
- `APP_PASSCODE`

Redeploy after changing environment variables.

## Health Check

The application includes a health-check endpoint:

```text
/api/health
```

It reports whether the required environment variables are configured and whether the Supabase tasks table can be accessed.

The endpoint does not expose the actual secret values.

## Security Considerations

- API keys are accessed only from server-side code.
- Supabase secret credentials must never be exposed to the browser.
- Team authentication uses HTTP-only session cookies.
- Tool inputs are validated using Zod.
- Environment files containing credentials are excluded from Git.
- Database operations are performed through server-side API routes.

## Demo Scenarios

The following prompts can be used to demonstrate the application:

**Retrieve tasks**

```text
Show me all the tasks currently stored in the database.
```

**Filter tasks**

```text
Which tasks are still open?
```

**Create a task**

```text
Create a task to prepare the final project presentation.
```

**Complete a task**

```text
Mark task number 3 as completed.
```

The agent will select and execute the appropriate database tools.

## Project Information

**Project:** CampusBite

**Category:** AI / Agentic AI Demonstration

**AI Integration:** Google Gemini API

**Database:** Supabase PostgreSQL

**Deployment:** Vercel

**Repository:** https://github.com/Banisher2005/Campusbite_Abhinav_Kumar

---

*CampusBite is a hackathon demonstration project exploring how large language models, function calling, and database integrations can be combined to create interactive AI-powered applications.*