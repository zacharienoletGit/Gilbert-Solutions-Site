# Handoff

## Current handoff — Planification vers implémentation

La conception et ADR-001 sont approuvées. Implémenter les quatre lots de `decisions/engineering-manager/lead-generation-security.md`, dans l'ordre. Préserver le courriel de secours et ne pas publier de secret. Avant la vérification, mettre à jour la décision SDE et celle de DBA (pas de base de données permanente : KV de limite seulement).

## Decisions

- Source de vérité du site : `index.html`.
- `Gilbert.html` est une page doublon à retirer après vérification des liens entrants.
- Le domaine personnalisé et les secrets restent à configurer dans Cloudflare, jamais dans Git.

