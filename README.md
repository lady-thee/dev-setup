# Microservices Local Development Stack

![Docker](https://img.shields.io/badge/Docker-✓-blue?logo=docker)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-✓-blue?logo=postgresql)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-✓-orange?logo=rabbitmq)

This Docker Compose configuration provides a complete local development environment for a microservices architecture.

## Quick Start

### Prerequisites
- Docker 20.10+
- Docker Compose 2.0+
- Unix-like system (Linux/macOS/WSL2)

### Installation
```bash
git clone https://github.com/lady-thee/dev-setup.git 
docker-compose up -d
```

## Services

| Service         | Description                      | Ports               | Credentials           |
|-----------------|----------------------------------|---------------------|-----------------------|
| API Gateway     | HTTP entry point                 | 3000                | -                     |
| Auth Service    | JWT authentication               | -                   | -                     |
| RabbitMQ        | Message broker                   | 5672, 15672 (UI)    | guest/guest           |
| PostgreSQL      | Primary database                 | 5433                | From `.env`           |
| pgAdmin         | Database management              | 5050                | From `.env`           |


## Configuration
Create `.env` file

### PostgreSQL
POSTGRES_USER=dev_user
POSTGRES_PASSWORD=dev_password
POSTGRES_DB=auth_db

### pgAdmin
PGADMIN_DEFAULT_EMAIL=admin@example.com
PGADMIN_DEFAULT_PASSWORD=admin123

### Auth Service
JWT_SECRET_KEY=your_secure_secret_here

## Start
`docker compose up --build`


## Architecture
graph TD
    Client-->|HTTP| API_Gateway
    API_Gateway-->|AMQP| RabbitMQ
    RabbitMQ-->|RPC| Auth_Service
    Auth_Service-->|SQL| PostgreSQL
    PostgreSQL<-->pgAdmin