# DevOps Infrastructure  & Administration  Labs
Hands-on Infrastructure and administration scripts for Linux Infrastructure  services focusing on high availability ,  security hardening ,firewall and disk management .
## Project structure 
- **`nginx/`**: Nginx Reverse Proxy with HTTPS/SSL termination and upstream Load Balancing.

---

## BIND9 DNS Server (Containerized)

Production-ready BIND9 DNS infrastructure with security hardening, Access Control Lists (ACLs), Forward/Reverse zones, and custom Docker containerization.

* **Key Features:**
  * Custom ACLs restricting recursive queries to trusted internal networks.
  * Security hardening with version hiding (`version "None";`).
  * Forward Zone (`lab.internal`) and Reverse Zone (PTR) lookup support.
  * Fully dockerized for fast deployment and testing.

  **[ View Full BIND Configuration & Documentation](./bind-dns)**
