### 1. Python Flask — Local Web Application

# Python Flask — Local Web Application

## Overview

This project stage focuses on building a simple **Python Flask web application**. The app dynamically displays messages using environment variables, laying the foundation for Docker containerization and AWS ECR deployment.

## Configuration Details

Framework: Python Flask
Version: 3.0.3
Host: 0.0.0.0
Port: 5000
Environment Variables: APP_NAME, ENVIRONMENT

## Application Code (app.py)

from flask import Flask
import os

app = Flask(**name**)

@app.route('/')
def home():
app_name = os.getenv('APP_NAME', 'Dockerized Flask App')
environment = os.getenv('ENVIRONMENT', 'development')
return f"Welcome to {app_name}! Running in {environment} mode."

if **name** == '**main**':
app.run(host='0.0.0.0', port=5000)

## Steps to Run Locally

1. Install dependencies:
   pip install flask
2. Run the app:
   python app.py
3. Visit → [http://localhost:5000](http://localhost:5000)

Expected Output:
Welcome to Dockerized Flask App! Running in development mode.

## Summary

app.py — Main web app file
requirements.txt — Flask dependencies
.env — Environment variables
Port 5000 — Local testing

---

## 🧑‍💻 Author

**Akash V** — Cloud & DevOps Engineer ☁️
Specializing in Serverless Architectures, AWS Automation, and CI/CD Pipelines.
🌍 [LinkedIn](https://linkedin.com/in/akashvetriselvan/) | [GitHub](https://github.com/akashvetriselvan)

---

