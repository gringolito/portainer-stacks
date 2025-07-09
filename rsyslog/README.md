# Rsyslog Stack

This stack deploys [rsyslog](https://www.rsyslog.com/) as a syslog appliance using Docker Compose, with persistent configuration and logs.

## Services

- **rsyslog**: Syslog server for log aggregation.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable             | Description                          | Default Value           | Example                |
|----------------------|--------------------------------------|------------------------|------------------------|
| `RSYSLOG_TAG`        | rsyslog image tag                    | `latest`               | `8.2302.0`             |
| `RSYSLOG_TZ`         | Timezone                             | `America/Sao_Paulo`    | `Europe/Berlin`        |
| `NFS_SERVER`         | NFS server address                   |                        | `192.168.1.10`         |
| `NFS_LOGS_SHARE`     | NFS share for logs                   |                        | `/export/logs`         |
| `RSYSLOG_TCPUDP_PORT`| Syslog TCP/UDP port                  | `514`                  | `514`                  |
| `RSYSLOG_RELP_PORT`  | RELP port                            | `1601`                 | `1601`                 |

## Volumes

- `rsyslog_config`: rsyslog configuration
- `rsyslog_work`: rsyslog working directory
- `rsyslog_logs`: rsyslog logs (NFS)
