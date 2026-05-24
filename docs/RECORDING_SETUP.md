# Recording Setup

This document covers the physical recording setup required for live transcription and AI next-question assistance.

The software can only perform well if the audio is clean. For this product, audio quality is infrastructure.

## Recommended Interview Kit

For serious interviews, use a 2-4 microphone setup.

The setup has two jobs:

1. Send clean audio into the live transcription system.
2. Save the original interview recording separately as the permanent source file.

Do not treat the live transcript as the original record. The original record is the clean audio or video recording.

This document focuses on the physical setup. The tablet/interviewer console and 3-5 AI follow-up question workflow are covered in:

- [Live Transcription Summary](./LIVE_TRANSCRIPTION_SUMMARY.md)
- [Live Transcription Detail](./LIVE_TRANSCRIPTION_DETAIL.md)
- [AI Question Engine Summary](./AI_QUESTION_ENGINE_SUMMARY.md)
- [AI Question Engine Detail](./AI_QUESTION_ENGINE.md)

## Whole Setup In One Flow

```text
Guest + interviewer speak
  -> lav mics capture clean audio
  -> recorder saves original source recording
  -> recorder/interface sends clean live feed to laptop/tablet
  -> Next.js interviewer console streams audio to transcription provider
  -> transcription provider returns live transcript
  -> Convex saves final transcript segments
  -> OpenAI receives recent transcript context
  -> OpenAI returns 3-5 follow-up questions
  -> tablet/interviewer console displays the suggested questions
  -> interviewer chooses what to ask next
```

The tablet or laptop is the live control surface. It shows the interviewer:

- live transcript,
- current topic,
- 3-5 suggested follow-up questions,
- Mark as Asked,
- Regenerate,
- Save Important Moment,
- interview mode selector.

The recorder is the preservation device. It saves the original audio even if the internet, transcription provider, or AI question engine fails.

## Minimum Setup

Use this for early testing:

- 1 good USB microphone or wireless lav mic,
- laptop or tablet,
- stable internet,
- headphones for monitoring,
- local backup recording.

This is enough to test the software flow, but it is not ideal for client-quality interviews.

## Standard 2-Person Interview Setup

Use this for most founder, family, or leadership interviews:

- 2 lavalier microphones,
- 1 mic for the interviewer,
- 1 mic for the guest,
- audio interface or wireless receiver,
- laptop running the interviewer console,
- headphones for audio monitoring,
- backup recorder.

Good device options:

- DJI Mic 2,
- Rode Wireless Pro,
- Rode Wireless Go II,
- Zoom F3,
- Zoom H5,
- Zoom H6,
- Shure MV7 for desk/studio use.

## Why Two Lav Mics First

Start with two lav mics because the standard interview has two important speakers:

- the guest,
- the interviewer.

The guest needs the cleanest mic because most of the knowledge comes from them. The interviewer also needs a mic because their questions provide context for the answers.

If only the guest is mic'd, the transcript may contain answers without clear questions. That makes the AI weaker because it cannot always tell what the guest is responding to.

## How The Two Lavs Are Used

```text
Guest lav mic
  -> captures the guest's answers

Interviewer lav mic
  -> captures the questions and prompts

Both mic feeds
  -> mixed or routed into the laptop/tablet
  -> used for live transcription

Both mic feeds
  -> recorded locally on recorder/internal mic storage
  -> used as the permanent source recording
```

For live transcription, the system can use either:

- a mixed stereo/mono feed containing both speakers, or
- separate channels if the hardware supports multichannel input.

For the archive-quality recording, keep separate tracks when possible:

- track 1: guest,
- track 2: interviewer.

Separate tracks make cleanup, speaker separation, and future editing much easier.

## 4-Lav Mic Setup

Use this when there may be more than two people in the room.

Example:

- lav 1: main guest,
- lav 2: interviewer,
- lav 3: family member, assistant, or second guest,
- lav 4: spare mic or additional participant.

