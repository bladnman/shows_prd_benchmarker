# PLAN EVALUATION

This evaluation step is not used until after an entire plan has been written.

## PRD Info

The PRD is multiple files. All files are very important. You will find the PRD files in the `docs/prd/` folder. Start with `docs/prd/product_prd.md`, then read `docs/prd/infra_rider_prd.md`, then read all files under `docs/prd/supporting_docs/` recursively, including `docs/prd/supporting_docs/technical_docs/`. For evaluation purposes, all PRD files must be ingested to fully understand the scope of the request itself.

This benchmark version also has a frozen canonical requirement catalog at `evaluator/requirements_catalog_v1.md`. That catalog is the scoring denominator for this PRD version. It freezes requirement IDs, functional areas, labels, source citations, and severity tiers while staying outside `docs/prd/` so Step 1 does not see evaluator-only material.

If `evaluator/requirements_catalog_v1.md` is missing, first attempt to run `python3 tools/fetch_evaluator.py` from the repo root yourself. If you cannot run shell commands or the fetch fails, stop and tell the user exactly to run `python3 tools/fetch_evaluator.py` from the repo root before retrying Step 2. Do not try to reconstruct the catalog yourself.

## Instructions

Using the canonical requirement catalog as the denominator and the original PRD as the semantic source of truth, audit the plan found in the `results/` folder for coverage and alignment. The plan is called `PLAN.md`.

Before you write any files, create an internal checklist and complete it in this exact order:
1. Read `evaluator/requirements_catalog_v1.md`.
2. Read the PRD files to understand the semantics behind the catalog requirements.
3. Read `results/PLAN.md`.
4. Write the full markdown evaluation to `results/PLAN_EVAL.md`.
5. Re-open or re-read the completed `results/PLAN_EVAL.md`.
6. Generate the stakeholder report `results/PLAN_EVAL_REPORT.html` from that completed markdown evaluation.

Do **not** skip or reorder these phases. Do **not** start the HTML report until `results/PLAN_EVAL.md` is complete.

The markdown evaluation output MUST follow this exact structure, in this order:

### 1. Requirements Extraction

Do **not** perform a fresh requirement extraction for this benchmark version. The canonical requirement catalog already contains the approved denominator. Your job in this section is to reproduce that catalog exactly so the coverage table scores against the same requirement set every run.

#### Pass 1: Identify Functional Areas

Use the exact functional area taxonomy, in the exact order, from `evaluator/requirements_catalog_v1.md`:

1. Benchmark Runtime & Isolation
2. Collection Data & Persistence
3. App Navigation & Discover Shell
4. Collection Home & Search
5. Show Detail & Relationship UX
6. Ask Chat
7. Concepts, Explore Similar & Alchemy
8. AI Voice, Persona & Quality
9. Person Detail
10. Settings & Export

Do not create, rename, merge, split, or reorder areas.

#### Pass 2: Extract Requirements Within Each Area

Copy the requirements from `evaluator/requirements_catalog_v1.md` exactly.

The catalog is already the result of the benchmark's merge/split decisions. Preserve it exactly:

- Preserve every requirement ID, area, label, source citation, severity tier, and ordering.
- Do not add, remove, merge, split, rename, paraphrase, or renumber requirements.
- Do not rewrite labels or source citations.
- The final total line at the end of this section must match the catalog exactly.
- Use the PRD files to understand what each catalog requirement means and how strictly to score the plan against it.
- If you notice a discrepancy between the PRD and the catalog, do not change the denominator. Score against the catalog as written and note the discrepancy only if it materially affects your confidence in the evaluation.

**Output format for this section:**

Group requirements by functional area. Under each area heading, list requirements as:

```
- PRD-001 | `critical` | Label here | `source_file.md > Section Name`
- PRD-002 | `important` | Label here | `source_file.md > Section Name`
```

After all areas, include a summary line:

```
Total: N requirements (X critical, Y important, Z detail) across M functional areas
```

### 2. Coverage Table

Evaluate the plan against each requirement you extracted.

Output a markdown table with exactly these columns:

| PRD-ID | Requirement | Severity | Coverage | Evidence | Gap |
| ------ | ----------- | -------- | -------- | -------- | --- |

- **PRD-ID**: The ID from your extraction above.
- **Requirement**: The short label (8–12 words).
- **Severity**: The severity tier from your extraction (`critical`, `important`, or `detail`).
- **Coverage**: Exactly one of: `full`, `partial`, `missing`.
  - `full` — The plan explicitly addresses this with a concrete task or section. You can point to it.
  - `partial` — The plan touches on it but lacks specificity, only addresses part of it, or handles it by implication rather than directly.
  - `missing` — The plan does not address this at all.
- **Evidence**: Cite the specific section name, task ID, or short quote from the plan that addresses it. If `missing`, write `none`.
- **Gap**: If `partial` or `missing`, one sentence explaining what's lacking. If `full`, leave blank.

### 3. Coverage Scores

Calculate scores at three levels. Show the math for each.

**Overall score:**

```
score = (full_count × 1.0 + partial_count × 0.5) / total_count × 100
```

**Score by severity tier:**

Calculate the same formula separately for `critical`, `important`, and `detail` requirements. Display as:

