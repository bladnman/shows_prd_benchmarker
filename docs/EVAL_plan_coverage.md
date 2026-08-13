### 1. Requirements Extraction

#### Pass 1: Identify Functional Areas
1. Infrastructure & Execution Compliance
2. Identity, Isolation, and Authentication
3. Persistence Model, Mapping, and Merge Semantics
4. Collection Lifecycle and My Data Rules
5. Navigation, Home, and Search
6. Ask Conversational Discovery
7. Show Detail and Person Detail Experience
8. Concepts, Explore Similar, and Alchemy
9. Settings, Sync, and Data Portability
10. AI Voice and Prompting Contracts
11. Discovery Quality Assurance

#### Pass 2: Extract Requirements Within Each Area

**Infrastructure & Execution Compliance**
- PRD-001 | `critical` | Next.js latest stable runtime is required benchmark baseline | `showbiz_infra_rider_prd.md > 2. Benchmark Baseline (Current Round)`
- PRD-002 | `critical` | Supabase persistence via official clients is required benchmark baseline | `showbiz_infra_rider_prd.md > 2. Benchmark Baseline (Current Round)`
- PRD-003 | `important` | Docker-free execution with hosted-first path and optional local support | `showbiz_infra_rider_prd.md > 2. Benchmark Baseline (Current Round)`
- PRD-004 | `important` | Provide .env.example listing required variables with brief comments | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-005 | `important` | Exclude .env secrets in .gitignore except .env.example | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-006 | `critical` | Build config works via env vars without code edits | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-007 | `critical` | Keep secrets out of repo; elevated keys server-only | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-008 | `critical` | Provide scripts to start app, test, and reset data | `showbiz_infra_rider_prd.md > 3.2 One-command developer experience`
- PRD-009 | `critical` | Maintain deterministic schema creation via repeatable migrations artifacts | `showbiz_infra_rider_prd.md > 3.3 Database evolution artifacts`

**Identity, Isolation, and Authentication**
- PRD-010 | `critical` | Assign one stable namespace identifier per build lifetime | `showbiz_infra_rider_prd.md > 4.1 Build/run namespace (required)`
- PRD-011 | `critical` | Prevent cross-namespace reads and writes of persisted data | `showbiz_infra_rider_prd.md > 4.1 Build/run namespace (required)`
- PRD-012 | `critical` | Scope destructive operations strictly to current namespace | `showbiz_infra_rider_prd.md > 4.1 Build/run namespace (required)`
- PRD-013 | `critical` | Attach user_id to all user-owned persisted records | `showbiz_infra_rider_prd.md > 4.2 User identity (required)`
- PRD-014 | `important` | Support multi-user behavior with opaque stable user identifiers | `showbiz_infra_rider_prd.md > 4.2 User identity (required)`
- PRD-015 | `important` | Partition records by combined namespace_id and user_id keys | `showbiz_infra_rider_prd.md > 4.3 Relationship between namespace and user`
- PRD-016 | `important` | Allow documented dev identity injection gated outside production | `showbiz_infra_rider_prd.md > 5.1 Auth is not required to be “real” in benchmark mode`
- PRD-017 | `critical` | Swap in OAuth later without schema redesign | `showbiz_infra_rider_prd.md > 5.2 Migration to real OAuth must be straightforward`
- PRD-018 | `critical` | Treat backend persistence as authoritative source of truth | `showbiz_infra_rider_prd.md > 6.1 Source of truth`
- PRD-019 | `important` | Ensure local cache can be cleared without data loss | `showbiz_infra_rider_prd.md > 6.2 Cache is disposable`
- PRD-020 | `critical` | Enable namespace-scoped destructive tests without global teardown | `showbiz_infra_rider_prd.md > 7. Destructive Testing Rules`

