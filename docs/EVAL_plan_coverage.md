### 1. Requirements Extraction

#### Pass 1: Identify Functional Areas

- Core Domain Model
- Collection Navigation and Home
- Save and Removal Semantics
- Sync Persistence and Merge
- Search Experience
- Ask Chat Contracts
- Concepts and Alchemy
- Show Detail Experience
- Person Detail
- Settings and Export
- AI Voice and Quality
- Infrastructure and Isolation
- Storage Schema and Mapping

#### Pass 2: Extract Requirements Within Each Area

#### Core Domain Model

- PRD-001 | `critical` | Show object combines catalog data with My Data overlay. | `showbiz_prd.md > 4.1 Show (Movie or TV)`
- PRD-002 | `critical` | User-overlaid saved version displays everywhere and wins refreshes. | `showbiz_prd.md > 4.1 Show (Display rule)`
- PRD-003 | `important` | Status taxonomy includes active/later/wait/done/quit, with hidden next. | `showbiz_prd.md > 4.2 Status System`
- PRD-004 | `critical` | Interested and Excited map to Later plus matching interest. | `showbiz_prd.md > 4.2 Status System (Important nuance)`
- PRD-005 | `detail` | Tags support multi-label lists and personal tag library behavior. | `showbiz_prd.md > 4.4 Tags (User Lists)`
- PRD-006 | `critical` | Collection membership is defined by presence of saved status. | `showbiz_prd.md > 5.1 Collection Membership`

#### Collection Navigation and Home

- PRD-007 | `critical` | Collection filters include all/tag/no-tag/genre/decade/community-score views. | `showbiz_prd.md > 4.5 Filters (Ways to View the Collection)`
- PRD-008 | `important` | Media toggle All/Movies/TV applies on top of filters. | `showbiz_prd.md > 4.5 Filters (Ways to View the Collection)`
- PRD-009 | `critical` | App shell includes filters panel plus main content surfaces. | `showbiz_prd.md > 6. App Structure & Navigation`
- PRD-010 | `important` | Find hub exposes Search, Ask, and Alchemy mode switching. | `showbiz_prd.md > 6. Find/Discover hub modes`
- PRD-011 | `critical` | Home groups by required status order with collapsed other statuses. | `showbiz_prd.md > 7.1 Collection Home`
- PRD-012 | `important` | Home includes tile badges and empty-state behaviors. | `showbiz_prd.md > 7.1 Collection Home; 5.9 Tile Indicators`

#### Save and Removal Semantics

- PRD-013 | `critical` | Saving triggers include status, interest, rating-unsaved, and tag-unsaved. | `showbiz_prd.md > 5.2 Saving Triggers`
- PRD-014 | `critical` | Default save is Later+Interested; rating-first defaults to Done. | `showbiz_prd.md > 5.3 Default Values When Saving`
- PRD-015 | `critical` | Clearing status requires confirmation before destructive collection removal. | `showbiz_prd.md > 5.4 Removing from Collection`
- PRD-016 | `critical` | Removal clears all My Data including AI Scoop fields. | `showbiz_prd.md > 5.4 Removing from Collection`
- PRD-017 | `important` | Re-adding preserves latest My Data and refreshes public fields. | `showbiz_prd.md > 5.5 Re-adding the Same Show`
- PRD-018 | `important` | Per-field update timestamps exist for My fields and scoop. | `showbiz_prd.md > 5.6 Timestamps`

#### Sync Persistence and Merge

- PRD-019 | `critical` | User-field merge conflicts resolve using newest per-field timestamps. | `showbiz_prd.md > 5.5 Re-adding the Same Show`
- PRD-020 | `important` | detailsUpdateDate updates on merge; creationDate set only once. | `showbiz_prd.md > 5.6 Timestamps; storage-schema.md > Merge policy`
- PRD-021 | `important` | AI Scoop persists only for saved shows with freshness window. | `showbiz_prd.md > 4.9 AI Scoop; 5.7 AI Data Persistence`
- PRD-022 | `important` | Ask/Alchemy session artifacts remain non-persistent session-only data. | `showbiz_prd.md > 5.7 AI Data Persistence`
- PRD-023 | `critical` | AI recommendations map to real shows with fallback behavior. | `showbiz_prd.md > 5.8 AI Recommendations Map to Real Shows`
- PRD-024 | `important` | Sync keeps devices consistent and merges duplicates transparently. | `showbiz_prd.md > 5.10 Data Sync & Integrity`
- PRD-025 | `critical` | App upgrades preserve existing libraries and My Data continuity. | `showbiz_prd.md > 5.11 Data Continuity Across Versions`
- PRD-026 | `critical` | Backend is source of truth and client cache is disposable. | `showbiz_prd.md > 8. Cross-Cutting Rules & Principles`

