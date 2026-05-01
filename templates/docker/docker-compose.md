# Docker compose template

## What is this?
Base template for running a container

## When do I use this?
Starting any new Docker service

## Template

```yml
services:
  app:
    image: example:latest
    container_name: app
    ports:
      - "8080:80"
    environment:
      - VAR_NAME=value
    volumes:
      - ./config:/config:ro
      - data:/data
    restart: unless-stopped

volumes:
  data:
```

## Notes

- Use name volumes for persistent data.
- Use bind mounts for Configuration.
- Prefere `.env` over inline secrets.
