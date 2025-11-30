# n8n with Docker Compose & PostgreSQL

This repository provides a production-ready setup for deploying **[n8n](https://n8n.io/)** (Workflow Automation Tool) using Docker Compose, backed by a **PostgreSQL** database.

Using PostgreSQL instead of the default SQLite database ensures better performance, stability, and data integrity, particularly when handling a high volume of workflow executions or concurrency.

## 🚀 Features

- **n8n**: The latest version of the workflow automation tool.
- **PostgreSQL 15**: Robust database backend.
- **Auto-Recovery**: Services are configured to restart automatically on failure or system reboot.
- **Health Checks**: The n8n container waits until the database is healthy before starting to prevent connection errors.
- **Webhook Tunneling**: Configured with `--tunnel` for easy webhook testing without manual port forwarding.

## 📋 Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed on your machine or server.
- [Docker Compose](https://docs.docker.com/compose/install/) (usually included with Docker Desktop).

## 🛠 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/rifkikarimr/n8n-docker.git
cd n8n-docker
```

### 2. Configure Environment Variables
Create a .env file in the root directory. This file is required to inject configuration into the Docker containers.

Copy and paste the following into a new file named .env:
```bash
# --- Database Configuration ---
POSTGRES_USER=n8n_user
POSTGRES_PASSWORD=CHANGE_THIS_TO_STRONG_PASSWORD
POSTGRES_DB=n8n_db

# --- n8n Configuration ---
# The IP address or domain of your server (use localhost for local dev)
N8N_HOST=localhost

# Timezone for workflows
GENERIC_TIMEZONE=Asia/Jakarta

# Set to 'true' only if using SSL (HTTPS). Set 'false' for localhost/http.
N8N_SECURE_COOKIE=false

# --- Security (Basic Auth) ---
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=CHANGE_THIS_PASSWORD
```

### 3. Start the Services
Run the following command to download images and start the stack in the background:
```bash
docker compose up -d
```

## Usage
After running the start command, wait approximately 30 seconds for the application to initialize.

 - Open your web browser.

 - Navigate to http://localhost:5678 (or http://<YOUR_SERVER_IP>:5678).

 - Log in using the Basic Auth username and password defined in your .env file.

## Webhook Tunneling
This setup uses the --tunnel command. This automatically creates a secure tunnel URL (e.g., https://random-name.hooks.n8n.cloud) allowing external services to send webhooks to your local instance. You can see this URL in the n8n interface or logs.

