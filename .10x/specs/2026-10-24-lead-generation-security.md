# Design — conversion et sécurité du site Gilbert

**Statut :** Proposé
**Fonctionnalité :** `lead-generation-security`
**Date :** 2026-10-24

## Objectif

Augmenter les prises de contact sans dégrader la clarté ni la confidentialité : conserver la page vitrine statique, remplacer le contact `mailto:` par un formulaire sécurisé et le déployer sur Cloudflare Pages.

## Portée

1. Retirer `Gilbert.html`, page obsolète doublonnant l'accueil.
2. Extraire CSS, JavaScript et polices pour réduire le poids initial et permettre une CSP stricte.
3. Ajouter un formulaire, ses erreurs accessibles et une page de remerciement.
4. Ajouter une Pages Function `POST /api/contact` : validation serveur, vérification Turnstile, limite par IP via KV, journalisation des refus et envoi texte par Resend.
5. Créer les pages Confidentialité et Conditions, puis mettre à jour les liens du pied de page.
6. Ajouter les en-têtes de sécurité Cloudflare Pages et un CTA mobile fixe.
7. Mettre chaque programme d'aide à jour avec une source officielle et `Vérifié le …`; le contrôle récurrent est exécuté deux fois par semaine.

## Hors portée

- Pas de collecte analytique, cookies marketing, stockage de dossiers clients, ni témoignages fictifs.
- Pas de clé, identifiant Cloudflare, valeur de Turnstile ou clé Resend dans le dépôt.
- Pas de promesse d'admissibilité aux aides.

## Flux de contact

Visiteur → formulaire minimal + champ honeypot → Turnstile → Pages Function → validation/limite KV → Resend → adresse de réception définie comme secret Cloudflare → réponse JSON → page merci.

Le message est envoyé en texte brut ; les entrées sont limitées, normalisées et jamais interpolées comme HTML.

## Configuration Cloudflare requise après déploiement

- Projet Pages relié à `main`, domaine personnalisé et HTTPS forcé.
- Binding KV `CONTACT_RATE_LIMIT`.
- Secrets : `TURNSTILE_SECRET_KEY`, `RESEND_API_KEY`, `CONTACT_RECIPIENT`, `CONTACT_FROM`.
- Variables publiques : `TURNSTILE_SITE_KEY` si nécessaire au client.
- Compte Resend avec domaine expéditeur vérifié.

## Tests d'acceptation

- Soumission valide affiche la page merci et livre un message.
- Entrée invalide, honeypot, jeton absent/invalide et dépassement de limite renvoient une erreur exploitable sans divulguer de détail interne.
- Aucune clé ne se trouve dans Git.
- Les liens légaux, le CTA mobile, canonical, robots et sitemap fonctionnent.
- Les aides affichent une date de vérification et leurs liens officiels.

