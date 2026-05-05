# Adding an external disk to Ubuntu

## About 

Create a persistant mount for an exteranl disk in Ubuntu using `etc/fstab`

## Steps

1. Identify disk and UUID.

```bash
lsblk -f
```
Locate the correct disk (e.g. `/dev/sdb`) and note the UUIS

2. Create a mount point

```bash
sudo mkdir -p /mnt/backup
```

3. Backup `fstab`

```bash
sudo cp /etc/fstab /etc/fstab.bak
```

4. Add entry to `/etc/fstab`  

```text
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  /mnt/backup  ext4  defaults,nofail  0  2
```
- `ext4` Replace if your filesystem differs (`lsblk -f will show it).
- `nofail` Prevents boot issues if the disk is not connected.
- Each field must be separated by tabs or spaces.

5. Test the mount

```bash
# Reload Systemd units (optional)
sudo systemctl daemon-reload

# Mount all entries from fstab
sudo mount -a
```

6. Verify

```bash
df -h /mnt/backup
```

## Troubleshooting

- Check logs using `journalctl -xe`
- Restore good fstab using `sudo cp /etc/fstab.bak /etc/fstab`
