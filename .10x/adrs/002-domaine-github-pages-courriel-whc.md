# ADR-002: Domaine gilbert-solution.ca sur GitHub Pages, courriel et DNS chez WHC

**Status:** Accepted
**Date:** 2026-11-12
**Feature:** custom-domain-email
**Author:** 10x-Team (Architect + Staff Engineer)

## Context

Le domaine `gilbert-solution.ca` est enregistré chez WHC, avec un forfait Web Hosting Pro qui fournit la zone DNS (cPanel) et le courriel. Le site, lui, est publié sur GitHub Pages par le workflow `pages.yml` et répondait à `zacharienoletgit.github.io/Gilbert-Solutions-Site/`. La prospection commence : il faut une adresse de site et une adresse courriel au nom de Gilbert maintenant, sans attendre la migration Cloudflare prévue par ADR-001.

Au départ, le MX du domaine pointait vers l'apex (`gilbert-solution.ca`). Changer l'adresse de l'apex pour GitHub aurait donc coupé le courriel.

## Decision

Brancher le domaine sur GitHub Pages tout de suite, en gardant la zone DNS et le courriel chez WHC.

- Apex `gilbert-solution.ca` : quatre enregistrements A vers GitHub Pages (`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`).
- `www` : CNAME vers `zacharienoletgit.github.io` (GitHub redirige vers l'apex).
- Courriel découplé du site : `mail.gilbert-solution.ca` devient un enregistrement A vers le serveur WHC (`67.215.15.226`), et le MX pointe vers `mail.gilbert-solution.ca`.
- Domaine personnalisé inscrit dans **Settings → Pages** du dépôt, avec **Enforce HTTPS** coché. Pas de fichier `CNAME` : le site est publié par GitHub Actions, où ce fichier est ignoré.
- Les adresses annoncées par le site (`canonical`, Open Graph, JSON-LD, `sitemap.xml`, `robots.txt`) pointent vers `https://gilbert-solution.ca/` (PR #5).

## Alternatives Considered

| Alternative | Pros | Cons | Why Not |
|-------------|------|------|---------|
| Attendre la migration Cloudflare (ADR-001) et y brancher le domaine | Une seule bascule DNS | Pas d'adresse professionnelle pendant la prospection | Le besoin est immédiat |
| Héberger le site sur le forfait WHC déjà payé | Tout chez un seul fournisseur | Abandonne le déploiement automatique par Git, FTP à gérer | Régression du flux de publication |
| Déplacer la zone DNS chez Cloudflare dès maintenant | Prépare ADR-001 | Recréer MX, SPF, DKIM et DMARC à la main, risque de couper le courriel le jour même | Trop de risque pour le gain du jour |
| A ×4 + `www` chez WHC vers GitHub Pages | Aucun changement d'hébergeur, courriel intact, HTTPS gratuit | Deux fournisseurs à connaître, bascule à refaire pour Cloudflare | Choisi |

## Consequences

### Positive
- Le site répond en HTTPS sur `https://gilbert-solution.ca/` et `www` redirige vers l'apex.
- Le courriel ne dépend plus de l'adresse du site : on peut déplacer le site sans toucher au MX.
- L'ancienne adresse `github.io` redirige vers le domaine.

### Negative
- Le forfait d'hébergement WHC ne sert plus qu'au DNS et au courriel.
- L'enregistrement SPF contient encore `+a`, qui désigne maintenant les adresses de GitHub. C'est sans effet sur la livraison, mais inutile : à retirer lors d'un prochain passage dans la zone.
- GitHub Pages ne permet pas d'en-têtes de sécurité (HSTS, CSP) : ce point reste couvert par ADR-001.

### Risks
- **Migration Cloudflare Pages :** un domaine apex sur Cloudflare Pages exige que la zone soit chez Cloudflare. Le jour de la bascule, recréer d'abord dans Cloudflare les enregistrements du courriel (MX, `mail` en A sans proxy, SPF, DKIM `default._domainkey`, `_dmarc`), puis seulement changer les serveurs de noms. Garder GitHub Pages actif comme retour arrière.
- **Forfait WHC non renouvelé :** une suspension couperait le DNS et le courriel, donc aussi le site. Garder le renouvellement à jour.
- **DMARC à `p=none` :** aucune protection contre l'usurpation pour l'instant. Passer à `quarantine` après quelques semaines d'envois sans incident.

## Dependencies
- Zone DNS et courriel : cPanel WHC du domaine `gilbert-solution.ca`.
- Publication : workflow `pages.yml`, réglages Pages du dépôt.
- Contraint ADR-001 : la migration Cloudflare doit suivre l'ordre décrit dans les risques.
