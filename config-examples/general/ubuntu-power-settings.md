# Modify Power Settings in Ubuntu

## About

Config settings controling power button presses and lid switches on Ubuntu.

## Configure

1. Edit `/etc/systemd/conf`

```bash
sudo nano /etc/systemd/logind.conf
```

2. Uncomment the following lines

```bash
HandlePowerKey=ignore
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```

3. Save and exit.

4. Reload logind(or reboot)

```bash
sudo systemctl restart systemd-logind
```

5. Verify the changes

```bash
loginctl show-seat | grep Handle
# Newer versions of `systemd` can use the command `loginctl show-logind`.
```