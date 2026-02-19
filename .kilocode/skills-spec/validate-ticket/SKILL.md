---
name: validate-ticket
description: Scans generated tickets for forbidden code syntax or non-English content. Ensures strict adherence to "No Code" policy.
---

# Skill: Validate Ticket

## Objective

Act as a final quality gate to ensure that technical tickets are written in pure natural language (English) and contain zero code syntax.

## Forbidden Patterns

If any of the following are found, the ticket MUST be rejected and rewritten:
- **Braces/Brackets**: `{ }`, `[ ]` (unless used for checkboxes in markdown).
- **Arrows**: `=>`, `->`.
- **Keywords**: `interface`, `class`, `function`, `const`, `let`, `var`, `import`, `export`, `public`, `private`, `void`.
- **Logic syntax**: `if (`, `else {`, `for (`, `while (`, `switch`.
- **Decorators**: `@Component`, `@Injectable`, etc.

## Execution Workflow

1. **Read**: Load the content of the generated ticket.
2. **Scan**: Look for forbidden patterns listed above.
3. **Verify Language**: Ensure the text is in English.
4. **Outcome**:
   - **PASS**: If no code and language is correct.
   - **FAIL**: If any code syntax is detected. Provide the specific line numbers and reason for failure.

## Rules

- Do not compromise. Even a small interface definition or a single `const` is a failure.
- Suggest how to describe the logic in natural language instead of code.
