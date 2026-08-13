### 1. Requirements Extraction

#### Pass 1: Identify Functional Areas

- Infrastructure & Execution Boundaries
- Data Persistence & Merge Integrity
- Collection Model, Filters & Navigation
- Search Discovery
- Ask Conversational Discovery
- Concept System, Explore Similar & Alchemy
- Show Detail Experience
- Person Detail Experience
- Settings, Keys & Data Portability
- AI Voice, Guardrails & Discovery Quality

#### Pass 2: Extract Requirements Within Each Area

#### Infrastructure & Execution Boundaries

- PRD-001 | `critical` | Use Next.js runtime and Supabase persistence baseline | `showbiz_infra_rider_prd.md > 2. Benchmark Baseline (Current Round)`
- PRD-002 | `critical` | Provide env interface and strict secret-handling rules | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-003 | `critical` | Ship start, test, and namespace reset command workflow | `showbiz_infra_rider_prd.md > 3.2 One-command developer experience`
- PRD-004 | `critical` | Include deterministic schema evolution via repeatable migrations | `showbiz_infra_rider_prd.md > 3.3 Database evolution artifacts`
- PRD-005 | `critical` | Enforce stable namespace isolation and scoped destructive operations | `showbiz_infra_rider_prd.md > 4.1 Build/run namespace (required)`
- PRD-006 | `critical` | Associate all user-owned records with stable user_id | `showbiz_infra_rider_prd.md > 4.2 User identity (required)`
- PRD-007 | `critical` | Keep backend as source of truth; cache disposable | `showbiz_infra_rider_prd.md > 6. Data Ownership & Local Storage`
- PRD-008 | `important` | Keep migration path to OAuth without schema redesign | `showbiz_infra_rider_prd.md > 5.2 Migration to real OAuth must be straightforward`
- PRD-009 | `important` | Support cloud-agent runs without requiring Docker | `showbiz_infra_rider_prd.md > 8. Cloud Agent Compatibility`

#### Data Persistence & Merge Integrity

- PRD-010 | `critical` | Auto-save on status, interest, rating, and first tag | `showbiz_prd.md > 5.2 Saving Triggers`
- PRD-011 | `important` | Default new saves to Later with Interested interest | `showbiz_prd.md > 5.3 Default Values When Saving`
- PRD-012 | `important` | First save by rating defaults status to Done | `showbiz_prd.md > 5.3 Default Values When Saving`
- PRD-013 | `important` | Clearing status removes show and all My Data | `showbiz_prd.md > 5.4 Removing from Collection`
- PRD-014 | `critical` | Merge external/local via timestamp and non-empty rules | `showbiz_prd.md > 5.5 Re-adding the Same Show`
- PRD-015 | `important` | Track per-field update timestamps for user-owned data | `showbiz_prd.md > 5.6 Timestamps`
- PRD-016 | `important` | Persist Scoop conditionally; Ask/Alchemy data is session-only | `showbiz_prd.md > 5.7 AI Data Persistence`
- PRD-017 | `critical` | Map AI recommendations to real selectable catalog shows | `showbiz_prd.md > 5.8 AI Recommendations Map to Real Shows`
- PRD-018 | `critical` | Preserve user libraries safely across data model upgrades | `showbiz_prd.md > 5.11 Data Continuity Across Versions`

#### Collection Model, Filters & Navigation

- PRD-019 | `important` | Support all/tag/no-tag/data filters plus media toggle | `showbiz_prd.md > 4.5 Filters (Ways to View the Collection)`
- PRD-020 | `important` | Use split app shell with persistent Find and Settings | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-021 | `important` | Provide Search, Ask, Alchemy with explicit mode switching | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-022 | `important` | Group Home by status with Active visually prominent | `showbiz_prd.md > 7.1 Collection Home`
- PRD-023 | `detail` | Define explicit empty states for collection and filters | `showbiz_prd.md > 7.1 Collection Home`

#### Search Discovery

- PRD-024 | `important` | Search by text in poster grid with collection markers | `showbiz_prd.md > 7.2 Search (Find → Search)`
- PRD-025 | `detail` | Respect user Search-on-Launch preference from settings | `showbiz_prd.md > 7.2 Search (Find → Search)`

#### Ask Conversational Discovery

- PRD-026 | `important` | Ask supports mentions row and detail/search handoff | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-027 | `detail` | Show six random starter prompts with refresh option | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-028 | `important` | Summarize older chat turns after ~10 messages | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-029 | `important` | Ask-about-show mode must seed the show context | `showbiz_prd.md > 7.3 Ask (Find → Ask)`

#### Concept System, Explore Similar & Alchemy

