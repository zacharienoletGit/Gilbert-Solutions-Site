# Gilbert — Solutions IA

Site vitrine d'une page pour Gilbert, automatisation par IA pour les PME et les entreprises en démarrage du Centre-du-Québec.

## Structure

- `index.html` : la page complète (HTML, CSS et JavaScript inclus, sans dépendance externe).
- `assets/gilbert-mark.svg`, `assets/favicon.svg` : le cavalier vectoriel et le favicon.
- `assets/gilbert-hero-direction.png` : l'image affichée quand le lien est partagé; le cavalier du héros est dessiné en SVG pour rester net à toute taille.
- Les polices Bricolage Grotesque et Source Sans 3 sont intégrées dans `index.html`, donc la page fonctionne seule, même ouverte depuis le disque.
- `.github/workflows/pages.yml` : publication automatique sur GitHub Pages à chaque poussée sur `main`.

## Voir le site en local

Ouvrir `index.html` dans un navigateur suffit. Pour un serveur local :

```
npx http-server . -p 8080
```

## Publier

1. Dans les réglages du dépôt, section **Pages**, choisir **GitHub Actions** comme source.
2. Fusionner sur `main`. Le site est servi à `https://gilbert-solution.ca/`.
3. Le domaine personnalisé `gilbert-solution.ca` est inscrit dans **Settings → Pages** (pas de fichier `CNAME` : il est ignoré quand la source est GitHub Actions). La zone DNS et le courriel sont chez WHC ; voir `.10x/adrs/002-domaine-github-pages-courriel-whc.md` avant de modifier un enregistrement.
