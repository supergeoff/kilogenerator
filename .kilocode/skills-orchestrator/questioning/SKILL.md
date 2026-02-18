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

## Question Format

```
**Q1: [Title]**

[Context]

○ Option A
○ Option B
○ Option C
○ Other (specify)
```

## Process

1. Analyze the request: vague, implicit, ambiguous points
2. Cross-reference with context and codebase
3. Identify: edge cases, UX, performance, security, patterns

## Rules

- EXACTLY 7 questions
- ALWAYS 3 choices + 1 free-form
- Contextual and intelligent questions
- Each question adds value
