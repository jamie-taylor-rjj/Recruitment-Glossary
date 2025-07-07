---
title: "What is Kubernetes?"
description: "Just what is Kubernetes, why is it sometimes called k8s, and what can developers do with it?"
lead: "Just what is Kubernetes, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "kubernetes"
weight: 100
toc: true
---

## 10,000 ft Overview

Kubernetes (often abbreviated as "k8s" - the "8" represents the eight letters between "k" and "s") is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications across clusters of computers.

Think of Kubernetes as an intelligent conductor for an orchestra of containers. While [Docker]({{< relref "what-is-docker" >}}) handles individual containers, Kubernetes manages entire applications made up of many containers, ensuring they work together harmoniously, stay healthy, and can scale up or down based on demand.

Originally developed by Google and based on their internal Borg system, Kubernetes has become the de facto standard for container orchestration and is a cornerstone of modern [DevOps]({{< relref "what-is-devops" >}}) and cloud-native architectures.

Kubernetes provides a platform for running distributed systems resiliently, handling scaling, failover, deployment patterns, and providing service discovery, load balancing, and other critical capabilities.

## Beginner Information

Kubernetes solves the challenge of managing containers at scale. While you might manually start and stop a few Docker containers, imagine managing thousands of containers across hundreds of servers - that's where Kubernetes excels.

**Key Kubernetes Concepts:**

- **Cluster**: A set of computers (nodes) running Kubernetes
- **Node**: An individual computer in the cluster (physical or virtual machine)
- **Pod**: The smallest deployable unit, containing one or more containers
- **Service**: A stable way to expose pods to network traffic
- **Deployment**: Manages multiple replicas of pods

**A Simple Pod Example:**

{{< highlight yaml "linenos=inline">}}
apiVersion: v1
kind: Pod
metadata:
  name: my-web-app
  labels:
    app: web
spec:
  containers:
  - name: web-container
    image: nginx:1.21
    ports:
    - containerPort: 80
{{< /highlight >}}

**A Basic Deployment:**

{{< highlight yaml "linenos=inline">}}
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web-app
        image: my-web-app:v1.0
        ports:
        - containerPort: 8080
{{< /highlight >}}

**Essential kubectl Commands:**

{{< highlight bash>}}
# Get cluster information
kubectl cluster-info

# List all pods
kubectl get pods

# Create resources from YAML file
kubectl apply -f deployment.yaml

# Get detailed information about a pod
kubectl describe pod my-pod

# View logs from a pod
kubectl logs my-pod

# Scale a deployment
kubectl scale deployment web-app-deployment --replicas=5
{{< /highlight >}}

**Benefits of Kubernetes:**

- **Automatic Scaling**: Scale applications up or down based on demand
- **Self-Healing**: Restart failed containers and replace unhealthy ones
- **Load Balancing**: Distribute traffic across multiple container instances
- **Rolling Updates**: Deploy new versions without downtime
- **Service Discovery**: Containers can find and communicate with each other

## Intermediary Information

Kubernetes architecture consists of a control plane that manages the cluster and worker nodes that run the actual applications.

**Kubernetes Architecture:**

**Control Plane Components:**

- **API Server**: The front-end for the Kubernetes control plane
- **etcd**: Distributed key-value store for cluster data
- **Scheduler**: Assigns pods to nodes based on resource requirements
- **Controller Manager**: Runs controller processes that regulate cluster state

**Node Components:**

- **kubelet**: Agent that communicates with the control plane
- **kube-proxy**: Network proxy that maintains network rules
- **Container Runtime**: Software that runs containers (Docker, containerd, CRI-O)

**Advanced Resource Types:**

**Services for Network Exposure:**
{{< highlight yaml "linenos=inline">}}
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: web
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: web-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: web-service
            port:
              number: 80
{{< /highlight >}}

**ConfigMaps and Secrets:**

{{< highlight yaml "linenos=inline">}}
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  database_host: "db.example.com"
  database_port: "5432"
---
apiVersion: v1
kind: Secret
metadata:
  name: app-secrets
type: Opaque
data:
  database_password: cGFzc3dvcmQ=  # base64 encoded
{{< /highlight >}}

**Persistent Storage:**

{{< highlight yaml "linenos=inline">}}
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: database-storage
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: fast-ssd
{{< /highlight >}}

