---
name: name-epic
description: Standardize new epic folder names in specs/epics using sequential IDs and 3-word English verb-based naming.
---

# Epic Naming Standardization

This skill ensures that every new epic follows a strict naming convention to maintain a clean and predictable project structure in the `specs/epics/` directory.

## Workflow

### 1. Identify Next ID
- Scan the directory `specs/epics/`.
- List all existing files and folders.
- Extract the 3-digit prefix (`XXX-`) from each item.
- **Rule**: Find the highest existing ID and increment it by 1 (e.g., if `004` is the highest, the next is `005`). 
- **Rule**: Never fill gaps in the sequence. Always append.
- **Rule**: If the directory is empty or missing, start with `001`.

### 2. Normalize the Name
- **Translation**: Translate the user's request into technical English.
- **Verb Requirement**: The name must start with a **verb** (e.g., `create`, `manage`, `authorize`, `send`).
- **Word Limit**: The descriptive part (after the ID) must not exceed **3 words**.
- **Exclusion**: Remove generic technical terms such as "epic", "feature", "module", "system", "story", or "task".
- **Format**: `ID-word1-word2-word3` (Lowercase, kebab-case).

## Execution
- Once the name is calculated (e.g., `005-process-stripe-payment`), return the final string to the agent.
- The agent will then proceed to create the corresponding directory in `specs/epics/`.

## Examples
- User: "système de récupération de mot de passe" -> `006-recover-user-password`
- User: "gestion des stocks" -> `007-manage-inventory-stock`
- User: "intégration api météo" -> `008-integrate-weather-api`
- User: "envoi de facture auto" -> `009-send-automated-invoices`