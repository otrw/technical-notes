# SSH Config Example

## About

Example `~/.ssh/config` for aliasing hosts and setting defaults.

```plaintext
# Match any host starting with "web-"
Host web-*
    User ansible                   # Default user for matching hosts

# Example alias: web-prod
Host web-prod
    HostName prod.example.com       # Actual IP or hostname
    Port 22                         # Optional: override SSH port

# Example alias: web-staging
Host web-staging
    HostName staging.example.com
```

## Usage

```bash
ssh -G web-prod     # Show effective config (dry run)
ssh -v web-prod     # Connect with verbose output
```

> Be careful storing SSH config examples in shared repos or change records if they reference real usernames, hostnames, certificates, or key paths.
