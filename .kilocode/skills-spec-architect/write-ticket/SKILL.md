---
name: write-ticket
description: Transforms macro-features into atomic, standardized, and single-layer technical tickets in Markdown.
metadata:
  workflow: Epic-to-Atomic-Tickets
  granularity: technical-layer-isolated
---

# Ticket Architect Skill

This skill specializes in decomposing complex requirements (from PRDs, Epic or feature requests) into standardized, atomic, and self-contained developer tickets. It ensures each ticket is ready for development by any team member without further clarification.

## Core Principles

1. **Atomicity**: Every ticket must be "unit-sized." If a request is too broad, it MUST be automatically split.
2. **Technical Isolation**: Each ticket must impact only **one technical layer** (e.g., Backend only, Frontend only, Database only).
3. **Self-Contained**: Tickets must include all necessary context, business logic, and constraints.
4. **No Implementation Code**: Do not provide actual code. The implementation details are the responsibility of the developer. Use natural language for logic.

## Output Structure

Each ticket must be a separate Markdown file named following this convention: `NN-description-in-three-words.md` (where NN is an incremental number).

### Ticket Template

Each generated file must follow this exact structure:

1. **Summary/Goal**: A single sentence explaining the "What".
2. **Context & Rationale**: The "Why" and the value of this specific task.
3. **Requirements**: Exhaustive list of functional requirements.
4. **Technical Constraints**: 
   - Business objects definition (fields, types in plain text).
   - Algorithms described in natural language.
   - Architectural patterns to follow.
5. **Dependencies & Blockers**: List everything that must be ready before starting.
6. **Acceptance Criteria**: A precise checklist to validate the ticket.
7. **Testing Strategy**: Description of required Unit Tests, Integration Tests, and manual test scenarios.

## Execution Workflow

1. **Analyze**: Read the input.
2. **Decompose**: Identify the different technical layers involved.
3. **Draft**: Create the individual tickets in the current "Epic" directory.
4. **Verify**: Ensure no ticket crosses technical layers and that all business logic is described without code.

## Example Object Definition
- **Business Object: UserProfile**
  - Name: String (Required)
  - Email: String (Unique, Validated)
  - Role: Enum (Admin, Editor, Viewer)