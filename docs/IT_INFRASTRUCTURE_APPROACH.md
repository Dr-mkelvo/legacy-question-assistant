# IT Infrastructure Approach

This document explains how to approach the project from an engineering and infrastructure point of view. It is written as a practical delivery guide, not a theory document.

The goal is to keep the first version simple, fast to ship, secure enough for sensitive interviews, and structured so it can grow into a larger archive product later.

## Core Infrastructure Decision

Use a small number of strong services:

- Next.js for the interviewer web app.
- Convex for backend functions, database, realtime state, scheduled/background work, and initial file storage.
- A live transcription provider for speech-to-text.
- OpenAI for next-question generation and later analysis.
- Vercel for hosting the Next.js app.
- GitHub for source control and delivery workflow.

Do not start with Laravel, PostgreSQL, S3, Kubernetes, or a complex microservice setup. Those add operational weight before the product has proven the live interview loop.

## Main System Shape

```text
Interviewer browser
  -> microphone capture
  -> transcription provider WebSocket
  -> transcript chunks
  -> Convex mutations
  -> Convex database
  -> Convex action calls OpenAI
  -> suggested questions
  -> Convex realtime subscription
  -> interviewer browser updates
```

The product is one realtime workflow:

```text
capture audio -> transcribe -> save -> analyze -> suggest questions -> interviewer acts
```

## Recommended Repository Structure

Use a structure like this:

```text
app/
  interview/
    page.tsx
  review/
    page.tsx

components/
  interview/
    InterviewConsole.tsx
    LiveTranscript.tsx
    QuestionPanel.tsx
    InterviewControls.tsx
    ModeSelector.tsx

convex/
  schema.ts
  interviews.ts
  transcriptSegments.ts
  suggestedQuestions.ts
  bookmarks.ts
  questionEngine.ts
  http.ts
  convex.config.ts
  lib/
    ai.ts
    transcription.ts
    auth.ts
    validation.ts

docs/
  PROJECT_GOAL.md
  ARCHITECTURE.md
  BUILD_PHASES.md
  DATA_MODEL.md
  AI_QUESTION_ENGINE.md
  STORAGE_STRATEGY.md
  IT_INFRASTRUCTURE_APPROACH.md

scripts/
  env-check.ts
  convex-security-check.ts
  smoke-live-transcription.ts
  seed-demo-interview.ts

tests/
  question-engine.test.ts
  transcript-segments.test.ts
  interview-workflow.test.ts
```

Keep product code, backend workflow, docs, scripts, and tests separated. This makes it easier to explain the system to another developer or investor.

## Environments

Use three environments.

## 1. Local Development

Used by developers on the laptop.

Responsibilities:

- run the Next.js app locally,
- run Convex dev,
- test microphone capture,
- test transcription with dev API keys,
- test AI question generation with non-sensitive sample interviews.

Expected commands:

```bash
pnpm dev
npx convex dev
pnpm test
pnpm typecheck
```

## 2. Preview

Used for reviewing changes before production.

Responsibilities:

- deploy branch previews,
- test UI changes,
- test Convex preview backend,
- validate environment variables,
- run smoke tests with demo audio.

Preview should not contain real client interviews unless access control and data handling are already mature.

## 3. Production

Used for real interviews.

Responsibilities:

- stable deployed interviewer app,
- production Convex deployment,
- production transcription keys,
- production OpenAI keys,
- audit logging,
- backup/export process,
- stricter access controls.

## Deployment Model

Use Vercel for the Next.js app and Convex for backend deployment.

For Vercel + Convex, the build command should deploy Convex functions as part of the app deployment:

```bash
npx convex deploy --cmd 'pnpm build'
```

Production should have:

- `CONVEX_DEPLOY_KEY` in Vercel,
- `NEXT_PUBLIC_CONVEX_URL` available to the Next.js client,
- OpenAI API key stored in Convex environment variables,
- transcription provider API key stored server-side or issued through a controlled token endpoint,
- separate dev and production API keys.

Do not expose private API keys in browser code.

## Tooling Workflow

Use the laptop/tooling setup in a structured way.

## Research

Use Exa or web search for current technical research:

- transcription provider comparison,
- Convex/Vercel deployment updates,
- browser audio streaming limitations,
- model pricing and context limits,
- privacy/security guidance.

Only convert research into implementation after checking official documentation where possible.

## Source Control

Use GitHub and GitHub CLI for:

- repository creation,
- commits,
- pushes,
- pull requests,
- issue tracking,
- future release tags.

Keep the public repo free of secrets, private interview data, and client names.

## Backend and Data

Use Convex CLI for:

- local development,
- code generation,
- deployment,
- environment variables,
- function logs,
- function inspection.

