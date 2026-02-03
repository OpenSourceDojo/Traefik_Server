# Traefik Setup using Docker Compose

This guide explains a **basic Traefik setup using Docker Compose** with a sample application. It is designed to help understand Traefik concepts in a **hands-on and exam-friendly** way.

---

## 🎯 Goal of this Setup

* Run Traefik as a reverse proxy
* Enable Traefik Dashboard
* Route traffic to a sample web application
* Understand how Traefik uses Docker labels

---

## 🧱 Architecture Overview

```
Browser
   |
   |  http://localhost
   v
Traefik (Reverse Proxy)
   |
   |  Docker Service Discovery
   v
Sample App (Whoami container)
```

---

## 📁 Files Required

```text
.
├── docker-compose.yml
```

---

## 🐳 Docker Compose Configuration

```yaml
version: "3.9"

services:
  traefik:
    image: traefik:v2.10
    container_name: traefik
    command:
      - "--api.dashboard=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entrypoints.web.address=:80"
    ports:
      - "80:80"
      - "8080:8080"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro

  whoami:
    image: traefik/whoami
    container_name: whoami
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.whoami.rule=Host(`localhost`)"
      - "traefik.http.services.whoami.loadbalancer.server.port=80"
```

---

## 🔍 Explanation (Service by Service)

### 1️⃣ Traefik Service

#### Image

```text
traefik:v2.10
```

Runs Traefik v2.x (commonly used in production).

#### Command Flags

* `api.dashboard=true` → Enables Traefik dashboard
* `providers.docker=true` → Enables Docker service discovery
* `exposedbydefault=false` → Containers must explicitly opt-in
* `entrypoints.web.address=:80` → Defines HTTP entry point

#### Ports

* `80` → Application traffic
* `8080` → Traefik dashboard

#### Volume

```text
/var/run/docker.sock
```

Allows Traefik to **watch Docker events** (container start/stop).

---

### 2️⃣ Whoami Service (Sample App)

This is a lightweight test application that returns container details.

#### Labels (Most Important Part)

* `traefik.enable=true`
  → Explicitly exposes this service to Traefik

* `traefik.http.routers.whoami.rule=Host(`localhost`)`
  → Routes requests with host `localhost` to this container

* `traefik.http.services.whoami.loadbalancer.server.port=80`
  → Internal port used by the container

Labels are how **Traefik dynamically configures routing**.

---

## ▶️ How to Run

```bash
docker compose up -d
```

---

## 🌐 Access URLs

| Purpose           | URL                                            |
| ----------------- | ---------------------------------------------- |
| Sample App        | [http://localhost](http://localhost)           |
| Traefik Dashboard | [http://localhost:8080](http://localhost:8080) |

---

## 🧠 Key Takeaways

* Traefik does **not require static config files**
* Routing is defined using **Docker labels**
* No reloads needed when services change
* Perfect fit for microservices & dynamic environments

---

## 🔎 Common Interview Notes

* Traefik auto-discovers services via Docker API
* Uses **EntryPoints → Routers → Services** flow
* Dashboard helps visualize live routing

---

## ➕ Next Enhancements (Optional)

* Add HTTPS with Let’s Encrypt
* Add path-based routing
* Add middleware (auth, rate limit)
* Deploy on Kubernetes

---

➡️ **Next file to create:**
`traefik-vs-nginx-apache.md`
