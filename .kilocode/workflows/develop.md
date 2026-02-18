---
name: develop
---

# Develop Workflow (Orchestrator → Plan → Code)

You are executing the DEVELOP WORKFLOW. Follow this strict sequence.

## Phase 1: Orchestrator Mode (Current)

### 1.1 Context Loading
- Scan `context/` directory at workspace root
- Read all files present
- If non-existent/empty: note "first run" and proceed

### 1.2 Codebase Analysis
- Project structure (glob patterns)
- Tech stack detection (package.json, requirements.txt, etc.)
- Existing conventions and patterns

### 1.3 Questioning
- Call the `questioning` skill
- Ask EXACTLY 7 questions (3 choices + 1 free-form each)
- Wait for ALL user responses before proceeding

### 1.4 Transition to Plan Mode
Call `new_task()` to architect mode with the following context:
- Loaded context summary
- User responses to questions
- Original user request
- Instruction: "Generate a structured implementation plan"

## Phase 2: Plan Mode (Architect)

### 2.1 Plan Generation
Produce a structured plan with:
- **Objective**: Clear, measurable goal
- **Steps**: Numbered implementation steps
- **Files**: List of files to create/modify
- **Context Requirements**: What to update in `context/` after implementation
- **Risks**: Potential issues and mitigations

### 2.2 User Validation
- Present the complete plan
- Ask for explicit approval
- Incorporate modifications if requested
- Do NOT proceed without validation

### 2.3 Transition to Code Mode
After validation, call `new_task()` to code mode with:
- Validated implementation plan
- Context update requirements
- Instruction: "Execute the plan and update context at the end"

## Phase 3: Code Mode

### 3.1 Implementation
- Execute each step of the validated plan
- Write/modify files as specified
- Follow existing project conventions

### 3.2 Context Update
At completion, call the `update-context` skill:
- Update `context/` with new patterns
- Document decisions made
- Record any deviations from the plan

## Absolute Rules

1. **No code in Orchestrator or Plan modes** - only analysis and planning
2. **Exactly 7 questions** with 3 choices + free-form
3. **Explicit validation required** before Code mode
4. **Always update context** at the end of Code mode
5. **Use `new_task()` for all mode transitions**
