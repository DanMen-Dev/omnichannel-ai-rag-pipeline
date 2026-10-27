# Omnichannel AI Agent & High-Velocity RAG Architecture for Industrial E-Commerce

A production-ready, self-hosted AI Automation ecosystem deployed on a Linux VPS. This system orchestrates real-time customer support and complex multi-currency pricing matrices for a heavy industrial product catalog. It handles multi-parameter inputs (weight constraints, spatial/logistics routing, and promotional financing logic) with sub-second response times, reducing SaaS operational overhead by **93.5%**.

## 🚀 System Architecture Overview

The platform is designed to decouple reasoning from data storage, ensuring 100% mathematical accuracy on dynamic cost structures under macroeconomic volatility (e.g., currency gap mitigation).

## 🛠️ Core Technical Stack

- **Orchestration & DevOps:** n8n Core (Self-hosted via Docker Compose), Linux VPS (Hetzner), Nginx Proxy Manager, Cloudflare DNS.
- **AI & Data Semantics:** OpenAI API (`gpt-4o-mini`), OpenAI Embeddings (`text-embedding-3-small`), Pinecone Vector Database (RAG Architecture).
- **Data Pipeline:** Advanced Data Ingestion Pipelines using localized Python scripts and structured CSV/JSON matrices mapped through Linux secure copying (`scp`).

## ⚡ Key Engineering Achievements

### 1. Multi-Namespace Vector Partitioning (RAG)
Avoided vector collision and context dilution by implementing isolated **Pinecone Namespaces** inside a single index (`1536` dimensions, Cosine metric). 
- `products`: Houses complex metal-mechanical product specifications, raw material dimensions, and multi-tier pricing (FinTech/Cashea financing vs Cash/USDT).
- `delivery`: Stores geolocated spatial data, municipal routing, and discrete step-functions for logistics pricing based on payload mass boundaries ($M \le 800\text{ kg}$ vs $M > 800\text{ kg}$).

### 2. Multi-Parameter Deterministic Reasoning
Configured the AI Agent prompt engineering to act as an execution tool router. The agent calculates dynamic pricing matrices in real time, executes context-aware multiplication for bulk orders, and monitors weight triggers to gracefully enforce fallback loops (Human-in-the-Loop) when payload mass constraints require manual logistics intervention.

### 3. Symmetrical Latency Optimization
Migrated the entire ecosystem from asynchronous automation models (Make/ManyChat) to a custom synchronous webhook pipeline in n8n. This migration eliminated redundant cloud middleware database polls, dropping user request latency from a critical **120 seconds down to a < 3-second response time**.

## 📦 How to Replicate the Deployment

### Prerequisites
- Docker & Docker Compose installed on a Linux Ubuntu VPS.
- A Cloudflare account managing your domain DNS.
- Active API keys for OpenAI and Pinecone.

### 1. Docker Compose Infrastructure (`docker-compose.yml`)
n8n runs as a single container with a persistent volume. Public traffic reaches it only through HTTPS (Cloudflare DNS → Nginx Proxy Manager → n8n webhook).

```yaml
version: '3.8'

services:
  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    restart: always
    ports:
      - "5678:5678"
    environment:
      - N8N_HOST=SUBDOMAIN.{DOMAIN}
      - N8N_PORT=5678
      - N8N_PROTOCOL=https
      - NODE_ENV=production
      - WEBHOOK_URL=https://SUBDOMAIN.{DOMAIN}/
    volumes:
      - n8n_data:/home/node/.n8n

volumes:
  n8n_data:
```

Start the stack:
```bash
docker compose up -d
```

### 2. Data Ingestion Pipeline
To refresh the dynamic vector space without downtime, data is prepared locally and pushed to the German VPS via secure copying protocols:
```bash
cd ~/path_to_catalog/
scp dynamic_catalog.csv root@your_vps_ip:~/production_pipeline/
```
The ingestion workflow in n8n consumes the file, maps columns strictly through an `Edit Fields` schema, and flushes/re-populates the vector index coordinates in batches of `50` to maintain network thread stability.

## 🤝 Connect With Me
Driven by bridging the gap between heavy industrial engineering and core software architectures. Open to global remote opportunities in Python Backend Development, FinTech, and Data Engineering for industrial applications.
