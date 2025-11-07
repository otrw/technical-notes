# Change Ubuntu Static Address

How to change a statically assigned IP Address on an Ubuntu Server.

1. From the server, edit the `netplan` file (you may need to use `sudo`)

```bash
sudo vim /etc/netplan/50-cloud-init.yaml
```

The file should be similar to the one below:


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