**Persistence Model, Mapping, and Merge Semantics**
- PRD-021 | `critical` | Persist show records with catalog, My Data, and Scoop fields | `storage-schema.md > Show (movie or TV series)`
- PRD-022 | `important` | Persist user/app settings including autoSearch fontSize aiModel | `storage-schema.md > CloudSettings (optional synced settings)`
- PRD-023 | `important` | Keep transient media/detail fields non-persisted and refetchable | `storage-schema.md > Show (movie or TV series)`
- PRD-024 | `important` | Map external catalog payloads into normalized Show fields | `storage-schema.md > External catalog → Show mapping strategy`
- PRD-025 | `critical` | Merge non-my by non-empty, my-fields by newer timestamps | `storage-schema.md > Merge / overwrite policy (important)`
- PRD-026 | `important` | Preserve creationDate; set detailsUpdateDate on each metadata merge | `storage-schema.md > Merge / overwrite policy (important)`
- PRD-027 | `important` | Merge duplicate synced items transparently across devices | `showbiz_prd.md > 5.10 Data Sync & Integrity`
- PRD-028 | `critical` | Preserve all user libraries and My Data across upgrades | `showbiz_prd.md > 5.11 Data Continuity Across Versions`

**Collection Lifecycle and My Data Rules**
- PRD-029 | `important` | Define collection membership by presence of My Status | `showbiz_prd.md > 5.1 Collection Membership`
- PRD-030 | `critical` | Auto-save on status, interest, first rating, first tag | `showbiz_prd.md > 5.2 Saving Triggers`
- PRD-031 | `important` | Default unspecific saves to Later+Interested; rating-save to Done | `showbiz_prd.md > 5.3 Default Values When Saving`
- PRD-032 | `critical` | Clearing status removes show and clears all My Data | `showbiz_prd.md > 5.4 Removing from Collection`
- PRD-033 | `important` | Show removal confirmation with optional future suppression | `showbiz_prd.md > 5.4 Removing from Collection`
- PRD-034 | `critical` | Re-adding show keeps latest My Data while refreshing catalog | `showbiz_prd.md > 5.5 Re-adding the Same Show`
- PRD-035 | `critical` | Track per-field update timestamps for status/interest/tags/score/scoop | `showbiz_prd.md > 5.6 Timestamps`
- PRD-036 | `important` | Persist Scoop with 4-hour freshness; other AI data session-only | `showbiz_prd.md > 5.7 AI Data Persistence`
- PRD-037 | `important` | Show in-collection and rating badges on tiles | `showbiz_prd.md > 5.9 Tile Indicators`
- PRD-038 | `critical` | Always display user-overlaid show version; user edits win | `showbiz_prd.md > 4.1 Show (Movie or TV)`

**Navigation, Home, and Search**
- PRD-039 | `important` | Provide layout with filters/navigation panel and main content | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-040 | `important` | Keep Find/Discover and Settings as persistent navigation entries | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-041 | `important` | Offer Search Ask Alchemy modes with clear mode switcher | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-042 | `important` | Group Home by Active/Excited/Interested/Other plus media toggle | `showbiz_prd.md > 7.1 Collection Home`
- PRD-043 | `important` | Support tag/data filters including no-tags and media overlay | `showbiz_prd.md > 4.5 Filters (Ways to View the Collection)`
- PRD-044 | `detail` | Provide empty states for empty library and empty results | `showbiz_prd.md > 7.1 Collection Home`
- PRD-045 | `critical` | Search by text with poster grid, badges, and detail open | `showbiz_prd.md > 7.2 Search (Find → Search)`
- PRD-046 | `detail` | Support optional Search-on-launch behavior from user settings | `showbiz_prd.md > 7.2 Search (Find → Search)`
- PRD-047 | `detail` | Keep Search surface straightforward with no AI persona voice | `ai_voice_personality.md > 1. Persona Summary`

