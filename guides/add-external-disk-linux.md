# Adding an external disk to Ubuntu

A quick guide to creating a persistant mount to an external disk.

1. Get the disk UUID

```bash
lsblk -f
```

2. Find the disk/partition, e.g. `/dev/sdb1`, copy its `UUID`

3. Create a directory to mount the drive to.

```bash
sudo mkdir -p /mnt/backup
```

4. Backup `fstab`

```bash
sudo cp /etc/fstab /etc/fstab.bak
```

5. Open `/etc/fstab`

```bash
sudo vim /etc/fstab
```

6. Add a new line at bottom (replace UUID + mountpoint + fs type if needed):

```text
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  /mnt/backup  ext4  defaults  0  2
```

> Each field must be separated by tabs or spaces.

7. Test mount works

```bash
# Tell systemd to reload its generated unit files
sudo systemctl daemon-reload

# Test mounting everything
sudo mount -a

# Confirm mountpoint
lsblk
```
