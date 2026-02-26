# Torrent Stack

This stack deploys a full torrent/media automation suite with Docker Compose and Traefik integration.

## Services

- qBittorrent: Torrent client that downloads and seeds content.
- FlareSolverr: Proxy service used to bypass anti-bot protections on some indexers.
- Jackett: Aggregates torrent indexers and exposes them to the *arr apps.
- Seerr: Request management UI for users to request movies and series.
- Sonarr: TV series automation (search, grab, and library management).
- Radarr: Movie automation (search, grab, and library management).
- Prowlarr: Indexer manager and sync hub for Sonarr, Radarr, and other *arr apps.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `TORRENT_PUBLIC_DOMAIN` | Base domain used by all Traefik host rules | | `example.com` |
| `TORRENT_NETWORK` | External Docker network name used by this stack | | `proxy-network` |
| `DOWNLOADS_GROUPID` | Shared GID for containers that need access to downloads | `1000` | `1000` |

### qBittorrent

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `QBITTORRENT_TAG` | qBittorrent image tag | `latest` | `latest` |
| `QBITTORRENT_USERID` | UID used by qBittorrent | `1000` | `1000` |
| `QBITTORRENT_GROUPID` | GID used by qBittorrent | `1000` | `1000` |
| `QBITTORRENT_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `QBITTORRENT_MEM_LIMIT` | Memory limit for container | `1g` | `2g` |
| `QBITTORRENT_CONFIG_VOLUME` | External volume name for qBittorrent config | | `qbittorrent-config` |
| `TORRENT_DOWNLOADS_VOLUME` | External volume name for shared downloads | | `torrent-downloads` |

### FlareSolverr

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `FLARESOLVERR_TAG` | FlareSolverr image tag | `latest` | `latest` |
| `FLARESOLVERR_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `FLARESOLVERR_CAPTCHA_SOLVER` | CAPTCHA solver backend | `none` | `none` |
| `FLARESOLVERR_LANG` | Language | `en_US` | `en_US` |
| `FLARESOLVERR_LOG_LEVEL` | Log level | `info` | `debug` |
| `FLARESOLVERR_LOG_HTML` | Enable HTML logging | `false` | `true` |

### Jackett

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `JACKETT_TAG` | Jackett image tag | `latest` | `latest` |
| `JACKETT_USERID` | UID used by Jackett | `1000` | `1000` |
| `JACKETT_GROUPID` | GID used by Jackett | `1000` | `1000` |
| `JACKETT_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `JACKETT_CONFIG_VOLUME` | External volume name for Jackett config | | `jackett-config` |

### Seerr

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `SEERR_TAG` | Seerr image tag | `latest` | `latest` |
| `SEERR_USERID` | UID used by Seerr | `1000` | `1000` |
| `SEERR_GROUPID` | GID used by Seerr | `1000` | `1000` |
| `SEERR_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `SEERR_LOG_LEVEL` | Log level | `debug` | `info` |
| `SEERR_CONFIG_VOLUME` | External volume name used for Seerr config | | `seerr-config` |

### Sonarr

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `SONARR_TAG` | Sonarr image tag | `release` | `release` |
| `SONARR_USERID` | UID used by Sonarr | `1000` | `1000` |
| `SONARR_GROUPID` | GID used by Sonarr | `1000` | `1000` |
| `SONARR_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `SONARR_CONFIG_VOLUME` | External volume name for Sonarr config | | `sonarr-config` |

### Radarr

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `RADARR_TAG` | Radarr image tag | `release` | `release` |
| `RADARR_USERID` | UID used by Radarr | `1000` | `1000` |
| `RADARR_GROUPID` | GID used by Radarr | `1000` | `1000` |
| `RADARR_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `RADARR_CONFIG_VOLUME` | External volume name for Radarr config | | `radarr-config` |

### Prowlarr

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `PROWLARR_TAG` | Prowlarr image tag | `release` | `release` |
| `PROWLARR_USERID` | UID used by Prowlarr | `1000` | `1000` |
| `PROWLARR_GROUPID` | GID used by Prowlarr | `1000` | `1000` |
| `PROWLARR_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `PROWLARR_CONFIG_VOLUME` | External volume name for Prowlarr config | | `prowlarr-config` |

## Volumes

Declared volumes in this stack:

- `qbittorrent` (external, `QBITTORRENT_CONFIG_VOLUME`)
- `downloads` (external, `TORRENT_DOWNLOADS_VOLUME`)
- `jackett` (external, `JACKETT_CONFIG_VOLUME`)
- `seerr` (external, `SEERR_CONFIG_VOLUME`)
- `sonarr` (external, `SONARR_CONFIG_VOLUME`)
- `radarr` (external, `RADARR_CONFIG_VOLUME`)
- `prowlarr` (external, `PROWLARR_CONFIG_VOLUME`)
- `flaresolverr` (local Docker-managed volume)

## Networks

- `proxy-network` (external, name from `TORRENT_NETWORK`)

## Traefik Routes

- `torrent.${TORRENT_PUBLIC_DOMAIN}` → qBittorrent (port `8080`)
- `flaresolverr.${TORRENT_PUBLIC_DOMAIN}` → FlareSolverr (port `8191`)
- `jackett.${TORRENT_PUBLIC_DOMAIN}` → Jackett (port `9117`)
- `seerr.${TORRENT_PUBLIC_DOMAIN}` → Seerr (port `5055`)
- `sonarr.${TORRENT_PUBLIC_DOMAIN}` → Sonarr (port `8989`)
- `radarr.${TORRENT_PUBLIC_DOMAIN}` → Radarr (port `7878`)
- `prowlarr.${TORRENT_PUBLIC_DOMAIN}` → Prowlarr (port `9696`)

## Exposed Ports

- `6881:6881` for qBittorrent torrenting traffic
