# SWEOrchestrAI Local App

Electron desktop application for local SWEOrchestrAI workflows.

**Cloud-managed software delivery. Locally executed AI engineering.**

## Purpose

The `local-app` repository implements the desktop application for SWEOrchestrAI.

It provides the local user interface for runtime status, provider visibility, workspace registration, execution runs, live logs, approvals, and local workflow control.

## Architecture Role

```text
User
  -> local-app
  -> REST + WebSocket over localhost
local-service
  -> Local providers, repositories, MCP tools, and cloud sync
```

The `local-app` belongs to the Local Execution Plane. It provides local UX, but it does not directly execute provider commands. Execution is handled by `local-service`.

## Planned Stack

- Electron
- React
- TypeScript
- Vite
- Electron Builder
- React Router
- TanStack Query
- WebSocket client
- Typed preload API

## Responsibilities

The `local-app` repository is responsible for:

- desktop UI for local workflows,
- connecting to `local-service`,
- showing local-service health,
- showing available providers,
- registering local workspaces,
- starting execution runs,
- displaying live logs and run events,
- showing approval prompts,
- approving or rejecting requested actions,
- showing run results,
- managing local UX around provider configuration,
- providing a safe renderer/preload boundary.

## Non-Responsibilities

The `local-app` repository is not responsible for:

- directly executing shell commands,
- directly invoking AI providers,
- directly modifying local repositories,
- bypassing approval gates,
- owning canonical cloud project state,
- replacing `web`,
- replacing `api`,
- replacing `local-service`.

## Local Communication Model

The intended communication flow is:

```text
React Renderer
  -> Electron Preload API
  -> Electron Main Process
  -> REST + WebSocket over localhost
local-service
```

Example preload API shape:

```ts
window.sweLocalService.health()
window.sweLocalService.listProviders()
window.sweLocalService.startRun(...)
window.sweLocalService.subscribeToRun(...)
window.sweLocalService.approveAction(...)
window.sweLocalService.rejectAction(...)
```

## MVP Scope

Initial local app foundation should support:

- local-service connection status,
- provider list,
- workspace registration,
- start mock run,
- live WebSocket log stream,
- approval modal,
- approve/reject action,
- completed run view.

## Related Repositories

| Repository | Relationship |
|---|---|
| [`overview`](https://github.com/SWEOrchestrAI/overview) | Architecture, roadmap, ADRs, requirements, and contracts. |
| [`local-service`](https://github.com/SWEOrchestrAI/local-service) | Local backend consumed by `local-app`. |
| [`api`](https://github.com/SWEOrchestrAI/api) | Cloud backend that receives synced execution metadata. |
| [`web`](https://github.com/SWEOrchestrAI/web) | Cloud project management UI. |

## Current Status

MVP foundation planning. Implementation has not been scaffolded yet.

## License

Copyright (c) 2026.

This repository is currently shared for portfolio and documentation purposes only. No license is granted for reuse, redistribution, or derivative works unless explicitly stated.