#### Search Experience

- PRD-027 | `critical` | Search supports title/keyword queries with poster-grid results. | `showbiz_prd.md > 7.2 Search`
- PRD-028 | `important` | Search marks in-collection items and supports search-on-launch. | `showbiz_prd.md > 7.2 Search`
- PRD-029 | `important` | Search remains catalog-only and does not expose AI voice. | `ai_voice_personality.md > 1 Persona Summary; 8 Decisions`

#### Ask Chat Contracts

- PRD-030 | `critical` | Ask provides conversational chat with friendly spoiler-safe honesty. | `showbiz_prd.md > 7.3 Ask`
- PRD-031 | `detail` | Ask welcome view contains six random refreshable starter prompts. | `showbiz_prd.md > 7.3 Ask`
- PRD-032 | `important` | Ask retains session context and summarizes older turns around ten. | `showbiz_prd.md > 7.3 Ask; ai_prompting_context.md > 4 Conversation Summarization`
- PRD-033 | `important` | Mentioned shows appear inline and in horizontal strip. | `showbiz_prd.md > 7.3 Ask`
- PRD-034 | `important` | Mention taps open Detail or hand off to Search fallback. | `showbiz_prd.md > 7.3 Ask`
- PRD-035 | `important` | Ask-about-show entry seeds Ask session with show context. | `showbiz_prd.md > 7.3 Ask (Variants)`
- PRD-036 | `critical` | Ask structured output returns commentary with strict showList format. | `ai_prompting_context.md > 3.2 Ask with Mentions`
- PRD-037 | `important` | Structured parse failures retry once then fall back gracefully. | `ai_prompting_context.md > 5 Guardrails & Fallbacks`
- PRD-038 | `critical` | Chat surfaces stay constrained to TV/movie domain responses. | `ai_prompting_context.md > 1 Shared Rules`

#### Concepts and Alchemy

- PRD-039 | `critical` | Alchemy requires selecting two-plus input shows before generation. | `showbiz_prd.md > 4.7 Alchemy Session; 7.4 Alchemy`
- PRD-040 | `important` | Concept selection caps at eight and resets downstream outputs. | `concept_system.md > 5 Selection UX Rules`
- PRD-041 | `important` | Alchemy supports chained More Alchemy discovery rounds. | `showbiz_prd.md > 4.7 Alchemy Session`
- PRD-042 | `important` | Explore Similar flow is concepts, selection, then recommendations. | `showbiz_prd.md > 4.8 Explore Similar`
- PRD-043 | `critical` | Concept output is bullet-only evocative one-to-three spoiler-safe words. | `ai_prompting_context.md > 3.4 Concepts; concept_system.md > 4 Generation Rules`
- PRD-044 | `critical` | Multi-show concepts must represent shared traits across all inputs. | `concept_system.md > 4 Generation Rules`
- PRD-045 | `important` | Concept quality emphasizes specificity, diversity, and strength ordering. | `concept_system.md > 4 Generation Rules`
- PRD-046 | `critical` | Concept-based recs map to real shows with explicit linkage. | `concept_system.md > 6 Concepts → Recommendations Contract`
- PRD-047 | `critical` | Recommendation counts are five for Explore and six for Alchemy. | `concept_system.md > 6 Concepts → Recommendations Contract`
- PRD-048 | `detail` | Recommendations favor recent titles while allowing classics and gems. | `concept_system.md > 6 Concepts → Recommendations Contract`

#### Show Detail Experience

