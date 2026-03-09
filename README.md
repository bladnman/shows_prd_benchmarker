# Planning Benchmark

Benchmark how well coding agents plan against a real product spec. Feed it a PRD, get a plan, evaluate coverage, and generate a stakeholder-ready report.

## What This Repo Does

There is a product requirements document (PRD) in `docs/prd/`. You point a coding agent at it and ask it to produce an implementation plan. Then you evaluate how well that plan covers the PRD and generate the stakeholder report from that evaluation.

The default collection flow is now two steps. You run each step in a **fresh conversation** with the best model available.

## The Two-Step Default Workflow

### Step 1: Generate the Plan

Open a fresh conversation with your coding agent. Tell it:

> Read `1-START_HERE.md` and follow its instructions.

The agent will read all the PRD documents in `docs/prd/` and produce an implementation plan. Step 1 is planning only; it must not start implementation.

**Output:** `results/PLAN.md`

### Step 2: Evaluate the Plan

Open a **new conversation** (fresh context). Tell the agent:

> Read `2-EVALUATE_PLAN.md` and follow its instructions.

The agent will read both the PRD and the plan from Step 1, then audit the plan for coverage and alignment. It scores every requirement as full, partial, or missing, writes `PLAN_EVAL.md`, and then generates `PLAN_EVAL_REPORT.html` from that finished evaluation.
The denominator is frozen in `evaluator/requirements_catalog_v1.md`, so the evaluator scores against the same requirement list every run instead of re-deriving it from scratch.
If the `evaluator/` folder is missing, the Step 2 agent should first attempt to run `python3 tools/fetch_evaluator.py`. If the agent cannot do that, run it manually and retry Step 2.

**Requires:** `results/PLAN.md` from Step 1
**Primary output:** `results/PLAN_EVAL.md`
**Secondary output:** `results/PLAN_EVAL_REPORT.html`
**Derived output:** `results/PLAN_EVAL_DATA.json` (generated deterministically from the markdown evaluation by the control workflow)

For a finished benchmark submission, `results/PLAN_EVAL_REPORT.html` is still expected. It is now normally produced during Step 2.

## Optional Fallback

If `results/PLAN_EVAL.md` already exists and you only need to re-render the HTML report, you can still use the standalone report prompt:

> Read `3-PLAN_EVAL_REPORT.md` and follow its instructions.

## Why Fresh Conversations?

Each step consumes significant context. Starting fresh ensures the agent has maximum context window available for the task at hand. It also isolates each step so you can re-run one without re-running the others.

## Repo Structure

```
1-START_HERE.md              # Step 1 prompt — planning
2-EVALUATE_PLAN.md           # Step 2 prompt — evaluation
3-PLAN_EVAL_REPORT.md        # Optional fallback prompt — HTML report rerender only
docs/prd/                    # The product spec (PRD + supporting docs)
evaluator/requirements_catalog_v1.md  # Frozen Step 2 denominator, fetched on demand
tools/fetch_evaluator.py     # Downloads the public evaluator bundle into evaluator/
results/                     # All outputs land here
CLAUDE.md                    # Auto-loaded instructions for Claude Code
GEMINI.md                    # Auto-loaded instructions for Gemini
AGENTS.md                    # Auto-loaded instructions for other agents
INSTRUCTIONS.md              # Development guidelines (referenced by agent configs)
```

## Result Artifacts

Each completed run should end with these files in `results/`:

- `PLAN.md` — the implementation plan from Step 1
- `PLAN_EVAL.md` — the human-readable evaluation from Step 2
- `PLAN_EVAL_DATA.json` — the structured evaluation data derived from `PLAN_EVAL.md` by the control workflow
- `run_metadata.json` — structured run metadata captured by the control workflow, including series/case identity, declared scenario settings, observed timing/tool metrics, and plan-save outcome
- `PLAN_EVAL_REPORT.html` — the stakeholder-facing report normally generated during Step 2
