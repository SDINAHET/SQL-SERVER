# 🐳 SQL Server Docker Setup (Monitoring Stack)

## 📌 Overview

This project adds **Microsoft SQL Server** to your existing Docker monitoring stack.

It is designed for:

* Learning SQL Server
* Testing multi-database architectures
* Integrating with backend APIs (Spring Boot, Node.js, etc.)

---

## ⚙️ Requirements

* Docker
* Docker Compose
* Minimum: **4GB RAM** (recommended)

---

## 🚀 Quick Start

### 1. Add service to `docker-compose.yml`

```yaml
services:
  sqlserver:
    image: mcr.microsoft.com/mssql/server:2022-latest
    container_name: sqlserver
    restart: always

    ports:
      - "1433:1433"

    environment:
      ACCEPT_EULA: "Y"
      SA_PASSWORD: "YourStrong!Pass123"
      MSSQL_PID: "Express"

    volumes:
      - sqlserver_data:/var/opt/mssql

    networks:
      - monitoring_shared

    mem_limit: 1g

volumes:
  sqlserver_data:

networks:
  monitoring_shared:
    external: true
```

---

### 2. Start container

```bash
docker compose up -d
```

---

### 3. Verify

```bash
docker ps
```

You should see:

```
sqlserver   Up ...   0.0.0.0:1433->1433/tcp
```

---

## 🔐 Security Notes

### ⚠️ Change default password

SQL Server requires:

* Uppercase
* Lowercase
* Number
* Special character

Example:

```
YourStrong!Pass123
```

---

### ⚠️ Production recommendation

❌ Avoid exposing port publicly:

```yaml
ports:
  - "1433:1433"
```

✔ Better:

* Use internal Docker network only
* Access via backend API

---

## 🔌 Connection

### 📍 Local / Remote access

| Field    | Value                 |
| -------- | --------------------- |
| Host     | localhost / server IP |
| Port     | 1433                  |
| User     | sa                    |
| Password | your password         |

---

### 💻 CLI access

```bash
docker exec -it sqlserver /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 'YourStrong!Pass123'
```

---

## 🧪 Basic SQL Test

```sql
SELECT name FROM sys.databases;
GO
```

---

## 📊 Integration Ideas

* Spring Boot (JDBC)
* Node.js (mssql package)
* Python (pyodbc)

---

## 🧠 Performance Tips (4GB VPS)

* Limit memory: `mem_limit: 1g`
* Avoid running too many DBs simultaneously
* Monitor usage with:

```bash
docker stats
```

---

## 📦 Useful Tools

* Azure Data Studio
* DBeaver
* SQL Server Management Studio (Windows)

---

## ⚠️ Known Limitations

* SQL Server is resource-heavy
* Not ideal with many containers on small VPS
* Requires strong password

---

## 🟢 Status

✔ Dockerized
✔ Persistent storage
✔ Network integrated
✔ Ready for development

---

## 🚀 Next Steps

* Connect backend (Spring Boot)
* Add monitoring (Prometheus exporter)
* Create database schema

---

## 📄 License

Free to use for learning and development.
