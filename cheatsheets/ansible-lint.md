### **ansible-lint**

**Purpose:** Catch mistakes and bad practices in your playbooks **before** you run them.

**Common usage:**
```bash
# Check a single playbook
ansible-lint update.yml

# Check all playbooks in current directory
ansible-lint
```

**Typical warnings it finds:**

* Missing `name:` in tasks
* Deprecated modules/options
* Wrong indentation in YAML
* Commands that should use Ansible modules instead

---