**Ask Conversational Discovery**
- PRD-048 | `important` | Ask chat supports turns plus six refreshable starter prompts | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-049 | `critical` | Ask behavior stays spoiler-safe, honest, domain-limited, friendly | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-050 | `important` | Summarize older chat turns while preserving persona continuity | `ai_prompting_context.md > 4. Conversation Summarization (Chat Surfaces)`
- PRD-051 | `critical` | Emit Ask mentions as commentary plus exact showList format | `ai_prompting_context.md > 3.2 Ask with Mentions (Structured “Mentioned Shows”)`
- PRD-052 | `critical` | Resolve mentioned shows to catalog with fallback handoff behavior | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-053 | `important` | Seed Ask context when launched from “Ask about this show” | `showbiz_prd.md > 7.3 Ask (Find → Ask)`
- PRD-054 | `important` | On parser failure retry once then fallback to Search | `ai_prompting_context.md > 5. Guardrails & Fallbacks`
- PRD-055 | `detail` | Ask answers quickly and list multi-recs in bullet form | `discovery_quality_bar.md > 2.2 Ask / Explore Search Chat`

**Show Detail and Person Detail Experience**
- PRD-056 | `important` | Make Detail page single source for facts, My Data, discovery | `detail_page_experience.md > 1. Purpose`
- PRD-057 | `important` | Preserve required Detail section order and hierarchy | `detail_page_experience.md > 3. Narrative Hierarchy (Section Intent)`
- PRD-058 | `important` | Support media-rich header with graceful poster/backdrop/trailer fallback | `detail_page_experience.md > 3.1 Header Media`
- PRD-059 | `critical` | Use toolbar status chips mapping Interested/Excited to Later+Interest | `detail_page_experience.md > 3.3 My Relationship Controls`
- PRD-060 | `critical` | Auto-save via rating/tag actions with required default statuses | `detail_page_experience.md > 3.3 My Relationship Controls`
- PRD-061 | `important` | Include providers cast/crew seasons budget-revenue with media-conditional rules | `showbiz_prd.md > 7.5 Show Detail Page`
- PRD-062 | `important` | Implement Scoop toggle states, streaming feedback, freshness, persistence rule | `detail_page_experience.md > 3.4 Overview + Scoop`
- PRD-063 | `important` | Person detail includes gallery bio analytics and year-grouped credits | `showbiz_prd.md > 7.6 Person Detail Page`
- PRD-064 | `detail` | Handle critical states for unsaved, no concepts, missing media | `detail_page_experience.md > 5. Critical States`

**Concepts, Explore Similar, and Alchemy**
- PRD-065 | `critical` | Generate bullet-only 1-3 word spoiler-free concept ingredients | `concept_system.md > 4. Generation Rules`
- PRD-066 | `important` | Keep concepts specific, diverse across axes, and strength-ordered | `concept_system.md > 4. Generation Rules`
- PRD-067 | `important` | Explore Similar flow: get concepts, pick chips, explore shows | `showbiz_prd.md > 4.8 Explore Similar (Per-Show Concepts)`
- PRD-068 | `critical` | Alchemy flow supports 2+ inputs, cap-8 concepts, chaining | `showbiz_prd.md > 4.7 Alchemy Session`
- PRD-069 | `important` | Clear downstream concepts/results when inputs or selections change | `showbiz_prd.md > 7.4 Alchemy (Find → Alchemy)`
- PRD-070 | `critical` | Return 5 Explore Similar and 6 Alchemy recs with concept-linked reasons | `concept_system.md > 6. Concepts → Recommendations Contract`
- PRD-071 | `critical` | Resolve recommendations to real catalog items with valid identifiers | `showbiz_prd.md > 5.8 AI Recommendations Map to Real Shows`
- PRD-072 | `important` | Multi-show concepts are shared across inputs and broader pool | `concept_system.md > 8. Notes`

**Settings, Sync, and Data Portability**
- PRD-073 | `important` | Settings provide font size/readability and Search-on-launch controls | `showbiz_prd.md > 7.7 Settings & Your Data`
- PRD-074 | `important` | Settings cover username, provider/model keys, and secret-safety rules | `showbiz_prd.md > 7.7 Settings & Your Data`
- PRD-075 | `critical` | Export My Data as ZIP JSON with ISO-8601 dates | `showbiz_prd.md > 7.7 Settings & Your Data`

