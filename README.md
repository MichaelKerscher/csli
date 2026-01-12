# CSLI — Context-Stable LLM Integration

## Overview
**CSLI (Context-Stable LLM Integration)** is a structured integration subproject within the master thesis  
*“Development and Evaluation of a Context-Aware Mobile Support App Using Multimodal LLMs”*.

The purpose of CSLI is to integrate the external LLM service **506.ai** into the mobile support system in a **controlled, reproducible and context-preserving manner**, ensuring that experimental results remain comparable across different integration stages.

CSLI explicitly focuses on **integration stability and reproducibility**, not on performance, latency, or usability.

---

## Objectives
The CSLI subproject pursues the following objectives:

- Integrate 506.ai as an external LLM backend without introducing prompt or context drift
- Enable reproducible execution of a fixed test set (13 tests) after each integration step
- Maintain a clear separation between **context engineering** and **transport/integration layers**
- Establish a stable foundation for later evaluation of context-aware prompting strategies

---

## Integration Phases
CSLI follows a **three-stage incremental integration model**:

### Phase A — CLI → 506.ai
**Purpose:**  
Establish a direct baseline integration with 506.ai to understand API behavior, response formats, and ensure stable prompt execution.

**Key Principle:**  
No backend, no mobile app — direct CLI-based interaction only.

---

### Phase B — CLI → Backend → 506.ai
**Purpose:**  
Introduce a backend proxy layer responsible for logging, run management, and experiment reproducibility.

**Key Principle:**  
The backend must not alter prompt semantics or context structure compared to Phase A.

---

### Phase C — App → Backend → 506.ai
**Purpose:**  
Integrate the mobile application as a client while keeping the backend as the single source of truth for prompt construction and logging.

**Key Principle:**  
The mobile app submits structured inputs only; prompt construction and versioning remain centralized.

---

## Quality Principle: Reproducibility
A fixed set of **13 predefined tests** is executed:

- after completion of Phase A
- after completion of Phase B
- after completion of Phase C

This ensures functional equivalence and prevents integration-induced drift.

---

## In Scope
The CSLI subproject includes:

- Functional integration of 506.ai across all phases (A/B/C)
- Reproducible execution of the 13 tests at each phase
- Structured logging of inputs, context, prompts, and responses
- Versioning rules for prompt templates and context schemas

---

## Out of Scope
The following aspects are **explicitly excluded** from CSLI:

- Latency, performance, or cost evaluation
- Security hardening beyond minimal public-repository constraints
- Productive IAM, SSO, or enterprise authentication
- Usability studies or user-centered evaluation
- Retrieval-Augmented Generation (RAG) or data collections

---

## Repository Constraints
This repository is **public**.

- The 506.ai API key must **never** be committed to version control
- Configuration is handled via environment variables or `.env` files
- `.env` files are excluded via `.gitignore`
- `.env.example` files may be committed as documentation

---

## Documentation Structure
CSLI documentation is organized as **step-based project management artifacts**:

