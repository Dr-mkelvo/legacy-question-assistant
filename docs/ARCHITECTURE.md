# Architecture

## MVP Architecture

```text
Browser microphone
  -> Next.js interviewer console
  -> live transcription provider
  -> transcript chunks
  -> Convex mutations
  -> Convex database
  -> Convex action for AI question generation
  -> suggested questions
  -> live UI update
```

## Main Components

## 1. Next.js Interviewer Console

This is the main product screen.

It handles:

- microphone permission,
- start and stop interview controls,
- live transcript display,
- suggested question display,
- mark question as asked,
- regenerate questions,
- bookmark important moments,
- interview mode selection.

## 2. Live Transcription Provider

This receives audio from the browser and returns text in real time.

Good first options:

- Deepgram,
- OpenAI Realtime/audio models,
- AssemblyAI.

For the MVP, choose one provider and keep the integration replaceable.

## 3. Convex Backend

Convex handles:

- interview records,
- transcript segment records,
- suggested question records,
- bookmarks,
- realtime UI subscriptions,
- server actions that call AI models,
- initial file storage where needed.

## 4. AI Question Engine

This receives recent transcript context and generates better follow-up questions.

It should consider:

- guest profile,
- current interview mode,
- recent transcript,
- questions already asked,
- questions already suggested,
- topics already covered.

## 5. Storage

For MVP:

- store structured records in Convex,
- use Convex file storage for small files or exports.

Later:

- add Google Cloud Storage for large audio/video files if needed.

