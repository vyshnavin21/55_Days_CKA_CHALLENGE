# Kubernetes Multi-Cluster Setup with KIND (on WSL/Windows)

A step-by-step guide to setting up multiple Kubernetes clusters locally using **KIND (Kubernetes IN Docker)** on **WSL (Windows Subsystem for Linux)**.

> **Note:** There are other tools to run local Kubernetes clusters like **Minikube**, **k3d**, **MicroK8s**, etc. This guide uses KIND, which runs cluster nodes as Docker containers — making it lightweight and fast.

---

## Prerequisites

### Docker must be installed and running before proceeding.

Verify Docker is available in WSL:

```bash
docker --version
docker info
```

---

## Table of Contents

- [Step 1 — Install KIND](#step-1--install-kind)
- [Step 2 — Install kubectl](#step-2--install-kubectl)
- [Step 3 — Create a Single-Node Cluster (cka-cluster1)](#step-3--create-a-single-node-cluster-cka-cluster1)
- [Step 4 — Create a Multi-Node Cluster (cka-cluster2)](#step-4--create-a-multi-node-cluster-cka-cluster2)
- [Step 5 — Managing Multiple Clusters](#step-5--managing-multiple-clusters)
- [Quick Reference](#quick-reference)

---

## Step 1 — Install KIND

Download the KIND binary, make it executable, and move it to your PATH:

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

Verify the installation:

```bash
kind version
```

---

## Step 2 — Install kubectl

kubectl is the command-line tool used to interact with Kubernetes clusters.

```bash
# Download the latest stable release
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Download the checksum file for validation
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

# Validate the binary against the checksum
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

# Install kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Verify the installation:

```bash
kubectl version --client
```

---

## Step 3 — Create a Single-Node Cluster (cka-cluster1)

By default, KIND creates a cluster with a **single node** that acts as both the control plane and worker node.

```bash
kind create cluster \
  --image kindest/node:v1.34.3@sha256:08497ee19eace7b4b5348db5c6a1591d7752b164530a36f855cb0f2bdcbadd48 \
  --name cka-cluster1
```

> The `kindest/node` is the Docker image repository for KIND nodes. The `sha256` hash pins the exact image version for reproducibility.

**Expected output:**

```
Creating cluster "cka-cluster1" ...
 ✓ Ensuring node image (kindest/node:v1.34.3) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-cka-cluster1"
```

### Verify the cluster

```bash
# Get cluster info
kubectl cluster-info --context kind-cka-cluster1

# Check nodes
kubectl get nodes
```

**Expected nodes output:**

```
NAME                         STATUS   ROLES           AGE   VERSION
cka-cluster1-control-plane   Ready    control-plane   44m   v1.34.3
```

---

## Step 4 — Create a Multi-Node Cluster (cka-cluster2)

To create a cluster with **multiple nodes** (1 control plane + 2 workers), use a config file.

### 4a — Create the config file

```bash
vi config.yaml
```

Paste the following configuration:

```yaml
# config.yaml — Three-node cluster: 1 control plane + 2 workers
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

Save and exit (`:wq` in vi).

### 4b — Create the cluster using the config

```bash
kind create cluster \
  --image kindest/node:v1.34.3@sha256:08497ee19eace7b4b5348db5c6a1591d7752b164530a36f855cb0f2bdcbadd48 \
  --name cka-cluster2 \
  --config config.yaml
```

### Verify the cluster

```bash
kubectl get nodes
```

**Expected output:**

```
NAME                         STATUS   ROLES           AGE    VERSION
cka-cluster2-control-plane   Ready    control-plane   115s   v1.34.3
cka-cluster2-worker          Ready    <none>          104s   v1.34.3
cka-cluster2-worker2         Ready    <none>          105s   v1.34.3
```

---

## Step 5 — Managing Multiple Clusters

KIND automatically sets up **kubectl contexts** for each cluster. A context tells kubectl which cluster to talk to.

### List all available clusters/contexts

```bash
kubectl config get-contexts
```

**Expected output:**

```
CURRENT   NAME                CLUSTER             AUTHINFO            NAMESPACE
          kind-cka-cluster1   kind-cka-cluster1   kind-cka-cluster1
*         kind-cka-cluster2   kind-cka-cluster2   kind-cka-cluster2
```

> The `*` indicates the currently active context (cluster).

### Switch between clusters

```bash
# Switch to cluster1
kubectl config use-context kind-cka-cluster1

# Switch to cluster2
kubectl config use-context kind-cka-cluster2
```

**Expected output:**

```
Switched to context "kind-cka-cluster1".
```

### Get info about a specific cluster

```bash
kubectl cluster-info --context kind-cka-cluster1
kubectl cluster-info --context kind-cka-cluster2
```

---

## Quick Reference

| Command | Description |
|---|---|
| `kind version` | Check KIND version |
| `kubectl version --client` | Check kubectl version |
| `kind create cluster --name <name>` | Create a single-node cluster |
| `kind create cluster --name <name> --config config.yaml` | Create cluster from config |
| `kind get clusters` | List all KIND clusters |
| `kind delete cluster --name <name>` | Delete a cluster |
| `kubectl config get-contexts` | List all kubectl contexts |
| `kubectl config use-context <context>` | Switch active cluster |
| `kubectl cluster-info --context <context>` | Get cluster details |
| `kubectl get nodes` | List nodes in active cluster |

---

## Cluster Architecture Summary

```
cka-cluster1 (single-node)
└── cka-cluster1-control-plane  [control-plane + worker]

cka-cluster2 (multi-node)
├── cka-cluster2-control-plane  [control-plane]
├── cka-cluster2-worker         [worker]
└── cka-cluster2-worker2        [worker]
```

---

## Notes

- All KIND cluster nodes run as **Docker containers** on your host machine.
- The `sha256` digest in the image reference ensures you pull the exact same node image every time, regardless of tag changes.
- On WSL, make sure the Docker daemon (Docker Desktop on Windows) is running and WSL integration is enabled before creating clusters.
- Each cluster gets its own **kubeconfig context** automatically — no manual configuration needed.