**AI Voice and Prompting Contracts**
- PRD-076 | `critical` | Keep one consistent AI persona across surfaces; none in Search | `ai_voice_personality.md > 1. Persona Summary`
- PRD-077 | `critical` | Enforce voice pillars: warm, honest, vibe-first, specific reasoning | `ai_voice_personality.md > 2. Non-Negotiable Voice Pillars`
- PRD-078 | `important` | Scoop output includes defined sections and target length range | `ai_voice_personality.md > 4.1 Scoop (Show Detail “The Scoop”)`
- PRD-079 | `detail` | Concept recs bias recent titles while allowing classics/hiddens | `ai_voice_personality.md > 4.5 Concept-Based Recs (Explore Similar / Alchemy results)`
- PRD-080 | `important` | Feed AI with library/My Data/show/concept context for taste-awareness | `ai_prompting_context.md > 2. Shared Inputs (Typical)`

**Discovery Quality Assurance**
- PRD-081 | `important` | Validate discovery quality across voice taste surprise specificity integrity | `discovery_quality_bar.md > 1. Quality Dimensions`
- PRD-082 | `important` | Enforce surface minimum bars including default eight concepts output | `discovery_quality_bar.md > 2. Surface-Specific Minimum Bars`
- PRD-083 | `detail` | Apply scoring threshold: Voice>=1 Taste>=1 Integrity=2 Total>=7 | `discovery_quality_bar.md > 4. Scoring Rubric (Quick)`

Total: 83 requirements (34 critical, 42 important, 7 detail) across 11 functional areas

### 2. Coverage Table

