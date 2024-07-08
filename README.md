# Full-Stack FastAPI and React Template

## Contents

- [Project Overview](#project-overview)
- [Getting Started](#getting-started)
- [Docker Setup](#docker-setup)
- [AWS Deployment](#aws-deployment)
- [Service Details](#service-details)
- [Accessing Services](#accessing-services)
- [Development Setup](#development-setup)
- [Usage Instructions](#usage-instructions)
- [Deployment Guide](#deployment-guide)
- [Testing](#testing)

## Project Overview

This repository demonstrates setting up and running a full-stack application with a FastAPI backend and a ReactJS frontend using ChakraUI.

### Structure

- **frontend**: ReactJS application.
- **backend**: FastAPI application with PostgreSQL integration.
- **aws-server**: Terraform configuration for AWS EC2 deployment.

Each directory includes a README with detailed instructions.

## Getting Started

Follow the instructions in the respective directories:

- [Frontend README](./frontend/README.md)
- [Backend README](./backend/README.md)

## Docker Setup

The `docker-compose.yml` file is in the root directory. Dockerfiles for the frontend and backend are in their respective directories. A `.env` file stores environment variables for Docker Compose.

## AWS Deployment

Deployment uses an EC2 instance (t2.medium). Terraform configuration is available in the [aws-server](./aws-server/) folder.

## Service Details

### PostgreSQL

- **Image**: postgres:17beta1-alpine
- **Container Name**: postgresDb
- **Environment Variables**: POSTGRES_USER, POSTGRES_PASSWORD, POSTGRES_DB
- **Volumes**: postgres_data:/var/lib/postgresql/data
- **Port**: 5432
- **Network**: mynetwork

### Adminer

- **Image**: adminer:latest
- **Container Name**: postgresDbAdminer
- **Port**: 8080
- **Network**: mynetwork
- **Labels**: Configuration for Traefik routing

### Traefik

- **Image**: traefik:v2.5
- **Container Name**: traefikProxyManager
- **Ports**: 80 (HTTP), 443 (HTTPS), 8090 (Traefik dashboard)
- **Volumes**: Docker socket, Let's Encrypt certificates
- **Labels**: Configuration for Traefik dashboard and HTTPS redirection

### Backend

- **Build**: ./backend
- **Image**: backend:fastapi
- **Container Name**: backend
- **Port**: 8000
- **Network**: mynetwork
- **Labels**: Configuration for Traefik routing

### Frontend

- **Build**: ./frontend
- **Image**: frontend:react
- **Container Name**: frontend
- **Port**: 3000
- **Network**: mynetwork
- **Labels**: Configuration for Traefik routing

## Accessing Services

- **Adminer**: Accessible at `http://oshone.com.ng:8080`
- **Traefik Dashboard**: Accessible at `http://oshone.com.ng:8090`
- **Backend API**: Accessible at `https://oshone.com.ng/api`
- **Backend docs**: Accessible at `https://oshone.com.ng/docs`
- **Backend redoc**: Accessible at `https://oshone.com.ng/redoc`
- **Frontend**: Accessible at `https://oshone.com.ng`

## Development Setup

Local development access:

- **Adminer**: `http://db.localhost:8080` or `http://localhost:8080`
- **Traefik Dashboard**: `http://proxy.localhost:8090` or `http://localhost:8090`
- **Backend API**: `http://localhost/api`
- **Backend docs**: `http://localhost/docs`
- **Backend redoc**: `http://localhost/redoc`
- **Frontend**: `http://localhost`

## Usage Instructions

1. Ensure Docker and Docker Compose are installed.
2. Navigate to the project's root directory.
3. Create a `.env` file and add the necessary environment variables.
4. Run `docker-compose up -d` to start all services.
5. Access services using the URLs in the "Accessing Services" section.

## Deployment Guide

1. Ensure Docker and Docker Compose are installed on your EC2 instance.
2. Clone the repository to your EC2 instance.
3. Set up the `.env` file with necessary variables.
4. Run `docker-compose up -d` to start all services.

Monitor logs, perform regular updates, and back up the database and SSL certificates.

## Testing

Verify the deployment and functionality of:

- The main frontend application
- The backend API documentation (Swagger UI)
- The Adminer database management interface
- The Traefik dashboard