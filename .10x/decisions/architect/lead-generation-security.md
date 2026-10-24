# lead-generation-security

Voir ADR-001. `index.html` devient une page de présentation qui charge CSS/JS/polices locaux. La frontière de confiance est `POST /api/contact`; le navigateur ne détient qu'une clé publique Turnstile. L'API dépend de bindings et secrets Cloudflare, jamais du contenu Git.