- PRD-049 | `critical` | Detail combines facts, My Data, and discovery as source-of-truth. | `showbiz_prd.md > 7.5 Show Detail Page; detail_page_experience.md > 1 Purpose`
- PRD-050 | `important` | Detail narrative section order follows the defined hierarchy. | `detail_page_experience.md > 3 Narrative Hierarchy`
- PRD-051 | `important` | Header prioritizes trailers with graceful fallback to still media. | `detail_page_experience.md > 3.1 Header Media`
- PRD-052 | `important` | Top section exposes quick year-length-score-and-user relationship signals. | `detail_page_experience.md > 2 First-15-Seconds Experience`
- PRD-053 | `critical` | Toolbar status and interest controls drive auto-save interactions. | `detail_page_experience.md > 3.3 My Relationship Controls`
- PRD-054 | `important` | Scoop state includes copy states, progressive stream, and freshness. | `detail_page_experience.md > 3.4 Overview + Scoop`
- PRD-055 | `important` | Detail provides Ask CTA, traditional recs, and Explore Similar. | `detail_page_experience.md > 3.5-3.7`
- PRD-056 | `important` | Detail includes providers, cast/crew, seasons, and budget/revenue strands. | `showbiz_prd.md > 7.5 Show Detail Page`
- PRD-057 | `important` | Detail handles unsaved, missing-media, no-concepts, and media-type states. | `detail_page_experience.md > 5 Critical States`

#### Person Detail

- PRD-058 | `important` | Person page shows gallery/name/bio and year-grouped credits. | `showbiz_prd.md > 7.6 Person Detail Page`
- PRD-059 | `detail` | Person page includes ratings/genre/projects-per-year analytics charts. | `showbiz_prd.md > 7.6 Person Detail Page`
- PRD-060 | `important` | Selecting a person credit routes to the show detail page. | `showbiz_prd.md > 7.6 Person Detail Page`

#### Settings and Export

- PRD-061 | `important` | Settings include font size and search-on-launch preferences. | `showbiz_prd.md > 7.7 Settings & Your Data`
- PRD-062 | `important` | Settings include username, catalog key, AI key, and model. | `showbiz_prd.md > 7.7 Settings & Your Data`
- PRD-063 | `critical` | Export produces zip with JSON backup and ISO-8601 dates. | `showbiz_prd.md > 7.7 Settings & Your Data`
- PRD-064 | `critical` | Secrets never committed and env-sourced key flows are supported. | `showbiz_prd.md > 7.7 Settings & Your Data; showbiz_infra_rider_prd.md > 3.1`

#### AI Voice and Quality

- PRD-065 | `important` | All AI surfaces share one persona while Search stays non-AI. | `ai_voice_personality.md > 1 Persona Summary`
- PRD-066 | `important` | Voice pillars require warm, honest, specific spoiler-safe responses. | `ai_voice_personality.md > 2 Non-Negotiable Voice Pillars`
- PRD-067 | `important` | Scoop content includes take, stack-up, centerpiece, fit, and verdict. | `ai_voice_personality.md > 4.1 Scoop`
- PRD-068 | `important` | Ask answers quickly, concise, list-friendly, and confidently opinionated. | `discovery_quality_bar.md > 2.2 Ask / Explore Search Chat`
- PRD-069 | `detail` | Concepts default to eight items with concept-tied rec reasons. | `discovery_quality_bar.md > 2.3 Concepts; 2.4 Explore Similar / Alchemy Recs`
- PRD-070 | `important` | Discovery quality checks cover alignment, specificity, and surprise balance. | `discovery_quality_bar.md > 1 Quality Dimensions`
- PRD-071 | `critical` | Real-show integrity remains a non-negotiable quality gate. | `discovery_quality_bar.md > 4 Scoring Rubric`

#### Infrastructure and Isolation

