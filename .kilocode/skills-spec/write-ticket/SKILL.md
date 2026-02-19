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
4. **STRICTLY NO CODE**: You are FORBIDDEN from providing implementation code, snippets, or code-like structures. If you feel tempted to write code, STOP and ask for clarification.
5. **Natural Language Only**: All logic, algorithms, and data structures must be described in plain English.

## Anti-Patterns (NEVER DO THIS)

- **Snippet Injection**: Providing JSX/TSX/JS/TS components or functions.
- **Syntax Logic**: Using `if/else`, `for`, or `switch` syntax. Use bullet points or natural language instead.
- **Type Definitions**: Writing `interface` or `type` blocks. Describe fields and types in a list.
- **SQL/JSON Samples**: Writing raw SQL queries or JSON payloads. Describe the shape and content instead.

## Execution Workflow

1. **Analyze**: Read the input.
2. **Decompose**: Identify the different technical layers involved.
3. **Draft**: Create the individual tickets in the current "Epic" directory.
4. **Verify**: Ensure no ticket crosses technical layers and that all business logic is described without code.
5. **Code Check**: Before finalizing, scan the ticket for any code syntax (brackets, keywords). If found, rewrite in plain English.

## Example Object Definition
- **Business Object: UserProfile**
  - Name: String (Required)
  - Email: String (Unique, Validated)
  - Role: Enum (Admin, Editor, Viewer)