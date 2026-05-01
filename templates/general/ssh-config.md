# ssh config template

## What is this?
Example `~/.ssh/config` for host aliases

## When do I use this?
When connecting to servers regularly

## Template

```text
Host web-*
    User ansible

Host web-prod
    HostName prod.example.com
    Port 22

Host web-staging
    HostName staging.example.com
```

## Usage

```bash
ssh web-prod
ssh -G web-prod
ssh -v web-prod
```

## Notes

- Avoid commiting real hostnames or keys.
- use this to simplify SSH commands.