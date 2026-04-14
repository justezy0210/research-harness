---
name: data-intake-review
description: Analyze a scientific data file or dataset to understand its structure, quality, metadata, and suitability for downstream analysis. Best used at data intake before build or analysis planning.
---

# Exploratory Data Analysis

## Purpose

This skill performs initial exploratory analysis on scientific data files and datasets.

It should help answer the following questions:

- What kind of file or dataset is this?
- What does it contain?
- Is the data complete and usable?
- Are there quality issues or structural problems?
- What downstream analysis would make sense?
- What should be documented before moving into build or analysis?

This skill is intended to support the research harness workflow at the **data intake stage**.

---

## When to Use

Use this skill when:

- New raw or processed data arrives
- A file format is unfamiliar or needs confirmation
- A dataset should be inspected before writing a build plan
- A dataset should be inspected before writing an analysis plan
- Data quality, completeness, or metadata should be checked
- A markdown EDA report should be generated for project records

Typical stage in workflow:

1. Data arrives in `01_data/raw/` or `01_data/processed/`
2. Run this skill
3. Save findings to `00_docs/eda-reports/`
4. Use the report to inform build or analysis planning

---

## Expected Inputs

Possible inputs include:

- A path to a file
- A path to a dataset directory
- A short description of the file
- A research context describing how the file may be used

Examples:
- FASTQ / FASTA
- BAM / VCF
- GFF / GTF
- CSV / TSV / Excel
- count matrix
- h5ad / loom
- image files
- general scientific tabular or array data

---

## Expected Outputs

This skill should produce:

1. A concise understanding of file type and content
2. A quality and completeness assessment
3. A summary of important metadata
4. Suggestions for preprocessing or validation
5. Recommendations for downstream use
6. A markdown report suitable for saving in:
   - `00_docs/eda-reports/`

Recommended output filename pattern:

- `{input_name}_eda_report.md`

---

## Core Workflow

### Step 1. Identify the input

Determine whether the input is:

- a single file
- a directory of files
- a structured dataset
- an unknown scientific artifact

Record:
- file name
- extension
- file size
- path
- whether it appears raw or processed

---

### Step 2. Detect format and category

Infer the likely format and scientific category.

Possible categories include:

- sequencing / genomics
- annotation
- tabular metadata
- expression matrix
- image / microscopy
- spectroscopy / omics
- generic scientific array or table

If the format is uncertain:
- state uncertainty clearly
- perform generic inspection
- avoid overclaiming format-specific interpretation

---

### Step 3. Inspect structure and metadata

Check what the file contains.

Examples:
- number of rows / columns
- number of sequences
- sequence lengths
- quality score availability
- feature counts
- sample identifiers
- metadata fields
- dimensionality
- channel / time / spatial information for images
- annotation fields for GFF/GTF-like data

At this stage, prioritize:
- structure
- integrity
- completeness
- obvious inconsistencies

---

### Step 4. Assess quality

Look for issues such as:

- missing values
- malformed records
- duplicated identifiers
- inconsistent naming
- suspiciously small or empty files
- missing metadata
- extreme imbalance in values
- format compliance problems
- unexpected dimensionality

For sequence or omics data, include relevant quality indicators where possible.

Do not force domain-specific QC if the file does not support it.

---

### Step 5. Summarize downstream implications

Explain what this dataset appears suitable for.

Examples:
- assembly input
- annotation input
- comparative analysis
- variant analysis
- expression analysis
- metadata integration
- figure generation
- manuscript methods documentation

Also note what must happen before downstream use, such as:
- cleaning
- renaming
- validation
- normalization
- deduplication
- format conversion

---

### Step 6. Generate a markdown report

Generate a report with the following structure.

# EDA Report: [File or Dataset Name]

## Basic Information
- path
- detected type
- likely category
- file size
- timestamp

## Structural Summary
- main dimensions or counts
- important fields or records
- metadata summary

## Quality Assessment
- missingness
- integrity issues
- anomalies
- uncertainty

## Key Findings
- what stands out
- what is usable
- what is risky

## Recommendations
- immediate preprocessing steps
- suitable downstream analyses
- documentation that should be updated next

## Suggested Next Step
- write build plan
- write analysis plan
- collect missing metadata
- rerun QC
- archive or exclude unusable input

Save the report under:
- `00_docs/eda-reports/`

---

## Behavior Rules

- Be conservative when the format is uncertain
- Prefer clear description over aggressive interpretation
- Distinguish observed facts from inferred meaning
- Focus on helping the next research step
- Keep the report useful for later manuscript writing
- Do not assume every dataset requires the same QC logic
- For large files, sample where necessary and state that sampling was used

---

## Research Harness Integration

This skill supports the following folders:

- input from:
  - `01_data/raw/`
  - `01_data/processed/`

- report output to:
  - `00_docs/eda-reports/`

- informs:
  - `00_docs/build-plan/`
  - `00_docs/analysis-plans/active/`
  - `00_docs/experiment-log/`

This skill should usually run **before** major build or downstream analysis begins.

---

## Customization Points

You may customize this skill in the following ways.

### A. Restrict supported formats
You may narrow the scope to only:
- bioinformatics formats
- tabular research data
- genomics + annotation files

### B. Change reporting style
You may prefer:
- very short intake memo
- full markdown audit report
- QC-heavy report
- downstream-analysis recommendation report

### C. Add lab-specific rules
Examples:
- require sample ID format checks
- require species name validation
- require metadata completeness threshold
- require sequencing platform notes

### D. Add project-specific outputs
Examples:
- always generate a "next action" section
- always suggest one build path and one analysis path
- always include manuscript-relevant notes

---

## Minimal Decision Logic

Use this skill in the following way:

- New file arrives → run EDA
- File looks usable → write build or analysis plan
- File has major issues → document problem before proceeding
- File type uncertain → produce cautious structural report, not strong biological claims