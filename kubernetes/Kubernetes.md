# Kubernetes

## Overview

Kubernetes is an open-source container orchestration platform that automates many of the manual processes involved in deploying, managing, and scaling containerized applications. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF). Kubernetes allows you to run containers across multiple hosts, providing mechanisms for deployment, maintenance, and scaling of applications.

## Clusters

A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node. The worker node(s) host the Pods, which are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault tolerance and high availability.

### Architecture

Kubernetes architecture is composed of the following main components:

- **Control Plane:** The control plane manages the Kubernetes cluster. It is responsible for maintaining the desired state of the cluster, such as which applications are running and which container images they use. The control plane components include the API server, scheduler, controller manager, and etcd.

- **Nodes:** Nodes are the machines (either virtual or physical) that run containerized applications. Each node contains the necessary services to run Pods, including the container runtime, kubelet, and kube-proxy.

### Control Plane

The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a deployment's replicas field is unsatisfied).

Key components of the control plane include:

- **API Server:** The API server is the front end for the Kubernetes control plane. It exposes the Kubernetes API and is the entry point for all the administrative tasks in the cluster.

- **etcd:** etcd is a consistent and highly available key-value store used as Kubernetes' backing store for all cluster data.

- **Scheduler:** The scheduler watches for newly created Pods that have no node assigned and selects a node for them to run on.

- **Controller Manager:** The controller manager runs controller processes, which are responsible for regulating the state of the cluster, including node controller, replication controller, endpoints controller, and service account & token controllers.

### Data Plane

The data plane, also known as the runtime plane, consists of nodes that run containerized applications. Each node in the cluster has the necessary services to run pods, and they communicate with the control plane to receive and execute workloads.

Key components of the data plane include:

- **Node:** A node is a worker machine in Kubernetes. Each node contains the services necessary to run pods and is managed by the control plane.

- **Kubelet:** The kubelet is an agent that runs on each node in the cluster. It ensures that containers are running in a pod.

- **Container Runtime:** The container runtime is the software that is responsible for running containers. Kubernetes supports several container runtimes: Docker, containerd, CRI-O, and others.

- **Kube-proxy:** Kube-proxy is a network proxy that runs on each node in your cluster, maintaining network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.

By orchestrating containers across multiple nodes, Kubernetes provides a powerful platform for deploying, scaling, and managing containerized applications, ensuring they run reliably and efficiently.

## Pods

Pods are the smallest and simplest Kubernetes objects. A Pod represents a single instance of a running process in your cluster. Pods contain one or more containers, such as Docker containers. When multiple containers are run in a single Pod, they share the same network namespace, which means they can communicate with each other using `localhost`. They also share storage volumes.

Key characteristics of Pods include:

- **Lifecycle:** Pods are ephemeral and do not persist if the node hosting them fails. Kubernetes manages pod lifecycles, restarting or replacing them as necessary.

- **Networking:** Each Pod gets its own IP address, which is shared among all the containers within that Pod.

- **Storage:** Pods can specify how to access storage resources, such as persistent volumes, which remain available even if the Pod is destroyed and recreated.

## K8s CLI: kubectl

`kubectl` is the command-line interface for interacting with the Kubernetes cluster. It allows users to manage and deploy applications, inspect and manage cluster resources, and view logs.

