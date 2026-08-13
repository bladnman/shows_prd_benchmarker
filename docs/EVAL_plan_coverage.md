### 1. Requirements Extraction

#### Pass 1: Identify Functional Areas
- Core Show Model & Collection Semantics
- Persistence, Merge, and Lifecycle Rules
- Navigation and Feature Surfaces
- AI Contracts, Voice, and Discovery Quality
- Detail Page Experience Constraints
- Infrastructure, Identity, and Execution Rider

#### Pass 2: Extract Requirements Within Each Area

##### Core Show Model & Collection Semantics
- PRD-001 | `critical` | Store canonical show data plus user overlay fields | `showbiz_prd.md > 4.1 Show (Movie or TV)`
- PRD-002 | `critical` | Show user-overlaid version anywhere saved shows appear | `showbiz_prd.md > 4.1 Show (Movie or TV)`
- PRD-003 | `critical` | User edits must win against refreshed public metadata | `showbiz_prd.md > 4.1 Show (Movie or TV)`
- PRD-004 | `important` | Support core statuses and hidden Next in model | `showbiz_prd.md > 4.2 Status System (“My Status”)`
- PRD-005 | `critical` | Interested and Excited map to Later plus Interest | `showbiz_prd.md > 4.2 Status System (“My Status”)`
- PRD-006 | `critical` | Clearing status removes show and clears all My Data | `showbiz_prd.md > 4.2 Status System (“My Status”)`
- PRD-007 | `important` | My Interest applies only when status is Later | `showbiz_prd.md > 4.3 Interest Levels (“My Interest”)`
- PRD-008 | `important` | Tags are free-form and power app-wide filtering | `showbiz_prd.md > 4.4 Tags (User Lists)`
- PRD-009 | `important` | Filters include tags, No tags, data, media toggle | `showbiz_prd.md > 4.5 Filters (Ways to View the Collection)`
- PRD-010 | `detail` | Tiles show in-collection and user-rating indicators | `showbiz_prd.md > 5.9 Tile Indicators`

##### Persistence, Merge, and Lifecycle Rules
- PRD-011 | `critical` | Collection membership is defined by assigned My Status | `showbiz_prd.md > 5.1 Collection Membership`
- PRD-012 | `critical` | Auto-save triggers include status, interest, rating, tags | `showbiz_prd.md > 5.2 Saving Triggers`
- PRD-013 | `critical` | Default unspecific save sets Later plus Interested | `showbiz_prd.md > 5.3 Default Values When Saving`
- PRD-014 | `important` | First save via rating defaults status to Done | `showbiz_prd.md > 5.3 Default Values When Saving`
- PRD-015 | `important` | Status removal shows confirmation with optional suppression | `showbiz_prd.md > 5.4 Removing from Collection`
- PRD-016 | `important` | Re-adding preserves My Data and refreshes public metadata | `showbiz_prd.md > 5.5 Re-adding the Same Show`
- PRD-017 | `critical` | Track per-field update timestamps for My Data | `showbiz_prd.md > 5.6 Timestamps`
- PRD-018 | `important` | Persist Scoop with freshness and saved-show constraint | `showbiz_prd.md > 5.7 AI Data Persistence`
- PRD-019 | `important` | Keep Ask history and mentions as session-only data | `showbiz_prd.md > 5.7 AI Data Persistence`
- PRD-020 | `critical` | Map AI recs to real shows by ID/title | `showbiz_prd.md > 5.8 AI Recommendations Map to Real Shows`
- PRD-021 | `important` | Fallback unresolved recommendations to non-interactive or Search | `showbiz_prd.md > 5.8 AI Recommendations Map to Real Shows`
- PRD-022 | `critical` | Resolve sync conflicts per field via newest timestamp | `showbiz_prd.md > 5.10 Data Sync & Integrity`
- PRD-023 | `important` | Detect and merge duplicates transparently during sync | `showbiz_prd.md > 5.10 Data Sync & Integrity`
- PRD-024 | `critical` | Preserve libraries across data-model version upgrades | `showbiz_prd.md > 5.11 Data Continuity Across Versions`

