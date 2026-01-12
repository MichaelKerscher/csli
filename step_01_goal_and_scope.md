# Step 01 — Goal Definition & Scope

## Project
**CSLI — Context-Stable LLM Integration**

---

## Purpose of Step 01
The purpose of this step is to formally define the **goal, scope, constraints, and structural principles** of the CSLI subproject before any technical implementation begins.

This step establishes a shared understanding of *what CSLI is*, *what it is not*, and *how progress and completion are evaluated*.

No technical implementation is performed in this step.

---

## Subproject Goal
The goal of CSLI is to integrate the external LLM service **506.ai** into the mobile support system in a **controlled and context-stable manner**, enabling reproducible execution of context-engineering experiments.

The integration must ensure that:
- prompt semantics remain stable across integration stages
- contextual information is preserved without drift
- experimental results remain comparable across the system stack

---

## Integration Model
CSLI follows a **three-phase incremental integration model**:

### Phase A — CLI → 506.ai
**Objective:**  
Establish a direct command-line integration with 506.ai to create a baseline and validate prompt execution without intermediary components.

**Characteristics:**
- No backend
- No mobile application
- Direct API interaction via CLI tools

---

### Phase B — CLI → Backend → 506.ai
**Objective:**  
Introduce a backend proxy responsible for logging, run management, and experiment reproducibility.

**Characteristics:**
- CLI remains the client
- Backend acts as proxy and logging authority
- Prompt and context semantics must remain equivalent to Phase A

---

### Phase C — App → Backend → 506.ai
**Objective:**  
Integrate the mobile application as a client while keeping the backend as the single source of truth for prompt construction and logging.

**Characteristics:**
- Mobile app submits structured inputs only
- Backend controls prompt construction and versioning
- Logging and run management remain centralized

---

## Quality Principle: Reproducibility
A fixed catalog of **12 predefined tests** is executed after completion of each phase:

- after Phase A
- after Phase B
- after Phase C

This principle ensures:
- functional equivalence across integration stages
- early detection of integration-induced drift
- traceability of experimental results

---

## Scope Definition

### In Scope
The following aspects are included in CSLI:

- Functional integration of the external LLM service 506.ai
- Incremental integration across phases A, B, and C
- Reproducible execution of the predefined test catalog
- Structured logging of runs (inputs, context, prompts, outputs)
- Conceptual versioning of prompt templates and context schemas

---

### Out of Scope
The following aspects are explicitly excluded from CSLI:

- Latency, performance, or cost evaluation
- Security hardening beyond minimal public-repository constraints
- Productive identity management (IAM, SSO)
- Usability or user-experience studies
- Retrieval-Augmented Generation (RAG) or document ingestion pipelines
- Optimization of model parameters or decoding strategies

---

## Repository Constraints
The CSLI repository is public.

The following constraints apply:

- The 506.ai API key must never be committed to version control
- Configuration is handled via environment variables or `.env` files
- `.env` files are excluded using `.gitignore`
- `.env.example` files may be committed for documentation purposes

These constraints are treated as **project hygiene requirements**, not as security objectives.

---

## Definition of Done (Step 01)
Step 01 is considered complete when:

- the CSLI subproject goal is formally defined
- the three-phase integration model (A/B/C) is fixed
- the reproducibility principle (12 tests after each phase) is fixed
- scope and exclusions are explicitly documented
- repository constraints are documented
- this document is committed to the repository

---

## Status
**Step 01: Completed**