- **Commands:** [kubernetes.io/docs/reference/kubectl](https://kubernetes.io/docs/reference/kubectl)

## Persistent Volumes

Persistent Volumes (PVs) are a way to abstract storage in Kubernetes. A PV is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. PVs are independent of the lifecycle of any individual Pod that uses the PV.

### Persistent Volume Claims

Persistent Volume Claims (PVCs) are requests for storage by a user. A PVC specifies the desired storage capacity and access mode. When a PVC is created, Kubernetes finds a matching PV (if one exists) and binds them together. If no suitable PV exists, and dynamic provisioning is enabled, a new PV is automatically provisioned.

## Labels and Selectors

Labels are key-value pairs that are attached to Kubernetes objects, such as Pods, Nodes, and Services. They are used to organize and select subsets of objects based on their labels. Labels do not provide uniqueness; in fact, you can use the same key-value pair for multiple objects.

Selectors allow users to filter Kubernetes objects based on labels. There are two types of selectors:

- **Equality-based Selectors:** Allow matching objects that have a specific label or set of labels. For example, `environment=production`.

- **Set-based Selectors:** Allow matching objects based on a set of values. For example, `environment in (production, development)`.

## K8s Objects

Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Kubernetes objects include:

### Replica Sets

A Replica Set ensures that a specified number of pod replicas are running at any given time. It is a mechanism to maintain a stable set of replica Pods running at any given time, which can be scaled up or down.

### Deployments

A Deployment provides declarative updates for Pods and Replica Sets. You describe a desired state in a Deployment object, and the Deployment Controller changes the actual state to the desired state at a controlled rate.

### Stateful Sets

Stateful Sets manage the deployment and scaling of a set of Pods, and provide guarantees about the ordering and uniqueness of these Pods. Stateful Sets are used for stateful applications, which require persistent storage and stable network identities.

### Horizontal Pod Autoscalers

Horizontal Pod Autoscalers automatically scale the number of Pods in a Deployment, Replica Set, or Stateful Set based on observed CPU utilization or other select metrics.

### Services

A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them, sometimes called a microservice. Services enable loose coupling between dependent Pods.

### Ingresses

An Ingress is an API object that manages external access to the services in a cluster, typically HTTP. Ingress can provide load balancing, SSL termination, and name-based virtual hosting.

## Persistent Volumes (PVs)

Persistent Volumes (PVs) are a way to abstract storage in Kubernetes. A PV is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. PVs are independent of the lifecycle of any individual Pod that uses the PV.

### Persistent Volume Claims (PVCs)

Persistent Volume Claims (PVCs) are requests for storage by a user. A PVC specifies the desired storage capacity and access mode. When a PVC is created, Kubernetes finds a matching PV (if one exists) and binds them together. If no suitable PV exists, and dynamic provisioning is enabled, a new PV is automatically provisioned.

## K8s Manifests

Kubernetes resources are usually defined in manifest files. These files are written in YAML or JSON format and describe the desired state of the resource.

### Pod Manifest

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: my-pod
spec:
  containers:
  - name: my-container
      image: nginx
      ports:
      - containerPort: 80
```

### ReplicaSet Manifest

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
    name: my-replicaset
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
          - name: my-container
              image: nginx
              ports:
              - containerPort: 80
```

### Deployment Manifest

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: my-deployment
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
          - name: my-container
              image: nginx
              ports:
              - containerPort: 80
```

### HorizontalPodAutoscaler Manifest

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
    name: my-hpa
spec:
    scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: my-deployment
    minReplicas: 1
    maxReplicas: 10
    metrics:
    - type: Resource
        resource:
            name: cpu
            target:
                type: Utilization
                averageUtilization: 80
```

### Service Manifest

```yaml
apiVersion: v1
kind: Service
metadata:
    name: my-service
spec:
    selector:
        app: my-app
    ports:
    - protocol: TCP
        port: 80
        targetPort: 80
    type: ClusterIP
```

### Ingress Manifest

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
    name: my-ingress
spec:
    rules:
    - host: my-app.example.com
      http:
        paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: my-service
              port:
                number: 80
```

### PersistentVolume Manifest

```yml
apiVersion: v1
kind: PersistentVolume
metadata:
    name: my-pv
spec:
  capacity:
      storage: 10Gi
  accessModes:
      - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: my-storage-class
  hostPath:
      path: "/mnt/data"
```

### PersistentVolumeClaim Manifest

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: my-pvc
spec:
    accessModes:
        - ReadWriteOnce
    resources:
        requests:
            storage: 10Gi
    storageClassName: my-storage-class
```
