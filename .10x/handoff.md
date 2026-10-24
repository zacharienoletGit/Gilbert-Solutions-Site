# Handoff

## Current handoff — Design vers implémentation

Le site est une page HTML statique publiée par GitHub Actions. Aucun secret, backend ou formulaire ne figure dans le dépôt actuel. La conception propose Cloudflare Pages Functions pour `POST /api/contact`, avec Turnstile, limites KV et Resend configurés exclusivement comme secrets Cloudflare. Lire le spec et ADR 001 avant l'implémentation.

## Decisions

- Source de vérité du site : `index.html`.
- `Gilbert.html` est une page doublon à retirer après vérification des liens entrants.
- Le domaine personnalisé et les secrets restent à configurer dans Cloudflare, jamais dans Git.

