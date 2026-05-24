# Transcription Alternatives

This file documents the transcription options researched for the live interview assistant.

## Recommendation

Start with Deepgram.

Use OpenAI for the question engine. Consider OpenAI Realtime transcription only if keeping transcription and question generation inside the same provider becomes more valuable than Deepgram's specialized realtime transcription workflow.

Keep Google Cloud Speech-to-Text as the main fallback for Swahili/Kenyan language coverage.

## Option 1: Deepgram

## Best For

- live transcription,
- low latency,
- browser/WebSocket workflow,
- interim results,
- diarization,
- word timestamps,
- production voice applications.

## Why It Fits

This product needs live transcription during an active interview. Deepgram is purpose-built for realtime speech-to-text and has a practical WebSocket API. It is a strong first choice for getting an MVP working quickly.

## Tradeoffs

- Language coverage may be narrower than Google or OpenAI.
- Swahili and mixed Swahili/English should be tested with real Kenyan interview samples before finalizing.
- Some advanced analysis still belongs in our own AI pipeline, not the transcription provider.

## Role In Our System

Primary live transcription provider.

## Option 2: AssemblyAI

## Best For

- streaming transcription,
- diarization,
- turn-based transcription,
- audio intelligence features,
- summaries, topics, PII redaction, and other transcript analysis features.

## Why It Fits

AssemblyAI is attractive if we want the transcription provider to do more than raw transcription. Its streaming system can identify turns and supports speaker labels. It also has strong post-transcription intelligence features.

## Tradeoffs

- May be more expensive depending on usage.
- Streaming language support and exact model choices need to be validated against English/Swahili use.
- Some built-in intelligence may overlap with our own AI question engine and later archive analysis.

## Role In Our System

Best alternative if we want more built-in audio intelligence or if diarization quality becomes the main issue.

## Option 3: OpenAI Realtime Transcription

## Best For

- keeping transcription and AI reasoning close together,
- realtime transcription through WebSocket/WebRTC,
- voice/AI products where OpenAI is already central,
- multilingual transcription models.

## Why It Fits

OpenAI can handle realtime transcription sessions and also power the next-question engine. This could simplify vendor management because one provider handles transcription and reasoning.

## Tradeoffs

- Diarization and provider-specific realtime transcription controls may not be as mature as specialized transcription platforms for interview workflows.
- Cost and latency should be benchmarked directly.
- The architecture should avoid sending unnecessary audio to the AI model when text transcript is enough.

## Role In Our System

Secondary option. Use for question generation first. Test for transcription after Deepgram MVP is working.

## Option 4: Google Cloud Speech-to-Text

## Best For

- broad language coverage,
- Swahili/Kenyan language support,
- Google Cloud environments,
- enterprise-style cloud integration.

## Why It Fits

Google has strong language coverage and official Swahili support. This makes it an important fallback if Deepgram or AssemblyAI struggle with Swahili/code-switching.

## Tradeoffs

- Integration can be heavier than Deepgram for a fast MVP.
- Some streaming and diarization capabilities vary by model, region, and language.
- Long-running live workflows may require more careful session handling.

## Role In Our System

Fallback provider for Swahili accuracy and broader multilingual needs.

## Option 5: Azure Speech

## Best For

- broad language and accent coverage,
- enterprise Microsoft environments,
- regulated enterprise deployments.

## Why It Fits

Azure is useful if the project later needs enterprise procurement, compliance, or Microsoft ecosystem integration.

## Tradeoffs

- More cloud setup compared with Deepgram.
- Not the fastest path for the MVP.

## Role In Our System

Enterprise fallback, not first MVP choice.

## Option 6: Self-Hosted Whisper / WhisperX

## Best For

- maximum control,
- offline or private processing,
- batch transcription,
- custom diarization pipelines with tools like pyannote.

## Why It Fits

Self-hosting may become useful if long-term privacy, cost control, or offline archiving becomes important.

## Tradeoffs

- Requires GPU infrastructure.
- More engineering complexity.
- Realtime streaming is not as simple as using a dedicated streaming API.
- Diarization requires additional tooling.

## Role In Our System

Not for MVP. Consider later for archival batch processing or private deployments.

## Provider Decision Matrix

| Provider | MVP Fit | Realtime | Diarization | Swahili/Mixed Language | Complexity | Recommended Role |
| --- | --- | --- | --- | --- | --- | --- |
| Deepgram | High | Strong | Yes | Must test | Low/Medium | First choice |
| AssemblyAI | Medium/High | Strong | Yes | Must test | Medium | Best alternative |
| OpenAI Realtime | Medium | Yes | Limited/variable by workflow | Strong multilingual potential | Medium | AI first, transcription second |
| Google STT | Medium | Yes | Varies by model/language | Strong | Medium/High | Swahili fallback |
| Azure Speech | Medium | Yes | Yes | Broad | Medium/High | Enterprise fallback |
| Self-hosted Whisper | Low for MVP | Custom only | External tooling | Strong multilingual | High | Later archival/private option |

## Final MVP Decision

Use this order:

1. Build with Deepgram.
2. Use OpenAI for next-question generation.
3. Benchmark with real English, Swahili, and mixed-language samples.
4. If Swahili quality is weak, test Google Cloud Speech-to-Text.
5. If diarization or audio intelligence is weak, test AssemblyAI.
6. Keep OpenAI Realtime as a possible simplification later, not the first dependency for transcription.

## Research Sources

- Deepgram live audio WebSocket documentation: https://developers.deepgram.com/reference/speech-to-text/listen-streaming
- AssemblyAI Universal Streaming documentation: https://www.assemblyai.com/docs/streaming/universal-streaming
- AssemblyAI streaming diarization documentation: https://www.assemblyai.com/docs/streaming/label-speakers-and-separate-channels
- OpenAI realtime transcription documentation: https://platform.openai.com/docs/guides/realtime-transcription
- OpenAI speech-to-text documentation: https://platform.openai.com/docs/guides/speech-to-text
- Google Cloud Speech-to-Text supported languages: https://cloud.google.com/speech-to-text/v2/docs/speech-to-text-supported-languages
- Google Cloud speaker diarization documentation: https://docs.cloud.google.com/speech-to-text/docs/v1/multiple-voices

