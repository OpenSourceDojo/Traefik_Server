# Traefik – Personal Notes

## 📌 What is Traefik?

Traefik (pronounced *traffic*) is a **modern reverse proxy and load balancer** designed for **cloud-native and microservices architectures**. It automatically discovers services and configures routing dynamically, making it ideal for Docker, Kubernetes, and other dynamic environments.

Unlike traditional proxies, Traefik reacts in **real time** to infrastructure changes and requires minimal manual configuration.

---

## ✨ Key Features

* Dynamic service discovery
* Native Docker & Kubernetes integration
* Automatic HTTPS with Let’s Encrypt
* Layer 7 routing (host, path, headers)
* Built-in dashboard & metrics
* Load balancing out of the box

---

## 🧱 Core Concepts (High Level)

* **EntryPoints** – Where traffic enters (HTTP, HTTPS)
* **Routers** – Rules that match incoming requests
* **Services** – Backend applications
* **Middlewares** – Modify requests (auth, rate-limit, redirects)

---

## 📂 Repository Structure

```text
traefik-notes/
│
├── README.md
├── setup-docker-compose.md
├── traefik-vs-nginx-apache.md
├── traefik-vs-kong.md
├── traefik-vs-istio.md
├── real-world-use-cases.md
```

---

## 🐳 Setup Guide

➡️ **Basic Traefik setup using Docker Compose**
📄 [setup-docker-compose.md](./setup-docker-compose.md)

Includes:

* Traefik + sample app
* Dashboard enablement
* HTTP routing example

---

## 🔄 Traefik vs Traditional Web Servers

➡️ **Comparison with Nginx & Apache**
📄 [traefik-vs-nginx-apache.md](./traefik-vs-nginx-apache.md)

Covers:

* Static vs dynamic configuration
* Reload requirements
* Cloud-native readiness

---

## 🚪 Traefik vs API Gateway

➡️ **Traefik vs Kong**
📄 [traefik-vs-kong.md](./traefik-vs-kong.md)

Focus:

* Reverse proxy vs API gateway
* Authentication & plugins
* Typical usage scenarios

---

## 🌐 Service Mesh Comparison

➡️ **Traefik vs Istio**
📄 [traefik-vs-istio.md](./traefik-vs-istio.md)

Explains:

* Ingress vs Service Mesh
* Sidecar model
* Complexity vs control

---

## 🏭 Real-World Use Cases

➡️ **Where Traefik is used in practice**
📄 [real-world-use-cases.md](./real-world-use-cases.md)

Examples:

* Microservices routing
* Kubernetes ingress controller
* SaaS platforms
* Internal developer platforms

---

## 🎯 When to Use Traefik

Use Traefik if you need:

* Fast-changing services
* Minimal configuration overhead
* Docker / Kubernetes-first networking
* Automatic HTTPS

---