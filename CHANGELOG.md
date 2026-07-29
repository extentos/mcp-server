# Changelog

Release notes for [`@extentos/mcp-server`](https://www.npmjs.com/package/@extentos/mcp-server). The package is pre-1.0; tool surfaces may evolve between minor versions.

For the full version history, see the [npm versions page](https://www.npmjs.com/package/@extentos/mcp-server?activeTab=versions).

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
