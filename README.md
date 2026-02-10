🚀 Kubernetes Setup on AWS EC2 using Minikube (Ubuntu 24.04)

A hands-on guide to running Kubernetes locally on an AWS EC2 instance using Minikube & Docker
Built with ❤️ on Ubuntu 24.04 | t2.large | 8 GB RAM

📌 Project Overview

This repository demonstrates how to set up a single-node Kubernetes cluster on an AWS EC2 instance using:

🟢 Ubuntu 24.04 LTS

🐳 Docker as container runtime

☸️ Minikube for Kubernetes

🎯 kubectl via Snap

This setup is perfect for learning, testing, and demos — especially when you don’t want to spin up a full EKS cluster.

🧰 Prerequisites

Before starting, make sure you have:

AWS Side

EC2 Instance: t2.large

OS: Ubuntu 24.04 LTS

Storage: Minimum 10 GB

Security Group:

Port 22 open (SSH)

Local Machine

SSH client (PowerShell / Terminal)

.pem key file for EC2 access

🔐 Step 1: Connect to EC2 Instance

From your local machine:

ssh -i "k8s.pem" ubuntu@<EC2_PUBLIC_IP>


✔ This securely connects you to your Ubuntu EC2 instance.

🔄 Step 2: Update the System
sudo apt update && sudo apt upgrade -y

Why?

Updates system packages

Applies security patches

Prevents dependency issues later

🐳 Step 3: Install Docker
sudo apt install -y docker.io


Enable and start Docker:

sudo systemctl enable docker
sudo systemctl start docker


Add current user to Docker group:

sudo usermod -aG docker $USER
exit


🔁 Reconnect via SSH so group changes take effect.

Why Docker?

Minikube uses Docker to run Kubernetes components as containers.

🧪 Step 4: Verify Docker Installation
docker --version


✔ Confirms Docker is installed correctly.

📦 Step 5: Install Required Packages
sudo apt install -y apt-transport-https ca-certificates curl

Why?

These packages allow secure downloads over HTTPS.

☸️ Step 6: Install Minikube

Download Minikube binary:

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64


Install it:

sudo install minikube-linux-amd64 /usr/local/bin/minikube


Verify installation:

minikube version

🎯 Step 7: Install kubectl (Recommended Way)

Instead of broken apt repos, we use Snap 👇

sudo snap install kubectl --classic


Verify:

kubectl version --client

Why Snap?

Official

Stable

No repo errors on Ubuntu 24.04

⚠️ Common Issue Explained (Important!)

❌ kubernetes-xenial repository is deprecated
Trying to use it results in:

404 Not Found
does not have a Release file


✅ Solution:
Remove the repo and use Snap-based kubectl (done above).

🚀 Step 8: Start Kubernetes Cluster with Minikube
minikube start --driver=docker

What happens here?

Minikube pulls Kubernetes images

Creates a Docker-based control plane

Configures networking & storage

✔ Kubernetes cluster starts successfully 🎉

🧠 Step 9: Verify Kubernetes Cluster

Check node status:

kubectl get nodes


Expected output:

NAME       STATUS   ROLES           VERSION
minikube   Ready    control-plane   v1.35.0


🎉 Your Kubernetes cluster is LIVE!

🏗 Architecture Overview
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

Kubernetes learning & practice

CI/CD pipeline testing

Helm chart validation

Pod, Service & Deployment experiments

🧹 Cleanup (Optional)

Stop cluster:

minikube stop


Delete cluster:

minikube delete


Author:- Rahul Shukla DevOps Engineer