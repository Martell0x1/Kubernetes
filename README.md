<p align="center">
  <img src="https://raw.githubusercontent.com/kubernetes/kubernetes/master/logo/logo.png" alt="Kubernetes Study Notes banner" width="160">
</p>

<h1 align="center">Kubernetes Study Notes</h1>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=martell0x1&label=Profile%20Views&color=4aa3ff&style=flat" alt="visitor count badge">
</p>

<p align="center">
  <em>Personal learning log and reference while studying Kubernetes (K8s).</em><br>
  <sub>This is a living document — update it as you learn, not a one-time checklist.</sub>
</p>

---

## 📌 Status

| | |
|---|---|
| **Started** | `2026-9-27` |
| **Current focus** | Deployments & Services |
| **Environment** | minikube / kind / k3d / cloud cluster |

---

## 📖 Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Local Setup](#2-local-setup)
3. [Core Concepts Roadmap](#3-core-concepts-roadmap)
4. [Command Cheat Sheet](#4-command-cheat-sheet)
5. [Hands-On Labs](#5-hands-on-labs)
6. [Glossary](#6-glossary)
7. [Resources](#7-resources)
8. [Open Questions](#8-open-questions--things-to-revisit)
9. [Fundamentals — Deep Dive](#9-fundamentals--deep-dive)

---

## 1. Prerequisites

- [ ] Comfortable with Docker (images, containers, volumes, networking)
- [ ] Basic YAML syntax
- [ ] Linux CLI basics
- [ ] Networking basics (DNS, ports, load balancing)

---

## 2. Local Setup

| Tool | Purpose | Notes |
|---|---|---|
| `kubectl` | CLI to talk to the cluster | essential |
| `minikube` / `kind` / `k3d` | Local cluster | pick one |
| `k9s` | Terminal UI for the cluster | optional, but nice |
| `helm` | Package manager for K8s | later stage |

```bash
# Example: spin up a local cluster with kind
kind create cluster --name study
kubectl cluster-info
```

---

## 3. Core Concepts Roadmap

> Check these off once you *understand* each one — not just once you've read about it.

<details open>
<summary><strong>3.1 Architecture</strong></summary>

- [ ] Control plane components (API server, etcd, scheduler, controller manager)
- [ ] Node components (kubelet, kube-proxy, container runtime)
- [ ] How `kubectl` talks to the API server

</details>

<details open>
<summary><strong>3.2 Workloads</strong></summary>

- [ ] Pods (the atomic unit)
- [ ] ReplicaSets
- [ ] Deployments (rolling updates, rollbacks)
- [ ] StatefulSets (when/why vs. Deployments)
- [ ] DaemonSets
- [ ] Jobs & CronJobs

</details>

<details open>
<summary><strong>3.3 Networking</strong></summary>

- [ ] Services (ClusterIP, NodePort, LoadBalancer)
- [ ] Ingress & Ingress Controllers
- [ ] DNS inside the cluster (CoreDNS)
- [ ] NetworkPolicies

</details>

<details open>
<summary><strong>3.4 Configuration & Secrets</strong></summary>

- [ ] ConfigMaps
- [ ] Secrets
- [ ] Environment variables vs. mounted volumes for config

</details>

<details open>
<summary><strong>3.5 Storage</strong></summary>

- [ ] Volumes vs. PersistentVolumes (PV)
- [ ] PersistentVolumeClaims (PVC)
- [ ] StorageClasses & dynamic provisioning

</details>

<details open>
<summary><strong>3.6 Scheduling & Scaling</strong></summary>

- [ ] Resource requests/limits
- [ ] HorizontalPodAutoscaler (HPA)
- [ ] Node affinity / anti-affinity / taints & tolerations

</details>

<details open>
<summary><strong>3.7 Namespaces & Access Control</strong></summary>

- [ ] Namespaces (multi-tenancy basics)
- [ ] RBAC (Roles, RoleBindings, ClusterRoles)
- [ ] ServiceAccounts

</details>

<details open>
<summary><strong>3.8 Observability</strong></summary>

- [ ] `kubectl logs` / `kubectl describe` / `kubectl exec`
- [ ] Liveness / readiness / startup probes
- [ ] Metrics server, basic monitoring (Prometheus/Grafana — later)

</details>

<details open>
<summary><strong>3.9 Packaging & GitOps</strong> <sub>(later stage)</sub></summary>

- [ ] Helm charts
- [ ] Kustomize
- [ ] CI/CD basics for K8s (ArgoCD / Flux — optional)

</details>

---

## 4. Command Cheat Sheet

```bash
# Cluster info
kubectl cluster-info
kubectl get nodes

# Everyday resource inspection
kubectl get pods -A
kubectl describe pod <name>
kubectl logs <pod> -f
kubectl exec -it <pod> -- sh

# Apply / delete manifests
kubectl apply -f manifest.yaml
kubectl delete -f manifest.yaml

# Debugging
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl top pod
```

---

## 5. Hands-On Labs

| # | Lab | What it covers | Status |
|---|---|---|:---:|
| 1 | Deploy a single Pod manually | Pod spec basics | ⬜ |
| 2 | Deployment + Service | Rolling updates, ClusterIP | ⬜ |
| 3 | Expose app via Ingress | Ingress controller, routing | ⬜ |
| 4 | ConfigMap + Secret in a Pod | Config injection | ⬜ |
| 5 | StatefulSet + PVC (e.g. a small DB) | Persistent storage | ⬜ |
| 6 | HPA on a CPU-bound app | Autoscaling | ⬜ |
| 7 | Multi-namespace RBAC setup | Access control | ⬜ |
| 8 | Helm chart for your own app | Packaging | ⬜ |

---

## 6. Glossary

| Term | Definition (in your own words) |
|---|---|
| Pod | |
| Deployment | |
| Service | |
| Ingress | |
| ConfigMap | |
| PVC | |
| Namespace | |
| CRD | |

---

## 7. Resources

- 📘 [Official docs](https://kubernetes.io/docs/home/)
- ⚙️ [`kubectl` reference](https://kubernetes.io/docs/reference/kubectl/)
- 🧪 [Interactive playground (killercoda)](https://killercoda.com/kubernetes)
- 📋 [CKAD/CKA curriculum](https://github.com/cncf/curriculum) — a solid structured checklist even if you're not testing

---

## 8. Open Questions / Things to Revisit

- [ ] *e.g. When to use StatefulSet vs. Deployment for a stateful app?*
- [ ] *e.g. How does kube-proxy actually route traffic (iptables vs. IPVS)?*
- [ ] *e.g. Difference between Helm and Kustomize in practice*

---

## 9. Fundamentals — Deep Dive

### 9.1 What is Kubernetes?

Kubernetes is an **open-source container orchestration platform** (comparable to Docker Swarm). When a single container can't handle the load, Kubernetes steps in to orchestrate container creation, scaling, and removal.

It takes care of:

- **Scheduling** containers onto available nodes
- **Scaling** them up or down based on demand
- **Self-healing** when something fails
- **Load balancing** traffic across containers

Kubernetes is fundamentally about three things: **High Availability**, **Scalability**, and **Disaster Recoverability**.

| Goal | How it's achieved |
|---|---|
| **High Availability** | Replicas, via a `ReplicaSet` |
| **Scalability** | Load balancing across replicas |
| **Disaster Recovery** | If everything goes down, the cluster rebuilds itself quickly |

### 9.2 Architecture Overview

Kubernetes consists of two main types of components:

- **Control Plane** (the "manager" side)
- **Worker Nodes** (any number, depending on business needs)

> The number of worker nodes isn't fixed — it scales with your workload.

#### Control Plane Components

| Component | Role |
|---|---|
| **API Server** | The entry point to the cluster — conceptually similar to the Docker daemon. Just like `docker container ls` (client) talks to the Docker daemon (server), tools like `kubectl`, a web dashboard, or any REST client (cURL, Python, Java, etc.) talk to the API server. |
| **etcd** | A highly available, replicated key-value store — the cluster's source of truth. |
| **Scheduler** | Decides where new deployments, pods, and containers should run. |
| **Controller Manager** | Continuously compares *current state* vs. *desired state* — e.g., "I should have 117 replicas running, but only 116 are up → spin up 1 more." |
| **Cloud Controller Manager** | Optional — only needed when running on a cloud provider. |

#### Worker Node Components

| Component | Role |
|---|---|
| **kubelet** | Talks to the control plane, reports node status, and actually runs the workloads. |
| **kube-proxy** | Handles networking and load balancing on the node. |

### 9.3 The Building Blocks

The basic unit in Kubernetes is **not** the container — it's the **Pod**.

- A **Pod** wraps one or more containers (each container still has its own IP, but you now think in terms of *Pod IP*).
- You deploy **Pods**, not raw containers.
- Users don't interact with Pods directly — they work with a **Deployment**.

```
Container  →  Pod  →  Deployment  →  Service
```

| Layer | Description |
|---|---|
| **Pod** | One or more containers, the smallest deployable unit |
| **Deployment** | A group of Pods (adds replication, rolling updates, rollbacks) |
| **Service** | A group of Deployments across multiple nodes — acts as a **load balancer / abstraction layer** |
| **Ingress** | DNS-like routing — turns `my-app.node1.pod2` into a friendly `my-app.com` |
| **ConfigMap** | Shared, public configuration available to all Pods |

All of these components are **loosely coupled** by design.

### 9.4 Installation Modes

- **All-in-one** (`minikube`-style)
  - Runs inside a single VM or container
  - Everything you create (pods, containers, etc.) lives inside that VM/container
- **Distributed**
  - Control plane nodes run on **Linux only**
  - Worker nodes can run on nearly any environment

### 9.5 Talking to Pods

You can hit the local API proxy to inspect a Pod's configuration:

```bash
# Returns the configuration of the given pod
curl http://localhost:8001/api/v1/namespaces/default/pods/kubernetes-bootcamp-67fbdd6b79-b4nvm
```

Or open an interactive shell inside a running Pod:

```bash
kubectl exec -it kubernetes-bootcamp-67fbdd6b79-b4nvm -- bash
```

---

<p align="center"><sub>Keep this file updated as you progress — future you will thank present you. 🚀</sub></p>
