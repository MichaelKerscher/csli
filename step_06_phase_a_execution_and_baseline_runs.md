# Step 06 — Phase A Execution & Baseline Runs

## Project
**CSLI — Context-Stable LLM Integration**

---

## Purpose of Step 06
Step 06 executes **Phase A (Baseline)** of the CSLI evaluation.  
Its purpose is to establish a **stable, reproducible reference point** for all later experimental phases by running the full **test catalog** under **baseline conditions**, without any CSLI-specific interventions.

This step answers the question:

> *How does the system behave without context-stability mechanisms?*

All subsequent improvements (Phase B+) are measured **relative to these baseline runs**.

---

## Position in the Overall Methodology
Phase A is the **first execution phase** after all design decisions have been frozen:

- Step 02: Test catalog & conditions defined  
- Step 03: Instrumentation & logging fixed  
- Step 04: CSLI mechanisms specified  
- Step 05: Execution environment prepared  
➡ **Step 06: Baseline execution**

No experimental parameters may be changed after this step.


::contentReference[oaicite:0]{index=0}


---

## Definition of “Baseline”
A **baseline run** is defined as:

- identical prompts and inputs as defined in Step 02
- identical execution environment as defined in Step 05
- **no CSLI mechanisms applied**, specifically:
  - no context freezing
  - no context window normalization
  - no retrieval control beyond default system behavior
  - no memory or state stabilization
- default model behavior only

The baseline therefore reflects **typical real-world LLM usage**.

---

## Scope of Phase A
Phase A covers **all test scenarios** defined in the frozen test catalog.

| Dimension            | Scope                         |
|---------------------|-------------------------------|
| Test scenarios      | All 12 scenarios              |
| Prompt variants     | As defined in Step 02         |
| Runs per scenario   | ≥ 3 (minimum for variance)   |
| Total baseline runs | ≥ 36 executions               |
| Context resets      | Before *every* run            |

---

## Execution Procedure

### 1. Pre-Run Validation
Before executing Phase A, the following must be verified:

- test catalog hash unchanged  
- model version unchanged  
- temperature, top-p, max tokens unchanged  
- retrieval configuration unchanged  
- logging active and timestamped  

Any deviation invalidates the baseline.

---

### 2. Execution Loop
For each test scenario:

1. Reset conversation context
2. Inject test prompt exactly as specified
3. Execute the prompt
4. Capture:
   - full prompt
   - retrieved context (if applicable)
   - model output
   - metadata (latency, token counts, errors)
5. Repeat for all defined repetitions

No manual intervention is allowed during execution.

---

### 3. Data Recording
Each baseline run produces one immutable record containing:

- scenario ID
- run ID
- timestamp
- input prompt
- system configuration snapshot
- raw model output
- retrieval traces (if available)

All records are stored **append-only**.

---

## Quality Assurance Rules
To ensure scientific validity:

- No prompt tuning between runs
- No cherry-picking outputs
- No retries unless system failure occurred
- Failures are logged, not corrected
- Ambiguous outputs are preserved as-is

Baseline data must reflect **actual system behavior**, not ideal behavior.

---

## Expected Observations (Hypothesis-Neutral)
Phase A does **not** aim to prove improvement.  
Typical baseline characteristics include:

- output variability across runs
- sensitivity to prompt phrasing
- occasional context drift
- inconsistent grounding depth
- non-deterministic reasoning paths

These effects are **not flaws**—they are the reference condition.

---

## Outputs of Step 06
At completion, Step 06 produces:

1. **Baseline Execution Dataset**
2. **Execution Log Summary**
3. **Configuration Lock Confirmation**
4. **Phase A Completion Marker**