This setup is useful for:

- family legacy interviews,
- interviews with business partners,
- roundtable-style sessions,
- cases where an assistant or relative may add context,
- backup if one mic fails.

## Why Four Lav Mics

Four lav mics are not always required. They are used when the session may include more voices than the main interviewer and guest.

Use four lavs when:

- a spouse or family member may add memories,
- a business partner may join part of the discussion,
- an assistant may clarify dates, names, or events,
- two interviewers are present,
- the interview is more like a small roundtable,
- you want a spare mic ready in case one fails.

The reason for four lavs is control. Each important speaker gets a close microphone instead of relying on room audio.

Room audio alone is risky because people turn their heads, speak softly, interrupt each other, or sit far from the recorder.

## How The Four Lavs Are Used

Recommended assignment:

```text
Lav 1: main guest
Lav 2: interviewer
Lav 3: second guest / family member / business partner
Lav 4: assistant / second interviewer / spare
```

Live transcription can receive:

- a mixed feed of all active lavs, or
- a selected feed if only the main guest and interviewer are speaking,
- separate channels if the audio interface and transcription provider workflow support it.

Permanent recording should store:

- each lav as a separate track when possible,
- or a clean mixed backup if multitrack is not possible.

Best setup:

```text
Lav 1 -> recorder track 1 -> guest archive audio
Lav 2 -> recorder track 2 -> interviewer archive audio
Lav 3 -> recorder track 3 -> second speaker archive audio
Lav 4 -> recorder track 4 -> assistant/spare archive audio

Recorder mix out / interface out
  -> laptop/tablet
  -> live transcription
```

This means the live transcription system gets a practical combined feed, while the recorder keeps the clean individual tracks for preservation.

## Recommended 4-Mic Signal Flow

```text
Lav mics
  -> wireless receivers or audio recorder
  -> laptop/tablet audio input
  -> live transcription app
  -> Convex transcript storage
  -> AI next-question engine
```

If the recorder supports multitrack recording, keep each mic on a separate track. This improves speaker separation and post-session cleanup.

## Which Audio Is Used For Live Transcription

The live transcription system should use the cleanest real-time feed available.

Recommended order:

1. Mixed output from the audio recorder or interface.
2. USB audio feed from the wireless mic receiver.
3. Laptop-connected USB microphone.
4. Built-in laptop microphone only for emergency testing.

The transcription feed does not need to be perfect archive quality, but it must be clear enough for the AI to understand the conversation live.

The live transcription feed is used for:

- live transcript display,
- AI next-question generation,
- current topic detection,
- interviewer prompts.

It is not the final preserved recording.

## Which Audio Is Stored As The Actual Recording

The actual recording should be stored locally on reliable recording hardware.

Recommended order:

1. Multitrack recorder recording each lav separately.
2. Wireless lav internal recordings.
3. Camera audio backup.
4. Laptop local recording.

The stored recording is used for:

- archival preservation,
- post-interview transcript correction,
- future book/report creation,
- documentary editing,
- family archive delivery,
- reprocessing if the live transcript had errors.

## Live Transcription vs Source Recording

Use this distinction:

| Item | Purpose | Where It Comes From | Stored Where |
| --- | --- | --- | --- |
| Live transcription audio | Helps AI listen during the interview | mixed feed into laptop/tablet | temporary stream, optional app recording |
| Source recording | Permanent original interview record | recorder/internal lav recording | local recorder first, then Convex/Google storage later |
| Transcript segments | Searchable text for AI and review | transcription provider | Convex |
| Suggested questions | Interviewer guidance | OpenAI question engine | Convex |

The source recording is the authority. The transcript can be corrected later from the source recording.

## Backup Recording

Always record a backup locally.

The live transcription system should not be the only copy of the interview.

Backup options:

- Zoom H5/H6 recording to SD card,
- Rode Wireless Pro internal recording,
- DJI Mic internal recording,
- laptop local recording,
- camera audio backup if video is being recorded.

