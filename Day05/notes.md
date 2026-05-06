# Kubernetes Architecture

## What is a Node?

Before diving in — a **node** is just a virtual machine. It's where your actual workloads, pods, and containers run.

In Kubernetes, there are two types of nodes — the **Control Plane (Master Node)** and the **Worker Nodes.**

---

## Control Plane (Master Node)

Think of the control plane as the **brain of the cluster.** It makes all the decisions. It has four main components:

### 1. API Server

This is the **entry point** to the entire cluster. Every action — whether it's creating a pod, scaling a deployment, or checking cluster status — goes through the API server first. Nothing bypasses it.

### 2. Scheduler

The scheduler is always **watching the cluster.** When a new pod needs to be created, the scheduler figures out which worker node is the best fit — based on available CPU, memory, and other constraints — and assigns the pod there.

### 3. etcd

etcd is a **key-value data store.** It stores the entire state of your cluster — what pods are running, what nodes exist, what deployments are configured. If Kubernetes needs to remember something, it's stored in etcd.

### 4. Controller Manager

This is a **combination of multiple controllers** — Node Controller, Deployment Controller, Replication Controller, and more. Its one job is to make sure the **actual state of the cluster matches the desired state.** If something drifts, the controller manager fixes it.

---

## Worker Node

This is where your **actual application containers run.** Each worker node has two key components:

### 1. Kubelet

Kubelet is a **node-level agent** that runs on every worker node. It constantly watches the API server for updates. When it gets an instruction to run a pod, it does it. It also reports back the status of the node and pods to the control plane.

### 2. Kube Proxy

Kube Proxy handles **networking within the cluster.** It enables communication between pods — whether they're on the same node or different nodes.

---

## How it All Works Together — The Flow

Let's say you run this command:

```bash
kubectl create pod my-app
```

Here's exactly what happens step by step:

1. **kubectl** sends the request to the **API Server**
2. API Server **authenticates and validates** the request — is this user allowed to do this?
3. If valid, API Server stores the request in **etcd** — an entry is created saying "a pod needs to be created"
4. The **Scheduler** is watching the API server, sees that a pod needs a node, finds the most suitable worker node based on CPU and memory, and sends that decision back to the API server
5. The **Kubelet** on the selected worker node is also watching the API server, sees the instruction, and runs the container on that node
6. Kubelet **reports back** to the API server — "pod is running"
7. API Server updates **etcd** with the new state
8. The **response goes back to you** — pod created ✅

---

## Quick Revision Cheat Sheet

| Component | Where | What it does |
|---|---|---|
| API Server | Control Plane | Entry point for all requests |
| Scheduler | Control Plane | Assigns pods to suitable nodes |
| etcd | Control Plane | Stores entire cluster state |
| Controller Manager | Control Plane | Keeps actual state = desired state |
| Kubelet | Worker Node | Runs containers, reports status |
| Kube Proxy | Worker Node | Handles pod networking |
