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

The skill must read this state file BEFORE generating questions. Questions should be contextualized based on:
- What was found in the codebase
- What patterns/conventions exist in the context
- What gaps exist between user request and current project state

## Question Format

```
**Q1: [Title]**

[Context - reference specific findings from codebase]

○ Option A
○ Option B  
○ Option C
○ Other (specify)
```

## Process

1. **READ** state file to understand full context
2. Analyze the request against:
   - Loaded context (contextSummary)
   - Codebase analysis (codebaseAnalysis)
   - User's original request
3. Identify: edge cases, UX, performance, security, patterns, gaps
4. Generate EXACTLY 7 questions that address these gaps

## Rules

- EXACTLY 7 questions
- ALWAYS 3 choices + 1 free-form
- Questions must be contextualized using state file information
- Each question adds value and addresses a specific gap
- Reference specific findings from codebase analysis in question context
