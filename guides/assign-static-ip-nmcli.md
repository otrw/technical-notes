# Assign a Static IP using nmcli

## Overview

Assign static IP4 adderss to a `NetworkManager` connection using `nmcli`.

This example was written for Rocky Linux but should also applies to other NetworkManager-based distributions.

## Steps

1. Connect to the virtual machine using `ssh` if set up or `virsh console <vmname>` on the virtual host.

2. Configure your variables.

```bash
# NetworkManager connection profile
# List available profiles using `nmcli con show`
connection="enp1s0"
# IP Address and network you wish to use
ip="192.168.2.200/24"
# Default Gateway address
gw="192.168.2.20"
# Primary/Secondary/Local DNS providers
dns="1.1.1.1,8.8.8.8"
```

3. Use `nmcli` to set the addresses

```bash
sudo nmcli con mod $connection ipv4.address "$ip"
sudo nmcli con mod $connection ipv4.method manual
sudo nmcli con mod $connection ipv4.dns "$dns"
sudo nmcli con mod $connection ipv4.gateway "$gw"

sudo nmcli con down $connection
sudo nmcli con up $connection
```

4. Verify the addresses are correct

```bash
nmcli con show "$connection"
```

### Reset to DHCP

To revert the connection back to DHCP, clear the IPv4 settings.

```bash
sudo nmcli con mod $connection ipv4.gateway ''
sudo nmcli con mod $connection ipv4.dns ''
sudo nmcli con mod $connection ipv4.address ''
sudo nmcli con mod $connection ipv4.method auto

sudo nmcli con down $connection
sudo nmcli con up $connection
```


## References

- [Rocky Linux - Basic Network Configuration](https://docs.rockylinux.org/10/guides/network/basic_network_configuration/)
