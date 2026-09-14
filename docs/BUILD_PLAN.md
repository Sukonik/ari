# ARI build plan: Web, Desktop, iOS

**Status:** proposed implementation roadmap, September 2026. No application has been shipped from this repository.  
**Scope of this change:** planning only. Tooling choices and supported OS versions must be checked when implementation begins.

## Product boundary

ARI is the user-facing AI operating platform. Atlas is the local execution foundation underneath ARI Desktop and, later, Atlas OS. The [GoldenSunAI portfolio site](https://github.com/Sukonik/goldensunai) remains a separate company website; ARI Web is the ARI product experience, including its public introduction and signed-in application.

| Surface | Build approach | First meaningful capability | Network expectation |
| --- | --- | --- | --- |
| **ARI Web** | Responsive web client and a service API | Workspace, file, Chat, source, and review flow | Online for hosted services; no claim of offline inference |
| **ARI Desktop** | Tauri shell with shared web UI components plus native Atlas bridge | The same flow with explicit local-file access and an optional local model | Core local flow should work offline once dependencies are installed; connected providers remain optional |
| **ARI for iOS** | Native SwiftUI app using the same service contracts | Chat, workspace history, file capture/import, and review of synced work | Online-first initially; offline reading/draft queue only after sync semantics are proven |

Tauri is a choice for **desktop**, not a requirement that the iOS app use Tauri. SwiftUI is the proposed iOS client; share API schemas and behavior, not a forced web layout. See [Tauri's platform overview](https://tauri.app/start/) and [Apple's SwiftUI documentation](https://developer.apple.com/documentation/swiftui/).

## One common foundation

- **Identity and scope:** user identity; separate personal, household, and organization workspaces; explicit per-workspace permissions.
- **Conversation and evidence:** messages, source references, citations, provider identity, and clear error/cancel/retry states.
- **Provider contract:** one internal interface for hosted and local inference. Record capabilities, cost limits, model availability, and what data may leave the device. Provider failover requires consent and compatible context; it must not silently send sensitive content elsewhere.
- **Memory contract:** opt-in, inspectable, editable, and removable context, scoped to a person and workspace. No cross-workspace memory by default.
- **Files and actions:** upload/import permission, provenance, review flags, and confirmation before renaming, moving, sending, publishing, or changing files.
- **Sync boundary:** define stable IDs, revisions, deletion semantics, and conflict resolution before claiming seamless web/desktop/iOS continuity. A local-only workspace must not silently become cloud-synced.
- **Privacy and security:** secrets outside Git; narrowly scoped provider credentials; retention and export/delete controls; automated checks plus human review for AI-generated changes.

Initial development and demos use synthetic or explicitly authorized content. Do not import municipal, privileged, customer, or private household data into this public repository.

## Incremental delivery

### Phase 0 — Repo foundation

1. Agree on product vocabulary, module boundaries, and the first user journey.
2. Establish issue and PR templates, CONTRIBUTING guidance, tests, security reporting instructions, and brand-use guidance. Keep the existing MPL-2.0 license unchanged.
3. Add a small code workspace only when the first implementation PR begins. Suggested future shape:
   - `apps/web/` — responsive ARI web client and public ARI introduction;
   - `apps/desktop/` — Tauri desktop shell and native/local adapters;
   - `apps/ios/` — Xcode/SwiftUI project;
   - `services/api/` — hosted API, auth, permission checks, and provider gateway;
   - `packages/contracts/` — versioned API schemas, fixtures, and generated clients as needed;
   - `packages/ui/` — web/desktop visual components, not iOS source;
   - `docs/` — architecture decisions, user journeys, and release gates.
4. CI should check formatting, tests, dependency/security issues, and buildability for changed surfaces without committing secrets or signing credentials.

**Gate:** a new contributor can understand scope and run the first sample locally from written instructions. Do not add empty app directories merely to imply progress.

### Phase 1 — ARI Web: first complete journey

- Public ARI landing/introduction with a clear concept or beta label; the interactive app is a separate signed-in area. A static host can serve the introduction, but dynamic user work requires an application backend and storage—not GitHub Pages alone. [GitHub Pages overview](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages).
- Responsive Chat and one Workspace type; import a supported file; ask a question; show the cited passage and which provider answered; propose a draft/action that must be explicitly accepted or rejected.
- Begin with one authorized provider adapter and one fixture/test provider. Do not advertise a marketplace or automatic failover before they exist.
- Separate browser-safe public code from server-side secrets. Define account and workspace deletion/export behavior before real-user onboarding.

**Gate:** a user can complete the full file → answer → source → review loop on desktop and mobile browsers; tests cover permission denial, missing source, timeout, cancel, and provider failure.

### Phase 2 — ARI Desktop and Atlas Runtime

- Package the proven ARI interface with Tauri for Windows and macOS; introduce native file selection and per-directory permissions through a narrow capability boundary.
- Implement Atlas's local runtime behind the same provider contract. Start with one supported local inference path and a hardware/system check before expanding to additional model engines.
- Clearly show **Local / Connected / Offline** state and where each request is processed. Local-only projects should function without a network after setup; nothing uploads without a deliberate action.
- Test clean install/uninstall, file permissions, model unavailability, low-resource behavior, background process shutdown, and upgrades on declared OS versions. Validate any desired older-macOS support on real hardware before promising it.

**Gate:** the same reviewed source-backed journey works with a local model while disconnected, and desktop-specific permissions and cleanup pass Windows/macOS checks.

### Phase 3 — ARI for iOS

- Build a native mobile experience: fast Chat, recent workspaces, document/photo capture, source viewing, review/approval, and Planner entry points.
- Consume versioned ARI API contracts; store credentials using platform security facilities. Do not put provider secrets inside the app bundle.
- Scope initial sync to explicitly chosen workspaces. Add offline reading or queued drafts only when conflicts, retries, and data-removal behavior are testable.
- Test accessibility, small-screen interaction, account recovery, notifications/permissions, and device/simulator behavior before beta distribution.

**Gate:** mobile can safely start or continue the first ARI journey, identify its sources, and approve/reject a draft without bypassing workspace permissions.

### Phase 4 — Expand carefully

Prioritize on evidence from the first journey. Candidates include ARI Folder, Documents, Memory, Calendar, Planner, connected-provider routing and continuity, Code, Legal, Home, Local, ClearSky integration, Gemelli, and the AI Store. Each module needs its own scope, permissions, data ownership, success measure, and release gate. Paid plans, provider resale, and API inference pools require separate product, legal, billing, and privacy decisions.

**Atlas OS** is a later research track after Atlas Desktop has a stable, secure runtime; a bootable SSD image is not a prerequisite for Web or iOS.

## Open-source and product boundaries

The existing repository code license is **MPL-2.0**. Contributors can extend the platform under its terms; paid GoldenSunAI services or separately licensed additions must not misstate rights to MPL-covered source. Brand use is a different permission from code reuse: document how forks may describe compatibility without appearing official. Check third-party dependencies, models, weights, datasets, icons, and fonts individually before redistribution.

## Decisions to make before implementation

- What is the first provider/local-model combination for the prototype?
- Which data stays on-device, and which workspaces may sync?
- What is the first supported desktop OS matrix and the minimum iOS version?
- What is the initial hosted deployment and account model?
- Which ARI brand assets can forks use, if any?
- How do existing ClearSky and BlackBowAI products integrate while retaining their own identity, repositories, and data boundaries?
