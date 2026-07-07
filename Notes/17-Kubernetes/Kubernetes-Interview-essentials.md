<div align="center">

# Kubernetes Essentials

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![DevOps](https://img.shields.io/badge/DevOps-Container%20Orchestration-blue?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Interview%20Ready-blue?style=for-the-badge)

**A simple, beginner-friendly guide to understand Kubernetes and answer interview questions with confidence**

</div>

---

## Table of Contents

1. [What is Kubernetes](#what-is-kubernetes)
2. [Why Use Kubernetes](#why-use-kubernetes)
3. [Kubernetes vs Docker](#kubernetes-vs-docker)
4. [Kubernetes Architecture](#kubernetes-architecture)
5. [Pods](#pods)
6. [ReplicaSets](#replicasets)
7. [Deployments](#deployments)
8. [Services](#services)
9. [Namespaces](#namespaces)
10. [ConfigMaps and Secrets](#configmaps-and-secrets)
11. [Volumes and Persistent Storage](#volumes-and-persistent-storage)
12. [Ingress](#ingress)
13. [Labels and Selectors](#labels-and-selectors)
14. [Scaling](#scaling)
15. [Health Checks (Probes)](#health-checks-probes)
16. [Rolling Updates and Rollbacks](#rolling-updates-and-rollbacks)
17. [Helm Basics](#helm-basics)
18. [kubectl Commands](#kubectl-commands)
19. [Common Interview Questions](#common-interview-questions-spoken-style-answers)
20. [Quick Cheat Sheet](#quick-cheat-sheet)

---

## What is Kubernetes

Kubernetes, often shortened to K8s, is an open source platform that automates the deployment, scaling, and management of containerized applications. Instead of manually starting and monitoring containers on individual servers, Kubernetes handles that work across a cluster of machines automatically.

**Spoken answer:** I would describe Kubernetes as the system that manages containers at scale. Docker handles running a single container well, but once I have dozens or hundreds of containers across multiple servers, I need something to schedule them, restart them if they crash, and scale them up or down, and that is exactly what Kubernetes does.

---

## Why Use Kubernetes

- Automatically restarts containers that crash or become unresponsive
- Scales applications up or down based on demand
- Distributes traffic across multiple instances of an app
- Rolls out updates gradually and rolls back automatically if something breaks
- Works consistently across different cloud providers or on-premise servers

**Spoken answer:** The main reason teams adopt Kubernetes is reliability at scale. If a container crashes, Kubernetes notices and starts a new one without anyone getting paged in the middle of the night. It also makes scaling and deploying updates far less risky compared to doing it manually.

---

## Kubernetes vs Docker

| Docker | Kubernetes |
|---|---|
| Builds and runs individual containers | Orchestrates many containers across machines |
| Works on a single host by default | Manages a cluster of multiple hosts |
| No built-in auto healing | Automatically restarts failed containers |
| No built-in load balancing | Distributes traffic across pods |

**Spoken answer:** Docker and Kubernetes are not competitors, they actually work together. Docker is typically used to build the container image, and Kubernetes is used to run and manage many of those containers reliably across a cluster of machines.

---

## Kubernetes Architecture

| Component | Role |
|---|---|
| Control Plane | Makes global decisions about the cluster |
| API Server | Entry point for all commands and communication |
| etcd | Stores the cluster's state and configuration |
| Scheduler | Decides which node a new pod should run on |
| Controller Manager | Keeps the actual state matching the desired state |
| Node | A worker machine that runs the actual application containers |
| Kubelet | Agent on each node that manages pods |
| Kube-proxy | Handles networking rules on each node |

**Spoken answer:** A Kubernetes cluster has a control plane that makes decisions, and worker nodes that actually run the application. The API server is how I interact with the cluster, etcd stores the current state of everything, the scheduler decides where new workloads go, and the kubelet on each node makes sure containers are actually running as expected.

---

## Pods

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app-pod
spec:
  containers:
    - name: my-app
      image: myapp:latest
      ports:
        - containerPort: 5000
```

**Spoken answer:** A pod is the smallest deployable unit in Kubernetes. It usually wraps a single container, though it can hold more than one if they need to share storage or network closely. Pods are also temporary, if one dies, Kubernetes does not repair it, it simply creates a brand new one.

---

## ReplicaSets

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-app-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: myapp:latest
```

**Spoken answer:** A ReplicaSet makes sure a specified number of identical pods are running at all times. If a pod crashes or gets deleted, the ReplicaSet notices the mismatch and creates a new one to bring the count back to what was requested.

---

## Deployments

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: myapp:v2
```

```bash
kubectl apply -f deployment.yaml
kubectl rollout status deployment/my-app-deployment
```

**Spoken answer:** A Deployment sits on top of a ReplicaSet and adds features like rolling updates and rollback history. In practice, I almost always use a Deployment instead of a raw ReplicaSet, since it gives me a controlled way to update the application version without downtime.

---

## Services

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 5000
  type: ClusterIP
```

| Type | Description |
|---|---|
| ClusterIP | Default, accessible only inside the cluster |
| NodePort | Exposes the service on a static port on each node |
| LoadBalancer | Provisions an external load balancer, common on cloud providers |

**Spoken answer:** Since pods are temporary and get new IP addresses whenever they restart, a Service provides a stable network endpoint that automatically routes traffic to the currently running pods matching a label selector. This is how other parts of the system reliably reach an app without needing to track individual pod IPs.

---

## Namespaces

```bash
kubectl create namespace staging
kubectl get pods --namespace=staging
```

**Spoken answer:** Namespaces let me divide a single cluster into logically separate sections, like separating development, staging, and production resources, or separating different teams. It helps with organization and can also be used to apply different resource limits or access controls to each group.

---

## ConfigMaps and Secrets

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_MODE: production

---
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  DB_PASSWORD: c2VjcmV0
```

**Spoken answer:** A ConfigMap stores non-sensitive configuration values, like a feature flag or environment name, separately from the application code. A Secret works the same way but is meant for sensitive values like passwords or API keys, and Kubernetes handles it with a bit more care, though I still make sure to combine it with proper access controls and encryption at rest.

---

## Volumes and Persistent Storage

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-app-storage
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

**Spoken answer:** Since pods are disposable, any data written inside a container is lost when the pod is replaced. A PersistentVolume represents actual storage in the cluster, and a PersistentVolumeClaim is how a pod requests some of that storage, which allows data like database files to survive even if the pod running the database gets recreated.

---

## Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
spec:
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-app-service
                port:
                  number: 80
```

**Spoken answer:** Ingress manages external HTTP and HTTPS access into the cluster, routing traffic to the right internal service based on the hostname or URL path. It's especially useful when I have multiple services that all need to be reachable from outside, since I can route them all through a single entry point instead of creating a separate LoadBalancer for each one.

---

## Labels and Selectors

```yaml
metadata:
  labels:
    app: my-app
    environment: production
```

```bash
kubectl get pods -l app=my-app
```

**Spoken answer:** Labels are key-value pairs attached to resources like pods, and selectors are how other resources, like Services or Deployments, find and group those pods together. This label based system is really at the core of how most things in Kubernetes connect to each other.

---

## Scaling

```bash
kubectl scale deployment my-app-deployment --replicas=5
kubectl autoscale deployment my-app-deployment --min=2 --max=10 --cpu-percent=70
```

**Spoken answer:** Scaling can be manual, where I directly set the number of replicas, or automatic using something like the Horizontal Pod Autoscaler, which watches metrics like CPU usage and adjusts the number of running pods on its own to handle changing traffic.

---

## Health Checks (Probes)

```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 5000
  initialDelaySeconds: 5
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /ready
    port: 5000
  initialDelaySeconds: 5
  periodSeconds: 5
```

**Spoken answer:** A liveness probe tells Kubernetes whether a container is still healthy, and if it fails, Kubernetes restarts that container. A readiness probe tells Kubernetes whether a container is ready to receive traffic, and if it fails, the pod is temporarily removed from the service's routing until it passes again.

---

## Rolling Updates and Rollbacks

```bash
kubectl set image deployment/my-app-deployment my-app=myapp:v3
kubectl rollout status deployment/my-app-deployment
kubectl rollout undo deployment/my-app-deployment
```

**Spoken answer:** By default, Deployments update pods gradually, replacing old ones with new ones a few at a time, so there is no downtime during a release. If something goes wrong with the new version, `kubectl rollout undo` reverts the deployment back to the previous working version quickly.

---

## Helm Basics

```bash
helm install my-release ./my-chart
helm upgrade my-release ./my-chart
helm uninstall my-release
```

**Spoken answer:** Helm is often described as a package manager for Kubernetes. Instead of writing and applying many separate YAML files by hand, I define a chart, which is a reusable template with configurable values, and Helm handles installing, upgrading, and uninstalling that whole set of resources as one unit.

---

## kubectl Commands

```bash
kubectl get pods
kubectl get services
kubectl get deployments
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- bash
kubectl delete pod <pod-name>
kubectl apply -f file.yaml
```

**Spoken answer:** `kubectl` is the command line tool I use to interact with a cluster. `get` lists resources, `describe` shows detailed information and recent events for troubleshooting, `logs` shows container output, and `exec` lets me open a shell directly inside a running pod when I need to debug something closely.

---

## Common Interview Questions (Spoken-Style Answers)

**Q: What is the difference between a Pod and a Deployment?**
A Pod is the smallest unit that actually runs one or more containers, but it is not self-healing on its own. A Deployment manages a set of identical Pods through a ReplicaSet, and adds features like rolling updates, version history, and automatic recovery if a Pod fails.

**Q: What is the difference between a ReplicaSet and a Deployment?**
A ReplicaSet only makes sure a certain number of pod replicas are running. A Deployment sits on top of a ReplicaSet and adds the ability to update the application version gradually and roll back if something goes wrong, which is why Deployments are used far more often in practice.

**Q: How does a Service find the right Pods to send traffic to?**
It uses label selectors. The Service is configured with a set of labels to match, and Kubernetes automatically routes traffic to any currently running Pod that has those matching labels, regardless of how many times those Pods get replaced.

**Q: What is the difference between a liveness probe and a readiness probe?**
A liveness probe checks if a container is still alive, and Kubernetes restarts it if the check fails. A readiness probe checks if a container is ready to accept traffic, and if it fails, the Pod is temporarily taken out of load balancing without being restarted.

**Q: What happens when a node in the cluster fails?**
Kubernetes detects that the node is unreachable, and if the pods on that node were managed by a Deployment or ReplicaSet, it schedules replacement pods on other healthy nodes automatically to maintain the desired number of replicas.

**Q: Why would you use a ConfigMap instead of hardcoding configuration values?**
It separates configuration from the container image, so the same image can be reused across different environments, like development or production, just by pointing it to a different ConfigMap, instead of rebuilding the image every time a setting changes.

**Q: What is the role of etcd in a Kubernetes cluster?**
etcd is a distributed key-value store that holds the entire state of the cluster, including what resources exist and their current configuration. The control plane constantly reads from and writes to etcd to keep track of the cluster's actual and desired state.

---

## Quick Cheat Sheet

| Task | Command |
|---|---|
| Get pods | `kubectl get pods` |
| Get services | `kubectl get services` |
| Get deployments | `kubectl get deployments` |
| Describe a resource | `kubectl describe pod name` |
| View logs | `kubectl logs pod-name` |
| Shell into pod | `kubectl exec -it pod-name -- bash` |
| Apply a config file | `kubectl apply -f file.yaml` |
| Delete a resource | `kubectl delete pod pod-name` |
| Scale a deployment | `kubectl scale deployment name --replicas=5` |
| Update image | `kubectl set image deployment/name container=image:tag` |
| Rollback deployment | `kubectl rollout undo deployment/name` |
| Create namespace | `kubectl create namespace name` |
| Install with Helm | `helm install release ./chart` |

---

<div align="center">

**Made for interview prep by Haseeb Javed**
Good luck with your Kubernetes interviews.

</div>