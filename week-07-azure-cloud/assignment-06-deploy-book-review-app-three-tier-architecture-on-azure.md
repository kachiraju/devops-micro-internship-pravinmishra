# Assignment 6 — Capstone: Deploy Book Review App (Three-Tier Architecture) on Azure

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

This is the most important assignment of the course. You will deploy the Book Review App in a production-ready, best-practice-compliant three-tier architecture on Azure: separated presentation, application, and database tiers, least-privilege network access, a controlled public entry point, protected secrets, and availability/monitoring evidence.

---

# Task 1 — Design the Azure Three-Tier Architecture

## Goal

Create an architecture diagram and implementation plan identifying the presentation, application, and database components, the chosen Azure services, the public entry point, and the internal traffic paths.

### Evidence

#### Screenshot 1 — Architecture diagram showing the public entry point, three tiers, network boundaries, and traffic flow

![Architecture](./screenshots/AS6T1SS1.png)

---

#### Screenshot 2 — Written architecture assumptions and selected Azure services

![SERVICES](./screenshots/AS6T1SS2.png)

---

# Task 2 — Create the Azure Network Foundation

## Goal

Create a dedicated Resource Group and VNet with separate subnets for the web, application, and database tiers, keeping the application and database tiers without direct public access.

### Evidence

#### Screenshot 3 — Resource Group overview showing the assignment resources

![RG](./screenshots/AS6T2SS3.png).

---

#### Screenshot 4 — VNet overview showing the address space and all required subnets

![VNET](./screenshots/AS6T2SS4.png)

---

#### Screenshot 5 — Route-table or Private DNS evidence where applicable

![DNS](./screenshots/AS6T2SS5.png)

---

# Task 3 — Configure Security and Secret Management

## Goal

Apply least-privilege NSG rules so traffic flows Internet → public entry point → web tier → application tier → database tier, and store credentials in Azure Key Vault or another approved secure mechanism.

### Evidence

#### Screenshot 6 — NSG rules proving least-privilege access between the tiers

![NSG](./screenshots/AS6T3SS6_1.png)
![NSG](./screenshots/AS6T3SS6_2.png)
![NSG](./screenshots/AS6T3SS6_3.png)

---

#### Screenshot 7 — Key Vault or approved secret-management configuration (without displaying secret values)

![KV](./screenshots/AS6T3SS7.png)

---

# Task 4 — Deploy the Presentation (Web) Tier

## Goal

Deploy the Book Review App presentation layer on the approved web-tier compute service, configured to route requests to the internal application-tier endpoint, and not directly exposed except through the public entry service.

### Evidence

#### Screenshot 8 — Web-tier compute overview showing subnet and availability configuration

![WEBVM](./screenshots/AS6T4SS8.png)

---

#### Screenshot 9 — Terminal or service output proving the presentation layer is running

![FRONTEND](./screenshots/AS6T4SS9.png)
![FRONTEND](./screenshots/AS6T4SS9_1.png)
---

# Task 5 — Deploy the Business (Application) Tier

## Goal

Deploy the Book Review App backend privately in the application subnet, configured to use the private database endpoint and secured environment values, reachable only through its internal endpoint.

### Evidence

#### Screenshot 10 — Application-tier compute overview showing private subnet placement

![BACKEND](./screenshots/AS6T5SS10.png).

---

#### Screenshot 11 — Backend process, service, or listening-port evidence

![BACKEND](./screenshots/AS6T5SS11.png).

---

#### Screenshot 12 — Internal health-check or API response (without exposing secrets)

![BACKEND](./screenshots/AS6T5SS12.png).

---

# Task 6 — Deploy the Managed Database Tier

## Goal

Create a private Azure managed database (public access disabled), with availability/backup/retention settings, the Book Review App schema imported, and access restricted to the application tier only.

### Evidence

#### Screenshot 13 — Database overview showing private connectivity and public access disabled

![DB](./screenshots/AS6T6SS13.png).

---

#### Screenshot 14 — Availability, backup, and retention configuration


![DB](./screenshots/AS6T6SS14_1.png).
![DB](./screenshots/AS6T6SS14_2.png).

---

#### Screenshot 15 — Successful schema or connectivity verification (without exposing credentials)

![DB](./screenshots/AS6T6SS15.png).

---

# Task 7 — Configure Traffic Management, Availability, and Monitoring

## Goal

Configure the approved public entry service with health probes and backend pools, internal routing for the application tier where required, and enable Azure Monitor/diagnostics/logs/alerts for the key resources.

### Evidence

#### Screenshot 16 — Public entry service showing listener, frontend endpoint, and healthy web targets

![MGMT](./screenshots/AS6T7SS16.png).

---

#### Screenshot 17 — Internal application-tier load-balancing or routing configuration where applicable

![MGMT](./screenshots/AS6T7SS17.png).

---

#### Screenshot 18 — Azure Monitor, diagnostic settings, logs, metrics, or alert evidence

![MGMT](./screenshots/AS6T7SS18.png).

---

# Task 8 — Validate the Production-Style Deployment

## Goal

Confirm the Book Review App works end to end through the public endpoint, with at least one database read and one write, confirm private tiers are not internet-reachable, and complete a safe availability test.

### Evidence

#### Screenshot 19 — Browser showing the Book Review App through the public endpoint

![E2E](./screenshots/AS6T8SS19.png).

---

#### Screenshot 20 — Proof of successful database-backed read and write operations

![E2E](./screenshots/AS6T8SS20.png).

---

#### Screenshot 21 — Evidence that private tiers are not publicly accessible

![E2E](./screenshots/AS6T8SS21.png).

---

#### Screenshot 22 — Availability-test and healthy-target evidence

![E2E](./screenshots/AS6T8SS22.png).

---

#### Public Endpoint

Paste your public endpoint URL here:

http://172.198.228.2/

---

### Notes

Summarize what worked, issues encountered and how they were fixed, and the availability/security/secrets/monitoring/backup choices made.

The Book Review application was successfully deployed on Azure using a secure three-tier architecture. The Web VM hosts Next.js and Nginx, the Application VM runs the Node.js/Express backend in the private application subnet, and Azure Database for MySQL Flexible Server is deployed using private networking. Azure Application Gateway provides the public entry point, while private routing is used between the Web and Application tiers. The application was successfully tested end-to-end, including user registration and database connectivity.

During the deployment, issues such as Public IP quota, Nginx configuration, frontend /api/api routing, Next.js build permissions, duplicate PM2 processes, and CORS failures were encountered and resolved. Availability was addressed through Application Gateway health probes, backup and retention settings were configured for MySQL, and Azure Monitor/diagnostic settings were selected for monitoring. Azure Key Vault was created for secret management, with secret creation pending the required Key Vault Secrets Officer RBAC permission.

---

# Submission Instructions

- Add all required screenshots and links in your submission
- Do not expose passwords, keys, connection strings, or subscription IDs

---

# Completion Checklist

- [ ] Task 1: Architecture diagram and assumptions documented (Screenshots 1–2)
- [ ] Task 2: Network foundation created with isolated tiers (Screenshots 3–5)
- [ ] Task 3: Least-privilege security and secret management configured (Screenshots 6–7)
- [ ] Task 4: Presentation tier deployed (Screenshots 8–9)
- [ ] Task 5: Application tier deployed privately (Screenshots 10–12)
- [ ] Task 6: Managed database tier deployed privately (Screenshots 13–15)
- [ ] Task 7: Public entry, internal routing, and monitoring configured (Screenshots 16–18)
- [ ] Task 8: End-to-end validation and availability test completed (Screenshots 19–22, Public Endpoint, Notes)
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
