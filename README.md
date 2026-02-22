# Cloud Egress Cost Patterns
### Eliminating the NAT Gateway Double-Metering Trap

![Status](https://img.shields.io/badge/status-architectural--framework-blue)

> **Architecture Principle:** Data gravity creates financial gravity. Your baseline cost is dictated by data mass; your multipliers are dictated by routing.

---

## 📚 Canonical Architecture Reference  
This repository contains the Terraform decision matrices and cost surface models for optimizing egress routing.

**The continuously maintained architectural specification lives here:** 👉 [https://www.rack2cloud.com/physics-of-data-egress/](https://www.rack2cloud.com/physics-of-data-egress/)

---

## Problem Statement: The $180k Routing Trap

Cloud cost overruns are frequently attributed to compute scale but originate from underestimated data egress patterns. 

If your architecture uses a NAT Gateway for internal cloud service access (like AWS S3 or DynamoDB), you are paying for data transfer *twice*: once for the NAT processing fee ($0.045/GB), and once for the egress. This model maps cost as a function of data movement topology to eliminate double-metering.

---

## System Model

![Boundary Graph Model](https://www.rack2cloud.com/wp-content/uploads/2026/02/diagram-egress-topology.jpg)

**Nodes (Billable Boundaries):**
- Data Origin (VPC/Subnet)
- Inter-region traffic
- Cross-cloud transfer
- On-prem exit
- SaaS consumption

---

## Routing Decision Matrix

| Scenario | Recommendation |
| :--- | :--- |
| **High S3 Throughput (VPC)** | ✅ Use VPC Gateway Endpoint (Free) |
| **Cross-Region S3 Access** | ✅ Use VPC Interface Endpoint (PrivateLink) |
| **Public API Access only** | ⚠️ NAT Gateway is sufficient |
| **Multi-Region Peering** | ✅ Implement Hub-and-Spoke Transit Gateway |

---

## The "Physics" of the Fix
By implementing VPC Gateway Endpoints, traffic to cloud-native storage (like S3) remains on the cloud provider's global backbone. It bypasses the NAT Gateway entirely, dropping the per-GB processing fee to $0.00. 

---

## Support

**Star this repo if you are actively optimizing cloud spend.** *Architectural frameworks maintained by **[Rack2Cloud](https://www.rack2cloud.com)***.
