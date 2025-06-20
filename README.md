# Automated CI/CD Pipeline for Static Website Deployment

🚀 A Jenkins-powered CI/CD pipeline that automates the deployment of a static website to an Nginx server on AWS EC2, triggered by GitHub webhooks.

## 📌 Overview

This project demonstrates an end-to-end automated deployment pipeline for a static website using:
- **Jenkins** as CI/CD orchestrator
- **GitHub Webhooks** for real-time triggers
- **Nginx** as production web server
- **AWS EC2** as cloud infrastructure

## 📦 Prerequisites

Before you begin, ensure you have:
- AWS account with EC2 access
- GitHub account
- Basic understanding of:
  - Linux commands
  - Jenkins pipelines
  - Web servers

## 🛠️ Architecture

```plaintext
GitHub (Code) → Webhook → Jenkins (Build) → Nginx (Deploy)
                      ↳ AWS EC2 (Infrastructure)
```

## 🛠️ 🚀 Setup Guide

### 1. Infrastructure Provisioning

```
# Create EC2 instance (Amazon Linux 2)
- Open ports: 22 (SSH), 80 (HTTP), 8080 (Jenkins)
- Minimum specs: t2.micro (1 vCPU, 1GB RAM)

```

### 2. Software Installation

SSH into your EC2 instance and run:

```
#Installed OpenJDK 17 (required for Jenkins):
sudo apt install openjdk-17-jdk -y

# Install Jenkins
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

#Started & Enabled Jenkins
Sudo systemctl restart Jenkins
Sudo systemctl status jenkins

```

### 3. Jenkins Configuration

```
http://<EC2_IP>:8080
```
Configuring Jenkins Pipeline
Configured the pipeline to fetch code from GitHub.
Used GitHub Webhooks to trigger builds automatically on code push.


### 4. GitHub Webhook Setup

* Settings → Webhooks → Add webhook
* Payload URL: http://<EC2_Public_IP>:8080/github-webhook/
* Content type: application/json
* Events: "push and pull event"

### 3.	Setting Up Nginx as a Web Server


```
#Installed Nginx:
sudo apt install nginx -y
sudo systemctl status nginx

#add the Jenkins user to the www-data group.
sudo usermod -aG www-data Jenkins

#modify file permissions recursively in the Nginx web directory, 
sudo chmod -R 775 /var/www/html/

```

Add a build step to the pipeline as Execute shell.

## 🔍 Testing the Pipeline

browse EC2 Ip Address

![image](https://github.com/user-attachments/assets/4445e90e-3d59-40e3-9bb4-6dce646f6215)


## ▶️ Live Demo Video

[![CI/CD Pipeline Demo](https://github.com/user-attachments/assets/4445e90e-3d59-40e3-9bb4-6dce646f6215)](https://drive.google.com/file/d/1-hM_i3P-pC7P0OqY71DNOjRekxdpVX8T/view?usp=sharing)


