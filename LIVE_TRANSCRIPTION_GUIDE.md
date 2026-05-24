# Live Transcription + Next Question Assistant Guide

This guide describes how to build the first product from scratch: a live interview screen that transcribes speech and suggests the next best questions for the interviewer.

## Goal

Build a real-time assistant for legacy interviews.

The interviewer should be able to:

- Start and stop an interview session.
- See live transcription as the guest speaks.
- See AI-generated follow-up questions.
- Mark a suggested question as used.
- Regenerate deeper questions on demand.
- Save transcript segments and questions for later review.

The system should support English, Swahili, and code-switched conversations.

## Recommended MVP Stack

- App: Next.js
- UI: React
- Backend/data: Convex
- Realtime app state: Convex subscriptions
- Live transcription: Deepgram first, with OpenAI or AssemblyAI as alternatives
- Question generation: OpenAI API
- Storage: Convex file storage first; Google Cloud Storage later if long recordings and video workflows require it

Avoid Laravel for this product. The fastest path is a single Next.js app with Convex handling backend state, persistence, and server functions.

## High-Level Architecture

```text
Browser microphone
  -> Next.js interview screen
  -> live transcription WebSocket
  -> transcript chunks
  -> Convex mutation saves transcript
  -> Convex action calls AI question generator
  -> Convex saves suggested questions
  -> Next.js screen updates in real time
```

## Core Screens

Start with one main screen: the interviewer console.

It should include:

- Start interview button.
- Stop interview button.
- Live transcript panel.
- Current detected topic.
- Suggested questions list.
- Mark as asked button.
- Regenerate questions button.
- Important moment button.
- Interview mode selector.

Recommended interview modes:

- Life Story
- Business Builder
- Leadership
- Family Legacy
- Wisdom Extraction
- Deep Dive

## Data Model

Use Convex tables similar to these.

```ts
interviews
  title
  guestName
  guestProfile
  mode
  status
  startedAt
  endedAt

transcriptSegments
  interviewId
  speaker
  text
  language
  startMs
  endMs
  confidence
  createdAt

suggestedQuestions
  interviewId
  question
  reason
  topic
  priority
  status
  createdAt

bookmarks
  interviewId
  transcriptSegmentId
  note
  createdAt
```

Question status can be:

- suggested
- asked
- dismissed
- saved

## Live Transcription Flow

1. The interviewer clicks Start Interview.
2. The browser requests microphone permission.
3. The app opens a WebSocket connection to the transcription provider.
4. Browser audio is streamed in small chunks.
5. The transcription provider returns partial and final transcript segments.
6. Partial text is shown immediately in the UI.
7. Final transcript segments are saved into Convex.
8. Every 15-30 seconds, recent final transcript segments are sent to the AI question engine.

Do not generate questions after every word. It will be expensive and noisy.

Use these triggers:

- every 20 seconds,
- when the guest pauses for 3-5 seconds,
- when the interviewer clicks Regenerate,
- when the interviewer changes interview mode.

## Next Question Engine

The AI question engine receives:

- guest profile,
- interview mode,
- recent transcript,
- questions already asked,
- questions already suggested,
- current topic if known,
- the goal of the interview.

It returns 3-5 questions.

The best questions should be:

- specific,
- respectful,
- deeper than the current answer,
- tied to the guest's own words,
- useful for family or future generations,
- designed to reveal stories, decisions, values, principles, failures, turning points, and advice.

## AI Prompt Template

```text
You are assisting a human interviewer during a live legacy interview.

The goal is to extract the guest's life wisdom, decision-making patterns,
values, stories, failures, turning points, and advice for future generations.

Guest profile:
{{guestProfile}}

Current interview mode:
{{mode}}

Recent transcript:
{{recentTranscript}}

Questions already asked:
{{askedQuestions}}

Questions recently suggested:
{{recentSuggestedQuestions}}

Instructions:
- Suggest 5 next questions.
- Do not repeat questions.
- Prefer concrete stories over general opinions.
- Ask for examples, moments, decisions, consequences, people, and lessons.
- If the guest said something vague, ask for clarification.
- If the transcript includes Swahili, reason from the meaning and ask the question in English.
- Keep questions natural and respectful.
- Return JSON only.

JSON shape:
{
  "current_topic": "short topic name",
  "questions": [
    {
      "question": "question text",
      "reason": "why this is a good next question",
      "priority": 1
    }
  ]
}
```

## Example

Transcript:

```text
When I started the business, I trusted people too quickly. I lost money,
and that was when I realized that business requires discipline.
```

Good suggested questions:

- What happened in that specific situation where trust cost you money?
- What signs do you now look for before trusting someone in business?
- How did that experience change the way you lead people?
- What would you teach your children about trust and money?
- Did that failure make you more cautious, or did it make you more strategic?

## Swahili and Code-Switching

Store the original transcript exactly as spoken.

For AI question generation, the system can also create a clean English meaning layer when needed. Do not replace the original transcript.

Recommended transcript handling:

```text
originalText: exact spoken words
englishMeaning: translated/cleaned meaning when needed
language: en, sw, mixed
```

This matters because local idioms and Kenyan context may lose meaning if only direct translation is stored.

## Convex Responsibilities

Convex should handle:

- interview session records,
- transcript segment storage,
- suggested question storage,
- live UI updates,
- server-side actions for AI calls,
- file storage for small audio exports or related assets.

If full video production or very large media storage becomes central, add Google Cloud Storage later and store the Google file references in Convex.

## MVP Build Steps

1. Create a Next.js app.
2. Add Convex.
3. Create the Convex schema for interviews, transcript segments, questions, and bookmarks.
4. Build the interviewer console UI.
5. Add browser microphone capture.
6. Stream audio to the transcription provider.
7. Display partial transcript locally.
8. Save final transcript segments to Convex.
9. Add the AI question generation Convex action.
10. Render suggested questions from Convex.
11. Add Mark as Asked and Regenerate actions.
12. Test with English, Swahili, and mixed speech.

## First Version Acceptance Criteria

The MVP is working when:

- an interviewer can start a session,
- speech appears as live text,
- transcript segments are saved,
- suggested questions appear within 30 seconds,
- questions improve when more context is spoken,
- the interviewer can mark a question as asked,
- the session can be stopped without losing transcript data.

## Later Improvements

- Speaker diarization.
- Audio recording backup.
- Video support.
- Guest profile preparation form.
- Topic timeline.
- Post-interview report generation.
- Family archive portal.
- Long-term preservation exports.

