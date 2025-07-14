## Connect to host
```bash
ssh ubuntu-desktop
```

## Copy a file to host
```bash
scp /path/to/local/file ubuntu-server-1:/path/on/remote/server
```

## Copy a file from host
```bash
scp ubuntu-server-2:/path/on/remote/server /path/to/local/destination
```

## Run a command on a host
```bash
ssh ubuntu-server-3 'ls -l /home'
```

## Start an SSH session with X11 forwarding (for GUI applications)
```bash
ssh -X ubuntu-desktop
```

## Keep SSH connection alive (useful for unstable connections)
```bash
ssh -o ServerAliveInterval=60 ubuntu-desktop
```

## Key Management
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Copy your public key to a host
ssh-copy-id username@remote-server
```

## Port Forwarding
```bash
# Local port forwarding: access remote service locally
ssh -L 8080:localhost:80 ubuntu-server-1

# Remote port forwarding: expose local service to remote server
ssh -R 8080:localhost:3000 ubuntu-server-1
```

## SSH Configuration file
```bash
# Add to ~/.ssh/config
Host myserver
    HostName 192.168.1.100
    User ubuntu
    Port 22
    IdentityFile ~/.ssh/id_ed25519
```

# Usage
```bash
ssh myserver
```