##### Navigation and Feature Surfaces
- PRD-025 | `important` | App layout includes filters panel and main content | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-026 | `important` | Keep persistent global entry points for Find and Settings | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-027 | `important` | Find hub supports Search, Ask, Alchemy mode switching | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-028 | `important` | Home groups by Active, Excited, Interested, Other statuses | `showbiz_prd.md > 7.1 Collection Home`
- PRD-029 | `important` | Home supports media toggle and required empty states | `showbiz_prd.md > 7.1 Collection Home`
- PRD-030 | `important` | Search provides live grid with in-collection markers | `showbiz_prd.md > 7.2 Search (Find → Search)`
- PRD-031 | `detail` | Search can auto-open when Search-on-Launch enabled | `showbiz_prd.md > 7.2 Search (Find → Search)`
- PRD-032 | `important` | Ask displays chat turns and mentioned-show carousel | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-033 | `detail` | Ask welcome shows six random refreshable prompts | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-034 | `important` | Ask summarizes older turns after roughly ten messages | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-035 | `important` | Ask-about-show must seed conversation with show context | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-036 | `critical` | Alchemy flow supports 2+ inputs through chaining | `showbiz_prd.md > 7.4 Alchemy (Find → Alchemy)`
- PRD-037 | `important` | Alchemy backtracking clears concepts and recommendation results | `showbiz_prd.md > 7.4 Alchemy (Find → Alchemy)`
- PRD-038 | `critical` | Show Detail includes full discovery and metadata sections | `showbiz_prd.md > 7.5 Show Detail Page`
- PRD-039 | `important` | Person Detail supports bio, analytics, filmography, linkbacks | `showbiz_prd.md > 7.6 Person Detail Page`
- PRD-040 | `detail` | Settings include font size and Search-on-Launch controls | `showbiz_prd.md > 7.7 Settings & Your Data`
- PRD-041 | `important` | Settings include username, AI model, catalog key controls | `showbiz_prd.md > 7.7 Settings & Your Data`
- PRD-042 | `important` | Export produces zipped JSON backup with ISO timestamps | `showbiz_prd.md > 7.7 Settings & Your Data`

##### AI Contracts, Voice, and Discovery Quality
- PRD-043 | `important` | Restrict all AI responses to TV/movie domain only | `ai_prompting_context.md > 1. Shared Rules (All AI Surfaces)`
- PRD-044 | `critical` | Default AI behavior is spoiler-safe unless explicitly requested | `ai_prompting_context.md > 1. Shared Rules (All AI Surfaces)`
- PRD-045 | `important` | AI reasoning should be honest, specific, non-generic | `ai_prompting_context.md > 1. Shared Rules (All AI Surfaces)`
- PRD-046 | `important` | Keep one persona across AI; Search has none | `ai_voice_personality.md > 1. Persona Summary`
- PRD-047 | `important` | Ask responses are dialog-first with list formatting for recs | `ai_prompting_context.md > 3.1 Ask (Chat)`
- PRD-048 | `critical` | Ask mentions output strict commentary plus showList contract | `ai_prompting_context.md > 3.2 Ask with Mentions`
- PRD-049 | `important` | Scoop must include required sections and balanced structure | `ai_prompting_context.md > 3.3 Scoop (Detail Page)`
- PRD-050 | `important` | Scoop should stream progressively to avoid blank waiting | `ai_prompting_context.md > 3.3 Scoop (Detail Page)`
- PRD-051 | `critical` | Concepts output bullets, 1-3 words, spoiler-free phrasing | `ai_prompting_context.md > 3.4 Concepts (Single-Show and Multi-Show)`
- PRD-052 | `important` | Multi-show concepts must represent shared commonality across inputs | `ai_prompting_context.md > 3.4 Concepts (Single-Show and Multi-Show)`
- PRD-053 | `detail` | Concepts prioritize specificity, diversity, and strongest-first ordering | `concept_system.md > 4. Generation Rules`
- PRD-054 | `important` | Concept selection uses 1+, cap 8, clears downstream | `concept_system.md > 5. Selection UX Rules`
- PRD-055 | `critical` | Concept recs cite selected concepts and real IDs | `concept_system.md > 6. Concepts → Recommendations Contract`
- PRD-056 | `important` | Output counts: concepts 8, Explore 5, Alchemy 6 | `discovery_quality_bar.md > 2. Surface-Specific Minimum Bars`
- PRD-057 | `detail` | Summaries stay persona-consistent and 1-2 sentences long | `ai_prompting_context.md > 4. Conversation Summarization`
- PRD-058 | `important` | Parse failures retry once then fallback with Search handoff | `ai_prompting_context.md > 5. Guardrails & Fallbacks`
- PRD-059 | `important` | Discovery quality gate requires non-negotiable real-show integrity | `discovery_quality_bar.md > 4. Scoring Rubric (Quick)`

