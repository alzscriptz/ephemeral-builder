# K1pro☆ Ephemeral Builder

**Public** GitHub Actions backend for [K1pro☆](https://github.com/alzscriptz/k1pro).

## What this does

1. Receives a `workflow_dispatch` with a minimal build payload (no permanent source commit).
2. Builds the mobile artifact (APK / AAB / IPA) in an isolated `/tmp` workspace.
3. Uploads a short-lived artifact (1-day retention).
4. Runs an **`always()`** cleanup step that deletes the workspace — **zero source retention**.

## Trigger

Dispatched by the K1pro platform via the GitHub REST API:

```bash
gh api repos/alzscriptz/ephemeral-builder/actions/workflows/ephemeral-build.yml/dispatches \
  -f ref=main \
  -f inputs='{"build_id":"...","framework":"flutter","project_slug":"my-app","source_payload":"...","artifact_type":"apk"}'
```

## Security model

- This repository never stores user source code.
- Source is delivered ephemerally for the job only.
- Cleanup runs on success **and** failure (`if: always()`).

## License

MIT
