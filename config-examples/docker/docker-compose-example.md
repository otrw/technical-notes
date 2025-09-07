# Docker compose example

A `docker-compose.yml` example with several images, using the Minecraft project as an example.

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
  minecraft-admin:
  # This service is used for administrative tasks and scripts
  # It mounts the scripts and data directories for both Java and Bedrock servers
  # and runs a lightweight Alpine container to keep the environment ready for admin tasks
  # It does not run a Minecraft server but provides a persistent environment for management
    image: alpine
    container_name: mc-admin-server
    command: ["/scripts/start-admin.sh"]
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock # Allows the container to manage Docker
      - ./scripts:/scripts # Mount the scripts directory
      - ./java/data:/java_data:ro # Mount the Java server data directory as read-only
      - ./bedrock/data:/bedrock_data:ro # Mount the Bedrock server data directory as read-only
    restart: unless-stopped
```