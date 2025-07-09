# Portainer Stacks

This repository contains a collection of Docker Compose stacks managed via [Portainer](https://www.portainer.io/). Each stack is designed for easy deployment and management of self-hosted services, leveraging Traefik as a reverse proxy and NFS for persistent storage.

## Stacks Overview

- **traefik**: Reverse proxy and SSL termination for all services.
- **jellyfin**: Media server with related tools (Jellyseerr, Sonarr, Radarr, Prowlarr).
- **torrent**: Torrenting stack (qBittorrent, Jackett, FlareSolverr).
- **gitea**: Self-hosted Git service.
- **rsyslog**: Centralized syslog server.
- **serial**: Serial-to-network bridge (ser2net).
- **nutweb**: Web GUI for Network UPS Tools.
- **newrelic**: Infrastructure monitoring agent.

## Requirements

- Docker & Docker Compose
- Portainer (optional, but recommended)
- NFS server for persistent volumes
- Properly configured `.env` files for each stack

## Usage

1. **Clone this repository:**

   ```sh
   git clone https://github.com/gringolito/portainer-stacks.git
   cd portainer-stacks
   ```

1. **Configure environment variables:**
   - Copy and edit `.env.example` (if available) or set environment variables as needed for each stack.

1. **Deploy a stack:**
   - Using Docker Compose:

     ```sh
     docker compose -f <stack>/docker-compose.yaml up -d
     ```

   - Or import the stack YAML into Portainer.

1. **Access services:**
   - Services are available via Traefik at subdomains (e.g., `https://jellyfin.yourdomain.com`).

## Notes

- All stacks are configured to use a shared external network (`proxy-network`) for Traefik routing.
- NFS is used for persistent storage; ensure your NFS server and shares are accessible.
- Review and adjust environment variables and volume paths as needed for your environment.
