🛒 Python E-Commerce Website with CI/CD Pipeline

A Django-based eCommerce web application with a complete CI/CD pipeline using GitHub Actions.
The project is containerized using Docker and automatically builds Docker images on every code push.

📌 Project Overview

This project demonstrates how a real-world Django eCommerce application can be integrated with modern DevOps practices such as Docker and CI/CD.

Key Features

User authentication

Product browsing

Cart and checkout flow

Order management

Admin dashboard

Dockerized Django application

Automated CI/CD pipeline using GitHub Actions

🧱 Tech Stack

Application

Python 3.8

Django 3.1

HTML, CSS, Bootstrap

SQLite (development)

DevOps / CI-CD

Docker

GitHub Actions

Docker Hub

GitHub Secrets

📂 Project Structure
Python-Ecommerce-Website-Project/
│
├── manage.py
├── requirements.txt
├── Dockerfile
├── .dockerignore
├── .github/
│   └── workflows/
│       └── docker-ci.yml
├── templates/
├── static/
├── app/
└── README.md

⚙️ Local Setup (Without Docker)
1️] Clone Repository
git clone https://github.com/your-username/Python-Ecommerce-Website-Project.git
cd Python-Ecommerce-Website-Project

2️] Create Virtual Environment
python -m venv venv


Activate:

Windows

venv\Scripts\activate


Linux / macOS

source venv/bin/activate

3️] Install Dependencies
pip install -r requirements.txt

4️] Run Migrations
python manage.py migrate

5️] Create Superuser
python manage.py createsuperuser

6️] Run Server
python manage.py runserver


Open in browser:

http://127.0.0.1:8000/

 Docker Setup
Dockerfile (Used in Project)
FROM python:3.8

WORKDIR /app

COPY . .
RUN pip install -r requirements.txt

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

Build Docker Image
docker build -t grtkart .

Run Docker Container
docker run -p 8000:8000 grtkart


Access application:

http://localhost:8000

 CI/CD Pipeline (GitHub Actions)

This project includes an automated CI/CD pipeline that triggers on every push to the main branch.

CI/CD Workflow Steps

Checkout source code

Login to Docker Hub (using GitHub Secrets)

Build Docker image

Push Docker image to Docker Hub

GitHub Actions Workflow File

📁 .github/workflows/docker-ci.yml

name: Docker CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v4

    - name: Login to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build Docker Image
      run: docker build -t ${{ secrets.DOCKER_USERNAME }}/grtkart:latest .

    - name: Push Docker Image
      run: docker push ${{ secrets.DOCKER_USERNAME }}/grtkart:latest

🔐 GitHub Secrets Configuration

Go to:

Repository → Settings → Secrets and variables → Actions

Add:

DOCKER_USERNAME

DOCKER_PASSWORD

🚀 CI/CD Flow Diagram
Code Push →
GitHub Actions →
Docker Image Build →
Push to Docker Hub →
Ready for Deployment

Docker Hub Image

The Docker image is available on Docker Hub and can be pulled using:

docker pull poojadhawale/grtkart:latest

Learning Outcomes

Containerized a Django application using Docker

Created a CI/CD pipeline with GitHub Actions

Automated Docker image build and push

Used GitHub Secrets for secure credentials

Followed real DevOps workflow practices

Built a Django-based eCommerce web application and containerized it using Docker

Implemented CI/CD pipeline using
