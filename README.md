# Extentos MCP Server

[![npm version](https://img.shields.io/npm/v/%40extentos%2Fmcp-server)](https://www.npmjs.com/package/@extentos/mcp-server)
[![license: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

**Give your AI coding agent the tools to build smart-glasses apps.**

Extentos is an MCP (Model Context Protocol) server that lets agents like Claude Code, Cursor, and Cline add smart-glasses capabilities — camera capture, voice triggers, live transcription, audio playback — to any Android or iOS app. The tools are deterministic: discovery, scaffolding, validation, and a browser-based simulator for end-to-end testing without hardware.

Works with Meta smart glasses today (Ray-Ban Meta, Oakley Meta, Meta Ray-Ban Display), with a multi-vendor architecture by design.

This repository is the public home of [`@extentos/mcp-server`](https://www.npmjs.com/package/@extentos/mcp-server) — releases, changelog, and issue tracking. The package ships on npm.

## Install

**Claude Code**

```bash
claude mcp add extentos -- npx -y @extentos/mcp-server@latest
```

**Cursor** — one click:

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](cursor://anysphere.cursor-deeplink/mcp/install?name=extentos&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsIkBleHRlbnRvcy9tY3Atc2VydmVyQGxhdGVzdCJdfQ==)

**Cline / any MCP client**

```json
{
  "mcpServers": {
    "extentos": {
      "command": "npx",
      "args": ["-y", "@extentos/mcp-server@latest"]
    }
  }
}
```

Requires Node 20+.

## What your agent can do with it

| Tool group | What it does |
|---|---|
| **Discovery** | `getPlatformInfo`, `getCapabilityGuide`, `getCodeExample` — the SDK capability catalog, per-feature call shapes in Kotlin + Swift, and canonical end-to-end patterns (voice Q&A, photo-describe, live transcription UI, …) |
| **Scaffolding** | `generateConnectionModule` — generates the connection UI + manifest + platform config for your app (Android or iOS) |
| **Guidance** | `getVoiceCommandGuidance`, `getPermissions` — implementation guidance the agent queries instead of guessing |
| **Validation** | `inspectIntegration`, `validateIntegration` — deterministic checks of the integration in your repo |
| **Simulation** | `createSimulatorSession`, `getEventLog`, `getSimulatorStatus` — a browser simulator running the same SDK code as production with only the transport swapped; the agent drives it and reads the event log to verify behavior |
| **Production** | `getProductionChecklist`, `getCredentialGuide` — the path from simulator to real glasses |
| **Docs** | `searchDocs` — bundled, versioned documentation topics |

The workflow an agent typically runs: discover capabilities → scaffold the connection module → write handler code against the SDK → validate → simulate end-to-end → production checklist.

## How it fits together

- Your app depends on the native SDK: [`com.extentos:glasses`](https://central.sonatype.com/artifact/com.extentos/glasses) (Android, Maven Central) or the Swift package (iOS)
- Your code subscribes to capability primitives from its own handler classes — `glasses.audio.transcriptions()`, `glasses.camera.capturePhoto()`, `glasses.audio.speak()`
- The simulator is the same app on a different substrate: WebSocket transport instead of Bluetooth, so agent-verified behavior carries to hardware

Discovery, validation, and guidance tools work anonymously. Creating browser-simulator sessions and scaffolding require a free account — the server walks the agent (and you) through a device-code sign-in when needed.

## Links

- [Documentation](https://extentos.com/docs)
- [Getting started with an agent](https://extentos.com/docs/getting-started/with-agent)
- [MCP tools reference](https://extentos.com/docs/reference/mcp-tools)
- [The smart-glasses ecosystem reference](https://extentos.com/docs/ecosystem)

## Issues & feedback

Bug reports and feedback are welcome — [open an issue](https://github.com/extentos/mcp-server/issues). The package is pre-1.0; tool surfaces may evolve between minor versions.

For security reports, see [SECURITY.md](./SECURITY.md) — please don't open public issues for vulnerabilities.

## License

[MIT](./LICENSE)
