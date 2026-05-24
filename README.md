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
  -> Web app
  -> Live transcription service
  -> Backend server
  -> AI question engine
  -> Interviewer tablet interface
```

## Planned Stack

- Frontend: Next.js / React
- Backend: Node.js or Laravel
- Realtime: WebSockets
- Transcription: Deepgram, OpenAI, or AssemblyAI
- AI: OpenAI API
- Database: PostgreSQL
- Storage: S3-compatible object storage

