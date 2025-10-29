# Checkmk Stack

This stack deploys [Checkmk Raw Edition](https://checkmk.com/) using Docker Compose. It provides a monitoring server with an agent receiver and is integrated with Traefik for external access.

## Services

- **checkmk**: Checkmk monitoring server (web UI and monitoring core).

## Usage

1. Copy or clone this directory to your Docker host.
1. Set the required environment variables (see below).
1. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable                      | Description                               | Default Value         | Example                 |
|-------------------------------|-------------------------------------------|-----------------------|-------------------------|
| `CHECKMK_TAG`                 | Checkmk image tag                         | `latest`              | `2.4.0-latest`          |
| `CHECKMK_TZ`                  | Timezone                                  | `America/Sao_Paulo`   | `Europe/Berlin`         |
| `CHECKMK_PASSWORD`            | Initial admin password (site creation)    |                       | `super-secret`          |
| `CHECKMK_UID`                 | UID to run the container                  | `1000`                | `1000`                  |
| `CHECKMK_GID`                 | GID to run the container                  | `1000`                | `1000`                  |
| `CHECKMK_PUBLIC_DOMAIN`       | Public domain used by Traefik routing     |                       | `example.com`           |
| `CHECKMK_MONITORING_VOLUME`   | External volume name for monitoring data  |                       | `checkmk_monitoring`    |

## Volumes

- `monitoring`: Checkmk site data (external; name from `CHECKMK_MONITORING_VOLUME`)

## Networks

- `proxy-network`: External network for Traefik

## Traefik Integration

The service is labeled for Traefik routing. Ensure Traefik is running and attached to the `proxy-network`. Traefik will route the web UI to the container port configured by the stack.

## Accessing Checkmk

- Web UI (via Traefik):  
  `https://checkmk.<CHECKMK_PUBLIC_DOMAIN>`

- Agent Receiver (host port):  
  The docker-compose maps the Checkmk agent receiver to host port `8000` (TCP) — ensure this port is reachable for agent connections if you use direct agent pushes.
