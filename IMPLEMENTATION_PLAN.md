# Comprehensive Implementation Plan

This plan outlines the architecture, data modeling, and phased implementation strategy for the TV/Movie companion application, strictly adhering to the requirements in `showbiz_prd.md`, `showbiz_infra_rider_prd.md`, and all supporting documentation.

## 1. Architecture & Tech Stack
- **Framework:** Next.js (App Router, React).
- **Database / Backend:** Supabase (PostgreSQL).
- **Styling:** Tailwind CSS (or Vanilla CSS if preferred, but Tailwind is standard for Next.js unless constrained) - *Note: The system instructions suggest Vanilla CSS for maximum flexibility and avoid Tailwind unless requested, so we will use Vanilla CSS or CSS Modules.*
- **External Catalog API:** TMDB (or equivalent provider) for movie/TV metadata.
- **AI Provider API:** OpenAI / Anthropic / Gemini (configured via environment variables).
- **State Management:** React Context / Zustand + SWR/React Query for data fetching and caching.

## 2. Infrastructure & Execution (Benchmark Mode)
- **Environment Variables:** Define `.env.example` requiring `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, `CATALOG_API_KEY`, `AI_API_KEY`, etc.
- **Isolation Model:** Every database record must be scoped to `namespace_id` (build/run isolation) and `user_id` (user identity).
- **Auth:** Development identity injection (e.g., hardcoded `X-User-Id` or a simple dev selector) to allow seamless future transition to OAuth without schema changes.
- **Scripts:** 
  - `npm run dev` (Start app)
  - `npm test` (Run tests)
  - `npm run db:reset` or `test:reset` (Clear namespace data)

## 3. Data Schema (Supabase PostgreSQL)
Tables will include `namespace_id` and `user_id` as part of the primary key or RLS policies.

- **`shows`**: Matches `storage-schema.ts`.
  - Core Metadata: `id`, `title`, `showType`, `overview`, `posterUrlString`, etc.
  - "My" Data: `myStatus`, `myInterest`, `myTags` (array), `myScore`, `aiScoop`, plus timestamp fields (`myStatusUpdateDate`, etc.) for conflict resolution.
- **`user_settings`**: Matches `CloudSettings` and `LocalSettings`.
  - `autoSearch`, `fontSize`, `aiModel`.

*Merge Policy Rule:* When fetching updated catalog data, local "My" fields always win if they have a newer timestamp. Non-my fields prefer non-empty values.

## 4. Implementation Phases

### Phase 1: Scaffolding & Infrastructure
1. Initialize Next.js project.
2. Set up Supabase client and run database migrations for `shows` and `user_settings`.
3. Implement the Dev Identity/Namespace middleware or context.
4. Implement catalog API wrapper (TMDB) to fetch shows, search, and map to local `Show` interface.
5. Setup basic layout shell (Sidebar + Main Content).

### Phase 2: Core Library & Show Detail (Non-AI)
1. **Search (Find -> Search):** Live search against catalog, display grid of posters.
2. **Show Detail Page (Skeleton):**
   - Header carousel.
   - Core facts, community score.
   - Cast/Crew strands (and Person Detail Page).
   - Streaming providers.
3. **User Overlay ("My Data") Controls:**
   - Toolbar with Status (Active, Done, Wait, Quit) and Interest (Interested, Excited -> Later) chips.
   - Rating slider.
   - Tag picker.
4. **Collection Home:**
   - Fetch saved shows from Supabase.
   - Group by Status (Active -> Excited -> Interested -> Other).
   - Filtering sidebar (Tags, Media Type, Status).

### Phase 3: AI Foundation & Voice Persona
1. **AI API Wrapper:** Create a generic AI service enforcing the "Voice & Personality" (joy-forward, opinionated honesty, vibe-first, spoiler-safe).
2. **The Scoop:** 
   - Add "Give me the scoop!" toggle on Show Detail.
   - Prompt AI for the "mini blog-post of taste".
   - Cache locally for 4 hours; persist in DB if the show is saved.

### Phase 4: Concept System & Explore Similar
1. **Get Concepts:** 
   - Add "Get Concepts" button to Show Detail.
   - AI generates 1-3 word "ingredient" concepts based on show metadata.
2. **Explore Similar:**
   - UI to select generated concepts.
   - AI generates 5 recommendations with reasons citing the selected concepts.
   - Resolve AI text recommendations to real Catalog shows (search by title/ID).

### Phase 5: Ask (Conversational Discovery)
1. **Ask UI:** Chat interface with 6 starter prompts.
2. **Context Management:** Pass user library + chat history to AI. Summarize older turns to save tokens.
3. **Structured Mentions:** Enforce the AI to output `showList` (Title::externalId::mediaType).
4. **Mentioned Shows Strip:** Parse AI response, resolve shows, and render clickable tiles below the chat.

### Phase 6: Alchemy
1. **Alchemy UI:** Multi-show selection from library/search.
2. **Conceptualize Shows:** AI generates shared concepts across the selected inputs.
3. **Alchemize:** User selects up to 8 concepts, AI returns 6 recommendations with specific reasons.
4. **Chaining:** Allow feeding results back into a new Alchemy round.

### Phase 7: Polish & Export
1. **Settings Page:** UI for font sizes, search on launch, and API key configurations (if needed in UI).
2. **Export My Data:** Generate and download a `.zip` containing a JSON backup of the user's `shows` table.
3. **Quality Assurance:** Validate against the "Discovery Quality Bar" (no encyclopedic tone, real-show integrity).
4. **Data Sync Validation:** Ensure timestamp-based merging works correctly when "re-adding" a show.

## 5. Critical Constraints & Rules to Remember
- **Identity is Explicit:** All records require `user_id` and `namespace_id`.
- **User Wins:** User edits (`My Data`) always override refreshed public data.
- **Actionable AI:** All AI recommendations must resolve to real, clickable catalog items.
- **Destructive Testing:** Must be able to wipe a `namespace_id` without touching other data.
- **No Docker Required:** Should run with a hosted Supabase instance for cloud build agents.
