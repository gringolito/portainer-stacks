# Beszel Monitoring Stack

This stack deploys [Beszel](https://github.com/henrygd/beszel) system monitoring using Docker Compose, with persistent storage and Traefik integration.

## Services

- **beszel**: Web-based system monitoring dashboard.
- **beszel-agent**: Agent for collecting system metrics.

## Usage

1. Copy or clone this directory to your Docker host.
1. Set the required environment variables (see below).
1. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable                | Description                        | Default Value           | Example                |
|-------------------------|------------------------------------|------------------------|------------------------|
| `BESZEL_TAG`            | Beszel image tag                   | `latest`               | `0.1.0`                |
| `BESZEL_TZ`             | Timezone                           | `America/Sao_Paulo`    | `Europe/Berlin`        |
| `BESZEL_UID`            | UID for Beszel user                | `1000`                 | `1000`                 |
| `BESZEL_GID`            | GID for Beszel user                | `1000`                 | `1000`                 |
| `BESZEL_PUBLIC_DOMAIN`  | Public domain for Traefik routing  |                        | `example.com`          |
| `BESZEL_TOKEN`          | Agent authentication token         |                        | `your-secret-token`    |
| `BESZEL_KEY`            | Agent encryption key               |                        | `your-encryption-key`  |
| `BESZEL_DATA_VOLUME`    | External volume name for data      |                        | `beszel_data`          |
| `BESZEL_AGENT_VOLUME`   | External volume name for agent     |                        | `beszel_agent`         |

## Volumes

- `beszel-data`: Beszel application data (external)
- `beszel-agent`: Agent data (external)

## Networks

- `proxy-network`: External network for Traefik
- Agent uses `host` network mode for system monitoring

## Traefik Integration

The Beszel service is pre-configured for Traefik. Ensure Traefik is running and attached to the `proxy-network`.

## Accessing Beszel

Access the Beszel web interface at:  
`https://beszel.<BESZEL_PUBLIC_DOMAIN>`