Convex should be treated as the backend runtime, not only a database.

## UI Testing

Use browser-based testing for:

- microphone permission flow,
- live transcript rendering,
- question panel behavior,
- tablet viewport layout,
- start/stop session flow.

For this product, visual testing matters because the interviewer needs to read suggestions quickly during a live conversation.

## AI-Assisted Delivery

Use AI tools for:

- research summaries,
- implementation planning,
- code generation,
- test generation,
- architecture review,
- prompt iteration,
- documentation.

Do not let AI tools make final security or privacy decisions without human review.

## Security Principles

The interviews may contain sensitive family, business, political, or financial information. Treat all live interview data as private by default.

Minimum rules:

- no API keys in frontend code,
- no secrets committed to GitHub,
- no real interview transcripts in test files,
- no production data in local demos,
- access-controlled interviewer sessions,
- audit key actions such as start, stop, export, delete, and share,
- fail closed when required secrets are missing,
- separate dev and production environments,
- review all public Convex functions and HTTP routes.

## Recommended Security Checks

Add scripts similar to:

```bash
pnpm run security:env
pnpm run security:convex
pnpm test
pnpm typecheck
```

The security scripts should check:

- required environment variables are declared,
- no unexpected public Convex functions exist,
- public HTTP routes are on an allowlist,
- admin-only functions require an admin guard,
- API keys are not referenced by client components,
- `.env` files are not committed.

## Operational Scripts

Add small scripts for repeatable operations:

- `env-check.ts`: confirms required environment variables are present.
- `convex-security-check.ts`: checks public backend surface.
- `smoke-live-transcription.ts`: tests a sample transcription request.
- `seed-demo-interview.ts`: creates a fake interview for UI testing.
- `question-engine-eval.ts`: runs test transcripts through the AI question prompt.

These scripts should print clear pass/fail output and exit with non-zero status on failure.

## Observability

Track events that help debug live interviews:

- interview started,
- interview stopped,
- microphone permission denied,
- transcription connected,
- transcription disconnected,
- transcript segment saved,
- AI question generation started,
- AI question generation failed,
- question marked as asked,
- question regenerated,
- export created.

Store important operational events in Convex. For production, consider adding Sentry or another error tracker later.

## Failure Handling

The live interview system must degrade gracefully.

If transcription fails:

- show a visible connection warning,
- keep the interview session open,
- allow reconnection,
- keep local partial transcript if possible.

If AI question generation fails:

- keep showing the transcript,
- allow manual regenerate,
- show the last successful suggestions,
- log the error.

If Convex connection fails:

- warn the interviewer,
- pause saving,
- retry in the background,
- avoid pretending data is saved.

If internet fails:

- local recording backup becomes critical,
- the app should clearly show offline state.

## Data Retention

For MVP:

- keep interview transcripts in Convex,
- keep suggested questions in Convex,
- keep bookmarks in Convex,
- avoid storing raw audio unless needed.

When audio/video recording becomes part of the product:

- store smaller files in Convex storage if appropriate,
- use Google Cloud Storage for large recordings,
- store file metadata and access rules in Convex,
- define retention rules per client.

## Human Review

For anything that becomes part of a client-facing archive, keep a human review step.

AI can generate:

- questions,
- summaries,
- topic maps,
- draft reports.

A human should review before:

- sharing with a client,
- publishing,
- preserving as final archive material,
- translating sensitive meaning,
- extracting family/business conclusions.

## Delivery Roadmap

## Stage 1: Documentation and Skeleton

- finalize docs,
- create Next.js app,
- add Convex,
- create schema,
- create empty interviewer console.

## Stage 2: Live Transcript

- microphone capture,
- transcription provider integration,
- transcript display,
- transcript segment saving.

## Stage 3: Question Assistant

- AI prompt,
- Convex action,
- suggestion display,
- mark as asked,
- regenerate.

## Stage 4: Reliability

- reconnect behavior,
- error states,
- logs,
- smoke tests,
- security checks.

## Stage 5: Review Experience

- post-session transcript page,
- question history,
- bookmarks,
- export.

## Stage 6: Production Readiness

- auth,
- permissions,
- production env vars,
- Vercel deployment,
- Convex production deployment,
- monitoring,
- backup/export policy.

## Definition of Done for MVP

The MVP is ready when:

- an interviewer can start a session,
- live speech appears as transcript,
- final transcript segments save to Convex,
- AI suggestions appear within 30 seconds,
- the interviewer can mark questions as asked,
- the app handles transcription or AI errors without losing the session,
- tests and typecheck pass,
- security checks pass,
- the system is deployed to a preview URL for review.

