# UniFi Network Application Docker Setup

This repository contains the Docker configuration for running UniFi Network Application with MongoDB on a home server.

## Features

- Secure MongoDB instance with authentication
- Network isolation between containers
- Persistent data storage
- Automatic container restart
- Environment-based configuration

## Prerequisites

- Docker
- Docker Compose
- Git

## Setup Instructions

1. Create your environment file:
   ```bash
   cp .env.example .env
   ```

2. Edit the `.env` file and set your secure passwords:
   - `MONGO_ROOT_PASSWORD`: MongoDB root password
   - `MONGO_PASS`: MongoDB UniFi user password
   - `PUID`: User ID (run `id -u` to get your user ID)
   - `PGID`: Group ID (run `id -g` to get your group ID)
   - `TZ`: Your timezone (e.g., Europe/Amsterdam)

3. Start the containers:
   ```bash
   docker compose up -d
   ```

4. Access the UniFi Network Application:
   - Open https://192.168.1.200:8443 in your browser
   - Accept the self-signed certificate warning
   - Complete the setup wizard

## Directory Structure

```
.
├── .env                            # Environment variables (not in Git)
├── .env.example                    # Example environment file
├── .gitignore                      # Git ignore rules
├── docker-compose.yml              # Docker compose configuration
├── init-mongo.sh                   # MongoDB initialization script
├── docs/                           # Documentation
├── unifi-db/                       # MongoDB data (not in Git)
└── unifi-network-application/      # UniFi data (not in Git)
```

## Maintenance

### Updates
To update the containers:
```bash
# Pull new images
docker compose pull

# Restart containers with new images
docker compose up -d
```

### Logs
To view logs:
```bash
# All containers
docker compose logs

# Specific container
docker compose logs unifi-network-application
docker compose logs unifi-db

# Follow logs
docker compose logs -f
```

### Backup
Important directories to backup:
- `./unifi-db`: MongoDB data
- `./unifi-network-application`: UniFi configuration

Backup command example:
```bash
# Stop containers before backup
docker compose down

# Backup
tar -czf unifi-backup-$(date +%Y%m%d).tar.gz unifi-db/ unifi-network-application/

# Restart containers
docker compose up -d
```
# Test

