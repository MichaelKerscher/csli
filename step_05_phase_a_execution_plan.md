# Step 05 — Phase A: CLI → 506.ai (Execution Plan)

## Project
**CSLI — Context-Stable LLM Integration**

---

## Purpose of Step 05
The purpose of this step is to define and formalize **Phase A**, the baseline execution phase of CSLI.

In Phase A, all predefined tests and conditions are executed **directly via CLI against the 506.ai API**, without any intermediate backend or mobile application.

This phase establishes the **baseline reference** for all subsequent integration phases.

No execution, evaluation, or analysis is performed in this step.

---

## Role of Phase A within CSLI
Phase A has a strictly **methodological role**.

It is used to:
- validate direct interaction with the 506.ai LLM API
- confirm feasibility of multimodal and context-enriched requests at provider level
- generate baseline run artifacts for later comparison
- identify provider-level constraints before introducing system complexity

Phase A intentionally excludes all intermediate layers.

---

## Scope of Phase A

### In Scope
- CLI-based execution of CSLI test cases
- Direct API calls to 506.ai
- Use of predefined prompt and context rules (Step 04)
- Execution under all applicable conditions (Step 02)
- Logging of all runs according to Step 03

### Out of Scope
- Backend services
- Mobile application
- Authentication hardening or secret management
- Performance, latency, or cost analysis
- Retrieval, RAG, data collections, or assistants
- Evaluation or scoring of responses

---

## Execution Inputs (Fixed)

### Test Basis
- **12 CSLI test cases (T01–T12)** as defined in Step 02

### Conditions
- Global condition set **C1–C10**
- Non-applicable test–condition combinations are marked as **NA**
- Conditions are never modified per test

### Prompt & Context
- Prompt templates as defined in Step 04
- Fixed `template_id` and `template_version`
- Structured context only when enabled by condition

---

## Execution Method (Conceptual)

### CLI-Based Execution Model
Each execution is triggered via a CLI command or script that:

1. selects a `(test_id, condition_id)` pair
2. renders the prompt according to the Prompt & Context Contract (Step 04)
3. attaches modality inputs if required
4. sends a request directly to the 506.ai API
5. captures the API response
6. writes a run log following the CSLI logging schema (Step 03)

The CLI acts as a **thin execution harness** and must not contain business logic.

---

## Provider Assumptions — 506.ai

### Authentication
All API calls require the following HTTP headers:

- `api-organization-id`
- `api-key`

Key handling and security hardening are explicitly **out of scope** for CSLI.

---

### LLM Interaction Endpoint
Phase A uses the **non-streaming chat endpoint**:
`POST /api/v1/public/chatNoStream`

Characteristics:
- synchronous request–response interaction
- model selection via `model.id`
- messages passed as an ordered list
- optional parameters such as `temperature` may be specified but remain fixed

No streaming endpoints are used.

---

### Model Selection
- Available models can be queried via: `GET /api/v1/public/models`

- For Phase A:
- exactly one model ID is selected
- the model remains fixed across all runs
- the model ID is logged for every execution

Model comparison is out of scope.

---

### Multimodal Handling
506.ai supports multimodal inputs via media-related endpoints.

For Phase A:
- multimodal inputs are **conceptually supported**
- media handling is treated as CLI-level abstraction
- no persistent data collections are created
- no media reuse or retrieval is performed

Media files are not stored in public logs (see Step 03).

---

### Limits and Error Behavior
Known constraints:
- rate limits apply (approximately 10 requests per minute)
- standard HTTP error codes may occur (400, 401, 403, 429, 500)

Error handling rules:
- failed requests are logged with `status = error`
- error responses are preserved
- failed runs are not deleted

---

## Run Coverage Rules

### Required Coverage
Phase A must include:
- all 12 test cases
- all logically applicable conditions per test
- at least one successful run per `(test_id, condition_id)` pair

### Optional Repetitions
- repeated executions are allowed but not required
- each repetition generates a new `run_id`

---

## Logging Rules (Phase A)

All Phase A runs must:
- comply with the CSLI logging schema (Step 03)
- be stored under `results/phase-A/`
- include:
- `phase = A`
- `provider = 506ai`
- `test_id`, `condition_id`, `run_id`
- rendered prompt
- structured context (if applicable)

Logs created in Phase A are considered **baseline artifacts** and must not be modified retroactively.

---

## Definition of Done (Step 05)
Step 05 is considered complete when:

- Phase A scope and execution rules are fully documented
- provider assumptions and constraints are defined
- run coverage and logging requirements are fixed
- this document is committed to the repository

---

## Status
**Step 05: Completed**

---


