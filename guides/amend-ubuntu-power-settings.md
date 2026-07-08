# Amend Laptop Lid actions

## About 

Amend lid close settings for laptops on Ubuntu.

1. Create a new drop in directory

`sudo mkdir -p /etc/systemd/logind.conf.d/`

> A drop in will allow the original file to stay unmodified. The OS will make any amendments specified in the drop in file.

2. Create a new file and add the relevant power options

```bash
# Create a new drop in file
sudo touch /etc/systemd/logind.conf.d/lid-close-action.conf

# Edit the file and add the required options
sudo nano /etc/systemd/logind.conf.d/lid-close-action.conf

# Example
[Login]
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
```

3. Reboot the server

`sudo systemctl reboot`

---

>Ubuntu 24.04 -> 26.04 upgrade:
Selecting the maintainer version of logind-related configuration removed the lid-close override, causing the server laptop to suspend and become unreachable over the network.