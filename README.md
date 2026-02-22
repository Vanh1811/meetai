# MeetAI

MeetAI is a Next.js app for running AI-assisted meetings. Create AI agents with custom instructions, schedule meetings, and host calls with real-time chat, transcripts, and post-call summaries.

## Features
- AI agents with custom instructions
- Meeting scheduling and management
- Live video calls with Stream Video
- Real-time meeting chat with Stream Chat
- Automatic transcription and post-call summaries
- Auth with email/password and social providers (GitHub, Google)
- Usage limits and upgrades via Polar

## Tech Stack
- Next.js 15 (App Router), React 19, TypeScript
- tRPC + TanStack Query
- Drizzle ORM + Postgres (Neon)
- Stream Video + Stream Chat
- OpenAI + Inngest for transcript processing
- Better Auth + Polar
- Tailwind CSS

## Getting Started

### 1) Install dependencies
```bash
npm install
```

### 2) Configure environment variables
Create a `.env.local` file in the project root. Example:
```bash
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Database
DATABASE_URL=postgres://USER:PASSWORD@HOST:PORT/DB

# Auth providers
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

# Stream Video
NEXT_PUBLIC_STREAM_VIDEO_API_KEY=
STREAM_VIDEO_SECRET_KEY=

# Stream Chat
NEXT_PUBLIC_STREAM_CHAT_API_KEY=
STREAM_CHAT_SECRET_KEY=

# OpenAI
OPENAI_API_KEY=

# Polar (billing)
POLAR_ACCESS_TOKEN=
```

### 3) Push database schema
```bash
npm run db:push
```

### 4) Run the app
```bash
npm run dev
```

Open `http://localhost:3000`.

## Webhooks (Stream)
This app expects Stream webhooks for call lifecycle events and chat. For local development, you can expose your dev server:
```bash
npm run dev:webhook
```
Set the Stream webhook URL to `https://<ngrok-url>/api/webhook`.

## Background Processing (Inngest)
When a call transcription is ready, the webhook triggers an Inngest event that:
- Fetches the transcript
- Resolves speaker names
- Generates a summary via OpenAI
- Stores the summary in the meeting record

## Scripts
- `npm run dev`: Start Next.js dev server
- `npm run build`: Production build
- `npm run start`: Run production server
- `npm run lint`: Lint
- `npm run db:push`: Push Drizzle schema
- `npm run db:studio`: Drizzle Studio
- `npm run dev:webhook`: Expose local server via ngrok

## Project Structure
- `src/app`: Routes and layouts
- `src/modules`: Feature modules (agents, meetings, call, auth, dashboard)
- `src/db`: Drizzle config and schema
- `src/inngest`: Inngest client and functions
- `src/trpc`: tRPC routers and client setup
- `src/lib`: Integrations (Stream, OpenAI, auth, etc.)

## Notes
- Stream Video and Chat require API keys and webhooks.
- OpenAI is used for live agent behavior and post-call summaries.
