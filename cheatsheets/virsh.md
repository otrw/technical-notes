# Using virsh

Basic commands for managing virtial machines with `virsh`.

List virtual machines:

```bash
# List running vms
virsh list
# List all availble vms
virsh list --all
```

Request a clean shutdown:

```bash
virsh shutdown <vmname>
```

Force the VM off immediately:

```bash
virsh destroy <vmname>
```

> `destroy` is the equivalent of pulling the power cable. It does not delete the VM.

Remove the VM definition:

```bash
virsh undefine <vmname>
```

Delete the VM disk manually:

```bash
rm /var/lib/libvirt/images/vmname.qcow2
```

Remove the VM definition and its managed storage:

```bash
virsh undefine <vmname> --remove-all-storage
```
