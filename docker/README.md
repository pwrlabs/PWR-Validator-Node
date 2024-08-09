# PWR Validator Node Docker Setup

This guide explains how to run a PWR Validator Node using Docker. Docker helps avoid cluttering your local environment with unfamiliar dependencies and ensures a clean, isolated setup.

## Requirements

- Docker ([Installation Guide](https://docs.docker.com/engine/install/))
- Public IP address
- Ensure the following ports are not in use: 8231/tcp, 8085/tcp, 7621/udp

## Quick Start

1. **Download Dockerfile and docker-compose.yaml**

   ```bash
   wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/docker/Dockerfile
   wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/docker/docker-compose.yaml
   ```

2. **Create a `password` file**

   ```bash
   echo "your_password_here" > password
   ```

3. **Choose your setup method**

### A. Using Docker Compose

1. Replace `<YOUR_PUBLIC_IP>` in `docker-compose.yaml` with your actual public IP.
2. Run:

   ```bash
   docker compose up -d
   ```

### B. Using Dockerfile Only

1. Save the provided `Dockerfile` in a directory.
2. Build and run:

   ```bash
   docker build -t pwr-validator .
   docker run -d --name pwr-validator \
     -p 8231:8231 -p 8085:8085 -p 7621:7621/udp \
     -e SERVER_IP=<YOUR_PUBLIC_IP> \
     -v pwr-validator-data:/app \
     pwr-validator
   ```

   Replace `<YOUR_PUBLIC_IP>` with your public IP.

## Backup Private Key
```bash
docker exec -it pwr-validator sh -c 'java -jar /app/validator.jar get-private-key password'
```
you can replace  `pwr-validator` with the container id or name

## Management Commands 

- **Stop:** `docker compose down` or `docker stop pwr-validator`
- **Start:** `docker compose up -d` or `docker start pwr-validator`
- **Restart:** `docker compose restart` or `docker restart pwr-validator`
- **Logs:** `docker compose logs -f` or `docker logs -f pwr-validator`

## Important Notes

- Ports used: 8231 (TCP), 8085 (TCP), 7621 (UDP)
- Data is stored in the `pwr-validator-data` Docker volume.
- The `config.json` and `validator.jar` files are downloaded automatically during setup.

## Updating

To rebuild the Docker image using the latest `config.json` and `validator.jar`:

### A. Using Docker Compose

1. Rebuild: `docker compose build`
2. Restart: `docker compose restart`

### B. Using Dockerfile

1. Rebuild: `docker build -t pwr-validator`
2. Restart: `docker restart pwr-validator`

---
