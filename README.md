# ephemeral-builder (ether)

Public GitHub Actions runner for **alzscriptz/compiler**.

- Receives Objective-C/C source via `repository_dispatch` (`build-dylib`) — **never committed here**
- Builds arm64 `.dylib` on `macos-15` + Xcode against **any major Apple SDK**
- Publishes the `.dylib` to **private** [alzscriptz/compiler](https://github.com/alzscriptz/compiler) Releases (`latest-build`)
- **Does not** create releases on this repo
- `always()` deletes the workspace so source does not remain on the runner

## Supported SDKs (`client_payload.sdk`)

`iphoneos` (default) · `iphonesimulator` · `macosx` (MacSDK) · `appletvos` · `appletvsimulator` · `watchos` · `watchsimulator` · `xros` · `xrsimulator`

## Secret required

| Name | Value |
|------|--------|
| `COMPILER_RELEASE_TOKEN` | Fine-grained PAT: Contents Read+Write on **only** `alzscriptz/compiler` |

Add under **Settings → Secrets and variables → Actions**.

## Workflow

`.github/workflows/ephemeral-dylib.yml`

Trigger: `repository_dispatch` type `build-dylib` with:

- `client_payload.source_b64`
- `client_payload.filename`
- `client_payload.sdk` (optional, defaults to `iphoneos`)
