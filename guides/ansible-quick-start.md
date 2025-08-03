# Ansible Quickstart install and setup

This is intended as a quick setup of Ansible on my Mac as the control node, with an aim to have a functional and *simple* working example to start off with.

## 1. Install via `brew`
```bash
brew install ansible 
```

## 2. Create a working directory:
```bash
mkdir -p ansible-projects && cd ansible-projects
```

## 3. Create an `inventory` file.

```bash
# Replace <server_ip> as required
# Using a user named ansible to manage servers. Change as necessary.
cat <<EOF > inventory
[ubuntu_servers]
<server_ip> ansible_user=ansible ansible_become=yes
EOF
```

The heading used here `[ubuntu_servers]` is a reference / label and can be amended as required.

## 4. Configure SSH Access

Ansible connects over SSH. Ensure you can log in to your target server manually:

```bash
ssh ansible@<server_ip>
````

If you use SSH keys:

```bash
ssh-copy-id ansible@<server_ip>
```

You may also want to configure `~/.ssh/config` to store host aliases. There is an example of one in the `/configs` directory.

## 5. Create a simple playbook

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
```

Save the file and run the playbook using:

```bash
ansible-playbook -i inventory server-updates.yml
````

## Resources

These additional utilities are not required to start off, but will become useful:
- `ansible-lint`: Catch mistakes and bad practices in playbooks before running them.
- `yq`: Read, query, and edit YAML from the command line.

Both of the above tools are available using `brew`

- [Ansible Inventory Basics](https://chatgpt.com/c/688f394a-838c-8320-87ab-05d0b737d926#:~:text=docs:Ansible%20Inventory-,Basics) 
- [ansible-lint Docs](https://ansible.readthedocs.io/projects/lint/)
- [yq Github](https://github.com/mikefarah/yq) 