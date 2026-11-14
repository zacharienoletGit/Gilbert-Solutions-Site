# custom-domain-email

## Revue du 2026-11-12

- **Transport :** HTTPS actif sur l'apex et sur `www`, Enforce HTTPS coché, `http://` redirige en 301 vers HTTPS (vérifié). GitHub Pages ne permet pas d'ajouter HSTS ni CSP : ces en-têtes restent à livrer avec la migration d'ADR-001.
- **Courriel :** SPF, DKIM (`default._domainkey`) et DMARC existent dans la zone. DMARC est à `p=none`, donc sans protection contre l'usurpation du domaine. À resserrer vers `quarantine` après quelques semaines d'envois sans incident.
- **SPF :** le mécanisme `+a` autorise maintenant les adresses de GitHub Pages, qui n'envoient aucun courriel pour le domaine. Risque faible, mais à retirer.
- **Secrets :** aucun secret dans le dépôt pour cette fonctionnalité. Le mot de passe de la boîte `zacharie@gilbert-solution.ca` n'est connu que du propriétaire.
- **Redirection de courriel :** une redirection `master@gilbert-solution.ca` vers une adresse personnelle existait déjà dans cPanel. Toute redirection copie le courrier chez un tiers : en tenir la liste à jour.

## Points ouverts

- Décider de la politique DMARC cible et de la date de passage.
