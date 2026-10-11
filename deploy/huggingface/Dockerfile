# n8n 2.43.3 con la interfaz en español rioplatense, para Hugging Face Spaces (SDK Docker).
# Usa la imagen oficial y reemplaza solo el frontend (editor-ui) por la versión traducida.
FROM n8nio/n8n:2.43.3

ARG EDITOR_UI_URL=https://github.com/franco-valenzuela/n8n/releases/download/es-AR-2.43.3/editor-ui-dist.tar.gz

USER root
ADD ${EDITOR_UI_URL} /tmp/editor-ui-dist.tar.gz
RUN set -eux; \
	DIST="$(node -e "console.log(require('path').dirname(require.resolve('n8n-editor-ui', { paths: ['/usr/local/lib/node_modules/n8n'] })))")/dist"; \
	rm -rf "$DIST"; \
	mkdir -p "$DIST"; \
	tar -xzf /tmp/editor-ui-dist.tar.gz -C "$DIST"; \
	rm /tmp/editor-ui-dist.tar.gz; \
	printf '#!/bin/sh\nif [ -n "$SPACE_HOST" ] && [ -z "$WEBHOOK_URL" ]; then export WEBHOOK_URL="https://$SPACE_HOST/"; fi\nif [ -n "$SPACE_HOST" ] && [ -z "$N8N_EDITOR_BASE_URL" ]; then export N8N_EDITOR_BASE_URL="https://$SPACE_HOST/"; fi\nexec /docker-entrypoint.sh "$@"\n' > /hf-entrypoint.sh; \
	chmod +x /hf-entrypoint.sh

USER node

# Hugging Face expone el puerto definido en app_port del README (7860).
ENV N8N_PORT=7860 \
	N8N_PROTOCOL=https \
	N8N_PROXY_HOPS=1 \
	N8N_DEFAULT_LOCALE=es \
	GENERIC_TIMEZONE=America/Argentina/Buenos_Aires \
	TZ=America/Argentina/Buenos_Aires \
	N8N_DIAGNOSTICS_ENABLED=false \
	N8N_RUNNERS_ENABLED=true

EXPOSE 7860
ENTRYPOINT ["tini", "--", "/hf-entrypoint.sh"]
