# Showbiz v1 End-to-End Build Plan (Decision-Complete)

## Summary
Build a full Next.js + Supabase implementation of the PRD and all required supporting-doc behaviors, excluding items explicitly marked as open/optional.  
Scope includes: collection home, search, ask chat, alchemy, show detail, person detail, settings/export, persistence/merge logic, namespace + user isolation, and benchmark-compatible DX/testing.

## Locked Decisions
- Include all required features described in PRD + supporting docs.
- Exclude “Open Questions / Optional Extensions” from v1.
- AI integration uses a provider abstraction with one default provider implementation.
- Benchmark identity injection uses `X-User-Id` + namespace header support, with env fallback defaults.
- Backend is source of truth; client cache is disposable.

## Architecture
- Runtime: Next.js (latest stable), TypeScript, App Router.
- Persistence: Supabase Postgres + official client libs.
- Validation: Zod on API boundaries.
- State/data fetching: TanStack Query for server state, local UI state in feature hooks.
- Styling: tokenized theme system (`src/theme`) with no inline style literals in TSX.
- Structure follows AGENTS fractal pattern: pages -> features -> sub-features, logic in hooks, TSX mostly binding/markup.

## Repo/File Plan
- `src/config/`
- `src/theme/`
- `src/components/`
- `src/hooks/`
- `src/utils/`
- `src/pages/HomePage/HomePage.tsx`
- `src/pages/FindPage/FindPage.tsx`
- `src/pages/ShowDetailPage/ShowDetailPage.tsx`
- `src/pages/PersonDetailPage/PersonDetailPage.tsx`
- `src/pages/SettingsPage/SettingsPage.tsx`
- Each page gets `features/` subfolders for isolated concerns (search, ask, alchemy, filters, statuses, tags, scoop, concepts, etc.).
- `src/server/` for API handlers, AI adapters, merge engine, catalog clients.
- `supabase/migrations/` for schema + policies + indexes.
- `tests/` for integration/e2e.
- `.env.example` with benchmark-facing variables and comments.

## Public Interfaces (API/Contracts)
- `GET /api/shows`  
  Query by filter/media type/status/tag/genre/decade/community-score; scoped by `(namespace_id, user_id)`.
- `GET /api/shows/:id`  
  Returns merged persisted + latest catalog details + transient strands (cast/recs/providers/etc.).
- `PUT /api/shows/:id/my-data`  
  Patch `myStatus`, `myInterest`, `myTags`, `myScore`; applies save defaults and timestamp updates.
- `DELETE /api/shows/:id/status`  
  Clears status and removes full saved record (all My Data + scoop) after confirmation path on client.
- `POST /api/search`  
  External catalog search by query/media type.
- `POST /api/ai/ask`  
  Input: user message + session context summary.  
  Output: `{ commentary, showList }` where `showList` format is `Title::externalId::mediaType;;...`.
- `POST /api/ai/scoop`  
  Input: show context + optional persisted state.  
  Output: streamable structured scoop text; persist only if show is in collection.
- `POST /api/ai/concepts`  
  Input: 1+ shows.  
  Output: bullet-list concepts (1–3 words each, spoiler-safe).
- `POST /api/ai/recommend`  
  Input: selected concepts + source shows + mode (`explore`|`alchemy`).  
  Output: mapped real-show recommendations with per-item reasons.
- `GET /api/person/:id`  
  Person profile + credits grouped by year + lightweight analytics inputs.
- `GET /api/settings`, `PUT /api/settings`
- `POST /api/export`  
  Returns zip containing JSON snapshot with ISO-8601 dates.
- `POST /api/test/reset`  
  Namespace-scoped destructive reset (test/dev only).

## Data Model (Supabase)
- `shows`
  - Partition keys: `namespace_id`, `user_id`, `id`.
  - Stores canonical fields from storage schema (`title`, `show_type`, catalog fields, `my_*`, `ai_scoop*`, provider blob, timestamps).
  - Unique key: `(namespace_id, user_id, id)`.
- `cloud_settings`
  - Keyed by `(namespace_id, user_id, id='globalSettings')`.
- `app_metadata`
  - Keyed by `namespace_id`.
- Optional lightweight `chat_sessions` and `alchemy_sessions` are not persisted in DB for v1; session-only in memory/cache per PRD.
- Indexes for filters/sorting:
  - status, interest, score, tags GIN, genres GIN, dates, `my*UpdateDate`, media type.
- Merge engine rules:
  - Non-My fields: keep non-empty/new external values without overwriting good stored data with empty/nil.
  - My fields + scoop: timestamp winner per field.
  - `detailsUpdateDate` set on catalog merge; `creationDate` only on first save.

## Core Feature Build Plan
1. Foundation
- Bootstrap Next app, lint/test tooling, theme tokens, shell layout, route skeleton.
- Add env/config loader and request context resolver (`namespace_id`, `user_id` from headers/env).
- Implement Supabase client split (server/client) and baseline migrations.

