# Live Transcription Summary

## Goal

Build the live part of the system: the interviewer speaks with a guest, the app transcribes the conversation in real time, and AI suggests the next best questions.

## Recommended First Approach

Use:

- Next.js for the interviewer app,
- Convex for session state, transcript records, realtime updates, and backend actions,
- Deepgram for live speech-to-text,
- OpenAI for next-question generation.

## Why Deepgram First

Deepgram is the recommended first transcription provider because it is strong for:

- real-time WebSocket transcription,
- low latency,
- diarization support,
- word timestamps,
- interim results,
- practical developer experience,
- long-running live sessions.

For this project, speed and reliability during a live interview matter more than heavy post-call analytics.

## Basic Flow

```text
Browser microphone
  -> stream audio to Deepgram
  -> receive partial and final transcript
  -> show partial transcript on screen
  -> save final transcript segments to Convex
  -> send recent transcript to OpenAI
  -> save suggested questions to Convex
  -> show suggestions to interviewer
```

## When To Generate Questions

Generate new questions:

- every 20 seconds,
- when the guest pauses for 3-5 seconds,
- when the interviewer clicks Regenerate,
- when the interviewer changes interview mode.

Do not generate questions after every word.

## What The Interviewer Sees

The interviewer console should show:

- Start Interview,
- Stop Interview,
- live transcript,
- current topic,
- 3-5 suggested questions,
- Mark as Asked,
- Regenerate,
- Save Important Moment,
- interview mode selector.

## Swahili and English

Store the original transcript exactly as spoken. If Swahili or mixed Swahili/English is used, keep the original text and optionally add an English meaning layer for AI processing.

## First Acceptance Criteria

The MVP works when:

- audio can be captured from the browser,
- live transcript appears,
- final transcript segments are saved,
- AI questions appear within 30 seconds,
- the interviewer can mark a question as asked,
- the session can stop without losing saved transcript data.

