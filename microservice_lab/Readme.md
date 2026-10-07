# Containerized Microservice Application

## 1. Experiment Overview

This experiment demonstrates the development, deployment, and performance analysis of a containerized microservice application under varying workloads.

The application consists of three independent microservices. Each microservice provides a REST API and is independently containerized using Docker. Docker Compose is used to deploy the complete application and establish communication between the services through a common Docker network.

## 2. Aim

To develop a microservice-based application containing three independent services, containerize and deploy the services using Docker, establish inter-service communication, generate varying workloads, monitor resource utilization, and analyze application performance.

## 3. Application Architecture

```text
                         CLIENT
                            |
                            v
                   +----------------+
                   |  ORDER SERVICE |
                   |    Port 8003   |
                   +--------+-------+
                            |
                     Docker Network
                       /          \
                      /            \
                     v              v
            +---------------+   +--------------------+
            | USER SERVICE  |   | RESTAURANT SERVICE |
            |   Port 8001   |   |     Port 8002      |
            +---------------+   +--------------------+



