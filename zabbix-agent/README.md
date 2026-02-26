# Zabbix Agent Stack

This stack deploys a Zabbix Agent 2 container configured to monitor the host and Docker runtime.

## Services

- Zabbix Agent 2: Collects host metrics and sends data to a Zabbix server.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable | Description | Default Value | Example |
|---|---|---|---|
| `ZABBIX_AGENT_TAG` | Zabbix Agent image tag | `ol-7.0-latest` | `ol-7.0-latest` |
| `ZABBIX_AGENT_TZ` | Timezone | `America/Sao_Paulo` | `Europe/Berlin` |
| `ZABBIX_AGENT_SERVER_HOST` | Zabbix server hostname or IP used by the agent | | `zabbix.example.com` |
| `ZABBIX_AGENT_HOSTNAME` | Hostname reported by the agent to Zabbix | | `docker-host-01` |
| `ZABBIX_AGENT_DOCKER_GROUPID` | GID used by the Docker daemon | `985` | `985` |
| `ZABBIX_AGENT_DOCKER_SOCKET` | Host path to Docker socket mounted into the container | `/var/run/docker.sock` | `/var/run/docker.sock` |

## Volumes

Bind mounts used by this stack:

- `${ZABBIX_AGENT_DOCKER_SOCKET:-/var/run/docker.sock}:/var/run/docker.sock:z` (Docker socket mount)

## Networks

The service runs with host networking (`network_mode: host`).

## Exposed Ports

The service uses host networking, so agent ports are exposed through the host network stack.
