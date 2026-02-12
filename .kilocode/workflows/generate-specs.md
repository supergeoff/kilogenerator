---
title: "Generate Spec Tickets"
description: "Interactive workflow to transform user needs into technical specifications (epics/tickets)."
---

# Specification Generation Pipeline

This workflow guides the creation of precise technical tickets from a user brief.

1. **Context & Briefing**
   - Command: ask `spec` to "Analyze the initial user brief provided in the chat context."
   - Parameter: `user_brief` (Ask user: "Please provide the global brief for this feature.")

2. **Epic Naming & normalization**
   - Command: ask `spec` to use `name-epic`
   - Input: `user_brief`
   - Goal: Generate a strictly formatted 'kebab-case' identifier for the epic.

3. **Structured Technical Interview**
   - Command: ask `spec` to "Conduct the 13-point technical interview regarding [epic_name]. Do not generate files yet. Ask clarifying questions one by one if critical information is missing regarding: Scope, Happy Path, Rules, Data, I/O, Errors, Security, Deps, Perf, Integration, Testability, Observability, UX."

4. **Architecture Synthesis**
   - Command: ask `spec` to "Summarize the final implementation plan based on the interview findings."

5. **Scaffold Directory**
   - Command: execute_command `mkdir -p specs/epics/[epic_name]`

6. **Generate Ticket Artifacts**
   - Command: ask `spec` to use `write-ticket`
   - Context: Use the synthesis from Step 4.