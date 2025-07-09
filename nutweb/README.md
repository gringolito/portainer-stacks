# NUT Web GUI Stack

This stack deploys a web interface for [Network UPS Tools (NUT)](https://networkupstools.org/) using Docker Compose, with Traefik integration.

## Services

- **nutweb**: Web GUI for NUT server.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable                | Description                        | Default Value           | Example         |
|-------------------------|------------------------------------|------------------------|-----------------|
| `NUTWEB_TAG`            | nutweb image tag                   | `latest-amd64-v3`      | `latest-amd64-v3`|
| `NUTWEB_NUT_SERVER`     | NUT server address                 |                        | `nut-server`    |
| `NUTWEB_NUT_PORT`       | NUT server port                    | `3493`                 | `3493`          |
| `NUTWEB_NUT_USERNAME`   | NUT username                       |                        | `admin`         |
| `NUTWEB_NUT_PASSWORD`   | NUT password                       |                        | `password`      |
| `NUTWEB_PORT`           | nutweb web port                    | `9001`                 | `9001`          |
| `NUTWEB_PUBLIC_DOMAIN`  | Public domain for nutweb           |                        | `example.com`   |

## Networks

- `proxy-network`: External network for Traefik

## Traefik Integration

The service is pre-configured for Traefik. Ensure Traefik is running and attached to the `proxy-network`.

## Accessing nutweb

Access the NUT web interface at:  
`https://nutweb.yourdomain.com`
