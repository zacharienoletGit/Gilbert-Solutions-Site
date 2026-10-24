# lead-generation-security

1. Créer ressources et pages légales, retirer le doublon, corriger SEO/aides.
2. Ajouter formulaire, merci et CTA mobile.
3. Ajouter Function, règles d'en-têtes et documentation de déploiement.
4. Vérifier HTML, liens, comportement client et absence de secrets.

### Découpage

- `index.html` : conserver le contenu commercial, remplacer le bloc contact, ajouter les liens légaux et la date des aides.
- `assets/site.css`, `assets/site.js`, `assets/fonts/` : extraire les ressources clientes et ajouter les états de formulaire/CTA.
- `functions/api/contact.js` : frontière serveur et traitement du formulaire.
- `confidentialite/index.html`, `conditions/index.html`, `merci/index.html` : pages informatives et retour de soumission.
- `_headers`, `DEPLOYMENT.md` : sécurité et procédure Cloudflare.
- `Gilbert.html` : suppression après vérification qu'aucun fichier ne le référence.

