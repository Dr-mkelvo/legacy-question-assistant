# Project Goal

## Working Name

Legacy Question Assistant

## What We Are Building

We are building a live interview assistant for legacy interviews. The product helps an interviewer capture a successful or accomplished person's stories, life lessons, values, decision-making process, and practical wisdom.

The first version focuses only on the live interview experience:

- live transcription,
- AI-generated follow-up questions,
- interviewer controls,
- transcript and question storage.

The system should help the interviewer go deeper while the conversation is happening.

## Why It Exists

Many accomplished people carry knowledge that is never properly documented. Their families, companies, communities, and future generations may lose access to how they thought, made decisions, handled failure, built relationships, led people, and created value.

This system is designed to preserve that knowledge while the person is still alive and able to explain it in their own voice.

## First Product Outcome

The first product should allow an interviewer to sit with a guest, start a session, and receive useful next-question suggestions as the guest speaks.

The interviewer remains in control. The AI does not replace the interviewer. It acts as a quiet research assistant that listens, detects important moments, and suggests deeper questions.

## Current Technical Direction

- Use Next.js for the app.
- Use Convex for backend, database, realtime updates, server functions, and initial file storage.
- Avoid Laravel.
- Avoid PostgreSQL for the MVP.
- Avoid S3 buckets for the MVP.
- Use Google Cloud Storage only later if large audio/video storage needs outgrow Convex.

## Primary MVP

The MVP is not the full archive, book, or family portal.

The MVP is:

```text
Listen live
  -> transcribe live
  -> understand the conversation
  -> suggest the next best questions
  -> save transcript and questions
```

## People Who Will Use It

- Interviewers capturing legacy stories.
- Families preserving family wisdom.
- Founders and executives documenting business lessons.
- Public figures and leaders preserving institutional memory.
- Researchers or archivists conducting guided interviews.

## Languages

The system should support:

- English,
- Swahili,
- mixed English/Swahili speech,
- local Kenyan context and idioms.

The interface and final documentation can be in English, while the transcript should preserve the original spoken language.

