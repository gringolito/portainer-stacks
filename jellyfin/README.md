# Jellyfin Media Stack

This stack deploys a full media management suite using Docker Compose, including Jellyfin, Jellyseerr, Sonarr, Radarr, and Prowlarr, with persistent storage and Traefik integration.

## Services

- **Jellyfin**: Media server for streaming.
- **Jellyseerr**: Media request and management.
- **Sonarr**: TV series management.
- **Radarr**: Movie management.
- **Prowlarr**: Indexer manager for Sonarr/Radarr.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

### Jellyfin

| Variable                    | Description                                | Default Value           | Example                   |
|-----------------------------|--------------------------------------------|------------------------|---------------------------|
| `JELLYFIN_TAG`              | Jellyfin image tag                         | `latest`               | `10.8.10`                 |
| `JELLYFIN_UID`              | UID for Jellyfin user                      | `1000`                 | `1000`                    |
| `JELLYFIN_GID`              | GID for Jellyfin user                      | `1000`                 | `1000`                    |
| `JELLYFIN_TZ`               | Timezone                                   | `America/Sao_Paulo`    | `Europe/Berlin`           |
| `JELLYFIN_PUBLIC_DOMAIN`    | Public domain for Jellyfin                 |                        | `example.com`             |

### Jellyseer

| Variable                    | Description                                | Default Value           | Example                   |
|-----------------------------|--------------------------------------------|------------------------|---------------------------|
| `JELLYSEERR_TAG`            | Jellyseerr image tag                       | `latest`               | `1.7.0`                   |
| `JELLYSEER_LOG_LEVEL`       | Log level for Jellyseerr                   | `debug`                | `info`                    |
| `JELLYSEER_TZ`              | Timezone for Jellyseerr                    | `America/Sao_Paulo`    | `Europe/Berlin`           |
| `JELLYSEERR_PUBLIC_DOMAIN`  | Public domain for Jellyseerr               |                        | `example.com`             |

### Sonarr

| Variable                    | Description                                | Default Value           | Example                   |
|-----------------------------|--------------------------------------------|------------------------|---------------------------|
| `SONARR_TAG`                | Sonarr image tag                           | `latest`               | `4.0.0.0`                 |
| `SONARR_UID`                | UID for Sonarr user                        | `1200`                 | `1200`                    |
| `SONARR_GID`                | GID for Sonarr user                        | `1000`                 | `1000`                    |
| `SONARR_UMAST`              | Umask for Sonarr                           | `002`                  | `002`                     |
| `SONARR_TZ`                 | Timezone for Sonarr                        | `America/Sao_Paulo`    | `Europe/Berlin`           |
| `SONARR_PUBLIC_DOMAIN`      | Public domain for Sonarr                   |                        | `example.com`             |

### Radarr

| Variable                    | Description                                | Default Value           | Example                   |
|-----------------------------|--------------------------------------------|------------------------|---------------------------|
| `RADARR_TAG`                | Radarr image tag                           | `latest`               | `5.0.0.0`                 |
| `RADARR_UID`                | UID for Radarr user                        | `1300`                 | `1300`                    |
| `RADARR_GID`                | GID for Radarr user                        | `1000`                 | `1000`                    |
| `RADARR_UMAST`              | Umask for Radarr                           | `002`                  | `002`                     |
| `RADARR_TZ`                 | Timezone for Radarr                        | `America/Sao_Paulo`    | `Europe/Berlin`           |
| `RADARR_PUBLIC_DOMAIN`      | Public domain for Radarr                   |                        | `example.com`             |

### Prowlarr

| Variable                    | Description                                | Default Value           | Example                   |
|-----------------------------|--------------------------------------------|------------------------|---------------------------|
| `PROWLARR_TAG`              | Prowlarr image tag                         | `latest`               | `1.0.0.0`                 |
| `PROWLARR_PUBLIC_DOMAIN`    | Public domain for Prowlarr                 |                        | `example.com`             |

### Persistent volumes

| Variable                    | Description                                | Default Value           | Example                   |
|-----------------------------|--------------------------------------------|------------------------|---------------------------|
| `NFS_SERVER`                | NFS server address                         |                        | `192.168.1.10`            |
| `NFS_JELLYFIN_MEDIA_SHARE`  | NFS share for media                        |                        | `/export/media`           |

## Volumes

- `media`: Media files (NFS)
- `data`: Downloaded data (external, named `torrent_data`)
- `config`, `cache`, `jellyseerr`, `sonarr`, `radarr`, `prowlarr`: App configs

## Networks

- `proxy-network`: External network for Traefik

## Traefik Integration

All services are pre-configured for Traefik. Ensure Traefik is running and attached to the `proxy-network`.

## Accessing Services

- Jellyfin: `https://jellyfin.yourdomain.com`
- Jellyseerr: `https://jellyseerr.yourdomain.com`
- Sonarr: `https://sonarr.yourdomain.com`
- Radarr: `https://radarr.yourdomain.com`
- Prowlarr: `https://prowlarr.yourdomain.com`