- PRD-072 | `critical` | Benchmark baseline uses Next.js latest stable plus Supabase clients. | `showbiz_infra_rider_prd.md > 2 Benchmark Baseline`
- PRD-073 | `important` | Docker is optional; hosted cloud-agent execution must be supported. | `showbiz_infra_rider_prd.md > 2 Benchmark Baseline; 8 Cloud Agent Compatibility`
- PRD-074 | `critical` | Repo includes env example, env-secret ignore, no code-edit setup. | `showbiz_infra_rider_prd.md > 3.1 Environment variable interface`
- PRD-075 | `critical` | Credential boundary keeps anon key client-side and elevated server-only. | `showbiz_infra_rider_prd.md > 3.1 Credential handling rules`
- PRD-076 | `critical` | Repo scripts cover start, test, reset, and repeatable migrations. | `showbiz_infra_rider_prd.md > 3.2 One-command DX; 3.3 DB artifacts`
- PRD-077 | `critical` | Stable namespace isolation scopes data access and destructive operations. | `showbiz_infra_rider_prd.md > 4.1 Build/run namespace`
- PRD-078 | `critical` | All records use opaque user_id with namespace+user partitioning. | `showbiz_infra_rider_prd.md > 4.2 User identity; 4.3 Relationship`
- PRD-079 | `important` | Dev identity injection is documented and disabled/gated in production. | `showbiz_infra_rider_prd.md > 5.1 Auth policy`
- PRD-080 | `important` | OAuth migration should require wiring changes, not schema redesign. | `showbiz_infra_rider_prd.md > 5.2 Migration to real OAuth`
- PRD-081 | `critical` | Destructive tests reset namespace data without global database teardown. | `showbiz_infra_rider_prd.md > 7 Destructive Testing Rules`

#### Storage Schema and Mapping

- PRD-082 | `important` | Persist canonical Show identity, catalog, my, AI, provider, timestamps. | `storage-schema.md > Show (stored fields)`
- PRD-083 | `detail` | Keep transient credits/videos/recs/images/seasons out of persistence. | `storage-schema.md > Show (Not stored/transient)`
- PRD-084 | `detail` | Persist autoSearch/fontSize plus removal-confirmation and last-filter UI state. | `storage-schema.md > Other persistent storage (Local settings/UI state)`
- PRD-085 | `important` | External mapping decodes catalog data, merges existing, then persists. | `storage-schema.md > External catalog → Show mapping strategy`
- PRD-086 | `detail` | Mapping infers media type/title and rejects unmappable unknown entries. | `storage-schema.md > Field mapping rules (Title/Show type)`
- PRD-087 | `critical` | Merge non-my first-non-empty; my/scoop by timestamps with dates. | `storage-schema.md > Merge / overwrite policy`

Total: 87 requirements (37 critical, 42 important, 8 detail) across 13 functional areas

### 2. Coverage Table

