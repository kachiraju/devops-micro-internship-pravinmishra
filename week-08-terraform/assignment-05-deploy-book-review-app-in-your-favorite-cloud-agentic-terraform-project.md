# Capstone Assignment — Deploy the Book Review App Using Terraform and Claude Code Agentic AI

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Student Details

**Full Name:** Add your full name here  
**Cloud Platform:** AWS or Azure  
**GitHub Repository URL:** Add your repository URL here  
**Public Application URL / Load-Balancer DNS:** Add the public URL or DNS here

---

## Purpose

Deploy the Book Review App using Terraform on AWS or Azure in a secure, highly available, production-style three-tier architecture. Use Claude Code, specialized subagents, Terraform MCP, and validation hooks to support the engineering workflow while keeping all infrastructure-changing operations under human control.

---

# Task 0 — Prepare the Project and Agentic AI Environment

## Goal

Prepare the Book Review App project and configure the provided Claude Code Agentic AI starter kit with project context, specialized subagents, Terraform MCP, validation hooks, and safety guardrails.

## Evidence

### Screenshot 1 — Project `CLAUDE.md`

Add a screenshot of the project `CLAUDE.md` showing the three-tier architecture, security boundaries, Terraform requirements, and human-approval rules.

![claude](./screenshots/AS5T0SS1_1.png)
![claude](./screenshots/AS5T0SS1_2.png)

---

### Screenshot 2 — Terraform Engineer Subagent

Add a screenshot showing the Terraform Engineer subagent configuration.

![SUBAGENT](./screenshots/AS5T0SS2.png)

---

### Screenshot 3 — Architecture and Security Reviewer Subagent

Add a screenshot showing the Architecture and Security Reviewer subagent configuration.

![SUBAGENT](./screenshots/AS5T0SS3.png)

---

### Screenshot 4 — Terraform MCP Connection

Add a screenshot showing Terraform MCP connected and available.

![MCP](./screenshots/AS5T0SS4.png)

---

### Screenshot 5 — Validation Hooks

Add a screenshot showing the configured Claude Code validation hooks.

![HOOKS](./screenshots/AS5T0SS5.png)

---

# Task 1 — Design the Three-Tier Architecture

## Goal

Design the required secure, highly available three-tier architecture and create an architecture diagram before building the infrastructure.

The diagram must show:

- VPC or VNet
- Availability Zones or equivalent availability locations
- Six subnets
- Internet connectivity
- NAT or outbound design
- Public load balancer
- Web Tier
- Internal load balancer
- Application Tier
- Managed MySQL
- Read replica
- Main traffic flow

## Architecture Diagram

![ARCH](./screenshots/AS5T1SS.png)

---

# Task 2 — Build the Terraform Networking and Security Layers

## Goal

Create the modular Terraform project and implement the network and security layers across the required public and private subnets.

## Evidence

### Screenshot 6 — Modular Terraform Project Structure

Add a screenshot showing the modular Terraform project structure.

![tf](./screenshots/AS5T2SS6.png)

---

### Screenshot 7 — Six-Subnet Architecture

Add a screenshot showing the six-subnet architecture across two availability locations.

![tf](./screenshots/AS5T2SS7.png)

---

### Screenshot 8 — Public and Private Tier Separation

Add a screenshot showing the public and private tier separation, including routing and security boundaries.

![tf](./screenshots/AS5T2SS8.png)

---

# Task 3 — Build the Load-Balancing and Compute Layers

## Goal

Deploy the public and internal load balancers and the Web and Application compute resources required by the Book Review App.

## Evidence

### Screenshot 9 — Web and Application Compute

Add a screenshot showing the Web and Application compute resources in their required subnets.

![ec2](./screenshots/AS5T3SS9.png)

---

### Screenshot 10 — Public Load Balancer

Add a screenshot showing the internet-facing public load balancer.

![lb](./screenshots/AS5T3SS10.png)

---

### Screenshot 11 — Internal Load Balancer

Add a screenshot showing the private internal load balancer.

![lb](./screenshots/AS5T3SS11.png)

---

### Screenshot 12 — Healthy Targets

Add a screenshot showing healthy target groups or backend pools.

![lb](./screenshots/AS5T3SS12.png)

---

# Task 4 — Build the Managed MySQL Database Layer

## Goal

Deploy a private, highly available managed MySQL database with a read replica and restrict database connectivity to the Application Tier.

