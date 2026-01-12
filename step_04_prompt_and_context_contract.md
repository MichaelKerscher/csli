# Step 04 — Prompt & Context Contract

## Project
**CSLI — Context-Stable LLM Integration**

---

## Purpose of Step 04
The purpose of this step is to **fully formalize how prompts and contextual information are structured, represented, injected, and versioned** within CSLI.

This step defines the **core Context Engineering approach** of the project and ensures that all prompt construction remains:

- stable across integration phases (A/B/C)
- reproducible across executions
- comparable across conditions

Step 04 is the conceptual and methodological foundation for all subsequent executions and evaluations.

---

## Design Principles

The Prompt & Context Contract follows these guiding principles:

1. **Context-first clarity**  
   Context is explicit, structured, and clearly separated from user intent.

2. **Separation of concerns**  
   - User intent is expressed via the user prompt  
   - Environmental and device state is represented via structured context  
   - Behavioral framing is defined via system instructions

3. **Stability over cleverness**  
   No adaptive prompt rewriting or provider-specific optimizations are applied.

4. **Reproducibility by construction**  
   Every rendered prompt must be reconstructable from logs.

---

## Prompt Architecture

### Logical Prompt Components
Each prompt consists of the following logical components:

1. **System Instruction**  
   Defines role, tone, and behavioral constraints.

2. **User Input**  
   Represents the original user query or description.

3. **Context Block (optional)**  
   Structured contextual information injected in a deterministic format.

---

### Rendering Model
Prompts may be rendered as:
- a single combined text prompt, or
- a role-based message structure (e.g. system + user)

The rendered form used in execution must always be logged.

---

## Context Representation

### Context Object
Context is represented as a **structured object**, not as free text.

Example (illustrative):

```json
{
  "location": {
    "lat": 47.8571,
    "lon": 12.1285,
    "label": "Substation West"
  },
  "time": "2025-07-13T18:30:00Z",
  "device": {
    "type": "mobile",
    "model": "Pixel 7"
  },
  "network": {
    "status": "offline"
  }
}
```

---

### Allowed Context Dimensions

Only following predefined context dimensions are permitted:
- `location` (coordinates, optional label)
- `time` (timestamp)
- `device` (type, model)
- `network` (status)
- `environment` (optional; e.g. noise level, light conditions)

No ad-hoc or unstructured context fields are allowed.

---

## Context Injection Strategy

### Injection Rules

If structured context is enabled for a condition:
- context is injected **after** the user input
- context is enclosed in a clearly delimited block
- the format is deterministic and human-readable

Example (illustrative):
```yaml
[Context]
Location: Substation West (47.8571, 12.1285)
Time: 2025-07-13 18:30 UTC
Device: Mobile (Pixel 7)
Network: Offline
```

---

### Non-Injection Rules

Context must never:
- overwrite user intent
- be implicity merged into user text
- contradict user input without explicit indication

Interpretation of context is the responsibility of the LLM, not the system.

---

## Prompt Template Definition

### Template Identification

Each prompt template is identified by:
- `template_id` (e.g. `csli-default`)
- `template_version` (integer, starting at `1`)

---

### Abstract Template Structure

Example abstract structure:
```makefile
System:
You are an AI assistant supporting field technicians.
Provide clear, concise, and actionable guidance.

User:
{user_input}

Context:
{context_block}
```

The exact wording may vary, but structure and semantics must remain stable within a template version.

---

## Versioning Rules

### When to Increment `template_version`
The template version must be incremented if any of the following change:

- prompt structure
- system instruction semantics
- context block formatting
- context injection order
- interpretation guidance related to context

---

### When NOT to Increment
Version increments are not required for:

- spelling or formatting corrections
- purely stylistic rephrasing with identical semantics
- documentation-only changes

---

## Stability Rules Across Integration Phases

For a given `(test_id, condition_id)` pair:

- the same `template_id` must be used
- the same `template_version` must be used
- the same context schema must be applied
- the rendered prompt must be semantically identical

Any deviation constitutes a **new experimental configuration**.

---

## Relationship to CSLI Steps

- **Step 02** defines *what* is tested (tests & conditions)
- **Step 03** defines *how* executions are logged and reproduced
- **Step 04** defines *how prompts and context are constructed*

All execution phases (A/B/C) must comply with this contract.

---

## Scope of Step 04

### In Scope
- prompt structure definition
- context schema definition
- context injection rules
- prompt template versioning
- stability constraints across phases

### Out of Scope
- prompt optimization or tuning
- provider-specific prompt engineering tricks
- automatic context inference
- evaluation of prompt effectiveness

---

## Definition of Done (Step 04)
Step 04 is considered complete when:

- the Prompt & Context Contract is fully specified
- all context dimensions and injection rules are fixed
- versioning rules are defined
- stability constraints across A/B/C are documented
- this document is committed to the repository

---

## Status
**Step 04: Completed**
