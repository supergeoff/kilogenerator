---
title: "Context Guidelines"
description: "Guidelines for what belongs in the context directory"
---

# Context Guidelines

## Purpose

The `context/` directory contains reusable methodology patterns, rules, and logic that can adapt to ANY project while maintaining rigorous conventions.

## What Belongs Here

### methodology/

Reusable patterns and standards:
- Naming conventions
- Documentation standards
- Workflow patterns
- Project-agnostic conventions

### docs/

Reference documentation:
- External documentation imports
- Tool/framework references
- Read-only documentation

## What Does NOT Belong

- Current file structure listings
- Specific configuration values
- Implementation state
- Project-specific paths
- Current task status
- Temporary decisions

## Philosophy

Context should be **methodology, not implementation**:

- ✅ Pattern: "Use kebab-case for files"
- ❌ State: "Current files are main.ts, utils.ts"

- ✅ Rule: "Update context after significant changes"
- ❌ Status: "Context last updated on 2026-02-18"

## Current Structure

```
context/
├── methodology/           # Reusable patterns, rules, logic
│   ├── naming-conventions.md
│   ├── documentation-standards.md
│   ├── workflow-patterns.md
│   └── context-guidelines.md
└── docs/                  # Reference docs
    ├── README.md
    ├── kilo-modes.md
    ├── kilo-skills.md
    └── kilo-workflows.md
```

## Usage

Agents should:
1. Read `context/methodology/` at workflow start for patterns and conventions
2. Read `context/docs/` for reference documentation
3. Update `context/methodology/` when new patterns are discovered
