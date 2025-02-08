## Overview

Kubernetes, often abbreviated as **K8s**, is an open-source container orchestration platform. It automates the deployment, scaling, and management of containerized applications.

### Key Features

- **Automated Scheduling**: Optimizes resource utilization by scheduling containers based on constraints.
- **Self-Healing**: Automatically restarts failed containers, replaces them, and reschedules when nodes go down.
- **Load Balancing**: Distributes traffic to maintain high availability.
- **Horizontal Scaling**: Automatically scales applications based on demand.
- **Storage Orchestration**: Mounts and manages storage (e.g., local storage, cloud, NFS).
- **Service Discovery**: Dynamically assigns IPs and names to services.

---

## Kubernetes Architecture

### Master Components

The **control plane** manages the Kubernetes cluster.

1. **API Server (`kube-apiserver`)**: The entry point to the cluster, exposing the Kubernetes API.
2. **Controller Manager (`kube-controller-manager`)**: Manages controllers for nodes, endpoints, replication, and more.
3. **Scheduler (`kube-scheduler`)**: Assigns workloads to nodes.
4. **ETCD**: A distributed key-value store for cluster data and configurations.

### Node Components

Each **worker node** runs these processes:

1. **Kubelet**: Agent ensuring container states match the desired configuration.
2. **Kube-proxy**: Handles networking and forwarding traffic to pods.
3. **Container Runtime**: The engine (e.g., Docker, CRI-O, containerd) that runs the containers.

---

## Core Kubernetes Concepts

### 1. **Cluster**

A set of nodes (machines) that run containerized applications. Includes:

- **Master Nodes**: Manage the cluster.
- **Worker Nodes**: Run application workloads.

### 2. **Pod**

The smallest deployable unit in Kubernetes, encapsulating one or more containers. Features:

- Shared storage and networking.
- Communication among containers.

### 3. **Service**

An abstraction to expose a set of Pods as a network service, enabling discovery and load balancing.

### 4. **Namespace**

Provides logical isolation within a cluster, commonly used to separate resources by environment (e.g., dev, test, prod).

### 5. **ConfigMap and Secret**

- **ConfigMap**: Stores configuration data as key-value pairs.
- **Secret**: Stores sensitive data like passwords and tokens.

### 6. **Deployment**

Manages the desired state of Pods using ReplicaSets, enabling scaling and updates.

### 7. **Ingress**

Manages external HTTP/S access to services within a cluster, often using custom rules for routing.

---

## Kubernetes Objects Example

### Deployment YAML

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21
        ports:
        - containerPort: 80

```

### Service YAML

```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer

```

## Workflows in Kubernetes

### 1. **Application Deployment**

- Create a **Pod**, **Deployment**, or **Job**.
- Expose the workload with a **Service**.
- Manage traffic with **Ingress**.

### 2. **Scaling Applications**

- **Horizontal Scaling**: Use a Horizontal Pod Autoscaler (HPA).
- **Vertical Scaling**: Modify the resource requests/limits of Pods.

### 3. **Rolling Updates**

- Deployments allow updates with minimal downtime.
- Use `kubectl rollout` for updates or rollbacks:

```
kubectl rollout status deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment
```

### 4. **Monitoring and Logging**

- Tools like **Prometheus** and **Grafana** for metrics.
- Integrations with **ELK Stack** or **Fluentd** for centralized logging.

---

## Kubernetes Commands

### Basic Operations

```
# Get all nodes in the cluster
kubectl get nodes

# List pods in a namespace
kubectl get pods -n <namespace>

# Describe a specific resource
kubectl describe pod <pod-name>

# Apply a YAML file
kubectl apply -f <file-name.yaml>

# Delete a resource
kubectl delete pod <pod-name>

```

### Troubleshooting
```
# View logs for a pod
kubectl logs <pod-name>

# Access a running container
kubectl exec -it <pod-name> -- /bin/bash

# Debug pod issues
kubectl describe pod <pod-name>

```

## Best Practices

1. **Namespace Isolation**: Separate environments using namespaces.
2. **Resource Quotas**: Enforce CPU and memory limits to prevent resource contention.
3. **Infrastructure as Code**: Manage YAML configurations with GitOps tools like ArgoCD.
4. **Use Liveness and Readiness Probes**: Ensure containers are healthy and ready for traffic.
5. **Regular Updates**: Keep Kubernetes and its components updated to avoid security risks.

---

## Kubernetes Ecosystem

### Tools and Add-ons

- **Helm**: Kubernetes package manager.
- **Kustomize**: Native support for managing configurations.
- **Istio**: Service mesh for traffic management and security.
- **Kubectl**: Command-line tool to interact with the cluster.
- **Minikube**: Local Kubernetes for development.

---

## Learning Resources

- **Official Documentation**: https://kubernetes.io/docs/
- **Interactive Labs**: [Katacoda Kubernetes Scenarios](https://www.katacoda.com/)
- **Books**:
    - _Kubernetes Up and Running_ by Brendan Burns et al.
    - _The Kubernetes Book_ by Nigel Poulton.
- **Online Courses**:
    - Kubernetes Basics by Google.
    - Certified Kubernetes Administrator (CKA) Prep.