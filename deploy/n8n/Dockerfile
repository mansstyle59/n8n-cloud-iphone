# Orbit n8n runtime — official upstream image, pinned to a release.
# Render free services have ephemeral storage and can sleep; use only for a prototype
# unless a persistent volume/database is configured.
FROM n8nio/n8n:2.44.4

ENV N8N_PORT=5678 \
    N8N_PROTOCOL=https \
    N8N_DIAGNOSTICS_ENABLED=false \
    N8N_PERSONALIZATION_ENABLED=false

# Render supplies PORT; keep n8n's listener aligned with the assigned port.
CMD ["sh", "-c", "export N8N_PORT=${PORT:-5678}; exec n8n start"]

EXPOSE 5678
