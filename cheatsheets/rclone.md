# Rclone Cheatsheet

## Setup

### Create new Remote Configuration
```bash
# Create a new config
rclone config

# Location of current config
rclone config file
# Credential file. Protect this file.
# Back this file up securely
```

### List configured remotes
```bash
rclone listremotes
```

## Browse

### List remote directories
```bash
rclone lsd <RemoteName>:
```

### List remote files
```bash
rclone ls <RemoteName>:
```

### List remote files - Tree view
```bash
rclone lsf <RemoteName>: -R
```

### List Remote Information
```bash
rclone about <RemoteName>:
```

## Transfer

### Create remote directory
```bash
rclone mkdir <RemoteName>:<RemoteDirectory>
```

### Copy

> Safe Default.  
> Copies new/changed files. **Does not delete remote files.** 

```bash
# Dry Run Copy
rclone copy <source> <RemoteName>:<RemoteDirectory> --dry-run

# Real Run Copy
rclone copy <source> <RemoteName>:<RemoteDirectory> -P
```

### Sync

> Makes destination match source exactly.  

> WARNING: sync can delete files on destination.  
> Always test with --dry-run first.

```bash
# Dry Run Sync
rclone sync <source> <RemoteName>:<RemoteDirectory> --dry-run

# Real Run Sync
rclone sync <source> <RemoteName>:<RemoteDirectory> -P
```

### Check integrity (Compare source & destination)
```bash
rclone check <source> <RemoteName>:<RemoteDirectory>
```
> Useful after large backups or first cloud sync.

### Local Copy Example

Rclone can also copy between local folders/disks.

```bash
rclone copy /source /backupdisk/folder -P
```

## Delete / Cleanup

### Delete a file
```bash
rclone deletefile <RemoteName>:<RemoteDirectory>/test.txt
```

### Delete a directory contents
```bash
rclone delete <RemoteName>:<RemoteDirectory>
```

### Delete empty directories
```bash
rclone rmdirs <RemoteName>:
```

## Common Flags

`-P` - Progress (real-time transfer statistics).  
`-v` - Verbose Logs.  
`--dry-run` - Trial run, no permanent changes.  
`--retries` - Number of retries on failure/timeout.  
`--bwlimit` - Bandwidth limit (default none).  
`--exclude` - Excludes files
