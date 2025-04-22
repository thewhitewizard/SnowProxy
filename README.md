# ❄️ SnowProxy

**SnowProxy** is a lightweight, containerized HAProxy relay for Avalanche RPC traffic, supporting both HTTP and WebSocket connections.  
It provides Prometheus-compatible metrics, secure SSL termination, and simple horizontal scaling with round-robin load balancing.

---

## 🔧 Features

- 🌐 Supports both HTTP and WebSocket traffic
- 🔒 TLS via `mkcert` (local self-signed certs)
- 📊 Exposes Prometheus metrics via `haproxy-exporter`
- ♻️ Automatic retries and connection timeouts
- 🧊 Minimal and production-ready setup

---

## 🚀 Getting Started

### 1. Clone the repo

``` bash
git clone https://github.com/yourusername/snowproxy.git
cd snowproxy
```

### 2. Generate TLS Certificates (using mkcert)
Install mkcert and run:

``` bash
mkcert -install
mkcert localhost
cat localhost.pem localhost-key.pem > ./certs/localhost-comb.pem
```
🔐 The certs directory is .gitignored – you won't commit private keys by accident.


### 3. Docker Compose Setup
``` bash
docker-compose up -d
```
* Avalanche RPC (HTTPS & WebSocket): https://localhost:8545
* HAProxy Stats Page: http://localhost:8404/stats
* Prometheus Metrics: http://localhost:9101/metrics

### 4. 🧪 Testing
Use curl or Postman to test RPC:
``` bash
curl -k https://localhost:8545/ext/bc/C/rpc -X POST \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"eth_chainId","params":[]}'
```

### 5. 📊 Monitoring
Prometheus-compatible metrics are exposed on port 9101, and HAProxy stats UI is available at:

``` bash
http://localhost:8404/stats
```
No authentication is configured for the stats page (for local/dev use only).


## 📁 Project Structure
``` bash
├── docker-compose.yml
├── haproxy.cfg
├── certs/                  # Not committed (add your own certs with mkcert)
│   └── localhost-comb.pem  # Combined cert + key for HAProxy SSL
└── README.md
```

## 📄 License
MIT — feel free to use, remix, and contribute!


## 🙌 Credits
* HAProxy
* Avalanche Network
* mkcert
* Prometheus HAProxy Exporter