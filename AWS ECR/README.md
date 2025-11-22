# AWS ECR — Push and Pull Docker Images

## Overview

This stage involves pushing the Docker image of the Flask app to **AWS Elastic Container Registry (ECR)** for cloud storage and deployment.
It demonstrates secure image management, tagging, and retrieval.

## Configuration Details

AWS Service: Elastic Container Registry (ECR)
Region: ap-south-1
Repository Name: my-docker-app
Authentication: AWS CLI
Image Tag: latest

## Steps to Push Image to ECR

1. Create Repository:
   aws ecr create-repository --repository-name my-docker-app
2. Login to ECR:
   aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-south-1.amazonaws.com
3. Tag and Push:
   docker tag my-docker-app:latest <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest
   docker push <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest

## Pull and Run Image from ECR

docker pull <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest
docker run -d -p 5000:5000 <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest

## Summary

AWS ECR — Secure container registry
Docker Image — Cloud-stored application
AWS CLI — Authentication and management
Port 5000 — Application endpoint

---

## 🧑‍💻 Author

**Akash V** — Cloud & DevOps Engineer ☁️
Specializing in Serverless Architectures, AWS Automation, and CI/CD Pipelines.
🌍 [LinkedIn](https://linkedin.com/in/akashvetriselvan/) | [GitHub](https://github.com/akashvetriselvan)

---