**Namespace Organization:**

- **Resource Isolation**: Separate environments (dev, staging, production)
- **Access Control**: Different permissions for different teams
- **Resource Quotas**: Limit resource usage per namespace

**Health Checks and Monitoring:**

- **Liveness Probes**: Determine if a container is running
- **Readiness Probes**: Determine if a container is ready to serve traffic
- **Startup Probes**: Handle slow-starting containers

## Advanced Information

Enterprise Kubernetes involves sophisticated patterns for security, networking, storage, and multi-cluster management.

**Advanced Deployment Strategies:**

{{< highlight yaml "linenos=inline">}}
apiVersion: argoproj.io/v1alpha1
kind: Rollout
metadata:
  name: web-app-rollout
spec:
  replicas: 10
  strategy:
    blueGreen:
      activeService: web-service-active
      previewService: web-service-preview
      autoPromotionEnabled: false
      scaleDownDelaySeconds: 30
      prePromotionAnalysis:
        templates:
        - templateName: success-rate
        args:
        - name: service-name
          value: web-service-preview
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: web-app
        image: myapp:v2.0
{{< /highlight >}}

**Service Mesh Integration:**

{{< highlight yaml "linenos=inline">}}
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: web-app-vs
spec:
  http:
  - match:
    - headers:
        canary:
          exact: "true"
    route:
    - destination:
        host: web-service
        subset: v2
      weight: 100
  - route:
    - destination:
        host: web-service
        subset: v1
      weight: 90
    - destination:
        host: web-service
        subset: v2
      weight: 10
{{< /highlight >}}

**Custom Resource Definitions (CRDs):**

{{< highlight yaml "linenos=inline">}}
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: webapps.stable.example.com
spec:
  group: stable.example.com
  versions:
  - name: v1
    served: true
    storage: true
    schema:
      openAPIV3Schema:
        type: object
        properties:
          spec:
            type: object
            properties:
              replicas:
                type: integer
              image:
                type: string
  scope: Namespaced
  names:
    plural: webapps
    singular: webapp
    kind: WebApp
{{< /highlight >}}

**Enterprise Security Features:**

- **RBAC (Role-Based Access Control)**: Fine-grained permissions
- **Pod Security Policies**: Enforce security standards
- **Network Policies**: Control network traffic between pods
- **Secret Management**: Integration with external secret stores (Vault, AWS Secrets Manager)
- **Admission Controllers**: Enforce policies and modify requests

**Multi-Cluster Management:**

- **Cluster Federation**: Manage multiple clusters as a single entity
- **GitOps**: Declarative cluster management using Git
- **Service Mesh**: Cross-cluster service communication
- **Disaster Recovery**: Backup and restore strategies

**Observability and Monitoring:**

{{< highlight yaml "linenos=inline">}}
apiVersion: v1
kind: ServiceMonitor
metadata:
  name: web-app-metrics
spec:
  selector:
    matchLabels:
      app: web-app
  endpoints:
  - port: metrics
    interval: 30s
    path: /metrics
{{< /highlight >}}

**Cloud Provider Integrations:**

- **Managed Kubernetes**: EKS (AWS), GKE (Google), AKS (Azure)
- **Auto-scaling**: Cluster autoscaler, vertical pod autoscaler
- **Load Balancers**: Cloud provider integration
- **Storage**: Dynamic provisioning with cloud storage
- **Identity**: Integration with cloud IAM systems

**Performance Optimization:**

- **Resource Requests and Limits**: Efficient resource allocation
- **Horizontal Pod Autoscaling**: Scale based on metrics
- **Node Affinity**: Control pod placement
- **Taints and Tolerations**: Dedicated nodes for specific workloads

Kubernetes has become the foundation for modern cloud-native applications and is essential knowledge for DevOps engineers, platform engineers, and anyone working with containerized applications at scale. Its ecosystem continues to evolve with innovations in security, networking, and developer experience.

## External Links

- [Kubernetes Documentation](https://kubernetes.io/docs/) @ Kubernetes
- [kubectl Reference](https://kubernetes.io/docs/reference/kubectl/) @ Kubernetes
- [Kubernetes Patterns](https://kubernetes.io/docs/concepts/cluster-administration/patterns/) @ Kubernetes
