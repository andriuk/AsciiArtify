ArgoCD Demonstration Guide
==========================

Introduction
------------

**ArgoCD** is a Kubernetes controller that continuously monitors applications and ensures that their current state aligns with the desired state defined in your repository. It visualizes differences and offers automated or manual synchronization options.

Getting Started
---------------

### Prerequisites

*   Kubernetes cluster
*   Basic knowledge of Helm and Kubernetes

### Setting Up

#### 1\. Prepare a Local Cluster

We'll start by setting up a local Kubernetes cluster specifically for ArgoCD. Use the following commands:



```bash
# Create a cluster named 'argo'
k3d cluster create argo

# Get cluster information
kubectl cluster-info

# Check kubectl version
kubectl version

# List all resources across all namespaces
kubectl get all -A
```

#### 2\. Install ArgoCD

For this demonstration, we'll install ArgoCD using a script from its official repository.



```bash
# Create a namespace for ArgoCD
kubectl create namespace argocd

# Install ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Check the system status
kubectl get all -n argocd
kubectl get pod -n argocd -w
```

#### 3\. Access the ArgoCD GUI Interface

To access the ArgoCD web interface, use port forwarding:



```bash
kubectl port-forward svc/argocd-server -n argocd --address 0.0.0.0 8081:443
```

**Note**: ArgoCD uses HTTPS by default. In production, ensure proper certificate installation and configuration.

#### 4\. Retrieve Admin Password

Use the following commands to retrieve the ArgoCD admin password:



```bash
# Get the encoded password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"

# Decode the password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"|base64 -d;echo
```

#### 5\. Log In to ArgoCD

Use the credentials obtained in the previous step to log in:

*   **Username**: admin
*   **Password**: \[Output from step 4\]

![demo](img/ArgoCD_demo.gif)



Conclusion
----------

This guide provides a basic overview of setting up and accessing ArgoCD in a local Kubernetes environment. For more detailed information, refer to the [ArgoCD Documentation](https://argo-cd.readthedocs.io/en/stable/).


