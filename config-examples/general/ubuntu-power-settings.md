# Modify Power Settings in Ubuntu

Settings to control power button presses and lid switches on Ubuntu laptops - useful for headless or shelf-mounted servers/labs.

1. Edit `/etc/systemd/conf`

```bash
sudo nano /etc/systemd/logind.conf
```

2. Uncomment the following lines:

```bash
HandlePowerKey=ignore
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```
Save and exit.

3. Reload logind(or reboot) :

```bash
sudo systemctl restart systemd-logind
```

4. Verify the changes:

```bash
loginctl show-seat | grep Handle
```
**Note:** Newer versions of `systemd` can use the command `loginctl show-logind`.
