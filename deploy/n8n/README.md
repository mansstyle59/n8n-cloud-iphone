# Orbit — n8n backend

This directory prepares a real, self-hosted n8n instance for Orbit. It is based on the official n8n Docker deployment approach and keeps the n8n database, workflows, credentials and encryption key in a persistent Docker volume.

## Important limitation

GitHub Pages only hosts the static Orbit interface. It cannot run n8n. This Compose stack must run on a machine or cloud service that supports persistent Docker containers and storage. A zero-cost permanent host is not guaranteed; check provider quotas and storage/billing before deploying.

## Start locally (test only)

1. Install Docker Engine + Docker Compose on a Linux server or a computer that will stay on.
2. Copy `.env.example` to `.env`.
3. Replace `N8N_ENCRYPTION_KEY` with a long random secret. Never commit `.env`.
4. Start n8n:

   ```sh
   docker compose up -d n8n
   docker compose logs -f n8n
   ```

5. Open `http://localhost:5678` on that same machine and create the n8n owner account.

This local-only configuration is not publicly reachable and is not a cloud deployment.

## Public access through Cloudflare Tunnel

Use this only after you have a persistent Docker host and a Cloudflare Tunnel:
1. In Cloudflare Zero Trust, create a Tunnel and configure its public hostname to forward to `http://n8n:5678`.
2. Copy the tunnel token into the untracked `.env` file.
3. Set `N8N_HOST` to your public hostname, `N8N_PROTOCOL=https`, `WEBHOOK_URL=https://YOUR_HOSTNAME/`, and `N8N_SECURE_COOKIE=true`.
4. Start both services:

   ```sh
   docker compose --profile public up -d
   ```

Do not expose port 5678 directly to the public internet. Protect the n8n editor with its owner account and keep the tunnel token private.

## Connect Orbit

Once n8n is actually hosted, import `../../n8n/workflow-chat-webhook.json`, add an AI model node with credentials configured inside n8n, restrict allowed origins to `https://mansstyle59.github.io`, activate the workflow and copy the production webhook URL into Orbit's webhook settings.

The workflow currently in this repository is a demonstration only; it does not call a language model yet. Do not consider Orbit's AI connection complete until a real prompt returns a model-generated response.
