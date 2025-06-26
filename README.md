# 🐳 Docker Config:

This project brings up the following services in Docker, configured via a .env file:

- ✅ **PostgreSQL** – Database service
- ✅ **pgAdmin 4** – GUI for PostgreSQL
- ✅ **Portainer CE** – Docker management panel

## 📦 Contents

```bash
docker-config/
├── .env                          # Environment variables
├── docker-compose.postgres.yml   # PostgreSQL + pgAdmin
├── docker-compose.portainer.yml  # Portainer
└── README.md                     # This documentation file
```
## ⚙️ 1. Setup

### 📁 Step 1: Create the .env file

Add the following content to your .env file:

```bash
# PostgreSQL
POSTGRES_USER=admin
POSTGRES_PASSWORD=secret
POSTGRES_DB=mydb
POSTGRES_PORT=5432
POSTGRES_CONTAINER_NAME=postgres_db

# pgAdmin
PGADMIN_DEFAULT_EMAIL=admin@admin.com
PGADMIN_DEFAULT_PASSWORD=admin123
PGADMIN_PORT=5050
PGADMIN_CONTAINER_NAME=pgadmin

# Portainer
PORTAINER_PORT=9000
PORTAINER_CONTAINER_NAME=portainer
```

### 🚀  Step 2: Start the services

PostgreSQL + pgAdmin:
```bash
docker-compose -f docker-compose.postgres.yml --env-file .env up -d
```

Portainer:
```bash
docker-compose -f docker-compose.portainer.yml --env-file .env up -d
```

Start all services at once:
```bash
docker-compose \
  -f docker-compose.portainer.yml \
  -f docker-compose.postgres.yml \
  --env-file .env up -d
```

## 🌐 Access Information

| Service       | 	URL/Address                | Default Credentials Bilgiler                             |
|--------------|----------------------|--------------------------------------------------|
| **pgAdmin**  | [http://localhost:5050](http://localhost:5050) | **Email:** `admin@admin.com`<br>**Password:** `admin123` |
| **PostgreSQL** | `localhost:5432`     | **User:** `admin`<br>**Password:** `secret`<br>**Database:** `mydb` |
| **Portainer**| [http://localhost:9000](http://localhost:9000) | **Password to be set on first login**               |


## 🧼 Cleanup

To stop and remove all services:
```bash
docker-compose \
  -f docker-compose.portainer.yml \
  -f docker-compose.postgres.yml \
  --env-file .env down
```

To remove the volumes as well:
```bash
docker volume rm docker-config_pgdata docker-config_portainer_data
```

> **Note**: Volume names might be automatically generated differently on your system. Before removing volumes, verify them with the following command:
>
> ```bash
> docker volume ls
> ```
