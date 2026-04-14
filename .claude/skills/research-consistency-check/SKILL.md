---
name: research-consistency-check
description: Check consistency across research question, build plan, analysis plan, experiment log, results, and draft writing. Use this skill to detect mismatches, missing steps, weak traceability, and structural gaps in the research workflow.
---

# Research Consistency Check

## Purpose

This skill checks whether the project is internally consistent.

Its role is to answer questions like:

- Does the current work still match the research question?
- Do build and analysis steps match the stated plan?
- Are the results traceable to actual runs and inputs?
- Do outputs match the documented workflow?
- Is the manuscript draft aligned with the recorded work?

This is not just a code or model cross-check.
It is a project-level consistency and traceability check.

---

## When to Use

Use this skill when:

- A new build plan is written
- A new analysis plan is written
- A major experiment run has completed
- Results are being consolidated
- A manuscript section is drafted
- The workflow feels messy or inconsistent
- A checkpoint review is needed before progressing

Typical project timing:
- after build planning
- after analysis planning
- after important results
- before manuscript expansion
- before submission-stage review

---

## Inputs

Review as many of the following as are available:

- `README.md`
- `CLAUDE.md`
- `00_docs/00_research-plan/`
- `00_docs/01_build-plan/`
- `00_docs/02_analysis-plans/active/`
- `00_docs/03_experiment-log/`
- `00_docs/04_eda-reports/`
- `02_build/`
- `03_analysis/`
- `04_outputs/`
- `05_manuscript/`

The check should adapt to the current project stage.
Do not require late-stage materials at early stages.

---

## Outputs

Produce:

1. A summary of what was checked
2. A list of consistent elements
3. A list of gaps, mismatches, or ambiguities
4. A judgment of project readiness
5. A short prioritized fix list

Recommended save locations:

- `06_review/`
- or `00_docs/05_review-notes/`

Recommended filename pattern:

- `consistency_check_YYYY-MM-DD.md`

---

## Core Questions

This skill should check the following.

### A. Research Question Alignment
- Is the current build or analysis related to the stated question?
- Has scope drift occurred?
- Are extra tasks being done without documented reason?

### B. Data and Input Traceability
- Is it clear what input data was used?
- Is raw vs processed input distinguishable?
- Are important dataset assumptions documented?

### C. Build Consistency
- If build exists, does it match build planning?
- Are assembly/annotation decisions documented?
- Are QC expectations stated and reflected?

### D. Analysis Consistency
- Does the active analysis plan match the actual analysis work?
- Are analysis outputs traceable to specific inputs and runs?
- Are figures/tables aligned with actual documented results?

### E. Documentation Completeness
- Are important steps missing from experiment logs?
- Are outputs present without documentation?
- Are there plans without execution, or execution without plans?

### F. Writing Consistency
- If manuscript files exist, do they match documented methods and outputs?
- Do methods describe work that actually happened?
- Do results sections align with outputs and logs?
- Are there claims stronger than the available evidence?

---

## Workflow

### Step 1. Determine project stage
Classify the project roughly as:
- intake stage
- build stage
- analysis stage
- output consolidation stage
- manuscript stage

The check should be appropriate to the stage.

### Step 2. Review core documents
Inspect the relevant planning, logging, and output locations.

### Step 3. Compare intentions vs actions
Check:
- planned work
- performed work
- documented work
- written interpretation

Look for mismatches between them.

### Step 4. Identify missing links
Examples:
- output exists but no experiment log
- analysis exists but no plan
- manuscript methods mention undocumented parameters
- figures exist without clear source path
- build outputs exist without QC rationale

### Step 5. Produce a judgment
Use one of:
- PASS
- PASS WITH NOTES
- FAIL

Definitions:

- PASS: workflow is coherent and traceable enough to proceed
- PASS WITH NOTES: usable, but important cleanup is needed
- FAIL: major inconsistency prevents reliable progression

---

## Report Format

# Research Consistency Check

## Scope of Review
- what stage was reviewed
- what files/folders were checked

## Consistent Elements
- items that are aligned and traceable

## Gaps and Mismatches
- missing plans
- missing logs
- undocumented outputs
- unclear data provenance
- writing vs workflow mismatches

## Readiness Judgment
- PASS / PASS WITH NOTES / FAIL

## Priority Fixes
1. highest-priority issue
2. second-priority issue
3. third-priority issue

## Suggested Next Step
- proceed
- revise documentation
- rerun QC
- reorganize outputs
- rewrite part of the manuscript
- stop and repair traceability first

---

## Optional External Verification Mode

This skill may optionally include external verification if the project is configured to do so.

Possible external inputs:
- Codex-based review
- another model-based structural review
- lint-like workflow checks

If external verification is used:
- clearly separate external findings from final judgment
- do not let external output replace project-level reasoning
- final judgment should still reflect the project record

---

## Project Integration

Likely output destinations:
- `06_review/`
- `00_docs/05_review-notes/`

This skill supports:
- stage transitions
- project cleanup
- pre-manuscript checks
- pre-review checks

---

## Behavior Rules

- Check consistency relative to project stage
- Prefer traceability over verbosity
- Do not invent missing history
- State uncertainty where records are incomplete
- Distinguish documented facts from inferred workflow
- Focus on actionable corrections

---

## Customization Points

You may customize:
- whether to use external model verification
- how strict PASS vs FAIL should be
- whether missing logs are hard failures
- whether manuscript checks are included by default
- whether figure/output traceability is mandatory
- stage-specific required folders or files