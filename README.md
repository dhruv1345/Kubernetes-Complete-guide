# Kubernetes Complete Guide

## Introduction to Kubernetes
Kubernetes is an open-source container orchestration platform that streamlines the deployment, scaling, and management of containerized applications. Originally developed by Google and now maintained by the Cloud Native Computing Foundation (CNCF), Kubernetes provides a robust framework for automating complex application deployments while ensuring high availability and fault tolerance.

## Why Use Kubernetes?
Kubernetes is widely adopted for its ability to handle modern cloud-native applications efficiently. Key benefits include:
- **Automated Scaling**: Dynamically adjusts workloads based on traffic and demand.
- **Self-Healing**: Automatically restarts failed containers and replaces unhealthy nodes.
- **Load Balancing**: Distributes incoming traffic across multiple instances to prevent overload.
- **Declarative Configuration**: Uses YAML and JSON to define and manage applications.
- **Rolling Updates & Rollbacks**: Ensures zero-downtime deployment of new versions.
- **Resource Optimization**: Efficiently allocates CPU and memory resources.

## Kubernetes Architecture

![Kubernetes-Architecture-Diagram](https://github.com/user-attachments/assets/9a1ccf3d-c1d5-473f-aef7-07830598f0d7)


Kubernetes follows a master-worker architecture to ensure scalability and resilience.
### 1. Master Node (Control Plane)
- **API Server**: Serves as the front end of the cluster and processes REST requests.
- **Controller Manager**: Oversees node health, replication, and job scheduling.
- **Scheduler**: Assigns pods to nodes based on resource requirements.
- **etcd**: A distributed key-value store that maintains cluster state.

### 2. Worker Nodes
- **Kubelet**: The agent that runs on each node, ensuring pod lifecycle management.
- **Kube Proxy**: Manages network routing and service discovery.
- **Container Runtime**: The environment in which containers run (Docker, containerd, etc.).

## Installing Kubernetes
### Using Minikube (For Local Development)
Minikube is a tool that runs a single-node Kubernetes cluster on your local machine.
```sh
minikube start
kubectl cluster-info
```

### Using Kubeadm (For Production Setup)
Kubeadm simplifies the installation of Kubernetes clusters.
```sh
kubeadm init
```

## Kubernetes Networking
Kubernetes uses a flat networking model that enables seamless communication between services. Popular networking solutions include:
- **Flannel**
- **Calico**
- **Cilium**
- **Weave Net**

## Kubernetes Objects & Resources
### Pods
Pods are the smallest deployable units in Kubernetes and can contain multiple containers.
```sh
kubectl get pods
kubectl describe pod <pod-name>
```

### Deployments
Deployments manage replicas of applications to ensure uptime and scaling.
```sh
kubectl create deployment <name> --image=<image>
kubectl scale deployment <name> --replicas=3
```

### Services
Services expose applications running in pods internally or externally.
```sh
kubectl expose deployment <name> --type=ClusterIP --port=80
kubectl expose deployment <name> --type=NodePort --port=30007
```

### ConfigMaps & Secrets
These store configuration data separately from application code.
```sh
kubectl create configmap <name> --from-literal=key=value
kubectl create secret generic <name> --from-literal=password=mypassword
```

### Persistent Volumes (PV) & Claims (PVC)
Persistent storage ensures data is retained when pods restart.
```sh
kubectl get pv
kubectl get pvc
```

### StatefulSets
StatefulSets manage stateful applications that require stable network identities.
```sh
kubectl get statefulsets
kubectl describe statefulset <name>
```

### Namespaces
Namespaces help in organizing and isolating resources in a Kubernetes cluster.
```sh
kubectl create namespace <namespace-name>
kubectl get namespaces
```

## Kubernetes Networking
Networking is a fundamental part of Kubernetes. Key components include:
- **Cluster IP**: The default service type, accessible only within the cluster.
- **NodePort**: Exposes services on a static port on each node.
- **LoadBalancer**: Integrates with cloud providers to create external load balancers.
- **Ingress**: Routes external requests to internal services.
```sh
kubectl get ingresses
kubectl describe ingress <ingress-name>
```

## Role-Based Access Control (RBAC)
RBAC ensures that users and applications have appropriate permissions.
```sh
kubectl create role <role-name> --verb=get,list,watch --resource=pods
kubectl create rolebinding <binding-name> --role=<role-name> --user=<username>
```

## Monitoring & Debugging
Monitoring is essential for maintaining cluster health and performance.
### Logging & Monitoring
```sh
kubectl logs <pod-name>
kubectl top pod
kubectl top node
```
### Debugging Common Issues
```sh
kubectl describe pod <pod-name>
kubectl get events --sort-by=.metadata.creationTimestamp
```

## Helm - Kubernetes Package Manager
Helm simplifies the deployment and management of Kubernetes applications.
```sh
helm repo add stable https://charts.helm.sh/stable
helm install <name> stable/<chart-name>
```

## Example: Deploying a Sample Application
To illustrate Kubernetes in action, let's deploy a simple Nginx web server.

### Step 1: Create a Deployment
This command deploys three replicas of an Nginx server.
```sh
kubectl create deployment nginx-deployment --image=nginx --replicas=3
```

### Step 2: Expose the Deployment as a Service
Exposing the deployment makes it accessible within the cluster.
```sh
kubectl expose deployment nginx-deployment --type=NodePort --port=80
```

### Step 3: Retrieve Service Information
Check the details of the exposed service.
```sh
kubectl get services
```

### Step 4: Access the Application
Use Minikube to get the service URL and open it in a browser.
```sh
minikube service nginx-deployment --url
```

## Kubernetes Best Practices
1. **Use Namespaces**: Organize workloads efficiently to improve cluster management.
2. **Monitor Resource Utilization**: Implement monitoring solutions like Prometheus and Grafana.
3. **Implement RBAC**: Apply least-privilege access principles for security.
4. **Use Readiness & Liveness Probes**: Ensure applications are functional before accepting traffic.
5. **Utilize ConfigMaps & Secrets**: Avoid hardcoding configuration values.
6. **Automate Deployments with CI/CD**: Use Jenkins, ArgoCD, or GitOps pipelines for seamless deployments.

## Conclusion
Kubernetes has revolutionized the way modern applications are deployed and managed. By leveraging its powerful orchestration capabilities, businesses can ensure their applications are highly available, scalable, and resilient. A strong understanding of Kubernetes architecture, commands, and best practices will empower teams to build efficient, cloud-native solutions.
