
# Install kubectl on Ubuntu

These are the official steps using the **new upstream apt repo (pkgs.k8s.io)**.  
This keeps `kubectl` up to date with `apt upgrade`.

---
## 1. Remove old repo (if it exists)

```bash
sudo rm -f /etc/apt/sources.list.d/kubernetes.list
sudo apt update
````

---
## 2. Install dependencies

```bash
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gnupg
```

---
## 3. Add Kubernetes apt repo (v1.33 stable)

```bash
# Create the keyrings directory and apply permissions
sudo mkdir -p -m 755 /etc/apt/keyrings
# Retrieve the Kubernetes keyring
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key \
  | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
# Modify the keyring permissions
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg
# Add the repo and keyring to the sources.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] \
https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' \
  | sudo tee /etc/apt/sources.list.d/kubernetes.list
# Modify sources.list for Kubernetes permissions
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list
```

---
## 4. Install kubectl

```bash
sudo apt-get update
sudo apt-get install -y kubectl
```

---
## 5. Verify

```bash
kubectl version --client
```

---
## Notes

- Updates come via `apt upgrade`.
- Change `v1.33` in the repo URL if you need a different minor version later.
- Official docs: [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).
