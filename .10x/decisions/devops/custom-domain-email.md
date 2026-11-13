# custom-domain-email

Domaine `gilbert-solution.ca` branché sur GitHub Pages le 2026-11-12. Voir ADR-002.

## État vérifié le 2026-11-12

| Élément | Valeur | Vérification |
|---|---|---|
| Apex A | `185.199.108.153`, `.109.153`, `.110.153`, `.111.153` | Résolution DNS publique |
| `www` CNAME | `zacharienoletgit.github.io` | Résolution DNS publique |
| MX | `0 mail.gilbert-solution.ca` | Résolution DNS publique |
| `mail` A | `67.215.15.226` (serveur WHC) | Résolution DNS publique |
| HTTPS apex | 200, certificat valide | `curl https://gilbert-solution.ca` |
| `www` | 301 vers l'apex | `curl` |
| Enforce HTTPS | Coché dans Settings → Pages | Relu après rechargement de la page |
| Redirection `http://` → `https://` | 301 vers `https://gilbert-solution.ca/` | `curl http://gilbert-solution.ca`, active environ 10 minutes après avoir coché (cache de GitHub) |

## Déploiement

Inchangé : une poussée sur `main` déclenche `pages.yml`, qui publie tout le dépôt. Le domaine personnalisé vit dans les réglages Pages, pas dans un fichier `CNAME`.

## Retour arrière

1. Dans cPanel WHC, éditeur de zone : remettre l'apex en A vers `67.215.15.226` et `www` en CNAME vers `gilbert-solution.ca`.
2. Dans Settings → Pages : retirer le domaine personnalisé. Le site redevient accessible à `zacharienoletgit.github.io/Gilbert-Solutions-Site/`.
3. Ne pas toucher au MX ni à `mail` : le courriel reste en service pendant le retour arrière.

## Enregistrements à ne jamais modifier sans plan

`MX`, `mail`, `default._domainkey`, `_dmarc`, SPF (TXT de l'apex), ainsi que `webmail`, `cpanel`, `ftp` et les autres sous-domaines de service WHC.
