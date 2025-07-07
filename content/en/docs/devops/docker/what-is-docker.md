---
title: "What is Docker?"
description: "Just what is Docker, and what can developers do with it?"
lead: "Just what is Docker, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "docker"
weight: 100
toc: true
---

## 10,000 ft Overview

Docker is a containerization platform that packages applications and their dependencies into lightweight, portable containers. These containers can run consistently across different computing environments, from a developer's laptop to production servers in the cloud.

Think of Docker containers like shipping containers - they provide a standardized way to package and transport applications, ensuring they work the same way regardless of where they're deployed. This solves the common problem of "it works on my machine" by creating consistent, reproducible environments.

Docker revolutionized software deployment by making applications more portable, scalable, and efficient compared to traditional virtual machines. It's become an essential tool in modern [DevOps]({{< relref "what-is-devops" >}}) practices and cloud computing.

## Beginner Information

Docker containers are much lighter than virtual machines because they share the host operating system's kernel rather than requiring a complete OS for each instance.

**Key Docker Concepts:**

- **Image**: A template or blueprint for creating containers
- **Container**: A running instance of an image
- **Dockerfile**: Instructions for building custom images
- **Registry**: Storage for Docker images (like Docker Hub)

**A Simple Dockerfile Example:**

{{< highlight dockerfile "linenos=inline">}}
# Use official Node.js runtime as base image
FROM node:18-alpine

# Set working directory inside container
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy application code
COPY . .

# Expose port 3000
EXPOSE 3000

# Command to run when container starts
CMD ["npm", "start"]
{{< /highlight >}}

**Basic Docker Commands:**

{{< highlight bash>}}
# Build an image from Dockerfile
docker build -t my-app .

# Run a container from image
docker run -p 3000:3000 my-app

# List running containers
docker ps

# Stop a container
docker stop container-name

# Remove a container
docker rm container-name
{{< /highlight >}}

**Benefits of Using Docker:**

- **Consistency**: Same environment across development, testing, and production
- **Portability**: Runs anywhere Docker is installed
- **Efficiency**: Lower resource usage than virtual machines
- **Scalability**: Easy to create multiple instances
- **Isolation**: Applications don't interfere with each other

## Intermediary Information

Docker's architecture consists of several components working together to provide containerization capabilities.

**Docker Architecture:**

- **Docker Engine**: The core runtime that manages containers
- **Docker Daemon**: Background service that handles container operations
- **Docker CLI**: Command-line interface for interacting with Docker
- **Docker Images**: Read-only templates for creating containers
- **Docker Registry**: Repository for storing and distributing images

**Multi-Stage Builds:**

{{< highlight dockerfile "linenos=inline">}}
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# Production stage
FROM node:18-alpine AS production
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
{{< /highlight >}}

**Docker Compose for Multi-Container Applications:**

{{< highlight yaml "linenos=inline">}}
version: '3.8'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    depends_on:
      - database
  
  database:
    image: postgres:13
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
{{< /highlight >}}

**Container Networking:**

- **Bridge Network**: Default network for container communication
- **Host Network**: Containers share host's network stack
- **Overlay Network**: Multi-host networking for distributed applications
- **Custom Networks**: User-defined networks for specific requirements

**Volume Management:**

- **Bind Mounts**: Direct mapping to host filesystem
- **Named Volumes**: Docker-managed persistent storage
- **tmpfs Mounts**: Temporary in-memory storage

**Security Best Practices:**

- Use non-root users inside containers
- Scan images for vulnerabilities
- Minimize image size and attack surface
- Keep base images updated
- Use secrets management for sensitive data

## Advanced Information

Enterprise Docker usage involves sophisticated orchestration, security, and management practices.

**Container Orchestration:**

While Docker can manage individual containers, production environments typically use orchestration platforms like [Kubernetes]({{< relref "what-is-kubernetes" >}}) for managing containerized applications at scale.

**Docker in CI/CD Pipelines:**

{{< highlight yaml "linenos=inline">}}
# GitHub Actions example
name: Build and Deploy
on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Build Docker image
        run: docker build -t myapp:${{ github.sha }} .
      
      - name: Run security scan
        run: docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image myapp:${{ github.sha }}
      
      - name: Push to registry
        run: |
          docker tag myapp:${{ github.sha }} registry.company.com/myapp:${{ github.sha }}
          docker push registry.company.com/myapp:${{ github.sha }}
{{< /highlight >}}

**Enterprise Features:**

- **Docker Enterprise**: Commercial platform with enhanced security and management
- **Image Scanning**: Automated vulnerability detection
- **Role-Based Access Control**: Fine-grained permissions
- **Registry Management**: Private, secure image storage
- **Compliance**: Meeting regulatory requirements

**Performance Optimization:**

- **Layer Caching**: Optimizing build times through efficient Dockerfile organization
- **Multi-Architecture Images**: Supporting different CPU architectures
- **Resource Limits**: Controlling CPU and memory usage
- **Health Checks**: Monitoring container status

**Monitoring and Logging:**

{{< highlight yaml "linenos=inline">}}
version: '3.8'
services:
  app:
    image: myapp:latest
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
{{< /highlight >}}

**Container Security:**

- **Runtime Security**: Monitoring container behavior for anomalies
- **Image Provenance**: Verifying image authenticity and integrity
- **Network Policies**: Controlling inter-container communication
- **Secrets Management**: Secure handling of sensitive configuration

**Cloud Integration:**

- **Serverless Containers**: AWS Fargate, Azure Container Instances
- **Managed Kubernetes**: EKS, GKE, AKS
- **Container Registries**: ECR, ACR, GCR
- **Service Mesh**: Istio, Linkerd for advanced networking

Docker has become fundamental to modern application development and deployment. Its ecosystem continues to evolve with innovations in security, performance, and developer experience. Understanding Docker is essential for any modern development or operations role, as it forms the foundation for cloud-native architectures and microservices deployment.

## External Links

- [Docker Documentation](https://docs.docker.com/) @ Docker
- [Docker Hub](https://hub.docker.com/) - Public container registry
- [Docker Best Practices](https://docs.docker.com/develop/best-practices/) @ Docker
