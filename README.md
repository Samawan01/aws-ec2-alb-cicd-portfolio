# AWS Cloud Infrastructure & CI/CD Automated Deployment Pipeline

A production-grade web hosting and automated deployment architecture built on Amazon Web Services (AWS), demonstrating hands-on cloud infrastructure, Linux systems administration, and automated CI/CD workflows.

## 🏗️ Architecture & Tech Stack
* **Storage (Single Source of Truth):** AWS S3 bucket storing static web assets (`index.html`).
* **Compute & Web Server:** AWS EC2 Red Hat Enterprise Linux (RHEL) instance running a Python HTTP server.
* **CI/CD Automation:** Custom Bash deployment script (`deploy.sh`) that syncs assets from S3, manages local processes, and restarts services.
* **Networking & Security:** Custom VPC routing, security groups, public/private subnet segmentation, and SSH access control via `.pem` keys.

## 🔄 Automated Deployment Workflow (`deploy.sh`)
1. Pulls the latest version of static web assets directly from the S3 bucket.
2. Safely terminates old background server processes using active TCP port mapping.
3. Automatically spins up the web server instance in the background with persistent logging (`server.log`).
