# Installation of Kubernets on AWS EC2 Single Node cluster 


## Below are the steps to install the Kubernets on EC2

#### Step 1.

```sh

sudo su  // Take the super user access 

setenforce 0

To disable SELinux temporarily (disable the security of Linux)

```

#### Step 2.

```sh
free -h 

The free command gives information about used and unused memory usage and swap memory of a system.

```

#### Step 3.
```sh
 
swapoff -a

To deactivate a swap space, use the command swapoff

```

#### Step 4.

Ubuntu 16.04 has reported issues with traffic being routed incorrectly due to iptables being bypassed.
Ensure net.bridge.bridge-nf-call-iptables is set to 1 in the sysctl config,

```sh
cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```
#### Step 5.

```sh
Installaton of Docker 

yum install docker 

systemctl enable docker 

systemctl start docker 

 ```
#### Step 6.

To configure the Kubernetes package in the System we will use this command.

 ```sh
 cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
        https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

#### Step 7. 

##### installation of Kubelet , Kubeadm, Kubectl

Kubelet : The kubelet is the primary "node agent" that runs on each node. 

Kubeadm: Kubeadm is a tool built to provide kubeadm init and kubeadm join as best-practice "fast paths" for creating Kubernetes clusters. 

Kubectl: The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters.

```sh 
yum install kubeadm kubectl kubelet

systemctl status kubelet

kubeadm init

mkdir -p $HOME/.kube
 
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

#### Step 8.

To See the list of pods 
```sh

kubectl taint nodes --all node-role.kubernetes.io/master-

kubectl apply -f https://docs.projectcalico.org/v3.9/manifests/calico.yaml 

kubectl get pods --all-namespaces

```





