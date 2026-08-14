# Assignment 5 — Deploy a Highly Available Two-Tier Application on AWS (VPC + ALB + ASG + Multi-AZ RDS)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will design and deploy a highly available two-tier web application on AWS: highly available networking across two Availability Zones, an Application Load Balancer, an Auto Scaling Group for the web tier, and a private Multi-AZ RDS database. You must prove high availability with real failure tests.

---

# Task 1 — Create HA Networking (VPC + 4 Subnets + IGW + NAT + Route Tables)

## Goal

Build a VPC (10.0.0.0/16) with two public and two private subnets across two Availability Zones, an Internet Gateway, a NAT Gateway, and the matching public/private route tables.

### Evidence

#### Screenshot 1 — VPC details showing CIDR 10.0.0.0/16

![VPC](./screenshots/AS5T1SS1.png)

---

#### Screenshot 2 — Subnets list showing four subnets and their Availability Zones

![SUBNET](./screenshots/AS5T1SS2.png)

---

#### Screenshot 3 — Public route table showing the Internet Gateway route and both public-subnet associations

![PUBLICKRT](./screenshots/AS5T1SS3.png)

---

#### Screenshot 4 — Private route table showing the NAT Gateway route and both private-subnet associations

![PRIVATERT](./screenshots/AS5T1SS4.png)

---

#### Screenshot 5 — NAT Gateway status showing Available and the Elastic IP

![NAT](./screenshots/AS5T1SS5.png)

---

# Task 2 — Create Security Groups (ALB, EC2, RDS) with Least Privilege

## Goal

Create `ha-alb-sg` (HTTP public), `ha-web-sg` (HTTP only from `ha-alb-sg`, SSH from your IP), and `ha-db-sg` (database port only from `ha-web-sg`).

### Evidence

#### Screenshot 6 — ALB Security Group inbound rules

![ALB](./screenshots/AS5T2SS6.png)

---

#### Screenshot 7 — EC2 Security Group inbound rules showing the ALB Security Group reference and SSH from your IP

![EC2](./screenshots/AS5T2SS7.png)

---

#### Screenshot 8 — RDS Security Group inbound rule showing the database port allowed only from the EC2 Security Group

![RDS](./screenshots/AS5T2SS8.png)

---

# Task 3 — Deploy Database Tier (RDS Multi-AZ in Private Subnets)

## Goal

Launch a private, Multi-AZ RDS database (MySQL or PostgreSQL) using the private DB Subnet Group and `ha-db-sg`.

### Evidence

#### Screenshot 9 — RDS summary showing Multi-AZ = Yes and Publicly accessible = No

![RDS](./screenshots/AS5T3SS9.png)
![RDS](./screenshots/AS5T3SS9_1.png)

---

#### Screenshot 10 — RDS connectivity section showing the DB Subnet Group and Security Group

![RDS](./screenshots/AS5T3SS10.png)

---

# Task 4 — Build a Launch Template (User Data Installs App + Connects to DB)

## Goal

Create a Launch Template whose user data installs the web-server runtime, deploys the application, configures the database connection, and starts the required services.

### Evidence

#### Screenshot 11 — Launch Template details showing that user data exists, including a visible snippet

![RDS](./screenshots/AS5T4SS11.png)

---

#### Screenshot 12 — A running instance created from the template showing that the application responds on port 80 through a local test or browser using its public IP

![BROWSER](./screenshots/AS5T4SS12.png)

---

# Task 5 — Create an Application Load Balancer (ALB) Across 2 Public Subnets

## Goal

Create an internet-facing ALB across both public subnets with an HTTP listener and a healthy instance target group.

### Evidence

#### Screenshot 13 — ALB details showing two public subnets in two Availability Zones

![ALB](./screenshots/AS5T5SS13.png)

---

#### Screenshot 14 — Target group showing at least one healthy target

![TG](./screenshots/AS5T5SS14.png)

---

# Task 6 — Create Auto Scaling Group (ASG) in 2 Public Subnets

## Goal

Create an Auto Scaling Group from the Launch Template across both public subnets, with desired capacity 2, minimum 2, and maximum 4, registered to the ALB target group.

### Evidence

#### Screenshot 15 — Auto Scaling Group showing desired, minimum, and maximum capacity and the selected subnet Availability Zones

![ALB](./screenshots/AS5T6SS15.png)

---

#### Screenshot 16 — EC2 instances list showing two running instances in different Availability Zones

![ALB](./screenshots/AS5T6SS16.png)

---

# Task 7 — Configure App to Use RDS + Validate Read/Write

## Goal

Confirm the application communicates with the RDS database through the ALB DNS name with at least one read and one write operation.

### Evidence

#### Screenshot 17 — Browser showing the application loaded through the ALB DNS name with the URL visible

