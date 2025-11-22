# Dockerized Web Application Deployment on AWS ECR

## **Project Overview**

This project demonstrates how to **containerize a Python Flask web application** using Docker and deploy it to **AWS Elastic Container Registry (ECR)**.
It covers the complete workflow — from creating the application, building Docker images, optimizing them using multi-stage builds, managing environment variables, and securely pushing the image to AWS ECR for future deployment on ECS, EKS, or EC2. This project helps you understand **core containerization principles**, **AWS ECR integration**, and real-world **DevOps workflows** involving Docker and AWS.

---

## **Architecture Diagram**

```
Local Flask App → Docker Build → Docker Image → AWS ECR → (ECS / EKS / EC2 Deployment)
```

<img width="1536" height="1024" alt="ChatGPT Image Nov 22, 2025, 12_22_30 PM" src="https://github.com/user-attachments/assets/9dfde01f-dad7-4f81-94ab-a21d54280eee" />

---

## **Tools & Technologies Used**

| Tool / Service            | Purpose                              |
| ------------------------- | ------------------------------------ |
| **Python (Flask)**        | Lightweight web application backend  |
| **Docker**                | Containerizes and isolates the app   |
| **AWS ECR**               | Secure container image registry      |
| **AWS CLI**               | Command-line tool for AWS management |
| **Environment Variables** | Dynamic app configuration            |
| **GitHub**                | Source control and portfolio hosting |

---

## **System Workflow**

1️⃣ A **Flask web application** (`app.py`) displays dynamic messages using environment variables.
2️⃣ A **multi-stage Dockerfile** builds an optimized container image.
3️⃣ The image is **built and tested locally** using Docker.
4️⃣ The image is **pushed to AWS ECR** for deployment.
5️⃣ You can later deploy it to **AWS ECS, EKS, or EC2**.

**Flow Summary:**

```
Flask App → Dockerfile → Docker Image → Local Test → AWS ECR Push → Cloud Deployment
```

---

## **Project Files Overview**

| File               | Purpose                                 |
| ------------------ | --------------------------------------- |
| `app.py`           | Main Flask web application              |
| `requirements.txt` | Lists required Python packages          |
| `Dockerfile`       | Defines build and run configuration     |
| `.env`             | (Optional) Stores environment variables |
| `README.md`        | Documentation for GitHub                |

---

## **Application Code**

### `app.py`

```python
from flask import Flask
import os

app = Flask(__name__)

@app.route('/')
def home():
    app_name = os.getenv('APP_NAME', 'Dockerized Flask App')
    environment = os.getenv('ENVIRONMENT', 'development')
    return f"Welcome to {app_name}! Running in {environment} mode."

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### `requirements.txt`

```
flask==3.0.3
```

---

## **Docker Configuration**

### `Dockerfile`

```dockerfile
# ---------- Stage 1: Build ----------
FROM python:3.11-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# ---------- Stage 2: Run ----------
FROM python:3.11-slim
WORKDIR /app
COPY --from=builder /usr/local /usr/local
COPY app.py .
EXPOSE 5000
CMD ["python", "app.py"]
```

---

## **Commands & Steps**

### Step 1 — Build the Image

```bash
docker build -t my-docker-app .
```

### Step 2 — Run Locally

```bash
docker run -d -p 5000:5000 my-docker-app
```

Visit → [http://localhost:5000](http://localhost:5000)

---

### Step 3 — Add Environment Variables

#### Using CLI:

```bash
docker run -d -p 5000:5000 -e APP_NAME="My Flask App" -e ENVIRONMENT="Production" my-docker-app
```

#### Using `.env` file:

```
APP_NAME=My Flask App
ENVIRONMENT=Production
```

Run with:

```bash
docker run --env-file .env -p 5000:5000 my-docker-app
```

Visit → [http://localhost:5000](http://localhost:5000)

---

### Step 4 — Push to AWS ECR

#### 1️-Create Repository

```bash
aws ecr create-repository --repository-name my-docker-app
```

#### 2️-Authenticate Docker with ECR

```bash
aws ecr get-login-password --region ap-south-1 |
docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-south-1.amazonaws.com
```

#### 3️-Tag Image

```bash
docker tag my-docker-app:latest <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest
```

#### 4️-Push Image

```bash
docker push <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest
```

---

### Step 5 — Pull & Run from ECR

```bash
docker pull <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest
docker run -d -p 5000:5000 <account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest
```

Verify: Open [http://localhost:5000](http://localhost:5000)

---

## **Environment Variables**

| Variable      | Description            | Example                  |
| ------------- | ---------------------- | ------------------------ |
| `APP_NAME`    | Application name       | My Flask App             |
| `ENVIRONMENT` | Deployment environment | Production / Development |

---

## **AWS ECR Overview**

| Resource   | Name                                                                 | Purpose                     |
| ---------- | -------------------------------------------------------------------- | --------------------------- |
| Repository | `my-docker-app`                                                      | Stores Docker image         |
| Region     | `ap-south-1 (Mumbai)`                                                | AWS Region                  |
| Image URI  | `<account-id>.dkr.ecr.ap-south-1.amazonaws.com/my-docker-app:latest` | Used for ECS/EKS deployment |

---

## **Testing Steps**

1️- Build and run the Flask app locally on port 5000.
2️- Pass environment variables to test configuration.
3️- Push Docker image to AWS ECR.
4️- Pull image back from ECR to confirm successful deployment.
5️- Optionally deploy to ECS or EKS for a production-grade setup.

---

## **Best Practices**

* Use **multi-stage builds** to reduce image size.
* Never store secrets directly in your Dockerfile.
* Use **AWS Secrets Manager** or `.env` files (ignored in `.gitignore`).
* Automate builds and pushes via **GitHub Actions CI/CD**.

---

## **Real-World Use Cases**

* Deploying microservices or APIs in containers.
* Cloud-native development workflows with Docker and AWS.
* Automated image builds for continuous delivery pipelines.
* Hosting scalable apps on ECS or Kubernetes.

---

## **Summary**

| Resource                | Purpose                                     |
| ----------------------- | ------------------------------------------- |
| `Dockerfile`            | Defines image build steps                   |
| `Flask App`             | Simple backend web app                      |
| `AWS ECR`               | Stores container images                     |
| `Environment Variables` | Makes app configurable at runtime           |
| `Docker CLI`            | Used for build, run, tag, and push commands |

---

## **🧑‍💻 Author**

**Akash V — Cloud & DevOps Enthusiast ☁️**
💼 **Focus:** AWS | Serverless | Terraform | CI/CD | Docker | Kubernetes
🌍 [**LinkedIn**](https://linkedin.com/in/yourprofile) | [**GitHub**](https://github.com/yourusername)