| PRD-ID | Requirement | Severity | Coverage | Evidence | Gap |
| ------ | ----------- | -------- | -------- | -------- | --- |
| PRD-001 | Show object combines catalog data with My Data overlay. | `critical` | full | Data Model: `shows` stores catalog fields plus `my_*`, `ai_scoop*`, and timestamps. |  |
| PRD-002 | User-overlaid saved version displays everywhere and wins refreshes. | `critical` | full | Summary commits to full PRD/supporting-doc behavior; `GET /api/shows/:id` returns merged persisted user-overlaid data. |  |
| PRD-003 | Status taxonomy includes active/later/wait/done/quit, with hidden next. | `important` | full | Persistence/domain plan covers status semantics and explicitly backlogs “Next as first-class UI status.” |  |
| PRD-004 | Interested and Excited map to Later plus matching interest. | `critical` | full | Persistence rules: “interest implies Later + interest.” |  |
| PRD-005 | Tags support multi-label lists and personal tag library behavior. | `detail` | full | Home filters include tag filters and no-tags handling; tags included in save and API patch contracts. |  |
| PRD-006 | Collection membership is defined by presence of saved status. | `critical` | full | Save/remove semantics are status-driven, and clear status removes record from collection. |  |
| PRD-007 | Collection filters include all/tag/no-tag/genre/decade/community-score views. | `critical` | full | Home plan explicitly lists all, tags/no-tags, genre, decade, community score filters. |  |
| PRD-008 | Media toggle All/Movies/TV applies on top of filters. | `important` | full | Home plan: “Media toggle all/movies/tv overlaying current filter.” |  |
| PRD-009 | App shell includes filters panel plus main content surfaces. | `critical` | full | Repo/page plan includes Home, Find, Show Detail, Person Detail, and Settings pages with shared shell layout. |  |
| PRD-010 | Find hub exposes Search, Ask, and Alchemy mode switching. | `important` | full | Find Hub section defines mode switcher Search/Ask/Alchemy. |  |
| PRD-011 | Home groups by required status order with collapsed other statuses. | `critical` | full | Home plan calls out required status order and collapsed “other statuses.” |  |
| PRD-012 | Home includes tile badges and empty-state behaviors. | `important` | full | Home plan includes tile badges and both empty states. |  |
| PRD-013 | Saving triggers include status, interest, rating-unsaved, and tag-unsaved. | `critical` | full | Persistence rules enumerate all four save triggers explicitly. |  |
| PRD-014 | Default save is Later+Interested; rating-first defaults to Done. | `critical` | full | Persistence rules include both default behaviors verbatim. |  |
| PRD-015 | Clearing status requires confirmation before destructive collection removal. | `critical` | full | `DELETE /api/shows/:id/status` and Show Detail plan include confirmation behavior. |  |
| PRD-016 | Removal clears all My Data including AI Scoop fields. | `critical` | full | Persistence plan states clear status removes record plus all My Data and scoop; suppression preference included. |  |
| PRD-017 | Re-adding preserves latest My Data and refreshes public fields. | `important` | full | Data model merge rules cover preserving user fields while merging refreshed catalog details. |  |
| PRD-018 | Per-field update timestamps exist for My fields and scoop. | `important` | full | Persistence plan includes timestamp updates for each user field and scoop. |  |
| PRD-019 | User-field merge conflicts resolve using newest per-field timestamps. | `critical` | full | Merge engine: “My fields + scoop: timestamp winner per field.” |  |
| PRD-020 | detailsUpdateDate updates on merge; creationDate set only once. | `important` | full | Merge engine explicitly sets detailsUpdateDate on merge and keeps creationDate first-save only. |  |
| PRD-021 | AI Scoop persists only for saved shows with freshness window. | `important` | full | Show Detail plan includes scoop persistence-if-saved and freshness around 4h. |  |
| PRD-022 | Ask/Alchemy session artifacts remain non-persistent session-only data. | `important` | full | Data model section marks chat/alchemy sessions as session-only, not persisted DB records. |  |
| PRD-023 | AI recommendations map to real shows with fallback behavior. | `critical` | full | AI behavior enforces ID/title validation and fallback to non-interactive/Search on failures. |  |
| PRD-024 | Sync keeps devices consistent and merges duplicates transparently. | `important` | partial | Plan includes sync fields and merge conflict logic. | It does not explicitly describe duplicate detection/transparent merge behavior as a planned deliverable. |
| PRD-025 | App upgrades preserve existing libraries and My Data continuity. | `critical` | missing | none | No migration/upgrade-forward compatibility plan is described beyond current schema setup. |
| PRD-026 | Backend is source of truth and client cache is disposable. | `critical` | full | Locked Decisions explicitly state backend source-of-truth and disposable client cache. |  |
| PRD-027 | Search supports title/keyword queries with poster-grid results. | `critical` | full | Public API includes `POST /api/search`; Find Hub defines search grid behavior. |  |
| PRD-028 | Search marks in-collection items and supports search-on-launch. | `important` | full | Find Hub section includes in-collection indicators and Search-on-Launch setting. |  |
| PRD-029 | Search remains catalog-only and does not expose AI voice. | `important` | missing | none | Plan lacks an explicit non-AI-voice contract for Search behavior/copy. |
| PRD-030 | Ask provides conversational chat with friendly spoiler-safe honesty. | `critical` | full | Ask section and shared AI guardrails cover conversational, spoiler-safe, opinionated behavior. |  |
| PRD-031 | Ask welcome view contains six random refreshable starter prompts. | `detail` | full | Ask plan explicitly includes six random refreshable starter prompts. |  |
| PRD-032 | Ask retains session context and summarizes older turns around ten. | `important` | full | Ask plan includes context retention and summarization after ~10 messages. |  |
| PRD-033 | Mentioned shows appear inline and in horizontal strip. | `important` | full | Ask plan includes mentioned-shows strip powered by structured showList. |  |
| PRD-034 | Mention taps open Detail or hand off to Search fallback. | `important` | full | Ask plan explicitly states mapping failures become non-interactive or Search handoff. |  |
| PRD-035 | Ask-about-show entry seeds Ask session with show context. | `important` | full | Ask plan includes “Ask about this show” seeding show context. |  |
| PRD-036 | Ask structured output returns commentary with strict showList format. | `critical` | full | API contract defines `{ commentary, showList }` with required delimiter format. |  |
| PRD-037 | Structured parse failures retry once then fall back gracefully. | `important` | full | AI behavior section includes retry-on-parse-failure once then graceful fallback. |  |
| PRD-038 | Chat surfaces stay constrained to TV/movie domain responses. | `critical` | full | Shared guardrails include “TV/movie domain only.” |  |
| PRD-039 | Alchemy requires selecting two-plus input shows before generation. | `critical` | full | Alchemy plan starts with selecting 2+ input shows. |  |
| PRD-040 | Concept selection caps at eight and resets downstream outputs. | `important` | full | Alchemy plan sets cap to eight and reset rules on upstream changes. |  |
| PRD-041 | Alchemy supports chained More Alchemy discovery rounds. | `important` | full | Alchemy plan includes chained “More Alchemy!” path. |  |
| PRD-042 | Explore Similar flow is concepts, selection, then recommendations. | `important` | full | Show Detail plan includes get concepts -> select -> explore (5 recs). |  |
| PRD-043 | Concept output is bullet-only evocative one-to-three spoiler-safe words. | `critical` | full | Concept API contract specifies bullet-list concepts, 1-3 words, spoiler-safe. |  |
| PRD-044 | Multi-show concepts must represent shared traits across all inputs. | `critical` | full | Alchemy plan explicitly generates shared concepts across selected inputs. |  |
| PRD-045 | Concept quality emphasizes specificity, diversity, and strength ordering. | `important` | partial | Plan defines evocative 1-3 word concepts. | It does not explicitly require diversity across axes or ordering by strongest concepts. |
| PRD-046 | Concept-based recs map to real shows with explicit linkage. | `critical` | full | Alchemy and AI behavior sections require mapped real-show recs with concept-reason linkage. |  |
| PRD-047 | Recommendation counts are five for Explore and six for Alchemy. | `critical` | full | Show Detail and Alchemy plans explicitly set 5 explore recs and 6 alchemy recs. |  |
| PRD-048 | Recommendations favor recent titles while allowing classics and gems. | `detail` | partial | Plan captures concept-linked mapped recommendations. | It does not specify recency bias versus classics/hidden-gems balancing. |
| PRD-049 | Detail combines facts, My Data, and discovery as source-of-truth. | `critical` | full | Show Detail section is explicitly scoped to required narrative hierarchy and discovery controls. |  |
| PRD-050 | Detail narrative section order follows the defined hierarchy. | `important` | full | Show Detail plan explicitly references required narrative hierarchy and sections from detail spec. |  |
| PRD-051 | Header prioritizes trailers with graceful fallback to still media. | `important` | full | Plan commits to implementing required detail-spec hierarchy, which includes media fallback behavior. |  |
| PRD-052 | Top section exposes quick year-length-score-and-user relationship signals. | `important` | full | Plan includes core facts and toolbar/rating controls in the primary detail hierarchy. |  |
| PRD-053 | Toolbar status and interest controls drive auto-save interactions. | `critical` | full | Show Detail plan calls out toolbar status/interest controls and auto-save rating/tag behaviors. |  |
| PRD-054 | Scoop state includes copy states, progressive stream, and freshness. | `important` | full | Show Detail plan includes scoop CTA state machine, progressive generation, and ~4h freshness. |  |
| PRD-055 | Detail provides Ask CTA, traditional recs, and Explore Similar. | `important` | full | Show Detail plan includes Ask-about-show, traditional recs, and Explore Similar flow. |  |
| PRD-056 | Detail includes providers, cast/crew, seasons, and budget/revenue strands. | `important` | full | Show Detail plan explicitly includes providers, cast/crew, seasons, and budget/revenue. |  |
| PRD-057 | Detail handles unsaved, missing-media, no-concepts, and media-type states. | `important` | partial | Plan covers persistence-if-saved scoop and core flows. | Explicit handling for missing trailers/backdrops and no-concepts initial state is not described. |
| PRD-058 | Person page shows gallery/name/bio and year-grouped credits. | `important` | full | Person Detail plan includes bio/images and credits grouped by year. |  |
| PRD-059 | Person page includes ratings/genre/projects-per-year analytics charts. | `detail` | full | Person Detail plan includes analytics widgets for ratings, top genres, and projects-per-year. |  |
| PRD-060 | Selecting a person credit routes to the show detail page. | `important` | full | Person Detail plan explicitly states credit taps route to show detail. |  |
| PRD-061 | Settings include font size and search-on-launch preferences. | `important` | full | Settings plan includes font size and search-on-launch local settings. |  |
| PRD-062 | Settings include username, catalog key, AI key, and model. | `important` | full | Settings plan includes synced username, catalog key, AI key, and model fields. |  |
| PRD-063 | Export produces zip with JSON backup and ISO-8601 dates. | `critical` | full | Export API contract and tests call out zip JSON snapshot with ISO date formatting. |  |
| PRD-064 | Secrets never committed and env-sourced key flows are supported. | `critical` | full | Assumptions state secrets never committed and env/model override behavior. |  |
| PRD-065 | All AI surfaces share one persona while Search stays non-AI. | `important` | partial | Plan includes shared AI guardrails and surface adapters. | It does not explicitly define Search as a non-AI voice surface in implementation tasks. |
| PRD-066 | Voice pillars require warm, honest, specific spoiler-safe responses. | `important` | full | AI behavior guardrails include spoiler-safe, opinionated honesty, and specific taste reasoning. |  |
| PRD-067 | Scoop content includes take, stack-up, centerpiece, fit, and verdict. | `important` | partial | Plan includes scoop mini-blog with fit/warnings/verdict. | It does not explicitly call out stack-up honesty and centerpiece emphasis as acceptance criteria. |
| PRD-068 | Ask answers quickly, concise, list-friendly, and confidently opinionated. | `important` | partial | Plan describes conversational Ask and starter prompts. | It does not specify direct-answer-within-3-5-lines behavior or confidence standard. |
| PRD-069 | Concepts default to eight items with concept-tied rec reasons. | `detail` | partial | Plan defines up-to-8 selection and concept-reason linkage. | It does not explicitly commit to generating eight concepts by default. |
| PRD-070 | Discovery quality checks cover alignment, specificity, and surprise balance. | `important` | full | Testing plan includes discovery rubric checks for voice, taste alignment, specificity, surprise, and integrity. |  |
| PRD-071 | Real-show integrity remains a non-negotiable quality gate. | `critical` | partial | Plan includes integrity in quality-bar checks. | It does not codify non-negotiable thresholding in acceptance criteria. |
| PRD-072 | Benchmark baseline uses Next.js latest stable plus Supabase clients. | `critical` | full | Architecture locks Next.js latest stable and Supabase official client usage. |  |
| PRD-073 | Docker is optional; hosted cloud-agent execution must be supported. | `important` | full | Benchmark compliance section requires cloud-agent docs and no Docker requirement. |  |
| PRD-074 | Repo includes env example, env-secret ignore, no code-edit setup. | `critical` | partial | Plan includes `.env.example` and env-based configuration assumptions. | It does not explicitly include `.gitignore` env-secret rule or “no source edits required” verification. |
| PRD-075 | Credential boundary keeps anon key client-side and elevated server-only. | `critical` | missing | none | Plan does not explicitly define client/server key separation enforcement. |
| PRD-076 | Repo scripts cover start, test, reset, and repeatable migrations. | `critical` | full | Benchmark compliance lists `dev`, `test`, `test:reset`, `db:migrate` and migrations path. |  |
| PRD-077 | Stable namespace isolation scopes data access and destructive operations. | `critical` | full | Namespace-scoped partition keys and test reset API are explicit. |  |
| PRD-078 | All records use opaque user_id with namespace+user partitioning. | `critical` | full | Data model keys and API scoping use `(namespace_id, user_id)`. |  |
| PRD-079 | Dev identity injection is documented and disabled/gated in production. | `important` | partial | Plan includes `X-User-Id` identity injection and docs. | Production gating behavior is not explicitly planned. |
| PRD-080 | OAuth migration should require wiring changes, not schema redesign. | `important` | partial | Plan includes identity abstraction and namespace/user partitioning. | It does not explicitly state or test schema-stable OAuth migration constraints. |
| PRD-081 | Destructive tests reset namespace data without global database teardown. | `critical` | full | Test reset API and integration tests explicitly scope destructive reset to namespace. |  |
| PRD-082 | Persist canonical Show identity, catalog, my, AI, provider, timestamps. | `important` | full | Data model `shows` definition commits to canonical storage-schema fields including my/ai/provider/timestamps. |  |
| PRD-083 | Keep transient credits/videos/recs/images/seasons out of persistence. | `detail` | full | `GET /api/shows/:id` distinguishes persisted data from transient strands for detail rendering. |  |
| PRD-084 | Persist autoSearch/fontSize plus removal-confirmation and last-filter UI state. | `detail` | partial | Plan includes autoSearch/font size and removal confirmation suppression behavior. | It does not explicitly include lastSelectedFilter persistence. |
| PRD-085 | External mapping decodes catalog data, merges existing, then persists. | `important` | full | Plan defines catalog merge engine and merged persisted+latest detail retrieval contract. |  |
| PRD-086 | Mapping infers media type/title and rejects unmappable unknown entries. | `detail` | partial | Plan enforces external ID + title validation for recommendations. | It does not explicitly define show-type inference/rejection rules at mapping boundaries. |
| PRD-087 | Merge non-my first-non-empty; my/scoop by timestamps with dates. | `critical` | full | Merge engine rules explicitly implement first-non-empty for non-My and timestamp winner for My/scoop fields. |  |

