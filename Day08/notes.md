
# ReplicationController, ReplicaSet & Deployment
---
In Kubernetes, if a user is accessing an application and the pod crashes, the user loses access. To avoid that, we use controllers.
ReplicationController is the older way — you tell it how many pods you need, it makes sure that many are always running. Pod crashes, it brings a new one. Extra pods, it removes them. But it's legacy now, we don't use it anymore.
ReplicaSet is the newer version of ReplicationController. It does the same job — maintains the desired number of pods. The difference is ReplicaSet can also manage existing pods using matchLabels in the selector. But we don't create ReplicaSet directly either.
Deployment is what we actually use. Deployment tells the ReplicaSet how many pods to maintain, and ReplicaSet creates them. On top of that, Deployment gives us rolling updates — when we upgrade our application, it replaces old pods with new ones one by one, so users never see downtime. If the new version has issues, we just run kubectl rollout undo and it goes back to the previous version."

The one key concept to always mention:
Deployment works on desired state vs actual state. You define what you want — say 3 pods. Kubernetes always watches and makes sure the actual state matches. Pod dies? It brings a new one. That's the reconciliation loop.


ReplicaSet maintains a stable number of pods. If one crashes, it spins up a new one. If there are extra ones, it removes them.But when we want to upgrade our application, ReplicaSet can't handle that smoothly — it would cause downtime. So we use Deployment, which sits on top of ReplicaSet and handles rolling updates — It gradually replaces old pods with new ones, so there's no downtime. If the new version has issues, we can go back to the previous version using kubectl rollout undo.
---

## The Problem It Solves

If a user is hitting your application and the pod crashes — the user loses access. To prevent this, Kubernetes gives us controllers that keep pods always running.

---

## ReplicationController

The old way. You tell it how many pod replicas you want, it makes sure that many are always running. Pod dies? It brings a new one. Too many? It kills the extras.

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
spec:
  replicas: 3
  selector:
    app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx
        ports:
        - containerPort: 80
```

> Legacy — still works but don't use it in new setups.

---

## ReplicaSet

The newer version of ReplicationController. Does the same job but smarter — using `matchLabels` in the selector, it can also manage **existing pods** that weren't created by it.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      env: demo           # any pod with this label gets managed by this RS
  template:
    metadata:
      labels:
        env: demo
    spec:
      containers:
      - name: myapp
        image: nginx
```

```bash
kubectl get rs                    # list replica sets
kubectl describe rs myapp-rs      # details + events
kubectl delete rs myapp-rs        # deletes RS and its pods
kubectl edit rs myapp-rs          # edit directly on cluster
kubectl scale rs myapp-rs --replicas=5   # scale up/down
```

> You rarely create a ReplicaSet directly. Use a Deployment instead — it manages the ReplicaSet for you.

---

## Deployment

A Deployment wraps a ReplicaSet and adds the things you actually need in real life — **rolling updates** and **rollbacks**.

```
User → Deployment → ReplicaSet → Pods
```

When you update a Deployment (say, a new image version), it gradually replaces old pods with new ones without downtime. If something breaks, you roll back with one command.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx:1.14
        ports:
        - containerPort: 80
```

### Deployment Commands

```bash
# Create / apply
kubectl apply -f deployment.yaml

# List deployments
kubectl get deployments

# See details and events
kubectl describe deployment myapp-deployment

# Check rollout status (is it done updating?)
kubectl rollout status deployment/myapp-deployment

# See rollout history
kubectl rollout history deployment/myapp-deployment

# Update image (triggers a rolling update)
kubectl set image deployment/myapp-deployment myapp=nginx:1.19

# Undo the last rollout (rollback)
kubectl rollout undo deployment/myapp-deployment

# Rollback to a specific revision
kubectl rollout undo deployment/myapp-deployment --to-revision=2

# Pause a rollout (useful when you want to make multiple changes)
kubectl rollout pause deployment/myapp-deployment

# Resume a paused rollout
kubectl rollout resume deployment/myapp-deployment

# Scale up or down
kubectl scale deployment myapp-deployment --replicas=5

# Delete deployment (also deletes RS and pods)
kubectl delete deployment myapp-deployment
```

---

## Quick Recap

| | ReplicationController | ReplicaSet | Deployment |
|---|---|---|---|
| Manages existing pods | No | Yes | Yes |
| Rolling updates | No | No | Yes |
| Rollbacks | No | No | Yes |
| Use today? | No | Rarely | Always |

**Rule of thumb** — always create a Deployment. Never create a ReplicaSet or ReplicationController manually unless you have a very specific reason.
