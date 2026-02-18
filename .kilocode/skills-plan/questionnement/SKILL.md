---
name: questionnement
description: Génère 7 questions pertinentes pour aligner la demande. Active ce skill pour clarifier une demande avant planification.
---

# Skill: Questionnement Intelligent

## Objectif

Identifier les zones d'ombre en croisant:
- Demande utilisateur
- Context existant
- Analyse codebase

## Format Question

```
**Q1: [Titre]**

[Contexte]

○ Option A
○ Option B
○ Option C
○ Autre (préciser)
```

## Processus

1. Analyser la demande: flou, implicite, ambigü
2. Croiser avec context et codebase
3. Identifier: edge cases, UX, performance, sécurité, patterns

## Règles

- EXACTEMENT 7 questions
- TOUJOURS 3 choix + 1 libre
- Questions contextuelles et intelligentes
- Chaque question apporte de la valeur