## Evidence

### Screenshot 13 — Managed MySQL Database

Add a screenshot showing the managed MySQL database deployment.

![db](./screenshots/AS5T4SS13.png)

---

### Screenshot 14 — High Availability

Add a screenshot showing the Multi-AZ or high-availability configuration.

![db](./screenshots/AS5T4SS14.png)

---

### Screenshot 15 — Read Replica

Add a screenshot showing the read replica configuration.

![db](./screenshots/AS5T4SS15.png)

---

### Screenshot 16 — Private Database Access

Add a screenshot showing that the database is private and accepts MySQL traffic only from the Application Tier.

![db](./screenshots/AS5T4SS16.png)

---

# Task 5 — Validate, Review, and Apply the Terraform Configuration

## Goal

Validate the Terraform configuration, review the execution plan using both Agentic AI and human judgment, and apply the infrastructure changes only after all required checks pass.

## Evidence

### Screenshot 17 — Terraform Validation

Add a screenshot showing successful `terraform validate` output.

![tf](./screenshots/AS5T5SS17.png)

---

### Screenshot 18 — Terraform Plan

Add a screenshot showing the Terraform plan output.

![tf](./screenshots/AS5T5SS18.png)

---

### Screenshot 19 — Terraform Apply

Add a screenshot showing successful `terraform apply` completion.

![tf](./screenshots/AS5T5SS19.png)

---

# Task 6 — Deploy and Configure the Book Review Application

## Goal

Deploy and configure the Book Review App across the Web, Application, and Database tiers and verify the complete application functionality.

## Evidence

### Screenshot 20 — Homepage

Add a screenshot showing the Book Review App homepage through the public endpoint.

![browser](./screenshots/AS5T6SS20.png)

---

### Screenshot 21 — Login or Authentication

Add a screenshot showing successful login or authentication.

![browser](./screenshots/AS5T6SS21.png)

---

### Screenshot 22 — Book Data

Add a screenshot showing the book listing or book details.

![browser](./screenshots/AS5T6SS22.png)

---

### Screenshot 23 — Review Functionality

Add a screenshot showing the review functionality working successfully.

![browser](./screenshots/AS5T6SS23.png)

---

### Screenshot 24 — Backend or API Evidence

Add a screenshot showing that the backend or API is working successfully.

![browser](./screenshots/AS5T6SS24.png)

---

### Screenshot 25 — Database Reads and Writes

Add a screenshot showing successful database reads and writes.

![browser](./screenshots/AS5T6SS25.png)


## Public Application URL

**Public Application URL / DNS:** http://book-review-capstone-public-alb-1064691467.ap-south-1.elb.amazonaws.com/

---

# Task 7 — Demonstrate the Agentic AI Workflow

## Goal

Demonstrate how Claude Code assisted with Terraform generation, architecture and security review, and evidence-based troubleshooting while infrastructure-changing decisions remained under human control.

You do not need to submit your complete Claude Code conversation history. Include only focused evidence.

## Evidence

### Screenshot 26 — AI-Assisted Terraform Generation

Add a screenshot showing one useful example of AI-assisted Terraform generation or improvement.

![ai](./screenshots/AS5T7SS26_1.png)
![ai](./screenshots/AS5T7SS26_2.png)

---

### Screenshot 27 — Architecture or Security Review

Add a screenshot showing one structured architecture or security review result.

![REVIEW](./screenshots/AS5T7SS27.png)

---

### Screenshot 28 — AI-Assisted Troubleshooting

Add a screenshot showing one AI-assisted troubleshooting interaction based on collected evidence.

![REVIEW](./screenshots/AS5T7SS28.png)

---

# Task 8 — Complete the Final Architecture Review

## Goal

Review the completed infrastructure against the original capstone requirements and resolve significant architecture, security, reliability, and cost issues.

Confirm that the final review covers:

- Tier separation
- Availability
- Public exposure
- Routing
- Security rules
- Load balancing
- Database privacy
- Secrets
- Terraform quality
- Module structure
- Reliability
- Obvious cost risks

Use Screenshot 27 as the focused evidence for the structured architecture or security review.

---

# Task 9 — Answer the Reflection Questions

## Goal

Reflect on the architecture, Terraform implementation, and Agentic AI workflow. Answer each question briefly in your own words.

## Architecture

### 1. Why did you separate the Web, Application, and Database tiers?

