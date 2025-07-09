# Traefik Reverse Proxy Stack

This stack deploys [Traefik](https://traefik.io/) as a reverse proxy and SSL provider for your Docker services, with persistent configuration and certificate storage on NFS.

## Services

- **Traefik**: Reverse proxy, SSL termination, and dashboard.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable                      | Description                                 | Default Value           | Example                |
|-------------------------------|---------------------------------------------|------------------------|------------------------|
| `TRAEFIK_TAG`                 | Traefik image tag                           | `latest`               | `2.10`                 |
| `TRAEFIK_TZ`                  | Timezone                                    | `America/Sao_Paulo`    | `Europe/Berlin`        |
| `TRAEFIK_PUBLIC_DOMAIN`       | Public domain for Traefik                   |                        | `example.com`          |
| `TRAEFIK_TRUSTED_NETWORKS`    | Trusted IPs for forwarded headers           |                        | `172.18.0.0/16`        |
| `TRAEFIK_LOG_LEVEL`           | Log level                                   | `INFO`                 | `DEBUG`                |
| `TRAEFIK_TRACING`             | Enable tracing                              | `false`                | `true`                 |
| `TRAEFIK_ACCESS_LOGS`         | Enable access logs                          | `false`                | `true`                 |
| `TRAEFIK_ACCESS_LOG_OLTP`     | Enable OTLP for access logs                 | `false`                | `true`                 |
| `LETSENCRYPT_EMAIL`           | Email for Let's Encrypt registration        |                        | `admin@example.com`    |
| `CLOUDFLARE_EMAIL`            | Cloudflare account email                    |                        | `user@example.com`     |
| `CLOUDFLARE_DNS_API_TOKEN`    | Cloudflare DNS API token                    |                        | `token`                |
| `NFS_SERVER`                  | NFS server address                          |                        | `192.168.1.10`         |
| `NFS_TRAEFIK_SHARE`           | NFS share for Traefik config                |                        | `/export/traefik`      |
| `NFS_LETSENCRYPT_SHARE`       | NFS share for Let's Encrypt certs           |                        | `/export/letsencrypt`  |

## Volumes

- `traefik`: Traefik configuration (NFS)
- `letsencrypt`: Let's Encrypt certificates (NFS)

## Networks

- `proxy-network`: External network for Traefik and services

## Traefik Dashboard

Access the dashboard at:  
`https://traefik.yourdomain.com`
