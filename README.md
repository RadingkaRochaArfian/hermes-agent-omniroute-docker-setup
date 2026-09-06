<div align="center">
    <a href="https://www.reddit.com/r/Gunners/comments/vdwmg0/let_him_cook">
        <img src="https://res.cloudinary.com/eugha5xa/image/upload/v1788697896/header.png" width="250">
    </a>
</div>

# Hermes Agent Setup with Omniroute (Docker)
In case you need.  
## Prerequisites  
- [Docker](https://docs.docker.com/get-started/get-docker/)  
- Any web browser

## Instalation Steps  

### 1. Create the Configuration File  

*Create a new file named `docker-compose.yml` in your directory with the following configuration:*  
<details>
<summary><b>docker-compose.yaml</b></summary>

```
services:
  omniroute:
    image: diegosouzapw/omniroute:latest
    container_name: omniroute
    restart: unless-stopped
    stop_grace_period: 40s
    ports:
      - "20128:20128"
    volumes:
      - omniroute-data:/app/data
  
  hermes:
    image: nousresearch/hermes-agent:latest
    container_name: hermes
    restart: unless-stopped
    ports:
      - "8642:8642"
    environment:
      - GATEWAY_ALLOW_ALL_USERS=true
    volumes:
      - ~/.hermes:/opt/data
    command:
      - ["gateway", "run"]

volumes:
  omniroute-data:
```
</details>

### 2. Compose the Containers  

```
docker compose up -d
```

### 3. Configure Omniroute

*Use your web browser and go to `http://localhost:20128` to get your API key and endpoint address.*

### 4. Run Hermes Setup on Docker
*Run this command to start your hermes setup.*
```
docker exec -it hermes hermes setup
```
