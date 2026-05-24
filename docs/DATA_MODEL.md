# Data Model

Use Convex as the primary database.

## interviews

Stores the interview session.

```ts
{
  title: string;
  guestName: string;
  guestProfile?: string;
  mode: "life_story" | "business_builder" | "leadership" | "family_legacy" | "wisdom_extraction" | "deep_dive";
  status: "draft" | "live" | "stopped" | "archived";
  startedAt?: number;
  endedAt?: number;
  createdAt: number;
}
```

## transcriptSegments

Stores final transcript chunks.

```ts
{
  interviewId: Id<"interviews">;
  speaker?: string;
  text: string;
  originalText?: string;
  englishMeaning?: string;
  language: "en" | "sw" | "mixed" | "unknown";
  startMs?: number;
  endMs?: number;
  confidence?: number;
  createdAt: number;
}
```

## suggestedQuestions

Stores AI-generated follow-up questions.

```ts
{
  interviewId: Id<"interviews">;
  question: string;
  reason?: string;
  topic?: string;
  priority: number;
  status: "suggested" | "asked" | "dismissed" | "saved";
  createdAt: number;
  askedAt?: number;
}
```

## bookmarks

Stores important moments from the conversation.

```ts
{
  interviewId: Id<"interviews">;
  transcriptSegmentId?: Id<"transcriptSegments">;
  note?: string;
  createdAt: number;
}
```

## providerEvents

Optional table for debugging transcription provider events.

```ts
{
  interviewId: Id<"interviews">;
  provider: string;
  eventType: string;
  payload: unknown;
  createdAt: number;
}
```

