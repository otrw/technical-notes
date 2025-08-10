# SSH Config Example
Example `~/.ssh/config` for aliasing hosts and setting defaults.

```plaintext
# Match any host starting with "web-"
Host web-*
    User ansible                   # Default user for matching hosts
    IdentityFile ~/.ssh/id_ed25519  # Private key (omit if default)
    ForwardAgent yes                # Forward SSH agent (use with care)

# Alias 'web-prod'
Host web-prod
    HostName prod.example.com       # Actual IP or hostname
    Port 22                         # Optional: override SSH port

# Alias 'web-staging'
Host web-staging
    HostName staging.example.com
```

# Quick Test
```bash
ssh -G web-prod     # Show effective config (dry run)
ssh -v web-prod     # Connect with verbose output
```

