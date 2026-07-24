---
title: "Workshop Overview"
date: 2026-07-15
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# WMS Pro: AWS Cloud Infrastructure Deployment Guide

### 1. Workshop Objectives

This workshop provides a step-by-step **Hands-on Lab** guiding you through provisioning and configuring production-ready **AWS Cloud** infrastructure for the **WMS Pro (Comprehensive Warehouse & Transportation Management System)** platform:

* **Cloud Database Deployment:** Provision an **Amazon RDS PostgreSQL** relational database cluster managing orders, warehouse inventory, driver wallet balances, and tracking history.
* **Application Server Provisioning:** Configure an **Amazon EC2 (Ubuntu 24.04 LTS)** virtual server serving as the core host running the NestJS Backend API and Next.js Web App Dashboard.
* **Network Connectivity & Security:** Configure **VPC Security Groups** firewall rules allowing secure EC2-to-RDS communication over port 5432 and activating Swagger API on port 3333.

{{% notice info %}}
**WMS Pro Platform** utilizes a 3-Tier Cloud Architecture:
1. **Frontend Layer:** Web App (Next.js 15) & Mobile App (Flutter).
2. **Application Layer:** Backend API (NestJS, PM2 Process Manager, Socket.io) on Amazon EC2.
3. **Database Layer:** Amazon RDS for PostgreSQL handling ACID compliant transactions.
{{% /notice %}}

---

### 2. Workshop Roadmap (Lab Modules)

The workshop is divided into 3 hands-on modules:

* 🔹 **[Module 1: Deploy Amazon RDS PostgreSQL Database](../5.2-rds-postgresql/):** Step-by-step guide to create RDS Instance (`wms-pro-db`), select Free Tier, configure Master Credentials, and initialize `logistics` database.
* 🔹 **[Module 2: Deploy Amazon EC2 Application Server](../5.3-ec2-server/):** Step-by-step guide to launch EC2 Instance (`wms-pro-server`), assign Public IP, create SSH Key pair (`wms-server-key`), and configure Security Group inbound rules (ports 22, 80, 443, 3333).
* 🔹 **[Module 3: Connect EC2 Backend with RDS & API Activation](../5.4-connect-ec2-rds/):** Step-by-step guide to extract RDS Endpoint, open port 5432 Inbound Rule, SSH into EC2 to install Node.js 20 LTS / PM2, set up `.env`, and activate Swagger API Documentation.

---

### 3. Prerequisites

Recommended requirements before starting the lab:

1. **AWS Account:** Active AWS Account (preferably within the **AWS Free Tier** 12-month period).
2. **Tools & Software:**
   * A modern web browser (Chrome, Edge, Firefox) to access the AWS Management Console.
   * Terminal/SSH client on your computer (MobaXterm, PuTTY, VS Code Terminal, or Windows PowerShell).
3. **Fundamental Knowledge:** Basic Linux command-line usage, IP/Port networking concepts, and SQL database basics.

{{% notice tip %}}
**Cost Optimization Tip:** All steps in this workshop leverage 100% **AWS Free Tier** eligible services (750 hours of EC2 `t2.micro`/`t3.micro`, 750 hours of RDS `db.t4g.micro`, 20GB SSD storage), ensuring zero unexpected charges.
{{% /notice %}}
