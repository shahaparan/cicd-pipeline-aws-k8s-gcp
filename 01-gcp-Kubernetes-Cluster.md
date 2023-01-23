
# GCP Installation of Kubernetes Cluster

## Step-01: Introduction
- Create k8s Cluster
- Connecting with SSH
- Testing Cluster
- Deleting the cluster

## Step-02: Create k8s Cluster
- **console k8s->cluster-> Enable**
- **Name:** k8s-manager
- **Default :** All
  ### Step-02.01: Create Node
  - **Click-> default Node**
  - **Name:** node
  - **Size :** 2
  - **Default :** All

## Step-03: Connecting with SSH
- **Click -> Labels: Connect**
- **Connect to the cluster** : Run Cloud Shell
   ```t
    gcloud container clusters get-credentials k8s-manager --zone us-central1-c --project quantum-fusion-374819
   ```
   
## Step-04: Testing Cluster

   ```t
    https://github.com/shahaparan/k8s-demo.git

    kubectl get nodes
    kubectl get all
    
    kubectl get pods --all-namespaces
    
    kubectl create -f nginx-deployment.yaml
    kubectl create -f nginx-svc-loadbalancer.yaml

    kubectl get pods -o wide 
    kubectl delete sv  nginx-svc-loadbalancer.yaml
    kubectl delete -f  nginx-deployment.yaml

    http://<master-public-ip>:<nodeport>
    http://<node1-public-ip>:<nodeport>
    http://<node2-public-ip>:<nodeport>

   ```
   ## Step-05: Deleting the cluster
   

 
