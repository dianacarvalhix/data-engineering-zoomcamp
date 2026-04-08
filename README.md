# 🚕 NYC Taxi Data Ingestion Pipeline (Docker)

This project implements a simple end-to-end data ingestion pipeline using Docker, PostgreSQL, and Python.

It was developed as part of a Data Engineering workshop, with an extension to integrate the ingestion process into a Docker Compose workflow.

---

## 🧠 Overview

The pipeline:

1. Downloads NYC taxi trip data (CSV)
2. Processes the data using Python (pandas)
3. Loads the data into a PostgreSQL database
4. Uses Docker Compose to orchestrate all services

---

## 🧱 Architecture

The system is composed of three services:

* **PostgreSQL** → stores the data
* **pgAdmin** → database UI
* **Ingestion service** → Python script that loads data into PostgreSQL

All services run inside Docker containers and communicate via Docker networking.

---

## 📁 Project Structure

```
pipeline/
│
├── ingest_data.py        # Main ingestion script
├── docker-compose.yaml   # Orchestrates all services
├── Dockerfile            # Builds ingestion container
├── pyproject.toml        # Python dependencies
├── uv.lock               # Locked dependency versions
│
├── main.py               # (not used in final pipeline)
├── notebook.ipynb        # (exploration only)
├── pipeline.py           # (not used)
```

---

## ⚙️ How It Works

### 1. Start all services

```bash
docker compose up --build
```

This will:

* Start PostgreSQL database
* Start pgAdmin (UI available at http://localhost:8085)
* Build and run the ingestion container

---

### 2. Ingestion process

The ingestion service runs:

```
ingest_data.py
```

It:

* Downloads taxi data from the NYC dataset
* Reads data in chunks
* Inserts data into PostgreSQL

---

## 🔗 Database Connection

### From local machine:

```
host: localhost
port: 5432
```

### From inside Docker:

```
host: pgdatabase
port: 5432
```

---

## 💾 Data Persistence

Docker volumes are used to persist data:

* `ny_taxi_postgres_data` → PostgreSQL data
* `pgadmin_data` → pgAdmin configuration

This ensures data is not lost when containers are stopped.

---

## 🚀 Key Learnings

* Running pipelines locally vs inside containers
* Docker networking (localhost vs container names)
* Data persistence using Docker volumes
* Building reproducible environments with Docker

---

## 🛠️ Tech Stack

* Python (pandas, SQLAlchemy)
* PostgreSQL
* Docker & Docker Compose

---

## 📌 Notes

* The ingestion logic is implemented in `ingest_data.py`
* Supporting files like notebooks and older pipeline scripts were used for exploration but are not part of the final pipeline

---

## 🙌 Acknowledgment

This project was developed as part of a Data Engineering workshop by DataTalksClub, with additional improvements to integrate the ingestion step into the Docker Compose workflow.