| PRD-ID | Requirement | Severity | Coverage | Evidence | Gap |
| ------ | ----------- | -------- | -------- | -------- | --- |
| PRD-001 | Next.js latest stable runtime is required benchmark baseline | critical | full | `1. Architecture & Tech Stack` lists Next.js. | |
| PRD-002 | Supabase persistence via official clients is required benchmark baseline | critical | full | `1. Architecture & Tech Stack` lists Supabase. | |
| PRD-003 | Docker-free execution with hosted-first path and optional local support | important | partial | `5. Critical Constraints` says “No Docker Required” and hosted Supabase path. | It does not explicitly document local Docker use as optional and documented. |
| PRD-004 | Provide .env.example listing required variables with brief comments | important | partial | `2. Infrastructure` mentions `.env.example` and required variables. | It omits the required short comments for each variable. |
| PRD-005 | Exclude .env secrets in .gitignore except .env.example | important | missing | none | No `.gitignore` handling for `.env*` is specified. |
| PRD-006 | Build config works via env vars without code edits | critical | partial | `2. Infrastructure` defines an environment-variable interface. | It does not state builds must run by env fill-in alone without source edits. |
| PRD-007 | Keep secrets out of repo; elevated keys server-only | critical | partial | `2. Infrastructure` names public and API keys. | It does not explicitly forbid committing secrets or restrict elevated keys to server-only usage. |
| PRD-008 | Provide scripts to start app, test, and reset data | critical | full | `2. Infrastructure` lists dev, test, and reset scripts. | |
| PRD-009 | Maintain deterministic schema creation via repeatable migrations artifacts | critical | partial | Phase 1 includes migrations for `shows` and `user_settings`. | Deterministic fresh-state recreation and repeatability expectations are not fully defined. |
| PRD-010 | Assign one stable namespace identifier per build lifetime | critical | full | `2. Infrastructure` and `5. Critical Constraints` require `namespace_id`. | |
| PRD-011 | Prevent cross-namespace reads and writes of persisted data | critical | full | Isolation model states every record is scoped by namespace. | |
| PRD-012 | Scope destructive operations strictly to current namespace | critical | full | Reset script clears namespace data and destructive testing is namespace-scoped. | |
| PRD-013 | Attach user_id to all user-owned persisted records | critical | full | Isolation model requires all records include `user_id`. | |
| PRD-014 | Support multi-user behavior with opaque stable user identifiers | important | partial | Plan includes user identity and dev identity injection. | Opaque ID semantics and explicit multi-user behavior expectations are not detailed. |
| PRD-015 | Partition records by combined namespace_id and user_id keys | important | full | `2. Infrastructure` scopes records to both identifiers. | |
| PRD-016 | Allow documented dev identity injection gated outside production | important | partial | Auth section proposes `X-User-Id` or dev selector injection. | It does not include documentation/gating requirements for production mode. |
| PRD-017 | Swap in OAuth later without schema redesign | critical | full | Auth section states transition to OAuth without schema changes. | |
| PRD-018 | Treat backend persistence as authoritative source of truth | critical | partial | Architecture centers Supabase as persistent backend. | The plan does not explicitly define backend-over-cache correctness rules. |
| PRD-019 | Ensure local cache can be cleared without data loss | important | missing | none | Disposable-cache behavior and safe local-storage clearing are not covered. |
| PRD-020 | Enable namespace-scoped destructive tests without global teardown | critical | full | Reset scripts and destructive-testing rule are namespace-scoped. | |
| PRD-021 | Persist show records with catalog, My Data, and Scoop fields | critical | partial | Data schema references `shows` and `storage-schema.ts`. | Required persistent fields and constraints are not concretely enumerated. |
| PRD-022 | Persist user/app settings including autoSearch fontSize aiModel | important | partial | Data schema includes `autoSearch`, `fontSize`, `aiModel`. | Full settings surface (username/version/provider keys) is underspecified. |
| PRD-023 | Keep transient media/detail fields non-persisted and refetchable | important | missing | none | The plan does not separate transient versus persisted show fields. |
| PRD-024 | Map external catalog payloads into normalized Show fields | important | partial | Phase 1 includes catalog wrapper mapping to local `Show`. | Detailed mapping rules (fallback title/type inference, providers, date parsing) are absent. |
| PRD-025 | Merge non-my by non-empty, my-fields by newer timestamps | critical | full | Merge policy explicitly states this behavior. | |
| PRD-026 | Preserve creationDate; set detailsUpdateDate on each metadata merge | important | missing | none | Creation/update timestamp management for catalog merges is not planned. |
| PRD-027 | Merge duplicate synced items transparently across devices | important | partial | Phase 7 includes data-sync validation on re-add. | Transparent duplicate detection/merge across devices is not concretely specified. |
| PRD-028 | Preserve all user libraries and My Data across upgrades | critical | missing | none | No migration/versioning strategy is included for schema evolution without data loss. |
| PRD-029 | Define collection membership by presence of My Status | important | partial | Home grouping and My Status controls are central in Phase 2. | The explicit membership definition tied to `myStatus` is not stated. |
| PRD-030 | Auto-save on status, interest, first rating, first tag | critical | partial | User overlay includes status/interest/rating/tag controls. | The full set of autosave triggers is not explicitly guaranteed. |
| PRD-031 | Default unspecific saves to Later+Interested; rating-save to Done | important | missing | none | Required default save outcomes are not documented. |
| PRD-032 | Clearing status removes show and clears all My Data | critical | partial | Status controls and data-sync handling are planned. | Full removal semantics (delete + clear all My Data fields) are not explicit. |
| PRD-033 | Show removal confirmation with optional future suppression | important | missing | none | Confirmation flow and suppression option are not included. |
| PRD-034 | Re-adding show keeps latest My Data while refreshing catalog | critical | partial | Phase 7 calls out timestamp merge validation when re-adding. | It does not explicitly guarantee preservation of each My Data field including Scoop. |
| PRD-035 | Track per-field update timestamps for status/interest/tags/score/scoop | critical | partial | Data schema includes My Data timestamp fields. | Timestamp usage for sorting/conflict/cache behavior is not fully specified. |
| PRD-036 | Persist Scoop with 4-hour freshness; other AI data session-only | important | partial | Phase 3 defines 4-hour Scoop cache and save-if-saved behavior. | Session-only persistence for Ask/Alchemy/mentioned strip is not captured. |
| PRD-037 | Show in-collection and rating badges on tiles | important | missing | none | Tile indicator requirements are not addressed. |
| PRD-038 | Always display user-overlaid show version; user edits win | critical | partial | `5. Critical Constraints` says user edits override refreshed public data. | The cross-surface display rule is not explicitly enforced across all entry points. |
| PRD-039 | Provide layout with filters/navigation panel and main content | important | full | Phase 1 includes sidebar + main content layout shell. | |
| PRD-040 | Keep Find/Discover and Settings as persistent navigation entries | important | missing | none | Persistent global navigation entry requirements are not specified. |
| PRD-041 | Offer Search Ask Alchemy modes with clear mode switcher | important | partial | Separate phases cover Search, Ask, and Alchemy modes. | Clear mode-switcher behavior is not described. |
| PRD-042 | Group Home by Active/Excited/Interested/Other plus media toggle | important | full | Collection Home grouping and media filters are explicitly listed. | |
| PRD-043 | Support tag/data filters including no-tags and media overlay | important | partial | Filtering sidebar includes Tags, Media Type, and Status. | Genre/decade/community-score/no-tags filters are missing. |
| PRD-044 | Provide empty states for empty library and empty results | detail | missing | none | Home empty-state behavior is not planned. |
| PRD-045 | Search by text with poster grid, badges, and detail open | critical | partial | Search phase includes live text search and poster grid. | In-collection markers and explicit detail-open behavior are not stated. |
| PRD-046 | Support optional Search-on-launch behavior from user settings | detail | partial | Settings phase includes a search-on-launch control. | Search behavior tied to that setting is not explicitly described in Search flow. |
| PRD-047 | Keep Search surface straightforward with no AI persona voice | detail | missing | none | The plan does not explicitly define Search as non-AI tone/behavior. |
| PRD-048 | Ask chat supports turns plus six refreshable starter prompts | important | full | Phase 5 defines Ask chat UI and six starter prompts. | |
| PRD-049 | Ask behavior stays spoiler-safe, honest, domain-limited, friendly | critical | partial | AI wrapper includes joy-forward, honest, vibe-first, spoiler-safe voice. | Domain-limiting/redirect rules and explicit Ask contract details are incomplete. |
| PRD-050 | Summarize older chat turns while preserving persona continuity | important | partial | Phase 5 includes summarizing older turns to save tokens. | Persona-preserving summary style and 1-2 sentence contract are not specified. |
| PRD-051 | Emit Ask mentions as commentary plus exact showList format | critical | partial | Phase 5 enforces `Title::externalId::mediaType` showList output. | Required `commentary` + `showList` structured object and strict parser alignment are incomplete. |
| PRD-052 | Resolve mentioned shows to catalog with fallback handoff behavior | critical | partial | Mentioned shows are parsed, resolved, and rendered clickable. | Fallback non-interactive or Search handoff behavior for unresolved items is not explicit. |
| PRD-053 | Seed Ask context when launched from “Ask about this show” | important | missing | none | Ask-about-this-show context handoff is not planned. |
| PRD-054 | On parser failure retry once then fallback to Search | important | missing | none | Retry-once parser fallback behavior is not included. |
| PRD-055 | Ask answers quickly and list multi-recs in bullet form | detail | missing | none | Ask response formatting minimum bar is absent. |
| PRD-056 | Make Detail page single source for facts, My Data, discovery | important | partial | Phase 2 builds Show Detail with core sections and controls. | The explicit single-source-of-truth product role is not codified. |
| PRD-057 | Preserve required Detail section order and hierarchy | important | missing | none | Required narrative section ordering is not specified. |
| PRD-058 | Support media-rich header with graceful poster/backdrop/trailer fallback | important | partial | Show Detail includes a header carousel. | Fallback behavior when rich media is unavailable is not defined. |
| PRD-059 | Use toolbar status chips mapping Interested/Excited to Later+Interest | critical | full | User overlay specifies toolbar status/interest mapping behavior. | |
| PRD-060 | Auto-save via rating/tag actions with required default statuses | critical | partial | Plan includes rating slider and tag picker controls. | Required autosave default statuses for these actions are not explicit. |
| PRD-061 | Include providers cast/crew seasons budget-revenue with media-conditional rules | important | partial | Show Detail includes streaming providers and cast/crew strands. | Seasons and budget/revenue conditional requirements are not explicitly planned. |
| PRD-062 | Implement Scoop toggle states, streaming feedback, freshness, persistence rule | important | partial | Phase 3 includes Scoop toggle, mini-blog output, 4-hour cache, save-if-saved. | Toggle copy states and progressive generating feedback are not included. |
| PRD-063 | Person detail includes gallery bio analytics and year-grouped credits | important | partial | Person Detail is referenced from cast/crew in Phase 2. | Analytics, year grouping, and full person-page content are underspecified. |
| PRD-064 | Handle critical states for unsaved, no concepts, missing media | detail | missing | none | Critical Detail-page states are not planned. |
| PRD-065 | Generate bullet-only 1-3 word spoiler-free concept ingredients | critical | partial | Phase 4 says AI generates 1-3 word ingredient concepts. | Bullet-only format, spoiler-free constraint, and generic-placeholder exclusions are incomplete. |
| PRD-066 | Keep concepts specific, diverse across axes, and strength-ordered | important | missing | none | No concept quality constraints for diversity/order are defined. |
| PRD-067 | Explore Similar flow: get concepts, pick chips, explore shows | important | full | Phase 4 defines this Explore Similar flow end-to-end. | |
| PRD-068 | Alchemy flow supports 2+ inputs, cap-8 concepts, chaining | critical | full | Phase 6 defines multi-show selection, cap-8, and chaining. | |
| PRD-069 | Clear downstream concepts/results when inputs or selections change | important | missing | none | Backtracking invalidation behavior is not included. |
| PRD-070 | Return 5 Explore Similar and 6 Alchemy recs with concept-linked reasons | critical | full | Phase 4/6 specify rec counts and concept-based reasons. | |
| PRD-071 | Resolve recommendations to real catalog items with valid identifiers | critical | full | Plan resolves AI recommendations to real catalog shows and flags actionable AI. | |
| PRD-072 | Multi-show concepts are shared across inputs and broader pool | important | partial | Phase 6 says concepts are shared across selected inputs. | It does not include the larger option-pool expectation versus single-show generation. |
| PRD-073 | Settings provide font size/readability and Search-on-launch controls | important | full | Phase 7 Settings explicitly includes both controls. | |
| PRD-074 | Settings cover username, provider/model keys, and secret-safety rules | important | partial | Settings includes API-key configuration and aiModel references. | Username sync expectations and explicit secret-safety/non-commit rules are missing. |
| PRD-075 | Export My Data as ZIP JSON with ISO-8601 dates | critical | partial | Phase 7 includes ZIP export containing JSON backup. | ISO-8601 date requirement and explicit full-data scope are not specified. |
| PRD-076 | Keep one consistent AI persona across surfaces; none in Search | critical | partial | Phase 3 creates shared AI voice/personality service. | Search exclusion from AI voice is not explicitly called out. |
| PRD-077 | Enforce voice pillars: warm, honest, vibe-first, specific reasoning | critical | partial | Plan references joy-forward, opinionated honesty, vibe-first, spoiler-safe voice. | Specific-reasoning and full non-negotiable pillar contract are not fully defined. |
| PRD-078 | Scoop output includes defined sections and target length range | important | partial | Plan calls Scoop a “mini blog-post of taste.” | Required section structure and 150-350 word target are missing. |
| PRD-079 | Concept recs bias recent titles while allowing classics/hiddens | detail | missing | none | Recency-bias guidance for concept recommendations is absent. |
| PRD-080 | Feed AI with library/My Data/show/concept context for taste-awareness | important | partial | Ask context includes user library and chat history. | Shared-input contract across all AI surfaces is incomplete. |
| PRD-081 | Validate discovery quality across voice taste surprise specificity integrity | important | partial | Phase 7 QA references Discovery Quality Bar and real-show integrity. | Coverage does not include all quality dimensions and pass criteria. |
| PRD-082 | Enforce surface minimum bars including default eight concepts output | important | missing | none | Surface-specific bars (including default 8 concepts) are not planned. |
| PRD-083 | Apply scoring threshold: Voice>=1 Taste>=1 Integrity=2 Total>=7 | detail | missing | none | No scoring-threshold rubric or acceptance gate is defined. |

