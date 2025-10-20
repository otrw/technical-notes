# Ansible Quickstart Guide

## Scope

This is intended as a quick setup of Ansible on my Mac as the control node, with an aim to have a functional and *simple* working example to start off with.

### 1. Install via `brew`
```bash
brew install ansible 
```

### 2. Create a working directory:
```bash
mkdir -p ansible-projects && cd ansible-projects
```

### 3. Create an `inventory` file.

```bash
# Replace <server_ip> as required or with host alias from  ~/.ssh/config if configured.
# Using a user named ansible to manage servers. Change as necessary.
cat <<EOF > inventory
[ubuntu_servers]
<server_ip> ansible_user=ansible
EOF
```
- The heading used here `[ubuntu_servers]` is a reference / label and can be amended as required.

### 4. Create the ansible user on the server

The ansible user on the server is going to run the ansible playbooks. We need to create the user, amend group access and remove password prompts.

```bash
# Using Ubuntu adduser
sudo adduser --disabled-password --gecos "" ansible
sudo usermod -aG sudo ansible
echo 'ansible ALL=(ALL) NOPASSWD:ALL' | sudo tee /etc/sudoers.d/ansible
sudo chmod 440 /etc/sudoers.d/ansible

# Copy your ssh public key to the server
scp .ssh/id_ed25529.pub <user>@<serverIP>:/tmp/

# ssh to the server as admin and set ansible user permissions

sudo mkdir -p /home/ansible/.ssh
sudo mv /tmp/id_ed25519.pub /home/ansible/.ssh/authorized_keys
sudo chown -R ansible:ansible /home/ansible/.ssh
sudo chmod 700 /home/ansible/.ssh
sudo chmod 600 /home/ansible/.ssh/authorized_keys

echo '#
# Disable password logins entirely (key-only SSH)
PasswordAuthentication no

# Never allow direct root SSH
PermitRootLogin no' | sudo tee -a /etc/ssh/sshd_config

# Reload the ssh config
sudo systemctl reload ssh

```

### 5. Configure SSH Access

Ansible connects over SSH. Ensure you can log in to your target server manually:

```bash
ssh ansible@<server_ip>
```

If you use SSH keys:

```bash
ssh-copy-id ansible@<server_ip>
```

**Tip**: Configure `~/.ssh/config` for host aliases — see [ssh-config-example](../config-examples/general/ssh-config-example.md).


### 6. Create a simple playbook

Create a `yml` file in the same folder and give it a suitable name i.e. `server-updates.yml`

```yml
---
- name: Update Ubuntu Server
  hosts: ubuntu_servers
  become: yes
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
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

Save the file and run the playbook using:

```bash
ansible-playbook -i inventory server-updates.yml
````

## Resources

These additional utilities are not required to start off, but will become useful:
- `ansible-lint`: Catch mistakes and bad practices in playbooks before running them.
- `yq`: Read, query, and edit YAML from the command line.

Both of the above tools are available using `brew install ansible-lint yq`

- [Ansible Inventory Basics](https://chatgpt.com/c/688f394a-838c-8320-87ab-05d0b737d926#:~:text=docs:Ansible%20Inventory-,Basics) 
- [ansible-lint Docs](https://ansible.readthedocs.io/projects/lint/)
- [yq Github](https://github.com/mikefarah/yq) 
