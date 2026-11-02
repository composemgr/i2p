## 👋 Welcome to i2p 🚀

An invisible network layer exposed as a full internet

## 📋 Description

I2P is an anonymous, decentralized network layer. It hides the applications
running on top of it from the network, so services are addressed by internal
`.i2p` destinations rather than public IP addresses and hostnames. This stack
runs the I2P Java router with its web console published on the assigned host
port.

## 🚀 Services

- **app**: geti2p/i2p:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/i2p/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/i2p" ~/.local/srv/docker/i2p
cd ~/.local/srv/docker/i2p
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install i2p
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
```

The router is configured from its web console; its settings are stored in
`volumes/config/i2p`.

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64204` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Router Console**: http://172.17.0.1:64204

Only the router console (7657) is published. The router's inbound peer transport
port (shown in the console) is not published here. Add a mapping and forward it
on your firewall if you want to accept inbound peer traffic.

Non-HTTP protocol ports are published identically in all three compose variants, because they cannot be proxied over HTTP: `4444`, `4445`, `6668`, `7654`, `7656`, `12345` (I2P proxies and bridges).

## 📂 Volumes

- `./volumes/config/i2p` - Router configuration, profile, keys, and reseed data
- `./volumes/data/i2p` - I2PSnark torrent data

## 🔐 Security

- Change all default passwords before deploying to production
- The router console has no authentication by default — do not publish it
- I2P is published on the Docker host gateway only; do not expose it directly
  to the internet
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly — reseed data takes time to rebuild if lost

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
