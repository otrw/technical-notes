# Ansible Quickstart Guide

## About

Intended as a quick setup of Ansible on my Mac as the control node, providing a simple and functional way to update my homelab server.

1. Install via `brew`

```bash
brew install ansible ansible-lint yq
```

- `ansible` - Main program. 
- `ansible-lint` - Catch mistakes or bad practices in playbooks before running them. 
- `yq` - Read, query, and edit YAML from the command line.

2. Create a working directory:

```bash
mkdir -p ansible-playbooks && cd ansible-playbooks
```

3. Create an `inventory` file.

```bash
# Replace <server_ip> as required or with host alias from  ~/.ssh/config if configured.
# Using a user named ansible to manage servers. Change as necessary.
cat <<EOF > inventory
[ubuntu_servers]
<server_ip> ansible_user=ansible
EOF
```
- `[ubuntu_servers]` is the inventory group name used by the playbook.

4. Create a dedicated `ansible` user on the server for running automation tasks.

```bash
# Copy your ssh public key to the server
scp ~/.ssh/id_ed25519.pub <user>@<server_ip>:/tmp/

# ssh to the server and create the ansible user account
sudo adduser --disabled-password --gecos "" ansible
sudo usermod -aG sudo ansible
echo 'ansible ALL=(ALL) NOPASSWD:ALL' | sudo tee /etc/sudoers.d/ansible
sudo chmod 440 /etc/sudoers.d/ansible

# Set ansible user permissions
sudo mkdir -p /home/ansible/.ssh
sudo mv /tmp/id_ed25519.pub /home/ansible/.ssh/authorized_keys
sudo chown -R ansible:ansible /home/ansible/.ssh
sudo chmod 700 /home/ansible/.ssh
sudo chmod 600 /home/ansible/.ssh/authorized_keys
```

### Optional: Harden SSH after confirming key login works

```bash
echo '#
# Disable password logins entirely (key-only SSH)
PasswordAuthentication no

# Never allow direct root SSH
PermitRootLogin no' | sudo tee -a /etc/ssh/sshd_config

# Reload the ssh config
sudo systemctl reload ssh
```

5. Configure `SSH` Access

Ansible uses `ssh`. Ensure you can log in to your target server manually

```bash
ssh ansible@<server_ip>
```

6. Create a simple playbook

Create a `yml` file in the same folder and give it a suitable name i.e. `server-updates.yml`

```yml
---
- name: Update Ubuntu Server
  hosts: ubuntu_servers
  become: true
  tasks:
    - name: Update apt cache
      apt:
        update_cache: true
        cache_valid_time: 3600

    - name: Upgrade all packages
      apt:
        upgrade: dist

    - name: Check if reboot is required
      stat:
        path: /var/run/reboot-required
      register: reboot_required_file

    - name: Display if reboot is required
      debug:
        msg: "Reboot required: {{ reboot_required_file.stat.exists }}"
```

7. Save the file.

> Folder layout should look similar to

```text
ansible-playbooks/
├── inventory
└── server-updates.yml
```

8. Test the ansible command

`ansible all -i inventory -m ping`

9. Run the playbook

```bash
# Dry run of the playbook
ansible-playbook -i inventory server-updates.yml --check

# Run the playbook if no issues
ansible-playbook -i inventory server-updates.yml
```

## Additional Resources

- [How to build your inventory](https://docs.ansible.com/projects/ansible/latest/inventory_guide/intro_inventory.html) 
- [ansible-lint Docs](https://ansible.readthedocs.io/projects/lint/)
- [yq Github](https://github.com/mikefarah/yq) 
