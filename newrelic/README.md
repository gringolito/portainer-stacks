# New Relic Infrastructure Agent Stack

This stack deploys the [New Relic Infrastructure Agent](https://docs.newrelic.com/docs/infrastructure/install-infrastructure-agent/) using Docker Compose for monitoring your Docker host and containers.

## Services

- **agent**: New Relic Infrastructure Agent

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable                | Description                         | Default Value           | Example                |
|-------------------------|-------------------------------------|------------------------|------------------------|
| `NEWRELIC_TAG`          | New Relic agent image tag           | `latest`               | `latest`               |
| `NEWRELIC_LICENSE_KEY`  | New Relic license key               |                        | `your_license_key`     |

## Accessing New Relic

View your infrastructure data in the [New Relic dashboard](https://one.newrelic.com/).
