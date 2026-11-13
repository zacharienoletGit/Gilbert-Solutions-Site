# Gilbert — statut

- **Fonctionnalité active :** `lead-generation-security`
- **Phase :** Planning Complete.
- **Portée approuvée :** retrait de la page doublon, migration prête pour Cloudflare Pages, formulaire sécurisé, performance, pages légales séparées, en-têtes et CTA mobile.
- **Automatisation :** vérification officielle des aides, lundi et jeudi à 09:00 America/Toronto.
- **Décision :** conserver le site statique et externaliser uniquement le contact sécurisé vers Cloudflare Pages Functions.
- **ADR :** ADR-001 accepté.
- **Plan :** quatre lots ordonnés dans la décision Engineering Manager.

## Fonctionnalité livrée — `custom-domain-email` (2026-11-12)

- **Phase :** Delivery Complete pour le site ; courriel partiellement en place.
- **ADR :** ADR-002 accepté (domaine sur GitHub Pages, DNS et courriel chez WHC).
- **Fait :** DNS branchés, domaine personnalisé inscrit, Enforce HTTPS coché, PR #5 fusionnée, boîte `zacharie@gilbert-solution.ca` créée.
- **Vérifié :** `https://gilbert-solution.ca` répond 200, `http://` redirige en 301 vers HTTPS, `www` redirige vers l'apex, la page annonce la nouvelle adresse canonique.
- **Reste à faire (propriétaire) :**
  - Créer la redirection `zacharie@gilbert-solution.ca` vers Gmail dans cPanel, puis ajouter l'adresse dans « Envoyer des courriels en tant que » de Gmail (SMTP `mail.gilbert-solution.ca`, port 465, SSL).
  - Garder le forfait WHC à jour : il porte le DNS et le courriel.
- **Impact sur `lead-generation-security` :** la bascule vers Cloudflare Pages doit suivre l'ordre décrit dans les risques d'ADR-002.

