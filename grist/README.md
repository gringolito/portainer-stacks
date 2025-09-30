# Grist Stack

This stack deploys [Grist](https://www.getgrist.com/) using Docker Compose, with persistent storage on NFS and Traefik handling external access.

## Services

- **grist**: Collaborative spreadsheet and database platform.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable                 | Description                          | Default Value        | Example                 |
|--------------------------|--------------------------------------|----------------------|-------------------------|
| `GRIST_TAG`              | Grist image tag                      | `latest`             | `1.1.11`                |
| `GRIST_UID`              | UID for Grist user                   | `1000`               | `1000`                  |
| `GRIST_GID`              | GID for Grist user                   | `1000`               | `1000`                  |
| `GRIST_TZ`               | Timezone                             | `America/Sao_Paulo`  | `Europe/Berlin`         |
| `GRIST_SESSION_SECRET`   | Session secret for authentication    |                      | `super-secret`          |
| `GRIST_EMAIL`            | Default account email                |                      | `admin@example.com`     |
| `GRIST_SANDBOX_FLAVOR`   | Sandbox flavor for document workers  | `gvisor`             | `gvisor`                |
| `GRIST_PUBLIC_DOMAIN`    | Public domain for Traefik routing    |                      | `example.com`           |
| `NFS_SERVER`             | NFS server address                   |                      | `192.168.1.10`          |
| `NFS_GRIST_PERSIST_SHARE`| NFS share for persistent data        |                      | `/export/grist-persist` |

## Volumes

- `persist`: Grist persistent storage (NFS)

## Networks

- `proxy-network`: External network for Traefik

## Accessing Grist

Access the Grist web interface at:  
`https://grist.<GRIST_PUBLIC_DOMAIN>`
