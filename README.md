# ARI 🧠

**One place for your AI, work, files, communications, home, and life.**

ARI is an open-source AI operating platform from [Team GoldenSun](https://github.com/Sukonik/goldensunai). It brings intelligence, context, applications, people, and workflows into one connected experience. ARI Chat is the conversational front door; workspaces and specialized modules give that conversation a place to do useful work.

> **Project status: concept and architecture.** This repository does not yet contain a working ARI application. The modules, integrations, tiers, and products below are plans—not released features, commitments, or offers.

## Product surfaces

| Surface | Purpose | Initial direction |
| --- | --- | --- |
| **ARI Web** 🌐 | ARI's own product website and browser-based application. The introduction and signed-in workspace are distinct from the existing GoldenSunAI company portfolio site. | Responsive Chat, workspaces, files, sources, and reviewed workflows backed by an ARI service API. |
| **ARI Desktop** 💻 | A Windows/macOS application for work on your computer, including local files and optional local AI. | Tauri desktop shell, shared web components where appropriate, and native Atlas integration. |
| **ARI for iOS** 📱 | A phone-native companion for conversations, capture, planning, and continuing permitted work. | Proposed SwiftUI client using versioned ARI API contracts rather than a compressed desktop UI. |
| **Atlas OS** 💾 | A future portable, bootable SSD-based Linux AI environment for ARI. | Research track after Atlas Desktop's local runtime is proven; not required for Web, Desktop, or iOS. |

The three ARI clients share **product concepts, API contracts, identity, permission rules, and design language**. They need not share every screen or implementation language. ARI Web may be online for hosted services; ARI Desktop's local capabilities should remain useful offline after setup; mobile sync needs explicit, tested rules. See the [build plan](docs/BUILD_PLAN.md) for delivery order and acceptance gates.

## The ARI architecture

ARI has four cooperating levels:

| Level | Responsibility | Boundary |
| --- | --- | --- |
| **1. Experiences** | Web, Desktop, iOS, and ARI Chat present the right interface for each device and task. | A client requests capabilities; it does not bypass data permissions or hold server-only provider secrets. |
| **2. Platform foundation** | Identity, workspace scope, permissions, provider routing, memory, files, source records, workflow approval, storage, and optional sync. | Every request declares whose data it can use, where it runs, and whether content may leave the device. |
| **3. Product modules** | Intelligence, Work, Home, Planner, Life, and Communications compose foundation capabilities into user journeys. | Modules use shared contracts instead of inventing separate accounts, memories, or permission systems. |
| **4. Atlas local runtime** | Hardware-aware local models, agents, tools, and resources support Desktop and future Atlas OS. | Local-only work must not silently upload data; connected providers remain opt-in. |

A typical first journey is **Workspace → permitted file → ARI Chat → chosen AI → answer with sources → user-reviewed draft/action**. The same contract should support a hosted provider in Web and a local model in Desktop without pretending the execution or privacy properties are identical.

### Shared foundation contracts

- **Identity and workspaces:** personal, household, and organizational contexts remain distinct; people and agents receive only explicit permissions.
- **Model routing and continuity:** choose a capable authorized provider or local model, show the choice, enforce budget/data rules, and fail over only when consent and compatibility permit it. A consumer subscription is not automatically API access.
- **Memory:** persistent, inspectable, editable, deletable context tied to the right user and workspace, never a global pool of everybody's information.
- **Files and documents:** record provenance, extracted text, versions, source citations, proposed changes, and review status. Import, rename, move, send, and publish require appropriate permission and confirmation.
- **Tools and workflows:** permission-scoped operations with visible status, cancel/error handling, audit history where needed, and a human review step for consequential actions.
- **Sync and storage:** local-only versus synced workspaces are explicit. Stable IDs, revisions, conflicts, deletion, retention, and export must be defined before promising seamless continuity.
- **Developer interfaces:** versioned API and extension contracts allow community-built agents, skills, connectors, and applications without giving them unrestricted platform access.

## Product pillars

### 🧠 ARI Intelligence

The intelligence and AI-discovery layer:

- **ARI Intelligence Free:** proposed free AI experience.
- **ARI Capsule AI:** proposed native efficient model; its relationship to earlier Capsule AI personalization concepts needs a naming decision.
- **AI connections:** opt-in support for compatible providers such as ChatGPT/OpenAI APIs, Claude, Gemini, Perplexity, Grok, Mistral, and open/local models, subject to each provider's actual interfaces and terms.
- **ARI AI Store:** future discovery and comparison of models, agents, skills, and workflows, with possible subscription management or sales after separate product and legal review.

ARI should help users choose the right intelligence for a task, not require them to know every model name. No price or availability is implied here.

### 🚀 ARI API Continuity

A future provider availability and budget layer. When an authorized API is rate-limited, unavailable, or out of capacity, ARI may suggest or use a compatible fallback **only within the user's provider permissions, data-sharing consent, and spending limit**. Basic/Enhanced/Pro/MAX are proposed plan concepts, not released tiers.

> Your AI may reach its limit. Your work doesn't.

### 🧠 ARI Memory

Context for preferences, projects, decisions, people, documents, routines, and organizational knowledge, subject to inspection and correction. Memory belongs to a scope: a personal preference is not automatically a family preference, and a work matter is not automatically available to another workspace.

### 💼 ARI Work

- **Workspace:** each project, matter, or department can bring together files, conversations, tasks, calendar, people, decisions, agents, models, and workflows.
- **ARI Folder:** classification, renaming, migration, deduplication, OCR, related-file discovery, semantic search, intake triage, and explainable filing. It draws on BlackBowAI ideas without merging that product's code or data by assumption.
- **ARI Documents:** read, search, compare, extract, OCR, summarize, annotate, redact, transform, draft, version, and review. The flagship pattern is **approved template → matter facts → sourced draft → changes and flags → human approval**.
- **ARI Code:** role-based AI development team (Architect, Developer, Tester, Security Reviewer, Code Reviewer, Project Manager) orchestrated in one workspace.
- **ARI Legal:** specialized Work environment for matters, research, intake, deadlines, prior-matter discovery, template transformation, and attorney review. No unsupervised final legal output is promised.
- **ARI Calendar:** meetings, deadlines, availability, projects, and focus time, with task-aware suggestions.

### 🏠 ARI Home

A permission-aware household layer for tasks, bills, subscriptions, shopping, maintenance, warranties, deliveries, appliances, home projects, and family coordination. Shared calendars and chores do not imply shared access to each family member's private data.

### 📋 ARI Planner

Personal tasks, goals, routines, reminders, habits, trips, and flexible scheduling. Planner can combine authorized context from Home, Calendar, Local, and ClearSky. It is a module of the larger ARI platform, even if presented independently on the GoldenSunAI portfolio.

### 🌎 ARI Life

- **ARI Local:** places, businesses, services, activities, neighborhood information, and events.
- **ARI ClearSky:** weather and environmental context via a future integration with the independent [ClearSky project](https://github.com/Sukonik/weather-app).
- **ARI Gemelli:** a future human-connection concept for friendship, dating, and activity partners; privacy and safety design come before implementation.

### 🗣️ ARI Communications

**ARI Chat** is the universal conversational front door. It routes a request to the appropriate permitted module—for example, “Draft this” to Documents, “When am I free?” to Calendar, or “Find something to do Saturday” to Local, ClearSky, and Planner. Future communication integrations must be opt-in and must not imply ARI can read or send a person's messages by default.

## Atlas inside ARI 🗺️

**Golden Sun Atlas is ARI's local and portable computing foundation—not a second, competing operating platform.**

| Atlas layer | Role |
| --- | --- |
| **Atlas Runtime** | Local model execution and orchestration shared by Atlas-powered environments. |
| **Model Router** | Selects a suitable installed model/engine for the permitted task and available resources. |
| **Agent Layer** | Coordinates bounded roles and multi-step local work. |
| **Memory and Tool Layers** | Provide local context and permission-scoped operations through ARI contracts. |
| **Hardware Profiler and Resource Manager** | Assess CPU, RAM, GPU/VRAM, and load; avoid overcommitting the device. |
| **Atlas Desktop integration** | Gives ARI Desktop native/local capabilities. |
| **Atlas OS** | Future bootable SSD-based Linux environment using the proven runtime. |

Candidates for later engine support include Ollama, llama.cpp, MLX, vLLM, and compatible open models; these are research candidates, not bundled dependencies. Atlas's geographic release train begins with the **Long Island Series**, reserving **Atlas 1.0 Long Beach**. ARI itself need not use Atlas's version numbers.

## First working milestone

Build one end-to-end, reviewable flow:

**Open a workspace → add a permitted file → ask ARI a question → inspect the cited source → approve or reject a proposed draft/action.**

Start with synthetic or personally authorized content. Never put municipal, privileged, customer, or other sensitive information in this public repository. Advanced modules, paid offerings, multi-provider failover, iOS sync, and Atlas OS follow only when the common foundation and relevant security gates work.

## Open source and brand

The source code in this repository is available under the [Mozilla Public License 2.0](LICENSE). Contributors can build on the platform, and paid services/products can coexist with the license while honoring rights to MPL-covered code. The code license does **not** grant rights to the ARI, Atlas, Team GoldenSun, or GoldenSunAI names or logos. Contribution and brand-use guidance should be reviewed before substantial outside contributions.

**Built by Team GoldenSun ☀️**
