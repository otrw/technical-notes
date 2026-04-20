# Using `yq`

Read, query, and edit YAML from the command line.

## Usage

```bash
# View a key
yq '.hosts' inventory.yml

# List all task names in a playbook
yq e '.tasks[].name' update.yml

# Change a value in-place
yq e '.hosts[0] = "new-host"' -i inventory.yml

# Convert YAML → JSON
yq -o=json eval inventory.yml

# extract variables from an Ansible vars file
yq e '.vars.my_var' vars.yml

```
