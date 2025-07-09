# Serial-over-IP Stack

This stack deploys [ser2net](https://github.com/cminyard/ser2net) to expose serial devices over TCP/IP using Docker Compose.

## Services

- **ser2net**: Serial-to-network proxy.

## Usage

1. Set the required environment variables (see below).
2. Deploy the stack:

   ```sh
   docker compose up -d
   ```

## Environment Variables

| Variable                  | Description                         | Default Value           | Example         |
|---------------------------|-------------------------------------|------------------------|-----------------|
| `SER2NET_TAG`             | ser2net image tag                   | `latest`               | `4.3.11`        |
| `SER2NET_SERIAL_DEVICE`   | Host serial device path             |                        | `/dev/ttyUSB0`  |
| `SER2NET_9600_PORT`       | TCP port for 9600 baud              | `4000`                 | `4000`          |
| `SER2NET_57600_PORT`      | TCP port for 57600 baud             | `4001`                 | `4001`          |
| `SER2NET_115200_PORT`     | TCP port for 115200 baud            | `4002`                 | `4002`          |
| `SER2NET_1500000_PORT`    | TCP port for 1500000 baud           | `4003`                 | `4003`          |
| `SER2NET_ADMIN_PORT`      | TCP port for admin interface        | `9999`                 | `9999`          |

## Volumes

- `ser2net_config`: ser2net configuration

## Accessing ser2net

Connect to the configured TCP ports on your host to access the serial devices.

e.g:

```sh
telnet 10.10.10.10 4001
```
