# ephemeral-builder (ether)

Public GitHub Actions runner for **alzscriptz/compiler**.

- Receives Objective-C/C source via `repository_dispatch` (`build-dylib`) — **never committed here**
- Builds arm64 iOS `.dylib` on `macos-15` + Xcode
- Publishes the `.dylib` to **private** [alzscriptz/compiler](https://github.com/alzscriptz/compiler) Releases (`latest-build`)
- **Does not** create releases on this repo
- `always()` deletes the workspace so source does not remain on the runner

## Secret required

| Name | Value |
|------|--------|
| `COMPILER_RELEASE_TOKEN` | Fine-grained PAT: Contents Read+Write on **only** `alzscriptz/compiler` |

Add under **Settings → Secrets and variables → Actions**.

## Workflow

`.github/workflows/ephemeral-dylib.yml`

Trigger: `repository_dispatch` type `build-dylib` with `client_payload.source_b64` and `client_payload.filename`.
