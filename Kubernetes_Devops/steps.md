## $100 Digital Ocean Referral Link
# Steps to Register on DigitalOcean and get Promo Code
First, open this Digital Ocean SignUp Reference Link and Sign Up to get your $100 credit.

While filling in your billing info, click on "Have a Promo Code?" at the bottom of the page.

Enter any one of the below codes to get extra credit:

CodeAnywhere10

LOWENDBOX

CODEANYWHERE

DOPRODUCT15

DO10

ALLSSD10

WP10

DROPLET10

BITNAMI

DEPLOY10

ACTIVATE10

DONEWS

FRANKFURT

From 1st step, you will get your first $100 credit and by using additional promo codes you can get up to $135 of total credits.

Note: Some codes only give more credit on higher plans.

------

# Install Kubernetes using MiniKube
********** Install Docker CE Edition **********

1. Uninstall old versions

sudo apt-get remove docker docker-engine docker.io containerd runc



2. Update the apt package index

sudo apt-get update

sudo apt-get install \    apt-transport-https \    ca-certificates \    curl \    gnupg \    lsb-release


3. Add Docker’s official GPG key:

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg



4. Use the following command to set up the stable repository

echo \  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


5. Install Docker Engine

sudo apt-get updatesudo apt-get install docker-ce docker-ce-cli containerd.io


6. verify Docker version

docker --version


********** Install KubeCtl **********

1. Download the latest release

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"



2. Install kubectl

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
3. Test to ensure the version you installed is up-to-date:

kubectl version --client





********** Install MiniKube **********

1. Download Binay

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64chmod +x minikube-linux-amd64
2. Install Minikube

sudo install minikube-linux-amd64 /usr/local/bin/minikube



3. Verify Installation

minikube version



4. Start Kubernetes Cluster

sudo apt install conntracksudo minikube start --vm-driver=none


5. Get Cluster Information

kubectl config view


----

# SetUp K8s HA Cluster (Updated)
## Kubernetes Installation Process

Note - Latest Ubuntu 22.04 and above is not compatible with Kubeadm, installation will end up with error. . Please use Ubuntu OS 20.04

************* Install Kubernetes on Master Node *************
Upgrade apt packages
sudo apt-get update

Create a configuration file for containerd:

cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF
Load modules:

sudo modprobe overlay
sudo modprobe br_netfilter


Set system configurations for Kubernetes networking:

cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF


Apply new settings:
sudo sysctl --system

Install containerd:

sudo apt-get update && sudo apt-get install -y containerd


Create a default configuration file for containerd:

sudo mkdir -p /etc/containerd


Generate default containerd configuration and save to the newly created default file:

sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml


Restart containerd to ensure new configuration file usage:

sudo systemctl restart containerd


Verify that containerd is running.

sudo systemctl status containerd


Disable swap:

sudo swapoff -a


Disable swap on startup in /etc/fstab:

sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab


Install dependency packages:

sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl


Download and add the GPG key:

sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg


Add Kubernetes to the repository list:

echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list


Update package listings:

sudo apt-get update


Install Kubernetes packages (Note: If you get a dpkg lock message, just wait a minute or two before trying the command again):

sudo apt-get install -y kubelet=1.24.0-00 kubeadm=1.24.0-00 kubectl=1.24.0-00


Turn off automatic updates:

sudo apt-mark hold kubelet kubeadm kubectl


Log into both Worker Nodes to perform previous steps 1 to 18.
Initialize the Cluster-

Initialize the Kubernetes cluster on the control plane node using kubeadm (Note: This is only performed on the Control Plane Node):

sudo kubeadm init --pod-network-cidr 192.168.0.0/16


Set kubectl access:

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config


Test access to cluster:

kubectl get nodes


Install the Calico Network Add-On -

On the Control Plane Node, install Calico Networking:

kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.24.5/manifests/tigera-operator.yaml
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.24.5/manifests/custom-resources.yaml


Confirm that all of the pods are running with the following command.

watch kubectl get pods -n calico-system


Wait for 2-4 Min and Check the status of the control plane node:

kubectl get nodes


Join the Worker Nodes to the Cluster

In the Control Plane Node, create the token and copy the kubeadm join command (NOTE: The join command can also be found in the output from kubeadm init command):

kubeadm token create --print-join-command
In both Worker Nodes, paste the kubeadm join command to join the cluster. Use sudo to run it as root:

sudo kubeadm join ...
In the Control Plane Node, view cluster status (Note: You may have to wait a few moments to allow all nodes to become ready):

kubectl get nodes


----
 # Upgrade Kubernetes Cluster
***************** Upgrade Control Plane Node ******************



1. Get the Running Node and Version

kubectl get nodes



2. Drain Master Node

kubectl drain <node-to-drain> --ignore-daemonsets



3. Upgrade kubeadm

sudo apt-get update
sudo apt-get install -y --allow-change-held-packages kubeadm=1.21.1-00


4. Verify that the download works and has the expected version:

kubeadm version



5. Verify the upgrade plan

sudo kubeadm upgrade plan v1.21.1-00



6. Apply the Upgrade

sudo kubeadm upgrade apply v1.21.1



7. Upgrade kubelet and kubectl packages

sudo apt-get update
sudo apt-get install -y --allow-change-held-packages kubelet=1.21.1-00 kubectl=1.21.1-00


8. Restart the kubelet:

sudo systemctl daemon-reload
sudo systemctl restart kubelet


10. Get the Running Node and Version

kubectl get nodes



11. Uncordon the Node

kubectl uncordon <node-to-uncordon>





***************** Upgrade Worker Node ******************



1. Drain Worker Node

kubectl drain <node-to-drain> --ignore-daemonsets --force



2. Upgrade kubeadm

sudo apt-get update
sudo apt-get install -y --allow-change-held-packages kubeadm=1.21.1-00

3. Verify that the download works and has the expected version:

kubeadm version



4. For worker nodes this upgrades the local kubelet configuration

sudo kubeadm upgrade node



5. Upgrade kubelet and kubectl packages

sudo apt-get update
sudo apt-get install -y --allow-change-held-packages kubelet=1.21.1-00 kubectl=1.21.1-00


6. Restart the kubelet:

sudo systemctl daemon-reload
sudo systemctl restart kubelet


7. Get the Running Node and Version

kubectl get nodes



8. Uncordon the Node

kubectl uncordon <node-to-uncordon>

-----------------------------------------------
