# AI Question Engine

## Purpose

The AI question engine suggests the next best questions during a live interview.

Its job is to help the interviewer go deeper, not to take over the conversation.

## Inputs

The engine should receive:

- guest profile,
- current interview mode,
- recent transcript,
- already asked questions,
- recently suggested questions,
- current topic,
- interview goal.

## Question Quality Rules

Good questions should:

- ask for specific stories,
- ask for moments and turning points,
- reveal decision-making,
- reveal values and principles,
- explore failure and recovery,
- connect lessons to family or future generations,
- avoid repeating what has already been asked.

Weak questions:

- are too broad,
- ask for generic advice,
- ignore what the guest just said,
- repeat earlier questions,
- move away from an emotionally important moment too quickly.

## Generation Timing

Generate questions:

- every 20 seconds during active speech,
- after a 3-5 second pause,
- when the interviewer clicks Regenerate,
- when the interviewer changes interview mode.

Do not generate after every word.

## Output Shape

```json
{
  "current_topic": "Hiring and trust",
  "questions": [
    {
      "question": "Can you describe one moment when trusting the wrong person cost you in business?",
      "reason": "This asks for a concrete story and reveals how the guest learned to judge people.",
      "priority": 1
    }
  ]
}
```

## Prompt Template

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
```

