# Pods in Kubernetes — Imperative vs Declarative

There are two ways to create a pod (or any resource) in Kubernetes.

**Imperative** — you tell Kubernetes exactly what to do, step by step, through commands directly in the terminal. Quick and useful for testing things out.

**Declarative** — you write a YAML file describing what you want, and Kubernetes figures out how to make it happen. This is the preferred way in real projects because it's repeatable and version-controllable.

---

## Imperative Way

Just run a single command, no YAML needed.

```bash
kubectl run nginx-pod --image=nginx:latest
```

Check if it's running:

```bash
kubectl get pods
```

```
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          91s
```

> `1/1` under READY means — the pod has 1 container and 1 is running. If it showed `0/1`, the container hasn't started yet.

---

## Declarative Way

Write a YAML file that describes the pod, then apply it.

```yaml
# pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
      - containerPort: 80
```

Apply it:

```bash
kubectl apply -f pod.yaml
```

---

## When to use which?

| | Imperative | Declarative |
|---|---|---|
| Speed | Fast, one command | Takes a minute to write YAML |
| Best for | Quick tests, debugging | Actual deployments, production |
| Reusable | No | Yes — commit the YAML to git |
| Repeatable | No | Yes — apply as many times as needed |

> A good habit — even when testing, use `--dry-run=client -o yaml` to generate the YAML from an imperative command, then save it as a file.
> ```bash
> kubectl run nginx-pod --image=nginx:latest --dry-run=client -o yaml > pod.yaml
> ```
