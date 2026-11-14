# Gilbert — statut

- **Fonctionnalité active :** `lead-generation-security`
- **Phase :** Planning Complete.
- **Portée approuvée :** retrait de la page doublon, migration prête pour Cloudflare Pages, formulaire sécurisé, performance, pages légales séparées, en-têtes et CTA mobile.
- **Automatisation :** vérification officielle des aides, lundi et jeudi à 09:00 America/Toronto.
- **Décision :** conserver le site statique et externaliser uniquement le contact sécurisé vers Cloudflare Pages Functions.
- **ADR :** ADR-001 accepté.
- **Plan :** quatre lots ordonnés dans la décision Engineering Manager.

## Fonctionnalité en attente de fusion — `demarrage-entreprises` (2026-11-14)

- **But :** parler aussi aux personnes qui lancent leur entreprise et leur donner confiance qu'elles peuvent commencer.
- **Fait (branche `feature/cool-noether-o0iedv`) :** section `#demarrer` dans `index.html`, lien « Démarrer » dans les deux menus, mention dans le héros, les offres, les aides, la FAQ (deux questions, aussi dans le JSON-LD), le contact et les métadonnées.
- **Offre de lancement :** le premier client ne paie rien (diagnostic et première automatisation), une seule place. Affichée à quatre endroits, tous marqués `data-premier-client`.
- **Quand la place est prise :** retirer les quatre éléments `data-premier-client` de `index.html` (bandeau du haut, lien dans « Par où commencer », bloc au-dessus des offres, paragraphe du contact). Retirer aussi les quatre commentaires HTML « Offre premier client » ; le CSS `.launch-bar`, `.free-pill` et `.first-free` peut ensuite être supprimé.
- **Connu, hors de cette fonctionnalité :** `Gilbert.html` (doublon déjà noté à retirer) est publié avec l'ancien prix fixe de 490 $ pour 4 heures ; en impression, le contenu `.reveal` reste invisible tant qu'on n'a pas défilé la page ; les réponses de la FAQ « Et si ça brise ? » et « Et si on arrête le suivi mensuel ? » diffèrent entre le texte visible et le JSON-LD.
- **Fourchettes de prix (2026-11-14) :** chaque offre affiche une plage selon la solution et le temps. Diagnostic 490 $ à 980 $ (490 $ restent crédités sur la première automatisation), première automatisation 1 900 $ à 3 900 $, suivi mensuel 149 $ à 349 $. La plage du diagnostic est un choix de l'assistant, à confirmer.
- **Mise en avant du démarrage (2026-11-14) :** héros recentré sur le lancement d'entreprise, section `#demarrer` placée avant les situations PME, nouvelle section `#donne` (ce que l'IA change, avant/aujourd'hui), question de FAQ sur les outils qui changent vite.
- **À confirmer (propriétaire) :** si le premier échange est gratuit, l'écrire ; décider d'un éventuel tarif de démarrage ; vérifier auprès des organismes les aides au démarrage avant d'afficher un montant (SADC, organisme de développement économique de la MRC, Futurpreneur : nommés sans montant).

## Fonctionnalité livrée — `custom-domain-email` (2026-11-12)

- **Phase :** Delivery Complete pour le site ; courriel partiellement en place.
- **ADR :** ADR-002 accepté (domaine sur GitHub Pages, DNS et courriel chez WHC).
- **Fait :** DNS branchés, domaine personnalisé inscrit, Enforce HTTPS coché, PR #5 fusionnée, boîte `zacharie@gilbert-solution.ca` créée.
- **Vérifié :** `https://gilbert-solution.ca` répond 200, `http://` redirige en 301 vers HTTPS, `www` redirige vers l'apex, la page annonce la nouvelle adresse canonique.
- **Reste à faire (propriétaire) :**
  - Créer la redirection `zacharie@gilbert-solution.ca` vers Gmail dans cPanel, puis ajouter l'adresse dans « Envoyer des courriels en tant que » de Gmail (SMTP `mail.gilbert-solution.ca`, port 465, SSL).
  - Garder le forfait WHC à jour : il porte le DNS et le courriel.
- **Impact sur `lead-generation-security` :** la bascule vers Cloudflare Pages doit suivre l'ordre décrit dans les risques d'ADR-002.