### 3. Coverage Scores

score = (20 × 1.0 + 42 × 0.5) / 83 × 100 = 49.4%

Critical:  (14 × 1.0 + 19 × 0.5) / 34 × 100 = 69.1%  (23.5 of 34 critical requirements)
Important: (6 × 1.0 + 22 × 0.5) / 42 × 100 = 40.5%  (17 of 42 important requirements)
Detail:    (0 × 1.0 + 1 × 0.5) / 7 × 100 = 7.1%  (0.5 of 7 detail requirements)
Overall:   49.4% (83 total requirements)

### 4. Top Gaps

1. PRD-028 | `critical` | Preserve all user libraries and My Data across upgrades  
   Why it matters: Without explicit version-migration planning, a schema change can silently drop saved shows, ratings, tags, statuses, and Scoop data.

2. PRD-051 | `critical` | Emit Ask mentions as commentary plus exact showList format  
   Why it matters: If the mention contract is ambiguous, UI parsing becomes brittle and the mentioned-shows strip breaks in core Ask workflows.

3. PRD-030 | `critical` | Auto-save on status, interest, first rating, first tag  
   Why it matters: Incomplete autosave semantics cause inconsistent collection state and user trust loss when actions do not persist as expected.

4. PRD-060 | `critical` | Auto-save via rating/tag actions with required default statuses  
   Why it matters: Missing default-status rules creates conflicting states between Detail interactions and collection grouping logic.

