# Executive Summary

## What This Project Is

Legacy Question Assistant is a live interview tool for capturing the knowledge, stories, values, and decision-making process of accomplished people.

The first product is focused on one workflow:

```text
live speech -> live transcript -> AI understands context -> AI suggests the next best questions
```

The interviewer remains in control. The AI acts as a quiet assistant that helps the interviewer go deeper.

## What Was Captured From The Conversation

The original idea is to preserve the wisdom of people who have achieved meaningful things in business, leadership, public life, family, and society. The concern is that when such people pass away, much of their thinking disappears with them, even if the family inherits their assets.

The system should help capture:

- how the person thinks,
- how they make decisions,
- how they built success,
- what mistakes shaped them,
- what principles guided them,
- what they would teach their children or future generations,
- what stories explain their values.

The long-term vision includes preservation, archives, family knowledge vaults, books, searchable records, and institutional partnerships. The current MVP is narrower: live transcription and next-question assistance.

## MVP Focus

For now, build only:

- browser microphone capture,
- live transcription,
- transcript storage,
- AI-generated next questions,
- interviewer screen,
- question controls,
- basic session records.

Do not start with the full archive, book generation, video editing, family portal, or preservation vault.

## Technical Direction

- App: Next.js
- Backend/data/realtime: Convex
- Live transcription: Deepgram first
- AI question generation: OpenAI
- Hosting: Vercel
- Storage: Convex first, Google Cloud Storage later if large media files require it

Avoid Laravel, PostgreSQL, S3, and complex infrastructure for the MVP.

## Main Shareable Document

For the person handling the IT/live transcription work, start with:

[Live Transcription Summary](./LIVE_TRANSCRIPTION_SUMMARY.md)

Then read:

[Live Transcription Detail](./LIVE_TRANSCRIPTION_DETAIL.md)

Provider options are documented in:

[Transcription Alternatives](./TRANSCRIPTION_ALTERNATIVES.md)