##### Detail Page Experience Constraints
- PRD-060 | `detail` | First-15-seconds should show mood, facts, relationship controls | `detail_page_experience.md > 2. First-15-Seconds Experience`
- PRD-061 | `detail` | Preserve defined narrative section order on Detail page | `detail_page_experience.md > 3. Narrative Hierarchy (Section Intent)`
- PRD-062 | `important` | Keep status, rating, tags in toolbar controls | `detail_page_experience.md > 3.3 My Relationship Controls`
- PRD-063 | `detail` | Scoop toggle copy changes by state and freshness | `detail_page_experience.md > 3.4 Overview + Scoop`
- PRD-064 | `detail` | Handle critical states for unsaved/media/type concept absence | `detail_page_experience.md > 5. Critical States`

##### Infrastructure, Identity, and Execution Rider
- PRD-065 | `critical` | Runtime baseline must be Next.js latest stable | `showbiz_infra_rider_prd.md > 2. Benchmark Baseline (Current Round)`
- PRD-066 | `critical` | Persistence must use Supabase official client libraries | `showbiz_infra_rider_prd.md > 2. Benchmark Baseline (Current Round)`
- PRD-067 | `important` | Docker must remain optional; hosted path must work | `showbiz_infra_rider_prd.md > 2. Benchmark Baseline (Current Round)`
- PRD-068 | `critical` | Repo includes .env.example with required variable comments | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-069 | `critical` | .gitignore excludes env secrets except .env.example file | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-070 | `critical` | App runs from env configuration without source edits | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-071 | `critical` | Secrets never committed; elevated keys server-side only | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-072 | `important` | Provide start, test, namespace-reset developer scripts | `showbiz_infra_rider_prd.md > 3.2 One-command developer experience`
- PRD-073 | `critical` | Include deterministic schema evolution via migrations artifacts | `showbiz_infra_rider_prd.md > 3.3 Database evolution artifacts`
- PRD-074 | `critical` | Stable namespace isolates data and destructive operations | `showbiz_infra_rider_prd.md > 4.1 Build/run namespace (required)`
- PRD-075 | `critical` | All user-owned records include opaque stable user_id | `showbiz_infra_rider_prd.md > 4.2 User identity (required)`
- PRD-076 | `critical` | Effective data partition uses namespace_id plus user_id | `showbiz_infra_rider_prd.md > 4.3 Relationship between namespace and user`
- PRD-077 | `important` | Benchmark auth injection must be documented and gated | `showbiz_infra_rider_prd.md > 5.1 Auth is not required to be real`
- PRD-078 | `important` | OAuth migration should require no schema redesign later | `showbiz_infra_rider_prd.md > 5.2 Migration to real OAuth must be straightforward`
- PRD-079 | `critical` | Backend is source of truth; client cache disposable | `showbiz_infra_rider_prd.md > 6. Data Ownership & Local Storage`
- PRD-080 | `critical` | Destructive tests reset namespace without global teardown | `showbiz_infra_rider_prd.md > 7. Destructive Testing Rules`

Total: 80 requirements (30 critical, 40 important, 10 detail) across 6 functional areas

### 2. Coverage Table

