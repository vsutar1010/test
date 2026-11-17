# Experiment 7: Introduction to Containerization and Application Deployment using Docker

This experiment demonstrates how to containerize a simple Flask web application using Docker and run it in an isolated container.

## Objective
- Understand the concept of containerization and Docker
- Learn how to create a Dockerfile
- Build a Docker image
- Run a container and access the deployed app

## Theory
Containerization is a lightweight form of virtualization that allows applications to run in isolated environments called containers. Unlike traditional virtual machines, containers share the host operating system kernel but keep application processes isolated.

Key features of containerization:
- Lightweight
- Portable
- Fast startup
- Isolated
- Scalable

Docker is the most popular containerization platform. It allows developers to package applications and dependencies into portable images.

Core components:
1. Docker Engine: Runs and manages containers
2. Docker Image: A read-only template for an application
3. Docker Container: A running instance of an image
4. Dockerfile: A script used to build the image
5. Docker Hub: A public registry for sharing images

## Prerequisites
- Docker installed and running on the system
- Internet access to pull the Python base image from Docker Hub
- A terminal with shell access

## Step 1: Verify Docker installation
Run:

```bash
docker --version
```

Expected output:

```bash
Docker version 29.x.x
```

## Step 2: Create a project folder
Create a folder for the Flask app:

```bash
mkdir flask-docker-app
cd flask-docker-app
```

## Step 3: Create the application file
Create `app.py`:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello, Docker!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

## Step 4: Create requirements file
Create `requirements.txt`:

```txt
Flask==2.3.2
```

## Step 5: Create Dockerfile
Create a file named `Dockerfile`:

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

Folder structure:

```text
flask-docker-app/
├── app.py
├── requirements.txt
└── Dockerfile
```

## Step 6: Build the Docker image
Run:

```bash
docker build -t flask-docker-app:1.0 .
```

To view the image:

```bash
docker images
```

## Step 7: Run the container
Start the container:

```bash
docker run -d -p 5000:5000 --name flask-docker-app-container flask-docker-app:1.0
```

Check running containers:

```bash
docker ps
```

## Step 8: Access the application
Open a browser and visit:

```text
http://localhost:5000
```

The page should display:

```text
Hello, Docker!
```

## Step 9: Verify with curl
Run:

```bash
curl http://localhost:5000
```

Expected output:

```text
Hello, Docker!
```

## Experiment execution status
This experiment was successfully executed in the environment. The Docker image built successfully and the Flask app responded properly on port 5000.

## Troubleshooting
- If Docker is not running, start the Docker daemon service.
- If port 5000 is already in use, stop the conflicting service or use a different port mapping.
- If the container exits immediately, check logs with:

```bash
docker logs flask-docker-app-container
```

## Conclusion
This experiment shows how Docker simplifies the packaging and deployment of an application by creating an image from a Dockerfile and running it inside a container. Containerization improves portability, scalability, and consistency across different environments.

## Note
The provided lab sheet mentions a Java application deployment problem statement, but the actual implementation steps included in the experiment are the Dockerization of a simple Flask web application. The same Docker concepts apply to Java applications as well.
