# Step 03 — Logging, Run Management & Reproducibility Rules

## Project
**CSLI — Context-Stable LLM Integration**

---

## Purpose of Step 03
The purpose of this step is to formally define:

- a uniform **run identification scheme**
- a fixed **logging schema** for all executions
- **reproducibility rules** across integration phases A/B/C
- **equivalence rules** defining what must remain identical and what may vary

This step ensures that all test executions are traceable, comparable, and reproducible across the complete CSLI integration pipeline.

No technical implementation is performed in this step.

---

## Definition of a Run
A **run** represents a single execution of a specific test under a specific condition.

Each run is uniquely identified by the tuple:
`(test_id, condition_id, run_id)`

---

## Integration Phase Label
Each run must explicitly record the integration phase in which it was executed:

- **Phase A** — CLI → 506.ai  
- **Phase B** — CLI → Backend → 506.ai  
- **Phase C** — App → Backend → 506.ai  

The phase label is mandatory for every run.

---

## Run Identification Scheme

### Requirements
A run identifier (`run_id`) must:
- be globally unique
- be independent of provider output
- allow temporal ordering

### Format (Specification)
The recommended format is:
`<timestamp>_<randomSuffix>`  
  
Example: `2026-01-12T14-22-31Z_a8f3`  


The exact generation mechanism is implementation-specific, but the format must be preserved.

---

## CSLI Logging Schema

### Goal
The logging schema must enable:
- full traceability of inputs and outputs
- reconstruction of the executed request
- comparison across phases A/B/C

Each run produces exactly **one log record**.

---

### Required Log Fields
The following fields **must be present in every log entry**.

#### Identification & Metadata
- `run_id`
- `timestamp_utc`
- `phase`
- `test_id`
- `condition_id`

#### Provider Execution
- `provider` (e.g. `506ai`)
- `provider_endpoint` (e.g. `chatNoStream`, `chatReferences`)
- `model`

#### Input Package
- `input.modality`
- `input.user_text`
- `input.media` (list, may be empty)
- `input.context` (object, may be empty)

#### Prompt Construction
- `prompt.template_id`
- `prompt.template_version`
- `prompt.rendered_prompt`  
  *(or a rendered message array, if applicable)*

#### Output Package
- `output.response_text`
- `output.references` (empty if not provided)

#### Status
- `status` (`success` or `error`)
- `error.message` (required if `status = error`)

---

### Optional Log Fields
The following fields may be logged if available without additional engineering effort:

- `output.raw_response`
- `output.response_language`
- `provider_request_id`
- `meta.notes`
- `meta.retry_count`

---

### Explicitly Excluded Metrics
The following metrics are **not required** for CSLI and must not be used for evaluation:

- latency
- performance
- token usage
- cost estimation

They may be logged optionally but are out of scope for CSLI analysis.

---

## Media Logging Rules (Public Repository Constraint)

### Rule
Because the repository is public:

- raw media files (images, audio, video) must **not** be stored in logs
- logs may reference media only via non-sensitive identifiers

### Required Media Fields
For each referenced media item:
- `media.type` (`image`, `audio`, `video`)
- `media.name` (non-sensitive label)
- `media.source` (`local`, `uploaded`)
- `media.hash` (optional, recommended)

---

## Reproducibility Rules

### Fixed Inputs Rule
For a given `(test_id, condition_id)`, the following must remain **identical across phases A/B/C**:

- user text content (semantic equivalence)
- context structure and values
- referenced media identifiers
- prompt template ID and version
- condition definition

---

### Prompt Drift Prevention
Prompt construction must not drift between integration phases.

Therefore:
- every prompt template is versioned
- any change to prompt structure or context formatting requires:
  - incrementing `template_version`
  - documenting the change in a short changelog

---

### Provider Variability
Variations in LLM output are expected due to stochastic generation.

This is acceptable provided that:
- all inputs and rendered prompts are logged
- the run remains fully traceable

---

## Equivalence Rules

### Must Be Identical
- `test_id`
- `condition_id`
- input content (text, context, media identifiers)
- `prompt.template_id`
- `prompt.template_version`
- `prompt.rendered_prompt`
- provider endpoint selection (if fixed)

### May Vary
- output wording and length
- formatting and structure of the response
- presence or absence of references
- provider-internal identifiers

---

## Artifact Organization
Run logs must be stored in a structured and phase-separated directory layout.

Recommended structure:
results/  
├─ phase-A/  
│  └─ &lt;date&gt;/  
│     └─ &lt;test_id&gt;/  
│        └─ &lt;condition_id&gt;_&lt;run_id&gt;.json  
├─ phase-B/  
│  └─ &lt;date&gt;/  
│     └─ &lt;test_id&gt;/  
│        └─ &lt;condition_id&gt;_&lt;run_id&gt;.json  
└─ phase-C/  
   └─ &lt;date&gt;/  
      └─ &lt;test_id&gt;/  
         └─ &lt;condition_id&gt;_&lt;run_id&gt;.json  



This structure supports traceability and later cross-phase comparison.

---

## Definition of Done (Step 03)
Step 03 is considered complete when:

- the run identification scheme is fixed
- the CSLI logging schema is fully defined
- reproducibility rules across phases A/B/C are defined
- equivalence rules are documented
- media handling rules for a public repository are defined
- this document is committed to the repository

---

## Status
**Step 03: Completed**