2. Persistence + Domain Logic
- Implement `Show` domain types matching PRD schema behavior.
- Build save/default/remove semantics:
  - status save trigger.
  - interest implies `Later + interest`.
  - rating on unsaved => save as `Done`.
  - tag on unsaved => save as `Later + Interested`.
  - clear status => remove record + all My Data + scoop.
- Implement timestamp updates for each user field and scoop.
- Implement export payload builder and zip response.

3. Home/Collection
- Filters panel: all, tags (+ no-tags when applicable), genre, decade, community score.
- Media toggle: all/movies/tv overlaying current filter.
- Status-grouped sections in required order with collapsed “other statuses.”
- Tile badges for in-collection and user rating.
- Empty states for zero library and zero filter results.

4. Find Hub
- Mode switcher: Search / Ask / Alchemy.
- Search grid with in-collection indicators and detail navigation.
- “Search on Launch” setting respected.

5. Ask
- Session chat UI with starter prompts (6 random, refreshable).
- Context retention + summarization after ~10 messages.
- Mentioned-shows strip powered by structured `showList`.
- Mapping failures become non-interactive or handoff to Search.
- “Ask about this show” entry seeds show context.

6. Alchemy
- Select 2+ input shows (library + catalog).
- Generate shared concepts, choose up to 8.
- Return 6 mapped real-show recs with concept-reason linkage.
- Allow chaining “More Alchemy!” with state reset rules on upstream changes.

7. Show Detail
- Required narrative hierarchy and sections from detail spec.
- Toolbar My Status/Interest controls with removal confirmation behavior + suppression preference.
- My rating + tag behaviors with auto-save triggers.
- Scoop CTA state machine, progressive generation, freshness (~4h), persistence-if-saved rule.
- Explore Similar flow: get concepts -> select (1+) -> explore (5 recs).
- Traditional recs, providers, cast/crew, seasons (tv), budget/revenue (movies).

8. Person Detail
- Bio/images + credits grouped by year.
- Analytics widgets: project ratings, top genres, projects-per-year.
- Credit taps route to show detail.

9. Settings & Data
- Font size and search-on-launch local settings.
- Cloud settings sync fields: username, catalog key, AI key, AI model.
- Export My Data zip endpoint + UI action.
- Import/restore excluded from v1.

10. Benchmark/Infra Compliance
- `.env.example` completed.
- Scripts: `dev`, `test`, `test:reset`, `db:migrate`.
- Namespace-scoped destructive test reset API and CLI wrapper.
- Clear docs for local + cloud-agent setup (no Docker requirement).

## AI Behavior Implementation
- Shared guardrails: TV/movie domain only, spoiler-safe default, opinionated honesty, specific taste reasoning.
- Surface adapters:
  - Ask conversational output + structured mentions.
  - Scoop mini-blog structure with fit/warnings/verdict.
  - Concepts as 1–3 word evocative bullets.
  - Recs with explicit concept mapping.
- Real-show integrity enforcement:
  - Resolve by external ID first, validate title case-insensitive.
  - Retry strategy for parse failures once, then graceful fallback.

## Testing & Acceptance
- Unit tests
  - Save/default/remove semantics.
  - Merge policy timestamp conflict resolution.
  - Concept/recommendation parser and mention string parser.
  - Filter grouping/order logic.
- Integration tests (API + DB)
  - Namespace/user partition isolation.
  - Export payload correctness and ISO date formatting.
  - Test reset scoping.
  - AI fallback behaviors (mapping/parse failure).
- E2E tests
  - Build collection journey.
  - Rate-to-save and tag-to-save journeys.
  - Ask recommendation to detail to save.
  - Explore Similar and Alchemy happy paths.
  - Status removal confirmation and full data wipe.
- Quality-bar checks
  - Discovery output rubric (voice, taste alignment, specificity, surprise, real-show integrity).
  - Surface minimums (counts and structure for scoop/concepts/recs).

## Assumptions and Defaults
- External catalog provider uses a TMDB-like API with stable external IDs.
- AI key/model can come from env and optionally be overridden in user settings; secrets never committed.
- Session-only data (chat/alchemy transient results) is not durable across reloads by design.
- Optional extensions remain backlog:
  - Import/restore.
  - Next as first-class UI status.
  - Named custom lists beyond tags.
  - Unsaved-scoop implicit save behavior changes.
  - Explicit unrated sentinel storage.
- Accessibility, responsive behavior, and lint-clean standards are required across all delivered pages.

## Delivery Sequence
1. Foundation + schema + identity/namespace plumbing.
2. Domain logic + APIs + tests for save/merge/remove.
3. Home + Search + Detail core flows.
4. Ask + Explore Similar + Alchemy.
5. Person + Settings + Export.
6. Infra scripts/docs + full test pass and PRD acceptance sweep.
