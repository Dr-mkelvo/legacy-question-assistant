# Legacy Question Assistant

Live transcription and AI-assisted next-question generation for legacy interviews.

## Purpose

This project helps an interviewer capture a person's knowledge, life stories, values, and decision-making process in real time. As the guest speaks, the system transcribes the conversation and suggests deeper follow-up questions for the interviewer.

## Initial Scope

- Capture live microphone audio.
- Produce live transcription.
- Support English and Swahili/code-switched conversations.
- Generate suggested next questions during the interview.
- Save transcript segments and suggested questions.
- Let the interviewer mark questions as used or save important moments.

## MVP Architecture

```text
Microphone
  -> Next.js interviewer app
  -> Live transcription provider
  -> Convex backend
  -> AI question engine
  -> Interviewer tablet interface
```

## Planned Stack

- App: Next.js / React
- Backend/data: Convex
- Transcription: Deepgram, OpenAI, or AssemblyAI
- AI: OpenAI API
- Storage: Convex file storage first; Google Cloud Storage if large media workflows require it

## First Build Target

The first version should do one job well:

1. Start an interview session.
2. Capture microphone audio in the browser.
3. Stream audio to a live transcription provider.
4. Show the transcript as the person speaks.
5. Send recent transcript context to an AI model.
6. Display 3-5 strong follow-up questions for the interviewer.
7. Save transcript segments, generated questions, and used questions in Convex.

## Documentation

- [Executive Summary](./docs/EXECUTIVE_SUMMARY.md): short overview of the full idea and MVP.
- [Project Goal](./docs/PROJECT_GOAL.md): what we are building and why.
- [Live Transcription Guide](./LIVE_TRANSCRIPTION_GUIDE.md): the main shareable guide for building live transcription and next-question assistance.
- [Live Transcription Summary](./docs/LIVE_TRANSCRIPTION_SUMMARY.md): short version of the live transcription approach.
- [Live Transcription Detail](./docs/LIVE_TRANSCRIPTION_DETAIL.md): detailed implementation plan for the live transcription workflow.
- [Transcription Alternatives](./docs/TRANSCRIPTION_ALTERNATIVES.md): provider options, tradeoffs, and recommendation.
- [Architecture](./docs/ARCHITECTURE.md): system components and data flow.
- [Build Phases](./docs/BUILD_PHASES.md): the order of work.
- [Data Model](./docs/DATA_MODEL.md): Convex tables and records.
- [AI Question Engine Summary](./docs/AI_QUESTION_ENGINE_SUMMARY.md): short version of how question generation works.
- [AI Question Engine Detail](./docs/AI_QUESTION_ENGINE.md): detailed next-question logic and prompt.
- [Storage Strategy](./docs/STORAGE_STRATEGY.md): Convex storage first, Google Cloud Storage later if needed.
- [IT Infrastructure Approach](./docs/IT_INFRASTRUCTURE_APPROACH.md): how to run the project from an engineering, deployment, security, and operations point of view.
