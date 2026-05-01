# docker .env template

## What is this?
Environment variables file used by docker-compose

## When do I use this?
When I want to:
- avoid hardcoding values in compose
- keep secrets out of the repo
- reuse config between environments

## Examples

```bash
EULA=TRUE
MEMORY=2G
DIFFICULTY=normal
MODE=survival
MOTD="Welcome to the Test Server!"
ENABLE_RCON=true
RCON_PASSWORD=changeme
```

## Usage

```yml
    environment:
      EULA: ${EULA}
      MEMORY: ${MEMORY}
      DIFFICULTY: ${DIFFICULTY}
      MOTD: ${MOTD}
      ENABLE_RCON: ${ENABLE_RCON}
      RCON_PASSWORD: ${RCON_PASSWORD}
```

## Defaults

```yml
environment:
  EULA: ${EULA:-true}    # if unset or empty, default to true
  MEMORY: ${MEMORY-4G}   # if unset, default to 4G (empty string stays empty)
```

## Notes

- `.env` should NOT be commited.
- Commit a `env.example` instead
- Defaults help with breakage
