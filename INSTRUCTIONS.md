# Planning Benchmark — Instructions

You are working inside a **planning benchmark** repository. This repo measures how well coding agents plan against a real product specification.

---

## Workflows

### 1. Run a New Benchmark

The user wants to generate an implementation plan.

- Open and follow `1-START_HERE.md` exactly.
- This is a **planning-only** task. Do not build or implement anything. Produce a plan.
- Use planning mode if your agent supports it.
- Output: `results/PLAN.md`

### 2. Evaluate a Benchmark

The user wants to audit a plan they already generated.

- Open and follow `2-EVALUATE_PLAN.md` exactly.
- This requires both the PRD (`docs/prd/`) and an existing `results/PLAN.md`.
- If `evaluator/requirements_catalog_v1.md` is missing, first attempt to run `python3 tools/fetch_evaluator.py` from the repo root yourself. If you cannot run it or it fails, tell the user exactly what command to run, then retry.
- Outputs: `results/PLAN_EVAL.md` and `results/PLAN_EVAL_REPORT.html`

### 3. Re-render the Evaluation Report (Optional Fallback)

The user wants to regenerate the visual HTML report from an existing completed evaluation.

- Open and follow `3-PLAN_EVAL_REPORT.md` exactly.
- This requires an existing `results/PLAN_EVAL.md`.
- Output: `results/PLAN_EVAL_REPORT.html`

---

## Development Guidelines

These guidelines apply when the benchmark PRD asks you to plan or reason about code architecture.

This structure optimizes for testability and change isolation — small, focused units with clear boundaries.

### Fractal Architecture

**Pattern:** Pages contain Features, Features contain Sub-Features — each following the same structure.

- **Pages:** Top-level routes/screens
- **Features:** Distinct UI sections within a page (what you see on screen)
- **Sub-Features:** Nested functionality within a feature

Every feature is self-contained: its own hooks, utils, and child features live inside its directory.

### Directory Structure

**Naming Rule:** Avoid `index.tsx`. Main file matches directory name (`MyFeature/MyFeature.tsx`).

```
src/
├── config/          # Global constants & env vars
├── theme/           # Design tokens & styling
├── components/      # Shared UI primitives
├── hooks/           # Global hooks
├── utils/           # Global pure functions
└── pages/
    └── PageName/
        ├── PageName.tsx
        └── features/
            └── FeatureName/
                ├── FeatureName.tsx
                ├── hooks/
                ├── utils/
                └── features/
                    └── SubFeature/
                        ├── SubFeature.tsx
                        └── hooks/
```

### Code Standards

**Humble Components**
- TSX files contain markup and binding only
- Extract all logic to custom hooks: `const { data, handlers } = useFeatureLogic()`

**No Magic Numbers or Inline Styles**
- Constants go in `src/config/` or local `constants.ts`
- No hex codes, colors, or pixel values in TSX — reference theme tokens only
- Styling concerns live in the style system, not in markup

**Co-location**
- Feature-specific hooks/utils live inside that feature's directory
- If SubFeature is only used by Parent, it lives in `Parent/features/SubFeature/`

**Quality**
- Lint-clean code
- Unit tests for critical logic (adjacent to source files)
- Visual testing highly preferred where valid and protective
