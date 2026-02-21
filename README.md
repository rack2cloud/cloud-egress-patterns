# Cloud Egress Cost Patterns
### Eliminating the NAT Gateway double-metering trap.

> **Architecture Principle:** Data gravity dictates your baseline cost. Routing dictates your multipliers.

## 📚 Canonical Architecture Reference  
This repository contains the Terraform decision matrices for cost-optimized egress routing.

**The continuously maintained architectural specification lives here:** 👉 [https://www.rack2cloud.com/physics-of-data-egress/](https://www.rack2cloud.com/physics-of-data-egress/)

---

## The $180k Routing Trap
If your architecture uses a NAT Gateway for internal AWS service access (like S3 or DynamoDB), you are paying for data transfer *twice*: once for the NAT processing fee, and once for the egress.

## When to Use This Routing Model

| Scenario | Recommendation |
| :--- | :--- |
| **High S3 Throughput (VPC)** | ✅ Use VPC Gateway Endpoint (Free) |
| **Cross-Region S3 Access** | ✅ Use VPC Interface Endpoint (PrivateLink) |
| **Public API Access only** | ⚠️ NAT Gateway is sufficient |
| **Multi-Region Peering** | ✅ Implement Hub-and-Spoke Transit Gateway |

## The "Physics" of the Fix
By implementing VPC Gateway Endpoints, traffic to S3 remains on the AWS global backbone. It bypasses the NAT Gateway entirely, dropping the per-GB processing fee to $0.00. 

---
**Star this repo if you are actively optimizing cloud spend.** *Maintained by [Rack2Cloud](https://www.rack2cloud.com)*