Separation provides clearer security boundaries, independent scaling, and easier troubleshooting. The web tier serves the frontend, the application tier processes API requests and business logic, and the database tier stores data. Each tier receives only the network access it needs.

### 2. Why is the Application Tier private?

The application tier is private so users cannot access the Express backend directly. Requests reach it only through the internal Application Load Balancer from the web tier, reducing attack surface.

### 3. Why is MySQL private?

MySQL contains application and user data, so it must not be exposed to the internet. Its security group allows port 3306 only from the application-tier security group.

### 4. Why are multiple Availability Zones used?

Resources are distributed across two Availability Zones to improve availability. If one Availability Zone has a failure, load balancers and Auto Scaling Groups can continue serving traffic from the other zone.

### 5. What is the difference between Multi-AZ/high availability and a read replica?

Multi-AZ provides high availability through a standby database and automatic failover; it is mainly for resilience. A read replica is a separate database copy used for read scaling and reporting. It has its own endpoint and is not the same as a failover standby.

## Terraform

### 6. How did you divide your Terraform into modules?

I separated Terraform into modules for network, security, load balancer, compute, database, secrets, and artifacts. The root module connects these modules and provides shared variables, provider configuration, and common tags.

### 7. How do the modules communicate through variables and outputs?

A module exports resource values through outputs, and the root module passes those values into another module as variables. For example, the network module outputs subnet IDs, the security module outputs security-group IDs, and those are passed to the load balancer, compute, and database modules.


### 8. What did you specifically check in `terraform plan`?

I checked that only expected resources would be created, changed, or destroyed; that no ports 3001 or 3306 were publicly exposed; that IAM access was least privilege; and that no unintended RDS password change was planned. For the phased deployment, I also verified that the artifact-bucket plan contained only four S3 resources.

## Agentic AI

### 9. What was the purpose of `CLAUDE.md`?

CLAUDE.md defined project-specific instructions, architecture requirements, safety expectations, validation steps, and the required security-review workflow for the AI agents.

### 10. What work did the Terraform Engineer subagent perform?

The Terraform Engineer planned and implemented the Terraform changes, created modules and user-data templates, wired variables and outputs, ran formatting and validation, and generated plans for review. It did not apply infrastructure without approval.

### 11. What did the Architecture and Security Reviewer identify?

The reviewer identified a stale plan, missing web-tier HTTPS egress, a secret-retrieval variable-scoping bug, missing AWS Region configuration, outdated comments, and missing deployment documentation. These findings were fixed before deployment.

### 12. Why did you use Terraform MCP instead of relying only on Claude's existing Terraform knowledge?

Terraform MCP provided current Terraform-specific context and validation support, rather than relying only on general model knowledge. This helped verify module structure, resource configuration, plans, and provider-related decisions against the actual project.

### 13. What was the purpose of your validation hooks?

The validation hooks ensured formatting and configuration checks ran consistently. They helped catch Terraform syntax, formatting, and configuration problems before infrastructure changes were applied.

### 14. Describe one real issue Claude helped you troubleshoot.

The app-tier target group was unhealthy because cloud-init failed during dnf install: installing curl conflicted with Amazon Linux’s existing curl package. This stopped the user-data script before the backend service was created. The issue was diagnosed through SSM logs and repaired manually so the backend returned HTTP 200.

### 15. Describe one recommendation you reviewed, modified, or rejected instead of accepting blindly.

I did not use the original Git-clone deployment approach because my frontend fixes were local and uncommitted. Instead, I adopted an S3 artifact approach: I created an archive containing the local frontend and backend source, uploaded it to a private versioned S3 bucket, and configured the instances to retrieve it. This ensured the deployed app included the local API-route fix.

---

# Task 10 — Publish the Mandatory LinkedIn Post

## Goal

Publish a LinkedIn post describing the capstone, the technical work completed, the Agentic AI workflow, and the lessons learned.

Write the post in your own words, include at least one project image or other proof, and ensure that it can be viewed by the submission reviewer.

## LinkedIn Post URL

**LinkedIn Post URL:** https://www.linkedin.com/posts/bharadwaja-kachiraju-78a45598_aws-terraform-devops-share-7503205105421160448-PgkM/?utm_source=share&utm_medium=member_desktop&rcm=ACoAABS2KxoBOPNTBIxog_qhN1vz4HLYmnjgQPY

---

