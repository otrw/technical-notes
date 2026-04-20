# Assign a Static IP Address in Ubuntu

## About

How to change a statically assigned IP Address on an Ubuntu Server. This was tested on `Ubuntu 24.04`

1. On the server, edit the `netplan` file.

```bash
sudo vim /etc/netplan/50-cloud-init.yaml
```

> The file should be similar to the one below:

```yaml
network:
  version: 2
  ethernets:
    enp0s31f6:
      addresses:
      - "192.168.0.2/24"
      nameservers:
        addresses:
        - 192.168.0.69
        search: []
      routes:
      - to: "default"
        via: "192.168.0.69"
```

2. Amend the IP Addresses for the NIC, Nameservers and Routes.

3. Save and quit.

4. Apply the configuration using:

```bash
sudo netplan apply
```