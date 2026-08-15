# Assignment 6 — Capstone Assignment — Deploy Book Review App (Three-Tier Architecture) on AWS

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

This is the most important assignment of the course. You will deploy the Book Review App in a fully production-style three-tier architecture on AWS: a Next.js Web Tier behind Nginx and a public ALB, a private Node.js/Express App Tier behind an internal ALB, and a private Multi-AZ MySQL RDS database with a read replica. You are expected to design, deploy, isolate, debug, and document the result independently.

---

# Task 1 — Architecture Diagram

## Goal

Create an architecture diagram showing the custom VPC (10.0.0.0/16), the six subnets across two Availability Zones (two public Web Tier, two private App Tier, two private Database Tier), the public ALB, Web Tier EC2/Nginx, internal ALB, private App Tier EC2, private Multi-AZ RDS with its read replica, and the permitted traffic flow.

### Evidence

#### Diagram image or link

![DIAGRAM](./screenshots/AS6T1SS1.png)

---

# Task 2 — AWS Region & Services Used

## Goal

Record the AWS Region used and list every AWS service used across networking, compute, load balancing, security, and the database.

### Notes

**Region:**

eu-north-1

---

**Services:**

Networking: Amazon VPC, subnets (six across two Availability Zones), Internet Gateway, NAT Gateway, route tables, Elastic IP (attached to the NAT Gateway only), Security Groups.

Compute: Amazon EC2 (two t3.micro instances running Ubuntu 24.04 LTS), EC2 key pairs.

Load balancing: Elastic Load Balancing, specifically two Application Load Balancers (one internet-facing, one internal) with their target groups and listeners.

Database: Amazon RDS for MySQL with Multi-AZ enabled, a read replica, and a DB subnet group spanning both private database subnets.

Supporting services: AWS Systems Manager Parameter Store (to resolve the current Ubuntu AMI), AWS Identity and Access Management, AWS CLI v2.

On the instances: Nginx as reverse proxy, Node.js 20, Next.js 15 for the web tier, Express with Sequelize for the app tier, and systemd to keep both services running.

---

# Task 3 — Public Entry Point

## Goal

Confirm the Book Review App loads through the public ALB DNS name.

### Evidence

#### Public ALB DNS

Paste your public ALB DNS name here:

http://book-review-web-alb-850427566.eu-north-1.elb.amazonaws.com/

---

# Task 4 — Evidence Screenshots

## Goal

Capture visual proof of every tier and load balancer.

### Evidence

#### Web EC2

![WEB](./screenshots/AS6T4SS1.png)

---

#### App EC2

![APP](./screenshots/AS6T4SS2.png)

---

#### Public ALB

![PALB](./screenshots/AS6T4SS3.png)

---

#### Internal ALB

![IALB](./screenshots/AS6T4SS4.png)

---

#### RDS + Replica

![RDS](./screenshots/AS6T4SS5.png)

---

#### App UI proof

![RDS](./screenshots/AS6T4SS6.png)

---

# Task 5 — Summary

## Goal

Summarize what worked in the final deployment, the issues encountered and how each was fixed, and the tools or sources used to research and debug.

### Notes

**What worked:**

The three-tier Book Review application was successfully deployed and made accessible through the internet-facing Web ALB. The Next.js frontend and Node.js/Express backend were both running on separate EC2 instances and managed by PM2. The backend successfully connected to the MySQL RDS database, and the complete application flow, including user registration, was working successfully.

---

**Issues + fixes:**

We troubleshot ALB connectivity, Nginx configuration errors, incorrect HTTP/HTTPS access, PM2-managed processes and port conflicts, duplicate /api/api paths, incorrect localhost:3001 API routing, RDS database access issues, and CORS configuration errors. We used target health checks, logs, browser Developer Tools, and application configuration to identify and fix each issue.

---

**Tools/sources used:**

AWS EC2, Application Load Balancers, Target Groups, Security Groups, RDS MySQL, Nginx, Next.js, Node.js, Express, PM2, MySQL, Linux commands, browser Developer Tools, and application/server logs.

---

# LinkedIn Post (Required)

## Goal

Publish a LinkedIn post sharing the capstone deployment, including the public ALB DNS (or a redacted screenshot), three to five lines on what you built and why it is production-style, and one proof screenshot.

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/bharadwaja-kachiraju-78a45598_beyond-high-availability-building-a-three-tier-share-7494066090776354817-iDAg/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABS2KxoBOPNTBIxog_qhN1vz4HLYmnjgQPY

---

#### Screenshot of LinkedIn post

![LINKEDIN](./screenshots/AS6_LINKEDIN.png)

---

# Submission Instructions

- Add all required screenshots and links in your submission
- Do not expose passwords, RDS credentials, connection strings, private keys, or account IDs

---

# Completion Checklist

- [ ] Task 1: Architecture diagram completed
- [ ] Task 2: AWS Region and services documented
- [ ] Task 3: Public ALB DNS confirmed working
- [ ] Task 4: All six evidence screenshots captured (Web Tier, App Tier, both ALBs, RDS + replica, app UI)
- [ ] Task 5: Deployment summary completed (what worked, issues/fixes, tools/sources)
- [ ] LinkedIn post published and URL submitted
- [ ] App Tier and Database Tier confirmed not publicly accessible
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*