### 3. Coverage Scores

Critical:  (33 × 1.0 + 2 × 0.5) / 37 × 100 = 91.89%  (34.0 of 37 critical requirements)
Important: (33 × 1.0 + 8 × 0.5) / 42 × 100 = 88.10%  (37.0 of 42 important requirements)
Detail:    (4 × 1.0 + 4 × 0.5) / 8 × 100 = 75.00%  (6.0 of 8 detail requirements)
Overall:   (70 × 1.0 + 14 × 0.5) / 87 × 100 = 88.51%  (77.0 of 87 total requirements)

### 4. Top Gaps

- PRD-025 | `critical` | App upgrades preserve existing libraries and My Data continuity. Without explicit migration/version-forward planning, schema changes can silently drop ratings, tags, statuses, and scoop during upgrades.
- PRD-075 | `critical` | Credential boundary keeps anon key client-side and elevated server-only. Missing explicit key-boundary implementation risks secret exposure and invalid benchmark compliance.
- PRD-074 | `critical` | Repo includes env example, env-secret ignore, and no-code-edit setup. If `.gitignore` and no-edit startup guarantees are unspecified, onboarding and benchmark reproducibility can fail.
- PRD-071 | `critical` | Real-show integrity remains a non-negotiable quality gate. Without hard pass/fail thresholds, hallucinated or mismapped titles can slip through despite general quality checks.
- PRD-079 | `important` | Dev identity injection is documented and disabled/gated in production. If production gating is unspecified, dev auth shortcuts can leak into deployable environments.

