# Docker Compose Template
services:
  <service-name>:
    image: <image-name>:<tag> # e.g. rmcrackan/libation:latest
    container_name: <container-name> # Optional
    ports:
      - "<host-port>:<container-port>" # Map host port to container port (optional)
    environment:
      - VAR_NAME=value # Environment variables (optional)
    volumes:
      # Local bind mount example (read‑only)
      - ./config:/config:ro
      # Named volume example (persistent data)
      - <named-volume>:/data
    restart: unless-stopped # Restart policy

volumes:
  <named-volume>: # Declare named volumes here
