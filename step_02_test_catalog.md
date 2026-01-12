# Step 02 — Test Catalog & Conditions Definition

## Project
**CSLI — Context-Stable LLM Integration**

---

## Purpose of Step 02
The purpose of this step is to **define, document, and freeze** the experimental foundation of CSLI by specifying:

- a fixed catalog of **13 test scenarios**
- a fixed set of **execution conditions**

These definitions apply uniformly across all CSLI integration phases (A/B/C) and ensure that experimental results remain comparable and reproducible.

No implementation or evaluation is performed in this step.

---

## Role of the Test Catalog
The test catalog represents the **experimental constant** of CSLI.

Across all integration phases:
- the same tests,
- executed under the same conditions,
- using the same prompt and context rules

This guarantees that observed differences are attributable to **integration effects**, not to changes in test design.

---

## Test Catalog (Final, Frozen)

Each test represents a **realistic field-support scenario** relevant to mobile or infrastructure-related operations.  
Tests are **scenario-centric**, not modality-centric.

| Test-ID | Title | Description | Primary Focus |
|-------|------|-------------|---------------|
| **T01** | Text Only | Pure text-based query without additional context or media | Text understanding |
| **T02** | Image Only | Single image without textual or contextual information | Image understanding |
| **T03** | Audio Only | Audio input without manual transcription | Audio understanding |
| **T04** | Text + Image | Text prompt combined with an image | Multimodal fusion |
| **T05** | Image + Location Context | Image combined with GPS/location data | Context utilization |
| **T06** | Text + Time & Device Context | Text input with time and device metadata | Device/time awareness |
| **T07** | Text + Image + Full Context | Multimodal input with full mobile context (location, time, network) | Real-world scenario |
| **T08** | QR / Barcode Interpretation | QR code or barcode provided as image or string | Structured data interpretation |
| **T09** | Video Only | Video input without preprocessing | Video understanding |
| **T10** | Misleading Context | Correct media combined with intentionally false context | Context robustness |
| **T11** | Prompt Variation | Semantically identical prompts with different formulations | Prompt sensitivity |
| **T12** | Corrupted Input | Partially corrupted or invalid media input | Error robustness |
| **T13** | Context Boundary Case | Reserved test for context or modality edge cases | Context limits |

---

## Condition Definition

### Purpose of Conditions
Conditions define **how** a test is executed with respect to:
- input modalities
- availability of structured contextual information

They enable controlled comparison of context enrichment effects.

---

### Condition Dimensions

**Dimension A — Input Modality**
- Text
- Image
- Audio
- Video

**Dimension B — Context Availability**
- No structured context
- Structured context enabled

---

### Global Condition Set (Fixed)

| Condition-ID | Modalities | Structured Context |
|-------------|------------|--------------------|
| **C1** | Text | No |
| **C2** | Text | Yes |
| **C3** | Image | No |
| **C4** | Image | Yes |
| **C5** | Text + Image | No |
| **C6** | Text + Image | Yes |
| **C7** | Audio | No |
| **C8** | Audio | Yes |
| **C9** | Video | No |
| **C10** | Video | Yes |

This condition set is **global** and applies uniformly to all tests.

---

## Test–Condition Execution Rules

- Each test must be executed under **all logically applicable conditions**
- If a condition is not applicable to a test, it is marked as **NA (Not Applicable)**
- Conditions themselves are **never modified, removed, or customized per test**

A single experimental run is uniquely identified by the pair:
'(test_id, condition_id)'

---

## Freeze Rules
After completion of Step 02, the following rules apply:

- No new tests may be added
- No tests may be removed
- No test descriptions may be semantically altered
- No new conditions may be added
- No condition definitions may be changed

Only editorial clarifications without semantic impact are permitted.

---

## Scope of Step 02

### In Scope
- Definition of the 13-test catalog
- Definition of the global condition set
- Identification and naming rules
- Freeze rules for tests and conditions

### Out of Scope
- Implementation of tests or conditions
- Automation or execution logic
- Evaluation metrics or scoring
- Interpretation of model outputs

---

## Definition of Done (Step 02)
Step 02 is considered complete when:

- all 13 tests are defined and documented
- the global condition set is finalized
- execution and freeze rules are defined
- this document is committed to the repository

---

## Status
**Step 02: Completed**