### 5. Coverage Narrative

The plan is structurally strong and close to implementation-ready, with an overall score of 88.51% and especially high coverage on critical requirements (91.89%). Core product surfaces, persistence contracts, and benchmark-oriented architecture are concretely represented. The posture is “strong plan with a small set of high-impact compliance and durability gaps,” not a plan that misses core workflows.

Strength is concentrated in collection lifecycle behavior, detail/find/person feature coverage, AI endpoint contracts, and namespace/user partitioning. The plan is explicit about save defaults, destructive removal semantics, timestamp-based merge logic, concept/recommendation flows, and required recommendation counts. It is also strong on test intent: unit, integration, and E2E scopes align with major user journeys and key business rules.

Weaknesses cluster in three places rather than being random: upgrade durability guarantees, infra/compliance hardening details, and strict AI quality gates. Specifically, migration continuity across app versions is absent, credential-handling boundaries are not explicitly enforced in the implementation tasks, and some quality-bar requirements remain implied (for example, non-negotiable integrity thresholds and specific ask/voice delivery constraints).

If executed as-is, the first stakeholder-visible failure mode is likely benchmark/compliance rejection or security/process review friction before UX failure: missing explicit `.gitignore`/credential-boundary guarantees and production-gating language for dev identity could fail acceptance despite a working app. The first user-visible failure mode after that would be regression risk during schema evolution (library/data continuity) and occasional AI output quality drift where hard thresholds are not codified.

Remediation work should focus on specification hardening rather than broad re-planning: add explicit migration/continuity acceptance criteria, formalize credential-boundary and env bootstrapping requirements, and convert AI quality-bar expectations into testable gates (especially real-show integrity pass/fail). A small infra/compliance appendix plus an AI acceptance-criteria appendix would likely close most remaining risk without changing architecture.