| PRD-ID | Requirement | Severity | Coverage | Evidence | Gap |
| ------ | ----------- | -------- | -------- | -------- | --- |
| PRD-001 | Store canonical show data plus user overlay fields | critical | full | `Proposed Changes > 1. Database Schema & Setup (Supabase)` defines `shows`, `user_shows`, and `ai_scoop`. | |
| PRD-002 | Show user-overlaid version anywhere saved shows appear | critical | partial | `Goal Description` references user-curated libraries driving discovery. | Plan does not explicitly require overlay precedence across every surface. |
| PRD-003 | User edits must win against refreshed public metadata | critical | full | `user_shows` field timestamps are defined for conflict resolution and merge tests. | |
| PRD-004 | Support core statuses and hidden Next in model | important | partial | `user_shows.my_status` exists and Home groups statuses. | Allowed status values and hidden `Next` are not specified. |
| PRD-005 | Interested and Excited map to Later plus Interest | critical | partial | Home grouping includes `Excited` and `Interested`. | Mapping rule (`Later + Interest`) is not explicitly specified. |
| PRD-006 | Clearing status removes show and clears all My Data | critical | full | `Manual Verification > Destructive Testing` checks clearing status wipes explicit `user_shows` data. | |
| PRD-007 | My Interest applies only when status is Later | important | missing | none | No rule ties interest applicability to `Later` status only. |
| PRD-008 | Tags are free-form and power app-wide filtering | important | full | `user_shows.my_tags` plus `layout.tsx` dynamic tag/data filters. | |
| PRD-009 | Filters include tags, No tags, data, media toggle | important | partial | `layout.tsx` dynamic filters and Home media toggle are specified. | `No tags` behavior and full filter taxonomy are not specified. |
| PRD-010 | Tiles show in-collection and user-rating indicators | detail | partial | `Collection Home` includes tile badges/quick actions. | Required indicator semantics are not explicitly defined. |
| PRD-011 | Collection membership is defined by assigned My Status | critical | partial | Plan centers collection grouping on statuses. | Formal membership definition based on status presence is missing. |
| PRD-012 | Auto-save triggers include status, interest, rating, tags | critical | partial | Detail includes status/interest/tags/rating controls; manual core loop uses status/tag. | Trigger rules for unsaved shows are incomplete and not explicit. |
| PRD-013 | Default unspecific save sets Later plus Interested | critical | missing | none | Default save behavior is not defined. |
| PRD-014 | First save via rating defaults status to Done | important | missing | none | Rating-to-Done rule is not specified. |
| PRD-015 | Status removal shows confirmation with optional suppression | important | partial | Destructive testing covers status clearing. | Confirmation UX and “stop asking” suppression rule are missing. |
| PRD-016 | Re-adding preserves My Data and refreshes public metadata | important | missing | none | Re-add behavior and merge expectation are not covered. |
| PRD-017 | Track per-field update timestamps for My Data | critical | full | `user_shows` includes per-field update timestamps; merge tests target timestamp resolution. | |
| PRD-018 | Persist Scoop with freshness and saved-show constraint | important | partial | `ai_scoop` persisted and Scoop streaming is planned. | 4-hour freshness and “persist only when in collection” are missing. |
| PRD-019 | Keep Ask history and mentions as session-only data | important | partial | `User Review Required` proposes transient Zustand chat/alchemy state. | Session-only lifecycle/clear-on-leave rules are not explicit. |
| PRD-020 | Map AI recs to real shows by ID/title | critical | partial | AI plan includes mention format and real catalog lookups. | Deterministic ID-first then case-insensitive title-match flow is absent. |
| PRD-021 | Fallback unresolved recommendations to non-interactive or Search | important | missing | none | Unresolved mapping fallback behavior is not defined. |
| PRD-022 | Resolve sync conflicts per field via newest timestamp | critical | full | Merge tests explicitly verify `my*` timestamp precedence on refresh. | |
| PRD-023 | Detect and merge duplicates transparently during sync | important | missing | none | Duplicate-detection and transparent merge behavior are not addressed. |
| PRD-024 | Preserve libraries across data-model version upgrades | critical | missing | none | No migration continuity strategy for existing user data is defined. |
| PRD-025 | App layout includes filters panel and main content | important | full | `layout.tsx` defines sidebar navigation/filtering and main content shell. | |
| PRD-026 | Keep persistent global entry points for Find and Settings | important | partial | Sidebar links include Find modes; Settings route is listed. | Persistent Settings entry from primary nav is not explicitly guaranteed. |
| PRD-027 | Find hub supports Search, Ask, Alchemy mode switching | important | partial | Separate routes exist for Search, Ask, Alchemy. | No explicit in-app mode switcher/hub behavior is defined. |
| PRD-028 | Home groups by Active, Excited, Interested, Other statuses | important | full | `page.tsx (Collection Home)` lists those exact groups. | |
| PRD-029 | Home supports media toggle and required empty states | important | partial | Media toggle is specified in Collection Home. | Empty-state behaviors/copy are not specified. |
| PRD-030 | Search provides live grid with in-collection markers | important | full | `search/page.tsx` covers live search, grid results, collection markers. | |
| PRD-031 | Search can auto-open when Search-on-Launch enabled | detail | missing | none | Search-on-launch setting and launch behavior are omitted. |
| PRD-032 | Ask displays chat turns and mentioned-show carousel | important | full | `ask/page.tsx` specifies chat UI and dynamic mentioned-shows carousel. | |
| PRD-033 | Ask welcome shows six random refreshable prompts | detail | partial | Ask page includes starter prompts. | Required count (6), randomness, and refresh action are not specified. |
| PRD-034 | Ask summarizes older turns after roughly ten messages | important | full | AI Services explicitly mention summarizing older turns. | |
| PRD-035 | Ask-about-show must seed conversation with show context | important | missing | none | Show-detail-to-Ask context seeding is not included. |
| PRD-036 | Alchemy flow supports 2+ inputs through chaining | critical | partial | Alchemy wizard includes 2+ input selection and chain button. | Selection cap/contract details are missing. |
| PRD-037 | Alchemy backtracking clears concepts and recommendation results | important | missing | none | Backtracking invalidation behavior is not defined. |
| PRD-038 | Show Detail includes full discovery and metadata sections | critical | partial | Plan covers header, status/interest/tags/rating bar, Scoop, Explore Similar. | Multiple required sections are absent (Ask CTA, providers, cast/crew, seasons, budget/revenue, recommendation strand details). |
| PRD-039 | Person Detail supports bio, analytics, filmography, linkbacks | important | missing | none | Person detail route/feature is not planned. |
| PRD-040 | Settings include font size and Search-on-Launch controls | detail | missing | none | Neither font-size nor search-on-launch settings are planned. |
| PRD-041 | Settings include username, AI model, catalog key controls | important | partial | Settings includes API key form and provider key mention. | Username and explicit AI model selection/sync behavior are not defined. |
| PRD-042 | Export produces zipped JSON backup with ISO timestamps | important | partial | Settings includes Export Data button producing ZIP of JSON. | ISO-8601 date encoding requirement is not specified. |
| PRD-043 | Restrict all AI responses to TV/movie domain only | important | partial | Product scope and AI surfaces are TV/movie focused throughout plan. | No explicit out-of-domain redirection rule is specified. |
| PRD-044 | Default AI behavior is spoiler-safe unless explicitly requested | critical | missing | none | Spoiler policy is not defined for Ask/Scoop/Alchemy outputs. |
| PRD-045 | AI reasoning should be honest, specific, non-generic | important | missing | none | Voice quality constraints are not captured as requirements or tests. |
| PRD-046 | Keep one persona across AI; Search has none | important | missing | none | Persona consistency and Search non-AI voice guardrail are missing. |
| PRD-047 | Ask responses are dialog-first with list formatting for recs | important | partial | Ask is described as conversational discovery. | Dialog/list formatting behavior is not explicitly required. |
| PRD-048 | Ask mentions output strict commentary plus showList contract | critical | partial | Plan includes `Title::externalId::mediaType` mention format. | Required structured object keys (`commentary`, `showList`) and parser contract are missing. |
| PRD-049 | Scoop must include required sections and balanced structure | important | partial | Scoop described as streamed opinionated mini blog-post. | Required section composition (take/stack-up/centerpiece/fit/verdict) is not specified. |
| PRD-050 | Scoop should stream progressively to avoid blank waiting | important | full | `show/[id]/page.tsx` includes streaming Scoop container; manual test verifies streaming behavior. | |
| PRD-051 | Concepts output bullets, 1-3 words, spoiler-free phrasing | critical | partial | AI services specify 1-3 word bulleted concept extraction. | Explicit spoiler-free concept constraint is missing. |
| PRD-052 | Multi-show concepts must represent shared commonality across inputs | important | partial | Multi-show concept extraction is planned in AI services. | “Shared across all inputs” requirement is not explicit. |
| PRD-053 | Concepts prioritize specificity, diversity, and strongest-first ordering | detail | missing | none | Quality constraints for concept ordering/diversity are absent. |
| PRD-054 | Concept selection uses 1+, cap 8, clears downstream | important | partial | Alchemy concept chips and selection step are defined. | Minimum selection, cap of 8, and downstream reset rules are incomplete. |
| PRD-055 | Concept recs cite selected concepts and real IDs | critical | full | AI recs are concept-grounded with real catalog lookups; manual AI verification checks tailored reasons. | |
| PRD-056 | Output counts: concepts 8, Explore 5, Alchemy 6 | important | partial | Alchemy step specifies 6 recommendations. | Explore Similar count of 5 and default concept count of 8 are missing. |
| PRD-057 | Summaries stay persona-consistent and 1-2 sentences long | detail | partial | Plan mentions summarizing older chat turns. | Summary length and persona-preservation constraints are not defined. |
| PRD-058 | Parse failures retry once then fallback with Search handoff | important | missing | none | Structured-output failure handling contract is not covered. |
| PRD-059 | Discovery quality gate requires non-negotiable real-show integrity | important | missing | none | No quality rubric or pass/fail gates are included. |
| PRD-060 | First-15-seconds should show mood, facts, relationship controls | detail | partial | Detail page includes cinematic header and sticky relationship controls. | Early visibility of quick facts/ratings orientation is not explicit. |
| PRD-061 | Preserve defined narrative section order on Detail page | detail | missing | none | Section order contract is not documented. |
| PRD-062 | Keep status, rating, tags in toolbar controls | important | full | Detail page specifies sticky/floating action bar for status/interest/tags/rating. | |
| PRD-063 | Scoop toggle copy changes by state and freshness | detail | missing | none | Toggle copy-state behavior and freshness copy transitions are missing. |
| PRD-064 | Handle critical states for unsaved/media/type concept absence | detail | missing | none | Critical-state behaviors are not specified. |
| PRD-065 | Runtime baseline must be Next.js latest stable | critical | full | `Proposed Architecture & Stack` sets Next.js 14+ App Router. | |
| PRD-066 | Persistence must use Supabase official client libraries | critical | full | Plan specifies Supabase PostgreSQL + Supabase JS client. | |
| PRD-067 | Docker must remain optional; hosted path must work | important | missing | none | Docker-optional/cloud-agent compatibility is not addressed. |
| PRD-068 | Repo includes .env.example with required variable comments | critical | partial | `Verification Plan > Environment Setup` includes creating `.env.example`. | Required variable inventory and inline comments are not specified. |
| PRD-069 | .gitignore excludes env secrets except .env.example file | critical | missing | none | `.gitignore` credential-exclusion requirement is not addressed. |
| PRD-070 | App runs from env configuration without source edits | critical | full | Environment setup test explicitly verifies `npm run dev` using env vars only. | |
| PRD-071 | Secrets never committed; elevated keys server-side only | critical | missing | none | Secret handling and client/server key-boundary rules are omitted. |
| PRD-072 | Provide start, test, namespace-reset developer scripts | important | partial | Plan references `npm run dev`, unit tests, and namespace test scenarios. | Explicit namespace-reset script deliverable is not defined. |
| PRD-073 | Include deterministic schema evolution via migrations artifacts | critical | full | Plan calls for migrations creating core tables. | |
| PRD-074 | Stable namespace isolates data and destructive operations | critical | full | Schema partitioning by `namespace_id` and namespace isolation verification steps are explicit. | |
| PRD-075 | All user-owned records include opaque stable user_id | critical | full | `user_shows` and `user_settings` include `user_id`; dev selector can switch users. | |
| PRD-076 | Effective data partition uses namespace_id plus user_id | critical | full | `user_shows` primary key is `(namespace_id, user_id, show_id)`. | |
| PRD-077 | Benchmark auth injection must be documented and gated | important | partial | Layout includes dev tools dropdown for namespace/user switching. | Documentation and production gating behavior are not specified. |
| PRD-078 | OAuth migration should require no schema redesign later | important | missing | none | Migration strategy to real OAuth is not discussed. |
| PRD-079 | Backend is source of truth; client cache disposable | critical | partial | Goal mentions user isolation and disposable local caches with Supabase backend. | Source-of-truth invariants and cache disposal guarantees are not explicit. |
| PRD-080 | Destructive tests reset namespace without global teardown | critical | partial | Plan includes destructive tests and namespace-isolation checks. | Concrete namespace-reset mechanism without global teardown is not specified. |

