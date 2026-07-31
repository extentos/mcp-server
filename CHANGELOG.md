# Changelog

Release notes for [`@extentos/mcp-server`](https://www.npmjs.com/package/@extentos/mcp-server). The package is pre-1.0; tool surfaces may evolve between minor versions.

For the full version history, see the [npm versions page](https://www.npmjs.com/package/@extentos/mcp-server?activeTab=versions).

## 0.11.29 — 2026-07-31

Round 2 of the fresh-agent audit. Every finding was verified against source
before anything changed, which reversed the answer on three of them.

- The simulator needs a camera source and nothing said so: `capturePhoto`
  returns `camera_not_started` until one is armed, while every other diagnostic
  reports healthy. Cost a fresh agent ~35 minutes. Simulator-only — real glasses
  photograph cold.
- `generateConnectionModule` still told developers to add their own OpenAI key
  in the dashboard. There is no BYOK into Extentos; the assistant is
  gateway-only.
- `getPermissions` pointed Meta credentials at a file that has no field for them.
- Conflicting history numbers, and a reference to a "BYOK key" that does not
  exist.
- The Android preflight said "before any other tool call" for a check that needs
  a project to already exist.
- `voice_command` never mentioned `firesWhen`, whose default silently stops a
  wake phrase firing once an assistant session is active.
- The generated manifest persisted an empty permissions array.

## 0.11.28 — 2026-07-31

Everything here came from one fresh-agent audit of the published surface: an
agent building a real camera + assistant app using only these tools and the
public docs. Every finding was reproduced before anything changed.

- `validateIntegration` now re-reads the credentials file it emits. It returned
  18/18 "Safe to test" for a project whose credentials were still `REPLACE_ME`.
  The new check warns rather than errors — the simulator genuinely does not need
  real credentials — and says the true thing: safe to simulate, cannot reach
  hardware.
- The retired `'ai'` event-log chip is gone from live output. Session setup and
  six code-example passages still recommended a filter value removed on
  2026-07-25, so following the freshest text produced a tool error. `ai_call_*`
  events live under `'custom'`.
- "Can I bring my own key for the assistant?" had four different answers in one
  session, including one example that contradicted itself. Managed gateway is
  the only path, and the text now says so consistently.
- The paste-ready Anthropic client no longer defaults to a previous-generation
  model id.
- BYOK examples pass `failureReason` to `aiCall`, so a typed failure stops
  logging as a success. Needs SDK 2.1.1.

Pairs with SDK **2.1.1**, which fixes a host-app crash when the vendor SDK never
initialised, and adds `failureReason` to `observability.aiCall`.

## 0.11.27 — 2026-07-31

Serves SDK **2.1.0** on both platforms (Maven Central + `swift-glasses`).

- Brilliant Labs no longer appears in `getPlatformInfo`'s Android artifact list. As of SDK 2.1.0 its transport ships inside `com.extentos:glasses`, so an agent that added `com.extentos:glasses-brilliant` was adding a dependency that does nothing. A vendor should cost an app exactly what the vendor charges, and Brilliant charges nothing — no SDK, no account, just BLE. The stub coordinate keeps publishing so existing builds still resolve.
- Meta stays a separate artifact, because Meta genuinely charges: its DAT artifacts sit behind a credentialed repo.

## 0.11.26 — 2026-07-30

- Brilliant capability corrections: still capture and the microphone work on both platforms; video is refused permanently, because neither Brilliant device has a video primitive or a codec.
- `createSimulatorSession` gained a platform × vendor gate. A vendor whose transport cannot exist on the session's platform is now refused at mint rather than offered and then failing — Android XR's model is a projected Android activity, so no iOS transport can exist for it.

## 0.11.20 — 2026-07-29

Catches this public changelog up: it had stopped at 0.11.0 while npm reached
0.11.20. Highlights across that span, newest first.

- **Brilliant Labs is a selectable vendor.** `createSimulatorSession({ glasses: "brilliant" })`
  mints a session for Brilliant Halo or Frame, so an app's behaviour under a round
  256×256 panel, a display-with-no-speaker, and hardware that cannot traverse focus
  is testable without owning either device. The `glasses` enum is now derived from
  the device registry rather than hand-listed.
- **`getPlatformInfo` artifact coordinates are correct again.** `glasses-meta` had
  been pinned at a version of that artifact which never existed, so agents following
  it dead-ended at "Could not find". The release tooling that let it drift is fixed
  too, not just the value.
- **Android XR display support**, and per-device panel geometry throughout — the
  simulator now draws each device's real panel rather than one vendor's shape for
  everyone.
- SDK artifacts referenced by the tools move to **2.0.1** (Android and iOS, lockstep).

Full detail lives in the [monorepo changelog](https://extentos.com/docs/resources/changelog).

## 0.10.2 — 2026-07-16

- Registered for the official MCP registry: the npm package now carries `mcpName` (`com.extentos/mcp-server`) and a `server.json` manifest
- Package metadata now points at this repository (issues, license) and [extentos.com/docs/mcp-server](https://extentos.com/docs/mcp-server)
- No tool changes

## 0.10.1 — 2026-07-15

Current release at the time this repository was created.
