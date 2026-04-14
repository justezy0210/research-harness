---
name: manuscript-review
description: Scientific manuscript reviewer for research-harness projects. Reviews manuscript drafts with mandatory literature search, competing work detection, internal data/value consistency checks, and prioritized revision guidance.
argument-hint: [manuscript_path] [research_field (optional)]
user-invocable: true
context: project
agent: general-purpose
allowed-tools: Read, Write, Edit, Glob, Grep, WebSearch, WebFetch
---

# Manuscript Review

## Purpose

Review a scientific manuscript draft as a constructive expert reviewer.

This skill is intended for the manuscript stage of the research harness and should help answer:

- Is the manuscript scientifically coherent?
- Are the claims supported by the available results?
- Is the literature framing up to date?
- Is there competing or overlapping work that should be acknowledged?
- Are numbers and values internally consistent across sections?
- What are the highest-priority revisions before the next draft or submission?

This skill is not only for writing quality.
It must also evaluate novelty framing, citation coverage, and numerical consistency.

---

## When to Use

Use this skill when:

- `05_manuscript/` contains a substantial draft
- methods, results, and discussion are present
- a pre-submission review is needed
- reviewer-style criticism is needed
- literature coverage needs updating
- internal consistency of values and claims must be checked

Typical project stage:
- after a substantial draft exists
- before submission-oriented revision
- after major result updates
- after new figures/tables are added

---

## Inputs

Primary manuscript inputs may include:

- `05_manuscript/outline.md`
- `05_manuscript/methods.md`
- `05_manuscript/results.md`
- `05_manuscript/discussion.md`
- a full draft if present

Supporting project materials may include:

- `04_outputs/figures/`
- `04_outputs/tables/`
- `04_outputs/final_datasets/`
- `00_docs/03_experiment-log/`
- `00_docs/02_analysis-plans/active/`
- `00_docs/00_research-plan/`

Use supporting materials when needed to verify whether manuscript claims are grounded in documented work.

---

## Outputs

Produce:

1. Executive summary
2. Impact-level recommendations
3. Literature search summary
4. Data/value consistency check
5. Detailed point-by-point review
6. Priority action list
7. Final constructive summary for authors

Recommended output location:
- `06_review/`

Recommended output filename:
- `{title}_from_reviewer.md`
- or `manuscript_review_YYYY-MM-DD.md`

---

## Workflow

### 1. Initial Assessment
Read the manuscript carefully and determine:

- research field
- specific topic
- main claim(s)
- methods used
- main conclusions
- current manuscript stage

Assess:
- overall structure
- clarity
- whether the argument flows logically
- whether the manuscript seems early, developing, or near-submission

---

### 2. Literature Search (CRITICAL)

Web-based literature review is mandatory unless the user explicitly disables it.

Use WebSearch / WebFetch to investigate:

- recent papers on the main topic
- prior art relevant to the main claim
- competing work with similar scope
- methodological references that should be cited
- recent studies that change context or interpretation

Example search patterns:

- `[main topic] [key method] recent research 2023 2024 2025 2026`
- `[specific finding] previous studies`
- `[technique used] [organism/system] published`
- `[organism] [phenomenon] recent review`
- `[key pipeline or method] benchmark paper`

Check for:

### Prior art
- similar studies that should be cited
- missing context in Introduction or Discussion

### Competing work
- very similar or overlapping studies
- possible novelty threats
- work that the authors must distinguish from their own

### Methodological references
- standard methods that need citations
- tools, algorithms, or QC methods lacking attribution

### Recent advances
- new findings that strengthen, weaken, or contextualize the manuscript

If strong overlap exists with recent work, state this clearly and explain how the authors might differentiate the manuscript.

---

### 3. Data / Value Consistency Check (CRITICAL)

Systematically verify numerical consistency across the manuscript and, when possible, against outputs.

Check:

### Cross-reference consistency
- Abstract vs Results
- Text vs Tables
- Text vs Figures
- Tables vs Figures
- Methods vs Results
- Manuscript claims vs project outputs

### Internal consistency
- sample sizes
- percentages summing appropriately
- means / ratios / derived values
- statistical values where reported
- decimal precision consistency
- naming consistency for groups, strains, samples, conditions

### Common problems to flag
- mismatched n values
- values copied incorrectly between sections
- wrong figure/table references
- percentages that do not add up
- claims unsupported by displayed values
- results described in text but absent from figure/table
- manuscript values not traceable to documented outputs

Where verification is incomplete because the manuscript lacks figures/tables or source materials, state the limitation explicitly.

---