### 3. Coverage Scores

score = (full_count × 1.0 + partial_count × 0.5) / total_count × 100

Critical:  (13 × 1.0 + 12 × 0.5) / 30 × 100 = 63.3%  (19.0 of 30 critical requirements)
Important: (8 × 1.0 + 18 × 0.5) / 40 × 100 = 42.5%  (17.0 of 40 important requirements)
Detail:    (0 × 1.0 + 4 × 0.5) / 10 × 100 = 20.0%  (2.0 of 10 detail requirements)
Overall:   47.5% (80 total requirements)

### 4. Top Gaps

1. PRD-071 (`critical`) — Secrets never committed; elevated keys server-side only  
   This is a hard security and benchmark-compliance requirement; without it, credential exposure and invalid deployment architecture are likely.

2. PRD-044 (`critical`) — Default AI behavior is spoiler-safe unless explicitly requested  
   Missing this breaks a core product promise and causes immediate trust damage in first-use recommendation and Scoop flows.

3. PRD-013 (`critical`) — Default unspecific save sets Later plus Interested  
   Without deterministic save defaults, collection state will be inconsistent and user actions (tag/rate/save) will produce unpredictable outcomes.

4. PRD-024 (`critical`) — Preserve libraries across data-model version upgrades  
   The plan lacks migration continuity safeguards, creating high risk of user data loss during schema evolution.

