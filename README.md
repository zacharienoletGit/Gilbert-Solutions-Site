# Gilbert — Solutions IA

Site vitrine d'une page pour Gilbert, automatisation par IA pour les PME du Centre-du-Québec.

## Structure

- `index.html` : la page complète (HTML, CSS et JavaScript inclus, sans dépendance externe).
- `assets/gilbert-mark.svg`, `assets/favicon.svg` : le logo vectoriel.
- `assets/og-image.png` : l'image affichée quand le lien est partagé (LinkedIn, Facebook, Messenger).
- Les polices Bricolage Grotesque et Source Sans 3 sont intégrées dans `index.html`, donc la page fonctionne seule, même ouverte depuis le disque.
- `.github/workflows/pages.yml` : publication automatique sur GitHub Pages à chaque poussée sur `main`.

## Voir le site en local

Ouvrir `index.html` dans un navigateur suffit. Pour un serveur local :

```
npx http-server . -p 8080
```

## Publier

1. Dans les réglages du dépôt, section **Pages**, choisir **GitHub Actions** comme source.
2. Fusionner sur `main`. Le site est servi à `https://zacharienoletgit.github.io/Gilbert-Solutions-Site/`.
3. Pour un domaine personnalisé, ajouter un fichier `CNAME` à la racine et remplacer l'adresse dans les balises `canonical`, `og:url`, `og:image` et dans `sitemap.xml`.