- PRD-030 | `important` | Generate bullet-only 1-3 word evocative concept outputs | `supporting_docs/concept_system.md > 4. Generation Rules`
- PRD-031 | `important` | Enforce concept selection caps and clear downstream state | `supporting_docs/concept_system.md > 5. Selection UX Rules`
- PRD-032 | `important` | Return 5/6 rec counts with concept-grounded reasons | `supporting_docs/concept_system.md > 6. Concepts → Recommendations Contract`

#### Show Detail Experience

- PRD-033 | `important` | Preserve detail-page narrative hierarchy and core sections | `supporting_docs/detail_page_experience.md > 3. Narrative Hierarchy (Section Intent)`
- PRD-034 | `critical` | Keep toolbar My Data controls with removal confirmation | `supporting_docs/detail_page_experience.md > 3.3 My Relationship Controls`

#### Person Detail Experience

- PRD-035 | `important` | Include person gallery, analytics, yearly credits navigation | `showbiz_prd.md > 7.6 Person Detail Page`

#### Settings, Keys & Data Portability

- PRD-036 | `important` | Provide settings, key handling, and zip JSON export | `showbiz_prd.md > 7.7 Settings & Your Data`

#### AI Voice, Guardrails & Discovery Quality

- PRD-037 | `important` | Maintain unified AI persona with spoiler-safe constraints | `supporting_docs/ai_voice_personality.md > 1. Persona Summary`
- PRD-038 | `important` | Meet discovery quality bar and real-show integrity standards | `supporting_docs/discovery_quality_bar.md > 1. Quality Dimensions`

Total: 38 requirements (12 critical, 23 important, 3 detail) across 10 functional areas

### 2. Coverage Table