5. PRD-069 (`critical`) — .gitignore excludes env secrets except .env.example file  
   This is required repo hygiene for benchmark runs; omission materially increases accidental secret-commit risk.

### 5. Coverage Narrative

This plan is structurally sound at a high level, but it is not implementation-ready against the full PRD surface. The overall score (47.5%) and especially the important/detail tier scores indicate that major behavioral contracts are either implied or omitted. The current plan can bootstrap architecture and major routes, but it does not yet specify enough deterministic behavior for parity-focused delivery.

Coverage is strongest in core platform scaffolding and broad feature skeletons: stack selection (Next.js + Supabase), namespace/user partitioning, migrations, home/search/ask/alchemy routing, and foundational AI integration entry points. The plan also captures several high-value mechanics such as timestamp-based merge testing, streaming Scoop behavior, and concept-grounded recommendation lookup intent.

Gaps cluster in three areas rather than being random: lifecycle business rules (auto-save defaults, re-add semantics, session-only AI persistence, upgrade continuity), AI behavioral contracts (spoiler policy, strict mention schema, fallback contracts, voice/persona guarantees, quality gates), and infra compliance hygiene (secret handling, `.gitignore`, Docker/cloud-agent requirements, auth migration path). This pattern shows strong architectural direction but weak behavioral specificity.

If executed as-is, the most likely failure mode is a product that looks complete in UI routes but fails acceptance during QA on deterministic behavior and benchmark compliance. A reviewer would likely notice first that key interaction outcomes are ambiguous (for example, save defaults and removal semantics), AI outputs are not constrained enough for reliable mapping/tone safety, and repo/security requirements are incompletely codified.

Remediation work should focus on plan precision, not broad scope expansion: add explicit acceptance criteria for all lifecycle rules, define AI contracts at parser/format/fallback level, and add an infra-compliance section with concrete secret/key boundaries, `.env`/`.gitignore` deliverables, Docker optionality, and namespace-reset mechanics. In parallel, expand the feature plan to include missing pages and settings contracts (Person Detail, search-on-launch/font-size, detail-page state/ordering rules) so execution teams can implement without interpretation drift.
