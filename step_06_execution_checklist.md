# Step 06 — Phase A Execution Checklist (Baseline)

## Project
**CSLI — Context-Stable LLM Integration**

## Purpose
This checklist defines the **mandatory operational steps** required to
execute **Phase A (Baseline Runs)** in a reproducible and scientifically
valid manner.

Completion of this checklist is required before proceeding to Step 07.

---

## 1. Pre-Execution Freeze Confirmation

The following elements MUST be frozen and unchanged:

- [ ] Test catalog (Step 02) finalized and versioned
- [ ] Execution environment (Step 05) finalized
- [ ] Model provider and model version fixed
- [ ] Region / deployment location fixed
- [ ] Inference parameters frozen:
  - temperature
  - top-p
  - max tokens
- [ ] Retrieval configuration frozen (if applicable)
- [ ] Logging format and storage location fixed

❗ Any change after this point INVALIDATES Phase A.

---

## 2. Configuration Snapshot

A configuration snapshot MUST be created **once** before execution.

- [ ] `config_snapshot.json` created
- [ ] Includes:
  - model name and version
  - provider / platform
  - region
  - inference parameters
  - date and time of freeze
  - execution toolchain

---

## 3. Baseline Execution Rules

Each baseline run MUST adhere to the following rules:

- [ ] Fresh context for every run
- [ ] Prompt used exactly as defined in Step 02
- [ ] No CSLI mechanisms applied
- [ ] No retries except for technical failures
- [ ] No manual intervention or correction
- [ ] Output captured verbatim

---

## 4. Execution Coverage

- [ ] All test scenarios executed
- [ ] Minimum runs per scenario: **3**
- [ ] All runs uniquely identified (scenario_id + run_id)
- [ ] Failed runs logged (not deleted)

---

## 5. Data Integrity & Storage

For each run, the following MUST be stored:

- [ ] Scenario ID
- [ ] Run ID
- [ ] Timestamp
- [ ] Input prompt
- [ ] Raw model output
- [ ] Execution metadata (latency, token usage, errors)

Data must be stored **append-only**.

---

## 6. Phase A Completion Criteria

Phase A is considered complete only if:

- [ ] All scenarios executed
- [ ] All baseline runs stored
- [ ] No configuration changes occurred during execution
- [ ] Completion timestamp recorded

Once completed, Phase A data is SEALED.

