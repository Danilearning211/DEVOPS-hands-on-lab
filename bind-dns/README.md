Enterprise BIND9 DNS Server Setup 

An enterprise-grade, secure, and production-ready BIND9 DNS Server implementation with containerized deployment, custom ACLs, Forward/Reverse lookup zones, and security hardening.

---

## 📌 Architecture & Features

- **Security Hardening:** Version hiding (`version "None";`), restricted recursion, and strict zone transfer policies.
- **Access Control Lists (ACL):** Query limits applied exclusively to trusted subnet ranges.
- **Zone Management:** 
  - **Forward Zone:** Maps domain names to IPv4 addresses (`lab.internal`).
  - **Reverse Zone:** PTR records mapping IPs back to domain names (`10.10.10.in-addr.arpa`).
- **Containerized:** Lightweight Docker setup for fast testing and continuous deployment.

---

## 📁 Repository Structure

```text
.
├── Dockerfile              # Docker build file for BIND9
├── config/
│   ├── named.conf          # Main entry configuration
│   ├── named.conf.options  # Global options, ACLs, and Forwarders
│   ├── named.conf.local    # Zone definitions
│   └── zones/
│       ├── db.lab.internal # Forward DNS lookup zone
│       └── db.10.10.10     # Reverse DNS lookup zone (PTR)
└── README.md
```

---

## 🚀 Quick Start with Docker

### 1. Build the Docker Image
Run the following command in the root directory:

```bash
docker build -t custom-bind-dns .
```

### 2. Run the Container
Start the container on DNS standard port `53`:

```bash
docker run -d \
  --name bind9-dns-server \
  -p 53:53/tcp \
  -p 53:53/udp \
  custom-bind-dns
```

---

## 🧪 Verification & Testing

### Test Forward Lookup (A Record)
```bash
dig @127.0.0.1 web.lab.internal +short
```

### Test Reverse Lookup (PTR Record)
```bash
dig @127.0.0.1 -x 10.10.10.10 +short
```

### Validate Configuration Files
Inside the container or host (if `bind9utils` installed):
```bash
named-checkconf ./config/named.conf
named-checkzone lab.internal ./config/zones/db.lab.internal
```

---

## 🛡️ Security Highlights

1. **Recursion Control:** Prevent DNS Amplification attacks by restricting recursive queries to trusted IP addresses.
2. **Zone Transfer Rules:** `allow-transfer { none; };` is configured globally to prevent unauthorized zone dumps.
