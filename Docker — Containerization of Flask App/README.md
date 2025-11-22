# Docker — Containerization of Flask App

## Overview

In this stage, the Flask web application is containerized using **Docker**. A Docker image is created to run the app consistently across different environments.

## Configuration Details

Base Image: python:3.11-slim
Working Directory: /app
Exposed Port: 5000
Command: python app.py

## Dockerfile

FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py .
EXPOSE 5000
CMD ["python", "app.py"]

## Steps to Containerize and Run

1. Build Image: docker build -t my-docker-app .
2. Run Container: docker run -d -p 5000:5000 my-docker-app
3. Access the app → [http://localhost:5000](http://localhost:5000)

## Key Features

* Multi-stage build support for efficiency
* Containerized runtime environment
* Easy local or cloud deployment

## Summary

Dockerfile — Defines build and runtime
Docker Image — Portable environment
Port 5000 — Application access
---

## 🧑‍💻 Author

**Akash V** — Cloud & DevOps Engineer ☁️
Specializing in Serverless Architectures, AWS Automation, and CI/CD Pipelines.
🌍 [LinkedIn](https://linkedin.com/in/akashvetriselvan/) | [GitHub](https://github.com/akashvetriselvan)

---
