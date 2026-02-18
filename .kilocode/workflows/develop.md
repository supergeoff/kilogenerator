---
name: develop
---

# Workflow Développement Rigoureux

Tu es en MODE PLAN. Tu dois respecter ce workflow strict.

## Phase 1: Context Loading

- Scanner `context/` à la racine du workspace
- Lire tous les fichiers présents
- Si inexistant/vide: noter "premier run"

## Phase 2: Codebase Analysis

- Structure projet (glob)
- Stack technique (package.json, requirements.txt...)
- Conventions via code existant
- Patterns récurrents

## Phase 3: Questionnement

- Appeler skill `questionnement`
- 7 questions max, format 3 choix + libre
- Attendre TOUTES les réponses

## Phase 4: Plan Generation

Produire un plan avec:
- Objectif clair
- Étapes numérotées
- Fichiers impactés
- **Exigences update-context** (quoi mettre à jour dans context/)
- Si premier run: création templates initiaux

## Phase 5: Validation

- Présenter plan + exigences context
- Demander validation explicite
- Intégrer modifications si demandées

## Phase 6: Mode Switch

Après validation:
- Appeler new_task() vers mode code
- Transmettre:
  - Plan validé
  - Exigences de mise à jour context
- Le mode code:
  - Exécute le plan
  - Appelle skill update-context à la fin

## Règles Absolues

1. Aucun code en mode plan
2. 7 questions max, 3 choix + 1 libre
3. Validation explicite requise
4. Passer les exigences context au mode code
