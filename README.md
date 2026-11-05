# Production-Grade AWS VPC Architecture & Automated Deployment Pipeline

An enterprise-ready cloud infrastructure and automated deployment solution engineered on Amazon Web Services (AWS). This architecture features a multi-AZ Virtual Private Cloud (VPC) with segregated public and private subnets, secure S3 gateway endpoints, Application Load Balancing, and continuous deployment automation using enterprise Linux (RHEL).

---

## 📐 Architecture Diagram

```text
+-----------------------------------------------------------------------------------+
| AWS Region                                                                        |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  | AWS S3 Bucket (Single Source of Truth: Static Assets & Web Code)            |  |
|  +-----------------------------------------------------------------------------+  |
|                                     |                                             |
|                                     v (S3 Gateway Endpoint)                       |
|  +-----------------------------------------------------------------------------+  |
|  | VPC (Virtual Private Cloud)                                                 |  |
|  |                                                                             |  |
|  |   +--------------------------+          +--------------------------+        |  |
|  |   | Availability Zone A      |          | Availability Zone B      |        |  |
|  |   |                          |          |                          |        |  |
|  |   |  +--------------------+  |          |  +--------------------+  |        |  |
|  |   |  | Public Subnet A    |  |          |  | Public Subnet B    |  |        |  |
|  |   |  | - NAT Gateway      |  |          |  | - NAT Gateway      |  |        |  |
|  |   |  +--------------------+  |          |  +--------------------+  |        |  |
|  |   |            |             |          |            |             |        |  |
|  |   |   +--------------------------------------------------------+   |        |  |
|  |   |   |            Application Load Balancer (ALB)             |   |        |  |
|  |   |   +--------------------------------------------------------+   |        |  |
|  |   |            |                                     |             |        |  |
|  |   |  +--------------------+             +--------------------+     |        |  |
|  |   |  | Private Subnet A   |             | Private Subnet B   |     |        |  |
|  |   |  | - RHEL Web Server  |             | - RHEL Web Server  |     |        |  |
|  |   |  +--------------------+             +--------------------+     |        |  |
|  |   |                          |          |                          |        |  |
|  |   +--------------------------+          +--------------------------+        |  |
|  |                                                                             |  |
|  |       [ Security Group Access Control & Auto Scaling Group Integration ]    |  |
|  +-----------------------------------------------------------------------------+  |
+-----------------------------------------------------------------------------------+
