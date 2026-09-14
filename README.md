# ARI 🧠

**One place for your AI, work, files, communications, home, and life.**

ARI is an open-source AI operating platform from [Team GoldenSun](https://github.com/Sukonik/goldensunai). It aims to connect intelligence, applications, data, communication, and workflows through a coherent experience. Ask ARI a question, continue work in a project, find a document, or plan your time without repeatedly teaching separate tools the same context.

> **Status: concept and planning.** The repository does not yet contain a working ARI application. Product areas and prices discussed elsewhere are proposals, not available features or offers.

## Three ways to use ARI

| Surface | Intended role |
| --- | --- |
| **ARI Web** | Browser-based product website and signed-in workspaces: Chat, files, sources, memory controls, and workflows. Distinct from the existing GoldenSunAI company portfolio site. |
| **ARI Desktop** | Windows and macOS app built with Tauri. Reuses appropriate web experience while adding native file access and, through Atlas, local/offline AI capabilities. |
| **ARI for iOS** | Native mobile app for conversations, projects, capture, planning, and appropriately scoped access to synced work. Designed for a phone, not a compressed desktop screen. |

The three clients should share product concepts, API contracts, permissions, and a design language—not necessarily identical layouts or implementation languages. See the [three-surface build plan](docs/BUILD_PLAN.md) for sequence, boundaries, and acceptance gates.

## Platform map

- **ARI Intelligence:** native and connected AI, provider selection, and future AI marketplace.
- **ARI API Continuity:** authorized, budget-aware provider failover when an API is unavailable or limited.
- **ARI Memory:** user-controlled context, scoped to the right person and workspace.
- **ARI Work:** workspaces, Folder, Documents, Code, Legal, and Calendar.
- **ARI Home and Life:** household tools, Planner, Local, ClearSky integration, and future Gemelli.
- **ARI Communications:** Chat as the conversational front door across the platform.

These are a **product map**, not a claim that each module is implemented. Provider connections require supported APIs and user authorization; a consumer subscription alone does not grant ARI API access.

## Atlas inside ARI 🗺️

**Golden Sun Atlas is ARI's local and portable computing foundation**, not a competing top-level operating platform:

- **Atlas Runtime:** model routing, agents, tools, hardware profiling, and resource management.
- **Atlas Desktop integration:** local model and file capabilities in ARI Desktop.
- **Atlas OS:** a future bootable SSD-based Linux environment, after the desktop runtime is proven.

Atlas retains its geographic release names, beginning with the Long Island Series and **Atlas 1.0 Long Beach**. ARI, Atlas, ClearSky, and BlackBowAI may connect or inform each other without implying that their existing code or data has been merged.

## First working milestone

Build one end-to-end, reviewable flow:

**Open a workspace → add a permitted file → ask ARI a question → see the source → approve or reject a proposed draft/action.**

Start with synthetic or personally authorized test content. Do not place municipal, privileged, customer, or other sensitive material in this public repository. Later releases can add local models, synchronization, mobile capture, and specialized modules against the same privacy and permission boundaries.

## Open source

The source code in this repository is available under the [Mozilla Public License 2.0](LICENSE). Contributions and commercial products can coexist with that license. The code license does **not** grant rights to the ARI, Atlas, Team GoldenSun, or GoldenSunAI names or logos. A contributor guide and precise brand-use policy should be reviewed and added before inviting substantial outside contributions.

**Built by Team GoldenSun ☀️**