5. PRD-075 | `critical` | Export My Data as ZIP JSON with ISO-8601 dates  
   Why it matters: Partial export definitions can produce unusable backups and break the explicit user-data portability promise.

### 5. Coverage Narrative

The implementation plan is structurally useful but not execution-ready against the full PRD corpus. It captures major modules and phases, so it is not a fundamentally broken plan, but coverage is only 49.4% by the rubric once detailed behavioral contracts are included. This places it in the “sound skeleton with concerning holes” category rather than “minor-gap ready.”

Its strongest coverage clusters are infrastructure baseline decisions (Next.js/Supabase/namespace/user partitioning), broad feature decomposition (Search, Ask, Alchemy, Detail, Settings), and high-level AI capability scaffolding (Scoop, concepts, recommendation resolution). The plan also handles key directional constraints such as actionable AI recommendations and timestamp-based merge policy at a conceptual level.

Gaps are concentrated in behavioral precision requirements: data lifecycle edge rules, strict AI I/O contracts, detail-page state handling, and quality-bar acceptance criteria. The missing/partial items are not random; they consistently appear where the PRD specifies exact conditions, fallback behavior, parser contracts, formatting minima, and migration durability guarantees. Detail-tier coverage is especially weak (7.1%), which is expected for a high-level phase plan but still risky because many “detail” items are user-visible quality gates.

If executed as-is, the most likely failure mode is a product that appears complete in demos but fails acceptance under realistic QA: Ask mention parsing intermittently breaks, autosave semantics are inconsistent, export files lack strict restore-safe formatting assumptions, and schema evolution risks data loss. Stakeholders would likely notice first in cross-surface consistency tests and destructive/rebuild benchmark runs, where edge-case behavior matters more than feature presence.

Remediation should focus on planning specificity, not adding entirely new epics. The plan needs a behavioral contract layer per surface (inputs, outputs, fallback paths), explicit persistence and migration acceptance criteria, and testable definition-of-done statements for each critical rule (autosave/removal/merge/export/parser). In short: keep the existing phase structure, but add a requirements-to-tasks traceability pass and concrete acceptance tests tied to the quality bar.
