# Torrent Stack

This stack deploys a torrent management suite using Docker Compose, including qBittorrent, Jackett, and FlareSolverr, with persistent storage and Traefik integration.

## Services

- **qBittorrent**: Torrent client with web UI.
- **Jackett**: Indexer proxy for torrent trackers.
- **FlareSolverr**: Proxy for bypassing anti-bot pages.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

### qBittorrent

| Variable                        | Description                                | Default Value           | Example                   |
|----------------------------------|--------------------------------------------|------------------------|---------------------------|
| `QBITTORRENT_TAG`               | qBittorrent image tag                      | `latest`               | `4.5.2`                   |
| `QBITTORRENT_TZ`                | Timezone for qBittorrent                   |                        | `Europe/Berlin`           |
| `QBITTORRENT_PUBLIC_DOMAIN`     | Public domain for qBittorrent              |                        | `example.com`             |

### Jackett

| Variable                        | Description                                | Default Value           | Example                   |
|----------------------------------|--------------------------------------------|------------------------|---------------------------|
| `JACKETT_TAG`                   | Jackett image tag                          | `latest`               | `0.21.0`                  |
| `JACKETT_TZ`                    | Timezone for Jackett                       |                        | `Europe/Berlin`           |
| `JACKET_PUBLIC_DOMAIN`          | Public domain for Jackett                  |                        | `example.com`             |

### Flaresolverr

| Variable                        | Description                                | Default Value           | Example                   |
|----------------------------------|--------------------------------------------|------------------------|---------------------------|
| `FLARESOLVERR_TAG`              | FlareSolverr image tag                     | `latest`               | `3.3.16`                  |
| `FLARESOLVERR_TZ`               | Timezone for FlareSolverr                  |                        | `Europe/Berlin`           |
| `FLARESOLVERR_PUBLIC_DOMAIN`    | Public domain for FlareSolverr             |                        | `example.com`             |
| `FLARESOLVERR_CAPTCHA_SOLVER`   | Captcha solver                             | `none`                 | `none`                    |
| `FLARESOLVERR_LANG`             | Language                                   | `en_US`                | `en_US`                   |
| `FLARESOLVERR_LOG_LEVEL`        | Log level                                  | `info`                 | `debug`                   |
| `FLARESOLVERR_LOG_HTML`         | Log HTML                                   | `false`                | `true`                    |

### Persistent volumes

| Variable                        | Description                                | Default Value           | Example                   |
|----------------------------------|--------------------------------------------|------------------------|---------------------------|
| `NFS_SERVER`                    | NFS server address                         |                        | `192.168.1.10`            |
| `NFS_QBITTORRENT_CONFIG_SHARE`  | NFS share for qBittorrent config           |                        | `/export/qbittorrent`     |
| `NFS_TORRENTS_SHARE`            | NFS share for torrents                     |                        | `/export/torrents`        |
| `NFS_DATA_SHARE`                | NFS share for data                         |                        | `/export/data`            |

## Volumes

- `config`: qBittorrent config (NFS)
- `torrents`: Torrent files (NFS)
- `data`: Downloaded data (NFS)
- `jackett-config`, `jackett-data`: Jackett configs

## Networks

- `proxy-network`: External network for Traefik

## Traefik Integration

All services are pre-configured for Traefik. Ensure Traefik is running and attached to the `proxy-network`.

## Accessing Services

- qBittorrent: `https://qbittorrent.yourdomain.com`
- Jackett: `https://jackett.yourdomain.com`
- FlareSolverr: `https://flaresolverr.yourdomain.com`
