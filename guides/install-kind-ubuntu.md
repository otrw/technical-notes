# Install kind on Ubuntu

`kind` = **Kubernetes in Docker**. It spins up a local K8s cluster (control plane as a container) for safe experiments.

---

## 1. Prereqs: Docker + user in docker group
```bash
# if Docker isn't installed yet (skip if you already have it)
# install via your preferred method; example (convenience script):
curl -fsSL https://get.docker.com | sh

# let your user run docker without sudo (log out/in afterwards)
sudo usermod -aG docker "$USER"
````

---

## 2. Install kind (official binary)

```bash
# download latest stable (adjust version if needed)
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

Verify:

```bash
kind --version
```

---

## 3. Create a cluster

```bash
kind create cluster --name mydemo
```

You’ll see it pull a `kindest/node` image, then configure the control plane.

---

## 4. Check kubectl context & nodes

```bash
kubectl config get-contexts
kubectl cluster-info --context kind-demo
kubectl get nodes
```

Expected: one `Ready` node like `demo-control-plane`.

> If you see “connection to localhost:8080 refused,” you haven’t created a cluster yet or your kubeconfig/context isn’t set. Running `kind create cluster` fixes this.

---

## 5. Quick test (whoami)

```bash
kubectl run whoami --image=traefik/whoami --port=80
kubectl expose pod whoami --type=NodePort --port=80
kubectl get svc whoami
# On Linux (native), curl nodeIP:nodePort should work:
# Example: curl http://$(hostname -I | awk '{print $1}'):3xxxx
# Or use port-forward everywhere:
kubectl port-forward svc/whoami 8080:80 &
curl http://localhost:8080
```

---

## 6. Clean up

```bash
# delete the app (keep cluster)
kubectl delete svc whoami
kubectl delete pod whoami

# or remove the cluster entirely
kind delete cluster --name mydemo
```

---
## Notes

* `kind` uses Docker under the hood; clusters are disposable.
* On **Linux**, NodePorts bind to the host NIC (reachable directly).
* On **Mac/Windows**, NodePorts sit inside Docker Desktop’s VM; use `kubectl port-forward` for localhost access.
* Pinning Kubernetes version: you can specify a node image (e.g. `--image kindest/node:v1.33.1`) when creating the cluster.
