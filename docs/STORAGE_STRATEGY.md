# Storage Strategy

## Decision

Use Convex first.

Convex should store:

- interview records,
- transcript segments,
- suggested questions,
- interviewer actions,
- bookmarks,
- small generated files or exports when needed.

## Why Convex First

Convex keeps the MVP simple because it can handle:

- backend functions,
- database records,
- realtime subscriptions,
- file storage,
- app state.

This reduces the amount of infrastructure needed for the first build.

## When To Add Google Cloud Storage

Add Google Cloud Storage later if the product needs:

- long raw audio recordings,
- video files,
- edited media exports,
- large archival packages,
- media workflows outside the app.

If Google Cloud Storage is added, Convex should still store the metadata and file references.

Example:

```ts
{
  interviewId: Id<"interviews">;
  storageProvider: "google_cloud_storage";
  bucket: "legacy-interviews";
  path: "interviews/session-id/audio.wav";
  createdAt: number;
}
```

