# DevOps Winter Arc — Day 12: Docker Compose Multi-Container Stack

A production-style multi-container application architecture orchestrating a Python/Flask web API, a PostgreSQL database, and a Redis cache using Docker Compose[cite: 13]. This project implements dependency health checks, state persistence across stack lifecycles, least-privilege container security, and automatic self-healing restart policies[cite: 13, 14, 15].

---

## 1. Architecture Overview

```text
               +-------------------------------------------------------+
               |                 compose-project-network               |
               |                                                       |
               |   +-------------------+        +------------------+   |
Clients ------>|   |    Flask (web)    |------->|   Redis (:6379)  |   |
 (Host :5000)  |   |    Port :5000     |        |   Cache engine   |   |
               |   +-------------------+        +------------------+   |
               |             |                                         |
               |             v                                         |
               |   +-------------------+        +------------------+   |
               |   | PostgreSQL (:5432)|------->| Named Volume     |   |
               |   |   db service      |        | (pgdata)         |   |
               |   +-------------------+        +------------------+   |
               +-------------------------------------------------------+
