# Match any host that starts with "web-"
Host web-*
    User ansible # Default User for matching hosts.
    IdentityFile ~/.ssh/id_ed25519 # Private key for auth.
    ForwardAgent yes # Used for traversing to other hosts using established auth.

# Alias 'web-prod'
Host web-prod
    HostName prod.example.com # Actual IP or hostname.

# Alias 'web-prod'
Host web-staging
    HostName staging.example.com