Best practice:

- record live transcription audio,
- record local backup audio,
- if video is used, record camera audio as a third backup.

## Recommended Practical Setup

For the first real MVP test:

```text
2 lav mics
  -> wireless receiver
  -> laptop USB/audio input
  -> live transcription

Wireless lav internal recording or Zoom recorder
  -> saves clean backup audio

Next.js app
  -> runs on laptop/tablet
  -> displays live transcript
  -> displays 3-5 follow-up questions

Convex
  -> saves final transcript segments and AI questions
```

For higher-quality client sessions:

```text
4 lav mics
  -> multitrack recorder
  -> each speaker recorded separately

Recorder mix output
  -> laptop/tablet
  -> live transcription

Next.js app
  -> interviewer console
  -> live transcript
  -> 3-5 suggested follow-up questions

Convex
  -> transcripts, questions, bookmarks, session state

Google Cloud Storage or Convex storage
  -> final uploaded audio files if needed
```

## Device Roles

## Laptop or Tablet

Used for:

- running the interviewer console,
- receiving the live audio feed,
- showing the live transcript,
- showing suggested questions,
- marking questions as asked,
- bookmarking important moments.

## Audio Recorder

Used for:

- saving the actual interview recording,
- recording multiple mic tracks,
- protecting against internet or software failure.

## Wireless Lav System

Used for:

- close-mic capture of each speaker,
- reducing room noise,
- optionally recording internally on each transmitter.

## Headphones

Used by the operator to confirm:

- all mics are working,
- nobody is clipping,
- lavs are not rubbing against clothes,
- the live audio feed is usable.

## Audio Monitoring

The operator should wear headphones and monitor:

- mic connection,
- clipping,
- background noise,
- clothing rustle from lav mics,
- weak battery,
- participant too far from mic,
- internet/transcription connection state.

The interviewer should not need to manage audio during the conversation if there is an operator present.

## Room Setup

Choose a quiet room.

Avoid:

- echo-heavy empty rooms,
- fans,
- open windows,
- street noise,
- restaurants,
- loud air conditioning,
- hard surfaces without soft furnishings.

Improve the room with:

- curtains,
- carpets,
- sofas,
- soft chairs,
- closed doors and windows,
- phones on silent.

## Internet Setup

Live transcription needs stable internet.

Recommended:

- primary Wi-Fi,
- mobile hotspot backup,
- charger/power bank,
- test upload speed before the session.

If internet fails, the backup recorder protects the interview. The transcript can be generated later from the saved audio.

## Pre-Interview Checklist

Before the guest arrives:

- charge all microphones,
- charge laptop/tablet,
- format or check recorder SD card,
- test microphone levels,
- test live transcription connection,
- create interview session in the app,
- check guest name and profile,
- set interview mode,
- confirm local backup recording works,
- confirm headphones work,
- silence phones and room noise.

## During Interview Checklist

During the session:

- confirm transcript is appearing,
- confirm backup recorder is running,
- watch battery levels,
- watch connection status,
- bookmark important moments,
- mark asked questions,
- regenerate questions when needed.

## Post-Interview Checklist

After the session:

- stop live transcription,
- stop backup recorder,
- confirm transcript segments are saved,
- confirm backup audio exists,
- label audio files clearly,
- note any recording issues,
- export or back up raw files if needed.

## File Naming

Use predictable names:

```text
YYYY-MM-DD_guest-name_interview-session_audio-main.wav
YYYY-MM-DD_guest-name_interview-session_audio-backup.wav
YYYY-MM-DD_guest-name_interview-session_transcript.md
```

Example:

```text
2026-05-24_jane-doe_legacy-interview_audio-main.wav
```

## Important Principle

The live AI assistant depends on clean audio.

Bad audio creates:

- poor transcription,
- weak question suggestions,
- missed details,
- more manual cleanup,
- lower client confidence.

Treat microphones, backup recording, and monitoring as part of the core system, not optional accessories.
