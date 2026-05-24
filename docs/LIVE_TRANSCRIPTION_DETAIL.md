# Live Transcription Detail

## Purpose

This is the detailed implementation plan for the live transcription and next-question assistant.

The live system must help the interviewer capture deeper knowledge in the moment. It should not wait until after the interview to become useful.

## Selected MVP Architecture

```text
Lav microphones / room microphone
  -> browser MediaRecorder / Web Audio API
  -> transcription provider WebSocket
  -> transcript events
  -> Next.js client state for partial text
  -> Convex mutation for final transcript segments
  -> Convex action for AI question generation
  -> Convex suggestedQuestions table
  -> realtime subscription back to UI
```

For the physical recording setup, see [Recording Setup](./RECORDING_SETUP.md).

## Recommended Provider

Use Deepgram first for the MVP.

Recommended settings to evaluate:

- model: latest production realtime model available on the account,
- interim results: enabled,
- punctuation/smart formatting: enabled,
- endpointing or utterance end detection: enabled,
- diarization: enabled when speaker labels are needed,
- language: English first, then test Swahili and mixed-language behavior.

If Deepgram struggles with Swahili/code-switching in real interviews, test Google Cloud Speech-to-Text and AssemblyAI's multilingual streaming as alternatives.

## Browser Audio Capture

The Next.js app should:

1. Ask for microphone permission.
2. Create an audio stream from `navigator.mediaDevices.getUserMedia`.
3. Convert or package audio in the format required by the transcription provider.
4. Send audio chunks through WebSocket.
5. Keep the UI responsive while streaming.
6. Stop tracks and close WebSocket cleanly when the interview ends.

The app should show a clear state:

- idle,
- requesting microphone,
- connecting transcription,
- live,
- reconnecting,
- stopped,
- error.

## Transcript Handling

There are two transcript types:

- partial transcript,
- final transcript.

Partial transcript:

- used for live display,
- can change as the provider improves recognition,
- should not be permanently saved as final truth.

Final transcript:

- saved to Convex,
- used for AI question generation,
- used for post-session review.

## Convex Writes

Save final transcript segments with:

- interview ID,
- text,
- original text,
- optional English meaning,
- language,
- speaker label,
- start time,
- end time,
- confidence,
- provider event ID,
- created time.

## Question Generation Context

When generating next questions, send the AI:

- current interview mode,
- guest profile,
- last 2-5 minutes of final transcript,
- latest partial transcript if useful,
- questions already asked,
- questions recently suggested,
- important bookmarked moments,
- current topic if known.

## AI Generation Rhythm

Use four triggers:

1. Timed trigger every 20 seconds.
2. Pause trigger after 3-5 seconds of silence/end-of-turn.
3. Manual Regenerate button.
4. Interview mode change.

Add a simple debounce so multiple triggers do not call the AI at the same time.

## AI Output

The AI should return structured JSON:

```json
{
  "current_topic": "Trust and hiring",
  "questions": [
    {
      "question": "Can you describe one moment when trusting the wrong person cost you in business?",
      "reason": "This asks for a concrete story and reveals how the guest learned to judge people.",
      "priority": 1
    }
  ]
}
```

Save each question separately in Convex.

## UI Behavior

The question panel should:

- show 3-5 questions,
- keep questions readable from a tablet,
- avoid overwhelming the interviewer,
- show the best question at the top,
- allow Mark as Asked,
- allow Save,
- allow Dismiss,
- allow Regenerate.

## Error Handling

If transcription fails:

- keep the session open,
- show connection warning,
- allow reconnect,
- keep any already saved transcript.

If AI generation fails:

- keep showing the transcript,
- keep previous questions visible,
- allow manual regenerate,
- save the failure event for debugging.

If Convex fails:

- show that saving is interrupted,
- retry final segment writes,
- do not falsely claim the transcript is saved.

## Testing Plan

Test with:

- clean English,
- accented English,
- Swahili,
- mixed Swahili/English,
- two speakers,
- noisy room,
- long pauses,
- interruptions,
- 30-minute session,
- network disconnect and reconnect.

## MVP Definition of Done

The live transcription feature is ready for internal testing when:

- microphone capture works,
- transcription connects,
- transcript appears live,
- final segments save to Convex,
- questions generate automatically,
- manual regenerate works,
- question status updates save,
- stopping the interview closes streams cleanly,
- no API keys are exposed in browser code.
