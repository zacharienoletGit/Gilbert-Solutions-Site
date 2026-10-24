# lead-generation-security

La Function accepte seulement POST JSON, impose tailles et champs attendus, rejette le champ piège, vérifie Turnstile côté serveur, applique une fenêtre de limite et retourne des erreurs génériques. La notification est texte brut avec champs encodés, éliminant l'injection HTML.

L'interface valide d'abord les champs HTML, affiche les erreurs dans une région ARIA et bloque le double envoi. Elle dégrade vers l'adresse courriel visible si JavaScript est indisponible. Le script Turnstile est chargé seulement lorsqu'une clé publique a été configurée.

