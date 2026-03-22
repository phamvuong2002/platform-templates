PROJECT MEMORY

Deployment standard:

- Production deploy standard: Docker Swarm
- CI/CD standard: GitHub Actions self-hosted runner
- Registry standard: GHCR
- Release tag standard: immutable SHA tags
- Push to main triggers production deploy by default

Ingress standard:

- Public ingress standard: Traefik
- Shared ingress network: edge
- Frontend domain pattern: app-<app>.phamvuong.io.vn
- Backend domain pattern: api-<app>.phamvuong.io.vn
- No direct host port binding for standard public web/API apps unless explicitly approved

Repo standard:

- One backend repo per app: <app>-api
- One frontend repo per app: <app>-web

Filesystem standard:

- Backend stack path: /opt/stacks/<app>-api
- Frontend stack path: /opt/stacks/<app>-web
- Persistent data path: /srv/data/<app>

Service standard:

- Standard service names: api, web, worker, cron
- Cron belongs in the same backend stack

Frontend standard:

- Default frontend stack: React SPA + nginx
- SPA fallback routing via nginx try_files to /index.html
- Frontend env must contain public-safe values only

Backend standard:

- Typical runtimes: Node/NestJS, Python, Go
- Public APIs must have healthcheck
- Logs should go to stdout/stderr and be aggregatable

Data standard:

- Primary databases are cloud-managed, not hosted on this server by default

Observability standard:

- Production apps should support centralized logging
- Quick debug starts with docker stack/services/logs and health checks

Hard rules:

- No build step in production swarm stack files
- Production stacks must use prebuilt GHCR images
- Rollback must be possible by previous image tag
- Do not place real secrets in repo
- Do not hardcode real secrets in frontend builds

Open decisions:

- Standard template for worker-enabled backend
- Standard deployment checklist before adding new public domains
