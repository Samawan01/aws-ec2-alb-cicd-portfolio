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


---

## 📸 Deployment & Architecture Verification

### 1. Live Application Output (ALB DNS)
Web application running live over the AWS Application Load Balancer DNS endpoint across multi-AZ backend compute nodes.

![Live Web Application Render](./images/1-webserver-live.png)

### 2. Multi-AZ VPC Resource Map
AWS Console resource map detailing the isolated `project-testing-vpc` network layout, split across public/private subnets, custom route tables, Internet Gateway, and NAT Gateways.

![AWS VPC Resource Map](./images/2-aws-vpc-architecture.png)

### 3. Application Load Balancer (ALB) Details
Active internet-facing ALB listener setup routing incoming HTTP port 80 traffic down to registered RHEL target instances.

![AWS Application Load Balancer Configuration](./images/3-aws-alb-configuration.png)

### 4. S3 Source Bucket Storage
AWS S3 bucket deployment storing static application assets (`index.html`) used by automated shell scripts for backend code pulls.

![AWS S3 Buckets Overview](./images/4-aws-s3-buckets.png)
