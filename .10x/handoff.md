# Handoff

## Current handoff — Planification vers implémentation

La conception et ADR-001 sont approuvées. Implémenter les quatre lots de `decisions/engineering-manager/lead-generation-security.md`, dans l'ordre. Préserver le courriel de secours et ne pas publier de secret. Avant la vérification, mettre à jour la décision SDE et celle de DBA (pas de base de données permanente : KV de limite seulement).

## Decisions

- Source de vérité du site : `index.html`.
- `Gilbert.html` (page doublon, ancien prix fixe) a été remplacé le 2026-11-14, à la demande du propriétaire, par une page-relais : actualisation immédiate vers l'accueil, sans JavaScript, car GitHub Pages n'a pas de redirections serveur. Les anciens liens continuent de fonctionner.
- Les secrets restent à configurer dans Cloudflare, jamais dans Git.
- Le domaine personnalisé `gilbert-solution.ca` est déjà en service sur GitHub Pages depuis le 2026-11-12 (ADR-002). La zone DNS et le courriel sont chez WHC.

## Contexte pour la migration Cloudflare (lot DevOps)

Lire `adrs/002-domaine-github-pages-courriel-whc.md` et `decisions/devops/custom-domain-email.md` avant de toucher au DNS.

- Un domaine apex sur Cloudflare Pages exige la zone chez Cloudflare : recréer d'abord MX, `mail` (A, sans proxy), SPF, DKIM et DMARC dans Cloudflare, puis changer les serveurs de noms.
- Le courriel `zacharie@gilbert-solution.ca` sert à la prospection : aucune coupure acceptable.
- Retour arrière : GitHub Pages reste configuré, il suffit de remettre les quatre enregistrements A.