| PRD-ID | Requirement | Severity | Coverage | Evidence | Gap |
| ------ | ----------- | -------- | -------- | -------- | --- |
| PRD-001 | Use Next.js runtime and Supabase persistence baseline | critical | full | `IMPLEMENTATION_PLAN.md > 1. Infrastructure & Setup` ("Stack: Next.js ... + Supabase") |  |
| PRD-002 | Provide env interface and strict secret-handling rules | critical | partial | `IMPLEMENTATION_PLAN.md > 1. Infrastructure & Setup` (".env.example with required variables") | No explicit `.gitignore` secret rule or server-only elevated-key handling. |
| PRD-003 | Ship start, test, and namespace reset command workflow | critical | full | `IMPLEMENTATION_PLAN.md > 1. Infrastructure & Setup` ("npm run dev", "npm test", "npm run test:reset") |  |
| PRD-004 | Include deterministic schema evolution via repeatable migrations | critical | full | `IMPLEMENTATION_PLAN.md > 2. Database & Data Models` ("Create Supabase migrations") |  |
| PRD-005 | Enforce stable namespace isolation and scoped destructive operations | critical | partial | `IMPLEMENTATION_PLAN.md > 1. Infrastructure & Setup` ("inject namespace_id and user_id into ... destructive actions") | Stable namespace lifecycle and explicit test-reset scoping semantics are not fully specified. |
| PRD-006 | Associate all user-owned records with stable user_id | critical | partial | `IMPLEMENTATION_PLAN.md > 1. Infrastructure & Setup` ("inject ... user_id into all database queries") | Query-time injection is covered, but record-level ownership guarantees are not explicit in data model tasks. |
| PRD-007 | Keep backend as source of truth; cache disposable | critical | missing | none | Plan never states backend-truth/cached-disposable constraints or local-storage safety behavior. |
| PRD-008 | Keep migration path to OAuth without schema redesign | important | missing | none | No forward-compatibility plan for replacing dev identity with OAuth. |
| PRD-009 | Support cloud-agent runs without requiring Docker | important | missing | none | Docker-optional/cloud-agent compatibility requirements are not addressed. |
| PRD-010 | Auto-save on status, interest, rating, and first tag | critical | partial | `IMPLEMENTATION_PLAN.md > 4. Core Features` ("My Data Controls: Auto-save behavior") | Auto-save is mentioned, but explicit trigger completeness (status, interest chip, first tag) is incomplete. |
| PRD-011 | Default new saves to Later with Interested interest | important | missing | none | Default save behavior for unsaved shows is not defined. |
| PRD-012 | First save by rating defaults status to Done | important | full | `IMPLEMENTATION_PLAN.md > 4. Core Features` ("rating an unsaved show saves it as Done") |  |
| PRD-013 | Clearing status removes show and all My Data | important | missing | none | Removal semantics and My Data clearing are not planned explicitly. |
| PRD-014 | Merge external/local via timestamp and non-empty rules | critical | partial | `IMPLEMENTATION_PLAN.md > 2. Database & Data Models` ("timestamp resolution ... selectFirstNonEmpty") | Merge intent exists, but full field set and conflict edge cases are unspecified. |
| PRD-015 | Track per-field update timestamps for user-owned data | important | missing | none | Required timestamp fields and their usage are absent from task-level plan details. |
| PRD-016 | Persist Scoop conditionally; Ask/Alchemy data is session-only | important | partial | `IMPLEMENTATION_PLAN.md > 5. AI Discovery & Personality` ("Scoop ... cached for 4 hours") | Session-only lifecycle for Ask/Alchemy artifacts and conditional Scoop persistence are not explicit. |
| PRD-017 | Map AI recommendations to real selectable catalog shows | critical | partial | `IMPLEMENTATION_PLAN.md > 5. AI Discovery & Personality` ("recommendations mapped to real catalog IDs") | Mapping fallback behavior and deterministic matching rules are not specified. |
| PRD-018 | Preserve user libraries safely across data model upgrades | critical | missing | none | No migration/upgrade continuity strategy is included. |
| PRD-019 | Support all/tag/no-tag/data filters plus media toggle | important | partial | `IMPLEMENTATION_PLAN.md > 3. Architecture & UI Shell` (All Shows, tag filters, data filters, media-type toggle) | No-tag filter condition and concrete data-filter dimensions are not called out. |
| PRD-020 | Use split app shell with persistent Find and Settings | important | full | `IMPLEMENTATION_PLAN.md > 3. Architecture & UI Shell` (Sidebar routes include Find and Settings) |  |
| PRD-021 | Provide Search, Ask, Alchemy with explicit mode switching | important | partial | `IMPLEMENTATION_PLAN.md > 3. Architecture & UI Shell` (Find links to Search/Ask/Alchemy) | Mode-switcher interaction is implied but not concretely specified. |
| PRD-022 | Group Home by status with Active visually prominent | important | full | `IMPLEMENTATION_PLAN.md > 4. Core Features` ("Group by Status: Active (prominent)...") |  |
| PRD-023 | Define explicit empty states for collection and filters | detail | missing | none | Empty-state requirements for no-library and no-results cases are absent. |
| PRD-024 | Search by text in poster grid with collection markers | important | partial | `IMPLEMENTATION_PLAN.md > 4. Core Features` ("Text search ... indicate in-collection items") | Poster-grid presentation and some UX behavior details are not explicit. |
| PRD-025 | Respect user Search-on-Launch preference from settings | detail | partial | `IMPLEMENTATION_PLAN.md > 6. Settings & Data Export` ("auto-search") | Setting exists, but propagation to Search launch behavior is not clearly connected. |
| PRD-026 | Ask supports mentions row and detail/search handoff | important | partial | `IMPLEMENTATION_PLAN.md > 5. AI Discovery & Personality` ("Parses mentioned shows into interactive UI strips") | Mapping failure behavior and explicit handoff paths are not specified. |
| PRD-027 | Show six random starter prompts with refresh option | detail | missing | none | Ask welcome prompt experience is not planned. |
| PRD-028 | Summarize older chat turns after ~10 messages | important | partial | `IMPLEMENTATION_PLAN.md > 5. AI Discovery & Personality` ("Summarizes context after ~10 turns") | Persona-preserving summarization contract is not captured. |
| PRD-029 | Ask-about-show mode must seed the show context | important | missing | none | No task/section covers Ask entry from Show Detail with pre-seeded context. |
| PRD-030 | Generate bullet-only 1-3 word evocative concept outputs | important | partial | `IMPLEMENTATION_PLAN.md > 5. AI Discovery & Personality` ("Extract short, evocative concepts (1-3 words)") | Bullet-only formatting, anti-generic constraints, and spoiler guardrails are not explicit. |
| PRD-031 | Enforce concept selection caps and clear downstream state | important | missing | none | Selection-cap and state-reset UX rules are not represented in plan tasks. |
| PRD-032 | Return 5/6 rec counts with concept-grounded reasons | important | partial | `IMPLEMENTATION_PLAN.md > 5. AI Discovery & Personality` ("fetch actionable recommendations mapped to real catalog IDs") | Fixed rec counts and reason-level concept grounding are not specified. |
| PRD-033 | Preserve detail-page narrative hierarchy and core sections | important | partial | `IMPLEMENTATION_PLAN.md > 4. Core Features` ("Narrative Hierarchy ...") | Hierarchy is present but key requirements (e.g., Ask CTA and exact section intent) are incomplete. |
| PRD-034 | Keep toolbar My Data controls with removal confirmation | critical | partial | `IMPLEMENTATION_PLAN.md > 4. Core Features` ("My Data Controls ... auto-save") | Toolbar placement and destructive reselect-confirmation behavior are not defined. |
| PRD-035 | Include person gallery, analytics, yearly credits navigation | important | partial | `IMPLEMENTATION_PLAN.md > 4. Core Features` ("Bio, image gallery, analytics charts, and filmography grouped by year") | Credit-to-show navigation behavior is not explicitly included. |
| PRD-036 | Provide settings, key handling, and zip JSON export | important | partial | `IMPLEMENTATION_PLAN.md > 6. Settings & Data Export` | Export exists, but ISO date requirement, model setting, and key-handling constraints are not complete. |
| PRD-037 | Maintain unified AI persona with spoiler-safe constraints | important | partial | `IMPLEMENTATION_PLAN.md > 5. AI Discovery & Personality` ("fun, chatty ... spoiler-safe, opinionated") | Cross-surface consistency and full guardrail set are not codified as acceptance criteria. |
| PRD-038 | Meet discovery quality bar and real-show integrity standards | important | missing | none | No quality rubric or validation gate is planned for discovery outputs. |

