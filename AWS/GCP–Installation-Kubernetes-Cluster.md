
# GCP Installation of Kubernetes Cluster

## Step-01: Introduction
- Create Compute Engine (VM)
- Create  two Node(VM)  
- Cross Region S3Prod S3
- Updating Source Code
- Cloudwatch
- Delete All Resources 

## Step-02: Create Compute Engine (VM)
- **Name:** Manager
- **Region:** own-choice
- **Machine Configuration:** N2
- **Boot Disk: Click on ->** Change  
  - **Operating System:** Ubuntu  
  - **Version:** Ubuntu 18.04LTS  
  - **Click on Select**
- **Firewall** : Checked HTTP/HTTPS
- Click on **Create**
- click on **SSH -> Open Browser window**
- **Install Docker**
    ```t
    sudo su - 
    apt update
    apt install docker.io -y
    docker --version 
    docker images
    ```
    
- **Start Docker Service**
    ```t
    systemctl start docker 
    systemctl enable docker 
    sudo apt-get update && sudo apt-get install -y apt-transport-https curl
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list 
    deb https://apt.kubernetes.io/kubernetes-xenial main 
    EOF
   ```
   
 - **Install Kubelet & Kubeadm**
 
     ```t
   
    sudo apt-get update 
    sudo apt-get install -y kubelet kubeadm kubectl 
    sudo apt-mark hold kubelet kubeadm kubectl
       
       ```

## Step-02: Create  two Node(VM)  
- **Name:** Node-1
- **Region:** own-choice
- **Machine Configuration:** ec2
- **Boot Disk: Click on ->** Change  
  - **Operating System:** Ubuntu  
  - **Version:** Ubuntu 18.04LTS  
  - **Click on Select**
- **Firewall** : Checked HTTP/HTTPS
- Click on **Create**

- click on **SSH -> Open Browser window**

- **Install Docker**
    ```t
    sudo su - 
    apt update
    apt install docker.io -y
    docker --version 
    docker images
    ```
    
- **Start Docker Service**
    ```t
    systemctl start docker 
    systemctl enable docker 
    sudo apt-get update && sudo apt-get install -y apt-transport-https curl
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list 
    deb https://apt.kubernetes.io/kubernetes-xenial main 
    EOF
   ```
   
 - **Install Kubelet & Kubeadm**
 
     ```t
   
    sudo apt-get update 
    sudo apt-get install -y kubelet kubeadm kubectl 
    sudo apt-mark hold kubelet kubeadm kubectl
       ```

## Step-03: Create  two Node(VM)  
- **Name:** Node-1
- **Region:** own-choice
- **Machine Configuration:** ec2
- **Boot Disk: Click on ->** Change  
  - **Operating System:** Ubuntu  
  - **Version:** Ubuntu 18.04LTS  
  - **Click on Select**
- **Firewall** : Checked HTTP/HTTPS
- Click on **Create**

## Step -04 ** Create MASTER MACHINE (Master)**
    ```t
    apt install net-tools  
    ifconfig
    kubeadm init --apiserver-advertise-address=<VM-privateIP> --pod-network-cidr=192.168.0.0/16
    
    mkdir -p $HOME/.kube

    cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

    chown $(id -u):$(id -g) $HOME/.kube/config

    kubectl apply  -f  https://docs.projectcalico.org/v3.8/manifests/calico.yaml 

    kubectl get pods --all-namespaces
    
    kubectl get nodes
    kubectl get all
    git clone https:shahapara.com 
    kubectl create -f nginx-nodeport.yaml
    kubectl create -f service-nodeport.yaml

    kubectl get pods -o wide 
    kubectl delete sv service-nodeport.yaml
    kubectl delete -f nginx-nodeport.yaml
    
    ```

## Step-05 Join the cluster (node 1 & 2)
 
   ```t
    kubeadm join 10.128.0.13:6443 --token xxxxxxxxx --discovery-token-ca-cert-hash sha2xxxxxxxxxxxx 
   ```
   
   
## step-05 Testing 
   ```t
    - http://<master-public-ip>:<nodeport>
    - http://<node1-public-ip>:<nodeport>
    - http://<node2-public-ip>:<nodeport>
   ```

