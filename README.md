🚀 Kubernetes on AWS EC2 using Minikube

Run a single-node Kubernetes cluster on an AWS EC2 instance using Minikube + Docker.
Built for learning, testing, and demos without the overhead of EKS.

OS: Ubuntu 24.04 LTS
Instance: t2.large (8 GB RAM)
Kubernetes: Minikube (Docker driver)

📌 Overview

This project demonstrates how to set up Kubernetes on an AWS EC2 instance using:

Ubuntu 24.04 LTS

Docker as the container runtime

Minikube for Kubernetes

kubectl (Snap-based installation)

Ideal when you want hands-on Kubernetes experience without provisioning a full-managed cluster.

🧰 Prerequisites
AWS

EC2 Instance: t2.large

OS: Ubuntu 24.04 LTS

Storage: 10 GB minimum

Security Group:

Port 22 open (SSH)

Local Machine

SSH client (Terminal / PowerShell)

EC2 .pem key

🔐 Connect to EC2
ssh -i k8s.pem ubuntu@<EC2_PUBLIC_IP>

🔄 System Update
sudo apt update && sudo apt upgrade -y


Keeps packages secure and avoids dependency issues later.

🐳 Install Docker
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker


Add user to Docker group:

sudo usermod -aG docker $USER
exit


Reconnect via SSH after this step.

Verify:

docker --version

📦 Install Required Packages
sudo apt install -y apt-transport-https ca-certificates curl


Required for secure binary downloads.

☸️ Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube


Verify:

minikube version

🎯 Install kubectl (Recommended)

Ubuntu 24.04 breaks old Kubernetes apt repos.
Use Snap (official & stable):

sudo snap install kubectl --classic


Verify:

kubectl version --client

⚠️ Common Issue (Avoid This)

❌ Using kubernetes-xenial repo results in:

404 Not Found
does not have a Release file


✅ Solution: Use Snap-based kubectl (already done).

🚀 Start Kubernetes Cluster
minikube start --driver=docker


Minikube will:

Pull Kubernetes images

Create Docker-based control plane

Configure networking & storage

🧠 Verify Cluster
kubectl get nodes


Expected output:

NAME       STATUS   ROLES           VERSION
minikube   Ready    control-plane   v1.35.0


🎉 Kubernetes is up and running!

🏗 Architecture
Local Machine
     |
     | SSH
     v
AWS EC2 (Ubuntu 24.04)
     |
     | Docker
     v
Minikube
     |
     v
Single-node Kubernetes Cluster

🎯 Use Cases

Kubernetes learning & hands-on practice

CI/CD pipeline testing

Helm chart validation

Pod, Service & Deployment experiments

Debugging containerized workloads

🧹 Cleanup

Stop cluster:

minikube stop


Delete cluster:

minikube delete

👨‍💻 Author

Rahul Shukla
DevOps Engineer
AWS • Docker • Kubernetes • CI/CD
