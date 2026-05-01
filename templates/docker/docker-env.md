# Using `.env` files with Docker

## About

Docker environment file. A place for common and predefined variables to be used in conjuntion with the `docker-compose.yml` file.

> See official docs for most up to date info. 
https://docs.docker.com/compose/how-tos/environment-variables/variable-interpolation/

General rule of thumb would be to add `.env` to `.gitignore` and commit an example file, i.e. `env-example` as the `.env` can contain sensitive data. The `env-example` could be copied to `.env` for editing / use.

## Examples

```bash
# Docker .env example
EULA=TRUE
MEMORY=2G
DIFFICULTY=normal
MODE=survival
MOTD="Welcome to the Test Server!"
ENABLE_RCON=true
RCON_PASSWORD=changeme
```

Reference these in the `docker-compose.yml` file: 

```yml
    environment:
      EULA: ${EULA}
      MEMORY: ${MEMORY}
      DIFFICULTY: ${DIFFICULTY}
      MOTD: ${MOTD}
      ENABLE_RCON: ${ENABLE_RCON}
      RCON_PASSWORD: ${RCON_PASSWORD}
```

You can also set environment variables with default values:

```yml
environment:
  EULA: ${EULA:-true}    # if unset or empty, default to true
  MEMORY: ${MEMORY-4G}   # if unset, default to 4G (empty string stays empty)
```