### 3. Coverage Scores

score = (full_count × 1.0 + partial_count × 0.5) / total_count × 100

- full_count = 6
- partial_count = 20
- total_count = 38

Overall score = (6 × 1.0 + 20 × 0.5) / 38 × 100 = 42.1%

Critical:  (full × 1.0 + partial × 0.5) / critical_total × 100 = (3 × 1.0 + 7 × 0.5) / 12 × 100 = 54.2%  (6.5 of 12 critical requirements)
Important: (full × 1.0 + partial × 0.5) / important_total × 100 = (3 × 1.0 + 12 × 0.5) / 23 × 100 = 39.1%  (9.0 of 23 important requirements)
Detail:    (full × 1.0 + partial × 0.5) / detail_total × 100 = (0 × 1.0 + 1 × 0.5) / 3 × 100 = 16.7%  (0.5 of 3 detail requirements)
Overall:   42.1% (38 total requirements)

### 4. Top Gaps

- **PRD-007 (`critical`) — Keep backend as source of truth; cache disposable.**  
  This gap matters because correctness can silently depend on local cache behavior, causing data loss or inconsistency after storage clears, reinstalls, or multi-device usage.

- **PRD-018 (`critical`) — Preserve user libraries safely across data model upgrades.**  
  This gap matters because schema evolution can break or drop saved statuses/tags/ratings, which is a direct trust failure for the product’s core promise.

- **PRD-005 (`critical`) — Enforce stable namespace isolation and scoped destructive operations.**  
  This gap matters because benchmark/test runs can collide or delete unrelated data if namespace lifecycle and reset boundaries are not explicitly designed.

- **PRD-010 (`critical`) — Auto-save on status, interest, rating, and first tag.**  
  This gap matters because incomplete auto-save triggers create inconsistent collection membership and surprising behavior across equivalent user actions.

- **PRD-017 (`critical`) — Map AI recommendations to real selectable catalog shows.**  
  This gap matters because discovery becomes non-actionable if recommendations are not reliably resolvable, producing dead-end UI interactions.

### 5. Coverage Narrative

The plan is structurally coherent but under-specified against the PRD’s behavioral contract. It captures major feature surfaces and some critical technical foundations, yet it does not achieve execution-grade completeness for many required rules. At 42.1% weighted coverage, this is better described as a high-level implementation outline than a fully benchmark-ready delivery plan.

Coverage is strongest in macro architecture and core product surfaces: the stack baseline, migration intent, app shell, Home grouping, Search presence, and headline AI features are all present. The plan also demonstrates awareness of key product mechanics such as merge logic, AI Scoop caching, and the major discovery modes (Search, Ask, Alchemy, Explore Similar), which indicates broad functional alignment with the PRD.

Gaps cluster around operational guarantees and precise behavior specs. The largest concentration is in cross-cutting requirements: backend-source-of-truth constraints, namespace/isolation rigor, upgrade continuity, deterministic AI-to-catalog mapping behavior, and quality-bar enforcement. A second cluster appears in UX micro-contracts that are testable but omitted: empty states, Ask starter prompts, Ask-about-show handoff, concept selection caps/state clearing, and explicit fixed recommendation counts.

If executed as-is, the most likely failure mode is that the app “looks complete” in happy-path demos but fails acceptance under benchmark and QA conditions. Reviewers would likely notice first that AI discovery results are inconsistently actionable, state behavior differs between entry points, and data integrity/isolation expectations are insufficiently defended during repeat test runs or schema changes.

Remediation should focus less on adding net-new feature sections and more on raising specificity. The plan needs explicit acceptance criteria for cross-cutting data guarantees, identity/isolation boundaries, and AI behavioral contracts. It also needs a dedicated validation section that ties feature tasks to measurable UX/output requirements (counts, formats, fallbacks, and state transitions), so implementation can be verified rather than inferred.
