# Why Kubernetes?

## The Problem First

Let's say you have a small application running a few containers. If one container crashes,
someone from the ops team logs in, checks the logs, and fixes it manually. That works
fine — until it happens at 2AM.

Who handles it then? You either disturb someone's sleep or hire more people to cover
off-hours. Both options cost you — either in burnout or in money.

Now scale that problem up.

---

## The Enterprise Problem

Imagine an enterprise application with hundreds of containers running at once. You have
a full team managing it — that's fine. But what happens when 20 containers go down at
the same time? Your team is scrambling, users are affected, and it's chaos. No matter
how good your team is, humans can only move so fast.

---

## So Why Kubernetes?

This is exactly the problem Kubernetes was built to solve.

Kubernetes is a **container orchestration tool** — it automatically manages your containers
so your team doesn't have to babysit them.

- If a container crashes, Kubernetes **restarts it automatically**
- If traffic increases, it **scales up**
- If traffic drops, it **scales back down**
- All without anyone waking up at 2AM

In short, it handles what would otherwise take an entire ops team to manage manually.

---

## But Should You Always Use Kubernetes?

Honestly, no.

If your application is small and runs just a few containers, Kubernetes might be overkill.
It has a steep learning curve and adds complexity. The overhead might not be worth it
for a simple app.

> **Rule of thumb** — choose Kubernetes when the complexity of managing your containers
> manually starts to outweigh the cost of learning and running Kubernetes itself.

It's a powerful tool, but only use it when you actually need it.
