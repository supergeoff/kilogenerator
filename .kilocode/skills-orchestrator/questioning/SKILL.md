---
name: questioning
description: Generates 7 relevant questions to align the request. Activate this skill to clarify a request before planning.
---

# Skill: Intelligent Questioning

## Objective

Identify gray areas by cross-referencing:
- User request
- Existing context  
- Codebase analysis

## Input

**READ** the state file `.kilocode/.develop-state.json` to get:
- `contextSummary`: Summary of loaded context from context/ directory
- `codebaseAnalysis`: Analysis of project structure, tech stack, conventions
- User's original request (from conversation)

The skill must read this state file BEFORE generating questions. Questions MUST be deeply contextualized:
- Reference specific file paths and code patterns found in `codebaseAnalysis`.
- Cross-reference with methodology patterns found in `contextSummary`.
- Identify project-specific terminology and use it in the questions.
- Address gaps between the request and the detected architecture.

## Question Format

Each question must be preceded by a **Context** block that explains why this question is being asked based on the analysis.

```
**Q[X]: [Title]**

**Context**: Based on findings in [specific files/patterns]:
- Detected [Pattern A] in [File B]
- Context/methodology specifies [Rule C]
- This creates a choice regarding [Gap D]

[Question Text]

○ Option A
○ Option B  
○ Option C
○ Other (specify)
```

## Rules

- EXACTLY 7 questions.
- ALWAYS 3 choices + 1 free-form (Other).
- Questions MUST be contextualized using findings from the state file.
- Do NOT ask generic questions (e.g., "What language do you use?") if the information is already in `codebaseAnalysis`.
- Focus on architectural decisions, UX trade-offs, and implementation details.
