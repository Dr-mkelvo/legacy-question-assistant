# Recording Setup

This document covers the physical recording setup required for live transcription and AI next-question assistance.

The software can only perform well if the audio is clean. For this product, audio quality is infrastructure.

## Recommended Interview Kit

For serious interviews, use a 2-4 microphone setup.

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

