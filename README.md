## 👋 Welcome to i2p 🚀

Anonymous network layer - privacy and security

## 📋 Description

Anonymous network layer - privacy and security

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
docker compose up -d
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

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:7657

## 📂 Volumes

- `./rootfs/data/i2p` - Data storage
- `./rootfs/data/downloads` - Data storage

## 🔍 Logging

```shell
docker compose logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