# Submission Instructions

- Complete Tasks 0–10 in sequence.
- Include all Screenshots 1–28 exactly as specified.
- Ensure that your full name is visible in the required screenshots.
- Include the selected cloud platform.
- Include the completed architecture diagram.
- Include the modular Terraform project structure.
- Include the working public application URL or public load-balancer DNS.
- Include all required Agentic AI workflow evidence.
- Answer all 15 reflection questions briefly in your own words.
- Include the published LinkedIn post URL.
- Do not expose cloud credentials, database passwords, SSH private keys, JWT secrets, access tokens, account IDs, Terraform state containing sensitive values, or other confidential information.
- Review all screenshots and project files carefully before submitting through GitHub.

---

# Completion Checklist

- [ ] Selected AWS or Azure
- [ ] Added and reviewed the Agentic AI starter files
- [ ] Configured `CLAUDE.md`
- [ ] Configured the Terraform Engineer subagent
- [ ] Configured the Architecture and Security Reviewer subagent
- [ ] Connected Terraform MCP
- [ ] Configured validation hooks and safety guardrails
- [ ] Created the architecture diagram
- [ ] Created the six-subnet design
- [ ] Configured public Web Tier routing
- [ ] Kept the Application Tier private
- [ ] Kept the Database Tier private
- [ ] Configured tier-specific Security Groups or NSGs
- [ ] Restricted backend port `3001`
- [ ] Restricted MySQL port `3306` to the Application Tier
- [ ] Created the public load balancer
- [ ] Created the internal load balancer
- [ ] Configured listeners and health checks
- [ ] Deployed the Web Tier compute resources
- [ ] Deployed the private Application Tier compute resources
- [ ] Provisioned private managed MySQL
- [ ] Configured Multi-AZ or high availability
- [ ] Configured a read replica
- [ ] Created the modular Terraform project
- [ ] Used variables, outputs, and module dependencies
- [ ] Used current Terraform documentation through MCP
- [ ] Used hooks for deterministic validation
- [ ] Completed `terraform fmt`
- [ ] Completed `terraform validate`
- [ ] Reviewed `terraform plan`
- [ ] Completed the Terraform Engineer review
- [ ] Completed the Architecture and Security review
- [ ] Applied the infrastructure only after human approval
- [ ] Deployed and configured the backend
- [ ] Deployed and configured the frontend
- [ ] Configured Nginx where required
- [ ] Configured the internal backend endpoint
- [ ] Configured the public frontend endpoint
- [ ] Verified the homepage
- [ ] Verified login or authentication
- [ ] Verified book data
- [ ] Verified review functionality
- [ ] Verified the backend API
- [ ] Verified database reads and writes
- [ ] Verified healthy load-balancer targets
- [ ] Included AI-assisted Terraform generation evidence
- [ ] Included one architecture or security review
- [ ] Included one AI-assisted troubleshooting example
- [ ] Completed the final architecture review
- [ ] Answered all 15 reflection questions
- [ ] Published the mandatory LinkedIn post
- [ ] Added the LinkedIn post URL
- [ ] Captured all 28 required screenshots
- [ ] Confirmed that my full name is visible in the required screenshots
- [ ] Checked that no secrets or sensitive information are exposed

---

## About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory), focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations through hands-on experience.

---

## Resources

- Book Review App Repository: [https://github.com/pravinmishraaws/book-review-app](https://github.com/pravinmishraaws/book-review-app)
- DMI Official Website: [https://dmi.pravinmishra.com](https://dmi.pravinmishra.com)
- University: [https://university.pravinmishra.com](https://university.pravinmishra.com)
- Discord Community: [https://discord.pravinmishra.com](https://discord.pravinmishra.com)
- Blog: [https://dmi.pravinmishra.com/blog](https://dmi.pravinmishra.com/blog)
- YouTube Playlist: [https://www.youtube.com/playlist?list=PLFeSNDtI4Cho](https://www.youtube.com/playlist?list=PLFeSNDtI4Cho)
- Pravin Mishra on LinkedIn: [https://www.linkedin.com/in/pravin-mishra-aws-trainer/](https://www.linkedin.com/in/pravin-mishra-aws-trainer/)
- CloudAdvisory on LinkedIn: [https://www.linkedin.com/company/thecloudadvisory/](https://www.linkedin.com/company/thecloudadvisory/)

---

*This submission is part of the DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