![ALB](./screenshots/AS5T7SS17.png)

---

#### Screenshot 18 — Proof of a database write through a UI message or database query output

![ALB](./screenshots/AS5T7SS18.png)

---

# Task 8 — High Availability Tests (Must Do Both)

## Goal

Test A: terminate one web instance and confirm the Auto Scaling Group replaces it automatically without interrupting the ALB.

Test B: simulate an Availability Zone impact (stop, detach, or reduce desired capacity in one AZ) and confirm the application stays available.

### Evidence

#### Screenshot 19 — EC2 showing the terminated instance and the newly launched instance; timestamps are helpful

![ALB](./screenshots/AS5T8SS19_1.png)
![ALB](./screenshots/AS5T8SS19_2.png)

---

#### Screenshot 20 — Target group showing healthy targets after replacement

![ALB](./screenshots/AS5T8SS20.png)

---

#### Screenshot 21 — Evidence that an instance was removed, detached, placed in Standby, or stopped in one Availability Zone

![ALB](./screenshots/AS5T8SS21.png)

---

#### Screenshot 22 — Browser showing that the ALB DNS endpoint still works during the change

![ALB](./screenshots/AS5T8SS22.png)

---

# Task 9 — Architecture and Test-Results Summary

## Goal

Summarize the VPC/subnet layout, the ALB and Auto Scaling Group setup, the private Multi-AZ RDS setup, and the results of both high-availability tests.

### Evidence

#### Screenshot 23 — A simple architecture diagram, which may be hand-drawn, or an AWS console overview showing the components

![ALB](./screenshots/AS5T9SS23.png)

---

### Notes

Summarize the VPC and subnets across the two Availability Zones.

A VPC (vpc-02956991cabd04939) was configured in the AWS eu-north-1 Region with subnets distributed across two Availability Zones: eu-north-1a and eu-north-1b. The web application infrastructure was deployed across both AZs to provide high availability and avoid a single point of failure.

Summarize the ALB and Auto Scaling Group setup.

An internet-facing Application Load Balancer (ha-alb) was configured with an HTTP listener on port 80 and forwards traffic to the target group ha-web-tg. The Auto Scaling Group deploys WordPress EC2 instances across the two Availability Zones and registers them with the target group. The ALB continuously performs health checks and routes traffic only to healthy instances, while the Auto Scaling Group helps maintain the required number of instances.

Summarize the private Multi-AZ RDS setup.

A private Amazon RDS MySQL database was configured for the WordPress application using a Multi-AZ setup. The database is not directly exposed to the internet and is accessed only by the application instances on MySQL port 3306. Multi-AZ deployment provides database high availability by maintaining a standby instance in another Availability Zone for failover.

Summarize the results of both high-availability tests.

Both high-availability tests demonstrated that the architecture can tolerate infrastructure failures. When an application instance became unavailable, the Auto Scaling Group and ALB health checks ensured that unhealthy instances were removed from service and traffic could continue to be served by healthy instances. The Multi-AZ design also provides resilience across Availability Zones, reducing the impact of an AZ-level failure and helping maintain application availability.

---

# LinkedIn Post (Required)

## Goal

Publish a LinkedIn post about the high-availability build, including the ALB URL (or a redacted screenshot), three to five lines on what you built and how you tested high availability, and one proof screenshot.

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/bharadwaja-kachiraju-78a45598_devops-micro-internship-week-06-aws-cloud-share-7493982308044214272-ID2u/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABS2KxoBOPNTBIxog_qhN1vz4HLYmnjgQPY

---

#### Screenshot of LinkedIn post

![ALB](./screenshots/AWS_Linkedin.png)

---

# Submission Instructions

- Add all required screenshots in your submission
- Do not expose passwords, connection strings, private keys, or account IDs

---

# Completion Checklist

- [ ] Task 1: VPC, four subnets, IGW, NAT Gateway, and route tables created (Screenshots 1–5)
- [ ] Task 2: Least-privilege ALB, EC2, and RDS security groups created (Screenshots 6–8)
- [ ] Task 3: Private Multi-AZ RDS created (Screenshots 9–10)
- [ ] Task 4: Self-configuring Launch Template created and tested (Screenshots 11–12)
- [ ] Task 5: ALB created across both public subnets (Screenshots 13–14)
- [ ] Task 6: Auto Scaling Group running two instances across two AZs (Screenshots 15–16)
- [ ] Task 7: Application verified through the ALB with a database read and write (Screenshots 17–18)
- [ ] Task 8: Both high-availability tests completed (Screenshots 19–22)
- [ ] Task 9: Architecture and test-results summary completed (Screenshot 23 & Notes)
- [ ] LinkedIn post published and URL submitted
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