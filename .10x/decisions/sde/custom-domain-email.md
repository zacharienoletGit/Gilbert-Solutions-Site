# custom-domain-email

## Ce qui a été livré

- PR #5, fusionnée dans `main` (commit `79c523d`) : l'ancienne adresse `https://zacharienoletgit.github.io/Gilbert-Solutions-Site/` est remplacée par `https://gilbert-solution.ca/` dans `index.html` (`canonical`, `og:url`, `og:image`, `twitter:image`, JSON-LD), `sitemap.xml`, `robots.txt` et `README.md`.
- `README.md`, section Publier : la marche à suivre pour le domaine personnalisé décrit maintenant les réglages Pages, pas un fichier `CNAME`.

## Écarts par rapport au plan

Aucun lot de `lead-generation-security` n'a été touché. Ce travail est une fonctionnalité à part, décidée dans ADR-002.

## Vérifié

- Aucune occurrence restante de l'ancienne adresse du site.
- `sitemap.xml` est du XML valide, le bloc JSON-LD est du JSON valide.
- La page en ligne annonce `<link rel="canonical" href="https://gilbert-solution.ca/">`.

## Dette technique

- Les liens vers le portfolio (`https://zacharienoletgit.github.io/`) dans `Gilbert.html` sont volontairement inchangés. La page `Gilbert.html` reste un doublon à retirer (lot prévu dans `lead-generation-security`).