### 4. Review Structure

Organize the review into the following levels.

#### A. Major Issues (Must Address)
Examples:
- unsupported central claim
- fundamental methodological concern
- severe literature gap
- novelty threat from competing work
- major inconsistency in reported values
- results that cannot be traced to documented analysis

#### B. Minor Issues (Should Address)
Examples:
- missing methodological detail
- clarity problems
- figure/table presentation issues
- incomplete discussion of limitations
- citation improvements
- terminology inconsistencies

#### C. Optional Enhancements
Examples:
- additional framing improvements
- future work suggestions
- alternative interpretations
- stronger organization or visual presentation

---

### 5. Impact-Level Guidance

Provide tiered recommendations.

Use this structure:

## Impact-Level Recommendations

### Current State Assessment
- Estimated impact level: [Low / Medium / High]
- Main strengths
- Main limitations

### To achieve MEDIUM impact
- specific requirements
- moderate revision needs

### To achieve HIGH impact
- everything needed for medium, plus stronger additions
- missing evidence or contextualization
- stronger framing or analysis needed

### To achieve TOP impact
- major additions required
- honest note if unrealistic given current scope

Do not inflate impact unrealistically.
Be honest but constructive.

---

### 6. Point-by-Point Review

Review by section where possible.

Suggested format:

## Detailed Review

### Abstract
- issue
- suggestion

### Introduction
- literature gap
- framing issue
- competing work issue
- recommendation

### Materials and Methods
- missing details
- unclear reproducibility point
- missing citation

### Results
- unsupported statement
- weak figure linkage
- numerical inconsistency
- interpretation issue

### Discussion
- overclaim
- missing comparison with literature
- missing limitation
- recommendation

Where line or paragraph references are possible, include them.

---

### 7. Literature Findings Report

Document the literature review separately.

Use this structure:

## Literature Search Summary

### Papers That Should Be Cited
| Reference | Relevance | Suggested Section |

### Potentially Competing Work
| Reference | Overlap | Recommendation |

### Recent Advances to Consider
| Reference | Finding | Impact on This Work |

Do not merely list papers.
Explain why each matters to this manuscript.

---

### 8. Data Consistency Report

Use a dedicated section.

## Data Consistency Check

### Inconsistencies Found
| Location 1 | Value | Location 2 | Value | Issue |

### Verified Consistent
- list key values checked and found consistent

Where only partial checking was possible, state that clearly.

---

### 9. Author-Friendly Summary

End with a constructive summary.

Include:

## Summary for Authors

### Overall Assessment
- 2–3 sentences on contribution and current state

### Priority Actions
1. highest-priority revision
2. second-priority revision
3. third-priority revision

### What Works Well
- positive aspect 1
- positive aspect 2

### Encouragement
- constructive closing message

---

## Output File Format

Generate a reviewer report in markdown with the following structure:

# Reviewer Report: [Manuscript Title]

**Review Date:** [Date]  
**Manuscript:** [Filename]  
**Field:** [Research field]

---

## Executive Summary

## Impact-Level Recommendations

## Literature Search Summary

## Data Consistency Check

## Detailed Point-by-Point Review

## Priority Action List

## Conclusion

Save the report under:
- `06_review/`

---

## Project Integration

Primary manuscript source:
- `05_manuscript/`

Useful supporting sources:
- `04_outputs/`
- `00_docs/03_experiment-log/`
- `00_docs/02_analysis-plans/active/`

Default report destination:
- `06_review/`

This skill is best used after:
- figures/tables are reasonably stable
- methods and results drafts exist
- the manuscript is ready for critical review

---

## Review Principles

1. Be constructive
2. Be specific
3. Be realistic about effort
4. Be fair about strengths and limitations
5. Be thorough in literature checking
6. Be honest about impact and novelty
7. Distinguish writing problems from scientific problems
8. Distinguish confirmed inconsistencies from suspected ones

---

## Red Flags to Watch For

- claims without supporting data
- missing statistical analyses
- inappropriate controls
- overgeneralization
- weak novelty relative to competing work
- excessive citation gaps
- missing ethics or availability statements where relevant
- numerical inconsistencies across sections
- incorrect derived values
- unexplained sample size changes
- figure/table references that do not match the text

---

## Customization Points

You may customize:

- how aggressive the novelty / competing-work warning should be
- whether literature search is always mandatory or stage-dependent
- whether value consistency checking should be strict or moderate
- whether impact-tier guidance should be included every time
- whether the tone should resemble peer review or internal lab review
- whether output should prioritize section-by-section comments or top-priority issues first