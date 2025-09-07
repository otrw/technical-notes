# Docker `.env` example

Docker environment file. A place for common and predefined variables to be used in conjuntion with the `docker-compose.yml`

General rule of thumb would be to add `.env` to `.gitignore` and commit an example file, i.e. `env-example` as the `.env` can contain sensitive data. The `env-example` could be copied to `.env` for editing / use.

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

To use these in the `docker-compose.yml`, use the following format:

```yml
    environment:
      EULA: ${EULA}
      MEMORY: ${MEMORY}
      DIFFICULTY: ${DIFFICULTY}
      MOTD: ${MOTD}
      ENABLE_RCON: ${ENABLE_RCON}
      RCON_PASSWORD: ${RCON_PASSWORD}
```

**NOTE**: You can set environment variables with default values, for example:

```yml
environment:
  EULA: ${EULA:-true}    # if unset or empty, default to true
  MEMORY: ${MEMORY-4G}   # if unset, default to 4G (empty string stays empty)
```

More information in the [Official Docker Documentation](https://docs.docker.com/compose/how-tos/environment-variables/variable-interpolation/)
