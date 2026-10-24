# ADR-001: Formulaire de contact via Cloudflare Pages Functions

**Status:** Proposed
**Date:** 2026-10-24
**Feature:** lead-generation-security
**Author:** 10x-Team (Architect + Staff Engineer)

## Context

L'accueil n'offre qu'un lien `mailto:`. Il n'y a donc ni validation, ni protection anti-bot, ni confirmation de soumission. GitHub Pages ne fournit pas de backend ni d'en-têtes configurables par projet.

## Decision

Déployer le site statique sur Cloudflare Pages et utiliser une Pages Function pour le formulaire. La fonction valide les données, vérifie Turnstile, applique une limite par adresse IP dans KV et remet un courriel texte à Resend. Les secrets restent dans Cloudflare.

## Alternatives Considered

| Alternative | Pros | Cons | Why Not |
|-------------|------|------|---------|
| Garder `mailto:` | Aucun backend | Perte de conversions, aucun contrôle | Ne répond pas au besoin |
| Service de formulaires tiers seul | Mise en route rapide | Contrôles et données confiés au prestataire | Moins de maîtrise |
| Pages Function + Resend | Contrôles serveur, faible coût, secrets isolés | Configuration Cloudflare/Resend nécessaire | Choisi |

## Consequences

### Positive
- Formulaire accessible, traçable et protégé.
- Les clés ne sont jamais livrées au navigateur.
- Les en-têtes et HTTPS sont configurables par l'hébergeur.

### Negative
- Le propriétaire doit connecter le domaine, créer les secrets et vérifier l'expéditeur Resend.

### Risks
- Une configuration de secrets incomplète empêche l'envoi : la fonction retourne une erreur générique et journalise le problème.
- Les règles de programmes d'aide changent : l'automatisation utilise uniquement les sources officielles et conserve une date de vérification.

## Dependencies
- Compte Cloudflare et domaine.
- Compte Resend et expéditeur vérifié.