```
Critical:  (full × 1.0 + partial × 0.5) / critical_total × 100 = ___%  (n of N critical requirements)
Important: (full × 1.0 + partial × 0.5) / important_total × 100 = ___%  (n of N important requirements)
Detail:    (full × 1.0 + partial × 0.5) / detail_total × 100 = ___%  (n of N detail requirements)
Overall:   ___% (N total requirements)
```

### 4. Top Gaps

List the **top 5 gaps** (or fewer if there aren't 5), ranked by severity tier first (critical before important before detail), then by impact within tier. For each gap:

- State the PRD-ID, severity, and requirement label.
- Explain why this gap matters (what breaks or degrades without it).

### 5. Coverage Narrative

Write five short sub-sections that a human reader can use to understand the coverage posture without reading the table. Use these exact subheadings, in this exact order:

#### Overall Posture

In plain language, how ready is this plan? Is it a strong plan with minor gaps, a structurally sound plan with concerning holes, or a plan that misses fundamental requirements?

#### Strength Clusters

Where is the plan strongest? Which areas of the PRD are thoroughly and concretely covered? Name the functional areas, not just PRD-IDs.

#### Weakness Clusters

Where do gaps concentrate? Are the partial/missing items scattered randomly, or do they cluster around a specific functional area, a specific type of requirement, or a specific severity tier? Name the pattern.

#### Risk Assessment

If this plan were executed as-is without addressing any gaps, what is the most likely failure mode? What would a user, stakeholder, or QA reviewer notice first? Be specific.

#### Remediation Guidance

For the weakness clusters you identified, what category of work is needed — more detailed specification, architectural decisions, missing acceptance criteria, or entirely new plan sections? This is not a task list; it is guidance on what kind of planning work remains.

## Stakeholder Report

After `results/PLAN_EVAL.md` is complete, generate a single-file HTML page at `results/PLAN_EVAL_REPORT.html`.

Treat `results/PLAN_EVAL.md` as the fixed source of truth for requirements, scores, and gaps.

During the report phase:
- Do not reopen the PRD.
- Do not recompute the denominator.
- Do not reinterpret coverage from scratch.
- Do not change requirement IDs, totals, or scores in the report.
- If you revise `results/PLAN_EVAL.md` after starting the report, regenerate the report from the revised markdown.

Audience: A product lead or VP who needs to understand in under 60 seconds — what does this plan cover well, where are the risks, and how confident should they be in this plan's readiness?
The page must communicate ALL of the following:
1. The overall coverage score — make it prominent and immediately legible.
2. The before/after arc — show how coverage changed from the initial plan to the revised plan. This is the narrative spine: "we started here, we identified gaps, we improved to here."
3. What's strong — which areas of the PRD are well-covered? Give stakeholders confidence about what IS handled.
4. What's at risk — which requirements are still partial or missing after revision? Don't bury this. Stakeholders need to see the risks, not hunt for them.
5. The top gaps and why they matter — not just that something is missing, but what breaks or degrades without it.

Design guidance:
- This should feel like a stakeholder-ready dashboard or briefing page, not a raw data dump.
- You have full creative freedom on layout, visual style, chart types, color palette, typography, and how you organize the narrative. Make it yours.
- Prioritize visual hierarchy — the most important information should hit first.
- Think about how you'd want to present this in a meeting. What do you lead with? What's the flow?
- No external dependencies (no CDN links). Everything self-contained.
- Should look polished at 1200px wide (screenshot-ready for video).

Do not just render the coverage table with colored rows and call it done. Tell the story.

## Hard Rules

- Be honest. Do not inflate coverage. If something is only covered by implication or vague language, it is `partial`, not `full`.
- `evaluator/requirements_catalog_v1.md` is the authoritative denominator for this benchmark version.
- Do not invent requirements, delete requirements, or modify the catalog's IDs, areas, labels, sources, severity tiers, or ordering.
- Do not skip requirements because they seem minor — include every requirement in the table and let the scoring formula do its job.
- Use the exact table formats above. Do not add, remove, or rename columns.
- Use exactly the words `full`, `partial`, or `missing` for Coverage — no other labels.
- Use exactly the words `critical`, `important`, or `detail` for Severity — no other labels.
- Use the exact functional area names listed in Pass 1. Do not invent replacements or aliases.
- Use the exact five Coverage Narrative subheadings listed above. Do not rename them or collapse them into freeform paragraphs.
- The catalog rule is binding. If you disagree with the denominator, do not change it in the evaluation output.
- The Coverage Narrative must not merely restate the table data. It must synthesize and interpret. Saying "6 items are partial" is restating; saying "the partial items cluster around AI behavioral contracts, suggesting the plan treats AI as an implementation detail rather than a specifiable surface" is interpreting.
- Complete `results/PLAN_EVAL.md` before starting `results/PLAN_EVAL_REPORT.html`.
- During report generation, `results/PLAN_EVAL.md` is the only scoring source of truth.

## Output Locations

Write the full human-readable evaluation to: `results/PLAN_EVAL.md`

Do **not** append JSON, extra sections, or machine-readable blobs to this markdown file. The benchmark pipeline derives `results/PLAN_EVAL_DATA.json` deterministically from `results/PLAN_EVAL.md` after this step completes, so the markdown structure above must remain exact and parseable.

After the markdown evaluation is complete, write the stakeholder-ready HTML report to: `results/PLAN_EVAL_REPORT.html`
