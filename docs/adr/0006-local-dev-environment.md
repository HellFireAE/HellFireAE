# Local dev: containerised stack with reverse proxy

## Status
Accepted

## Context
Projects require a local runtime environment. A shared reverse proxy is needed to route multiple local sites by hostname without port collision. Platform-specific constraints (WSL2, Apple Silicon, etc.) may affect which Docker configurations are valid.

## Decision
Projects run locally via Docker Compose behind a shared reverse proxy (e.g. Caddy or Traefik) routing by hostname.

## Stack

| Component | Location | Notes |
|-----------|----------|-------|
| Proxy | `~/docker/proxy/` | Routes by hostname, owns ports 80/443 |
| Site | `src/[your-project]/` | `docker compose up -d` |
| URL | `http://[your-project].local` | Add `127.0.0.1 [your-project].local` to `/etc/hosts` |

## Consequences

- Proxy must be started before site containers
- `/etc/hosts` entry required; needs `sudo` (cannot be automated by AI agent)
- Each new project must add a stanza to the proxy config and join the proxy Docker network
- Document any platform-specific constraints (WSL2, Apple Silicon, etc.) here as they are discovered
