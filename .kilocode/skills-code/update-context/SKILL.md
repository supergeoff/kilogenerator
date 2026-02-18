---
name: update-context
description: Met à jour le dossier context/ après implémentation. Active ce skill à la fin de chaque implémentation pour standardiser.
---

# Skill: Update Context

## Objectif

Maintenir `context/` comme source de vérité.

## Entrée

Reçoit du mode plan:
- Plan validé
- Exigences de mise à jour context

## Actions

### CRÉER (si context vide)

Créer structure initiale selon besoins projet.

### AJOUTER

Nouveaux patterns, conventions, décisions.

### MODIFIER

Patterns existants qui ont évolué.

### SUPPRIMER/REMPLACER

Patterns obsolètes ou remplacés.

## Règles

1. Lire context/ existant
2. Comparer avec code implémenté
3. Appliquer les exigences reçues du plan
4. Context = état actuel du code
