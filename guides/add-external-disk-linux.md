# Adding an external disk to Ubuntu

A quick guide to creating a persistant mount to an external disk.

## 1. Get the disk UUID

```bash
lsblk -f
```

(find the right disk/partition, e.g. `/dev/sdb1`, copy its `UUID`)

## 2. Create a mount folder

Example folder under `/mnt`:

```bash
sudo mkdir -p /mnt/backup
```

## 3. Backup `fstab`

```bash
sudo cp /etc/fstab /etc/fstab.bak
```

## 4. Add entry to `/etc/fstab`

```bash
sudo vim /etc/fstab
```

Add line at bottom (replace UUID + mountpoint + fs type if needed):

```text
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  /mnt/backup  ext4  defaults  0  2
```

**Important**: Each field must be separated by tabs or spaces.

## 5. Test mount works

```bash
# Tell systemd to reload its generated unit files
sudo systemctl daemon-reload

# Test mounting everything
sudo mount -a

# Confirm mountpoint
lsblk
```
