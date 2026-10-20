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

## Déployer le vrai serveur n8n

Un guide de déploiement Docker avec stockage persistant est disponible dans [`deploy/n8n/README.md`](deploy/n8n/README.md), avec `compose.yaml` et `.env.example`.

**Important :** cette configuration prépare l'installation, mais ne crée pas à elle seule un serveur public. Il faut l'exécuter sur un hôte qui accepte les conteneurs Docker et conserve un volume de données. GitHub Pages ne peut pas exécuter n8n. Le workflow d'exemple reste une démonstration sans modèle IA connecté.


## Déployer n8n sur Render (prototype gratuit)

Le dépôt inclut maintenant :
- `deploy/n8n/Dockerfile`, basé sur l'image officielle n8n épinglée à la version `2.44.4` ;
- `render.yaml`, un Blueprint Render pour créer le service `orbit-n8n-iphone` ;
- `n8n/workflow-chat-webhook.json`, un workflow de test qui renvoie une réponse de démonstration.

### Lancement

1. Ouvrir [Render Blueprint](https://dashboard.render.com/blueprints) depuis le compte Render lié à GitHub.
2. Choisir le dépôt `mansstyle59/n8n-cloud-iphone` et le fichier `render.yaml`.
3. Examiner le plan affiché avant de confirmer : le Blueprint est prévu en `free`.
4. Attendre la fin du déploiement, puis ouvrir l'URL du service Render et créer le compte propriétaire n8n.
5. Dans n8n, importer `n8n/workflow-chat-webhook.json`, ouvrir le workflow, activer le workflow, puis copier l'URL **Production** du webhook.
6. Dans Orbit, ouvrir **Réglages** et coller cette URL. Le workflow actuel est un test et ne produit pas de réponse IA réelle avant l'ajout d'un nœud de modèle et la configuration de ses identifiants côté serveur.

### Limite importante du plan gratuit

Le service web gratuit Render peut se mettre en veille et son système de fichiers est éphémère. Les workflows, comptes ou identifiants peuvent être perdus après un redéploiement ou un redémarrage. Ce Blueprint sert à valider l'installation, pas à garantir une instance n8n durable. Pour une utilisation fiable, il faut une base PostgreSQL et un stockage persistant compatibles avec le plan choisi. Ne saisis pas de données sensibles tant que la persistance et la sécurité n'ont pas été vérifiées.

La Community Edition auto-hébergée de n8n est gratuite, mais l'hébergement permanent n'est pas automatiquement gratuit. Voir [la documentation officielle n8n](https://docs.n8n.io/deploy/host-n8n/) et [la licence d'utilisation](https://support.n8n.io/article/can-i-use-your-license-for-my-use-case).
