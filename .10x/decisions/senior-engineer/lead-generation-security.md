# lead-generation-security

La Function accepte seulement POST JSON, impose tailles et champs attendus, rejette le champ piège, vérifie Turnstile côté serveur, applique une fenêtre de limite et retourne des erreurs génériques. La notification est texte brut avec champs encodés, éliminant l'injection HTML.

