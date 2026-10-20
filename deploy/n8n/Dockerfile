# Orbit n8n runtime — official upstream image, pinned to a release.
# Render free services have ephemeral storage and can sleep; use only for a prototype
# unless a persistent volume/database is configured.
FROM n8nio/n8n:2.44.4

# Render's default web-service port is 10000. The upstream image runs n8n directly;
# do not use a shell wrapper because the image is intentionally minimal.
ENV N8N_PORT=10000 \
    N8N_PROTOCOL=https \
    N8N_DIAGNOSTICS_ENABLED=false \
    N8N_PERSONALIZATION_ENABLED=false

EXPOSE 10000
