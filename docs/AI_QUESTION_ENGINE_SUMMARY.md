# AI Question Engine Summary

## Goal

The AI question engine suggests the next best questions while the interview is happening.

It should help the interviewer go deeper into the guest's stories, decisions, values, failures, and lessons.

## Basic Flow

```text
recent transcript
  -> AI reads context
  -> AI detects topic and missing depth
  -> AI suggests 3-5 next questions
  -> interviewer chooses what to ask
```

## Inputs

The AI should receive:

- guest profile,
- interview mode,
- recent transcript,
- asked questions,
- recently suggested questions,
- current topic,
- important bookmarked moments.

## Good Questions

Good questions ask for:

- a specific moment,
- a concrete example,
- a difficult decision,
- a failure,
- a turning point,
- a principle,
- a person who influenced the guest,
- advice for children or future generations.

## Generation Timing

Generate questions:

- every 20 seconds,
- after a pause,
- when the interviewer clicks Regenerate,
- when interview mode changes.

## Output

Return structured JSON with:

- current topic,
- question,
- reason,
- priority.

