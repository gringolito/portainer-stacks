# Gitea Docker Compose Stack

This stack deploys a [Gitea](https://gitea.io/) server using Docker Compose, with persistent storage on NFS volumes and Traefik as a reverse proxy.

## Features

- Gitea server container
- NFS-backed volumes for data and repositories
- Traefik integration for HTTP routing
- SSH access for Git operations

## Usage

1. Copy or clone this directory to your Docker host.
1. Set the required environment variables (see below).
1. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable             | Description                        | Default Value           | Example                |
|----------------------|------------------------------------|------------------------|------------------------|
| `GITEA_TAG`          | Gitea image tag                    | `latest`               | `1.21.0`               |
| `GITEA_TZ`           | Timezone                           | `America/Sao_Paulo`    | `Europe/Berlin`        |
| `GITEA_USERID`       | UID/GID for Gitea user             |                        | `1000`                 |
| `GITEA_USER`         | Username for Gitea user            | `git`                  | `git`                  |
| `GITEA_SSH_PORT`     | Host port for SSH                  | `2222`                 | `2222`                 |
| `GITEA_PUBLIC_DOMAIN`| Public domain for Traefik routing  |                        | `example.com`          |
| `NFS_SERVER`         | NFS server address                 |                        | `192.168.1.10`         |
| `NFS_GITEA_SHARE`    | NFS share for Gitea data           |                        | `/export/gitea-data`   |
| `NFS_REPOS_SHARE`    | NFS share for repositories         |                        | `/export/gitea-repos`  |

## Volumes

- `data`: Gitea application data (NFS)
- `repos`: Git repositories (NFS)

## Networks

- `proxy-network`: External network for Traefik

## Traefik Integration

The stack is pre-configured for Traefik. Make sure Traefik is running and attached to the `proxy-network`.

## Accessing Gitea

Access the Gitea web interface at:  
`https://git.yourdomain.com`
