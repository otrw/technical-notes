# Docker compose example

## About

A `docker-compose.yml` using the Minecraft project as an example.

## Example

```yml
 services:
# Minecraft Java server configuration
  minecraft-java:
    image: itzg/minecraft-server
    container_name: mcj-server
    ports:
      - "25565:25565" # Port mapping
    environment: # Uses .env variables
      EULA: ${EULA}
      MEMORY: ${MEMORY}
      DIFFICULTY: ${DIFFICULTY}
      MODE: ${MODE}
      MOTD: ${MOTD}
      TZ: ${TZ}
      ENABLE_RCON: ${ENABLE_RCON}
      RCON_PASSWORD: ${RCON_PASSWORD}
    volumes:
      - ./java/data:/data # Bind local dir to container
    restart: unless-stopped
# Minecraft Bedrock server configuration
  minecraft-bedrock:
    image: itzg/minecraft-bedrock-server
    container_name: mcb-server
    ports:
      - "19132:19132/udp"
    environment:
      EULA: ${EULA}
      DIFFICULTY: ${DIFFICULTY}
      MOTD: ${MOTD}
      TZ: ${TZ}
    volumes:
      - ./bedrock/data:/data
    restart: unless-stopped
  ```
  