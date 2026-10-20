# N8N Cloud iPhone — portail Chat IA

Interface web mobile-first pour discuter avec un workflow n8n depuis iPhone. Le dépôt contient :
- une interface de chat responsive et installable comme raccourci Safari ;
- une configuration d'URL de webhook n8n côté navigateur ;
- un workflow d'exemple à importer dans n8n ;
- un workflow GitHub Actions pour publier l'interface statique sur GitHub Pages.

## Important
GitHub Pages héberge uniquement l'interface statique, pas le serveur n8n. Le serveur n8n doit être déployé séparément sur un hébergeur qui permet un processus persistant et un stockage durable.

Ne placez jamais de clés API de fournisseurs IA dans le code frontend ni dans ce dépôt. Stockez-les dans les identifiants n8n / variables secrètes du serveur.

## Déploiement de l'interface
1. Ouvrez **Settings → Pages** dans ce dépôt.
2. Dans **Build and deployment**, choisissez **GitHub Actions**.
3. Le workflow `.github/workflows/pages.yml` publiera `index.html` sur chaque push sur `main`.
4. L'URL du site sera affichée dans **Settings → Pages** après la réussite du workflow.

## Connexion à n8n
1. Déployez n8n séparément.
2. Importez `n8n/workflow-chat-webhook.json` dans n8n.
3. Configurez le nœud de réponse pour appeler le modèle IA voulu et ne partagez jamais ses clés avec le navigateur.
4. Activez le workflow, copiez son URL de production, puis collez-la dans **Réglages → Webhook n8n** de l'interface.

Le workflow fourni est un squelette pédagogique : il reçoit un message et renvoie une réponse de démonstration. Il n'appelle aucun modèle IA tant que vous ne l'avez pas connecté à un nœud de fournisseur IA et configuré ses identifiants.

## Fonctionnalités
- conversations locales dans le navigateur ;
- sélection de mode (Assistant, Rédaction, Code, Recherche) ;
- connexion configurable à un webhook n8n ;
- indicateur d'état de connexion ;
- interface adaptée aux écrans mobiles.
