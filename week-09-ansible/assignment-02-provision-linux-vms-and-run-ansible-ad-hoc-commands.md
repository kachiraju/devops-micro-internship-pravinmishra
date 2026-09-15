# Assignment 02 — Provision Linux VMs with Terraform and Run Ansible Ad-Hoc Commands

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will use Terraform to provision three or four Ubuntu Linux Virtual Machines on either Microsoft Azure or Amazon Web Services.

You will configure SSH key-based authentication, organize the servers using a custom Ansible inventory, and run Ansible ad-hoc commands across individual hosts and inventory groups.

---

# Task 1 — Create the Multi-Host Lab Structure

## Goal

Create a separate project directory for the multi-host lab and prepare the Terraform, Ansible, and documentation files.

This project will use the Git repository and Ansible controller prepared in Assignment 01.

### Evidence

#### Screenshot 1 — Terminal showing the complete `ansible-adhoc-lab` project structure

[structure](./screenshots/AS2T1SS1.png)!

---

#### Screenshot 2 — Terminal showing `git status --short` with the new project files and updated `.gitignore`

[gitstatus](./screenshots/AS2T1SS2.png)!

---

### Notes

Created the `ansible-adhoc-lab` project directory inside the existing `ansible-onboarding` Git repository. The project is organized into separate `terraform` and `ansible` directories.

Created the required Terraform files: `providers.tf`, `main.tf`, `variables.tf`, and `outputs.tf`. Also created `inventory.ini` for the custom Ansible inventory and `README.md` for project documentation.

Updated the existing `.gitignore` file to exclude Terraform state files, saved plans, crash logs, and the `.terraform/` working directory. This prevents sensitive Terraform state data from being committed to Git.

Verified the final project structure using the `find` command. No additional Git repository was created inside the lab directory.

---

# Task 2 — Create the Terraform Configuration

## Goal

Create the Terraform configuration required to provision three or four Ubuntu Linux VMs on your selected cloud platform.

Complete only one option:

- Option A — Microsoft Azure
- Option B — Amazon Web Services

Do not configure both providers for this assignment.

### Evidence

#### Screenshot 3 — Terraform configuration showing the three or four server roles and the `for_each` or `count` implementation

[tf](./screenshots/AS2T2SS3.png)!

---

#### Screenshot 4 — Terraform configuration showing SSH restricted to the controller IP and HTTP allowed only for web hosts

[tf](./screenshots/AS2T2SS4.png)!

---

#### Screenshot 5 — Terraform output configuration showing how public IP addresses are associated with the server roles

[tf](./screenshots/AS2T2SS4.png)!

---

### Notes

Created the Terraform configuration for the Azure three-VM option using the server roles `web1`, `app1`, and `db1`. The `for_each` expression uses the `vm_roles` map so that Terraform creates the required resources without repeating separate VM resource blocks.

Configured Azure resources including a resource group, virtual network, subnet, public IP addresses, network interfaces, network security groups, and Ubuntu Linux virtual machines. All servers use the same SSH public key and the `azureuser` administrator account.

SSH access on port 22 is restricted to the public IP address of the Ansible controller by using a `/32` CIDR value. HTTP traffic on port 80 is allowed only for the web server through the web network security group. The application and database servers receive a separate security group with no HTTP rule.

Created Terraform outputs that map each server role to its public IP address and generate SSH connection commands. The configuration was formatted, initialized, and validated successfully before deployment.

---

# Task 3 — Provision the Infrastructure with Terraform

## Goal

Initialize and validate the Terraform configuration, review the execution plan, provision the selected three or four VMs, and retrieve their public IP addresses.

### Evidence

#### Screenshot 6 — Final `terraform apply` output showing `Apply complete`

[tf](./screenshots/AS2T3SS6.png)!

---

#### Screenshot 7 — `terraform output public_ips` showing the role-to-IP mapping for all three or four VMs

[tf](./screenshots/AS2T3SS7.png)!

---

#### Screenshot 8 — Azure Portal or AWS Management Console showing all three or four VMs in the `Running` state, with their role-based names visible

[tf](./screenshots/AS2T3SS8.png)!

---

### Notes

Provisioned the Azure infrastructure using Terraform for the three-server option: `web1`, `app1`, and `db1`. Terraform created the resource group, virtual network, subnet, network security groups, public IP addresses, network interfaces, and Ubuntu Linux virtual machines.

The initial deployment in East US could not create the `Standard_B1s` VM size because of an Azure capacity restriction. The lab was then deployed successfully in the selected India region.

Terraform outputs confirmed the public IP address associated with each server role:

- `web1` — `172.198.77.221`
- `app1` — `172.198.77.185`
- `db1` — `172.198.77.156`

The completed deployment provides the managed servers required for SSH verification and the remaining Ansible ad-hoc command tasks.

---

# Task 4 — Verify SSH Key-Based Access

## Goal

Verify that each managed VM can be accessed from the Ansible controller using SSH key-based authentication.

### Evidence

#### Screenshot 9 — Terminal showing successful SSH hostname output from all VMs

[SSH](./screenshots/AS2T4SS9.png)!

---

### Notes

Verified SSH key-based access from the Ansible controller to all three Azure Ubuntu virtual machines. Connections used the private key stored at `~/.ssh/id_ed25519` and the Azure administrator username `azureuser`.

Ran the `hostname` command on each managed server through SSH. The returned hostnames confirmed successful access to `web1`, `app1`, and `db1`.

This confirms that the SSH public key configured by Terraform was installed correctly on every VM and that the network security rules allow SSH access from the Ansible controller.

---

# Task 5 — Create the Custom Ansible Inventory

## Goal

Create an Ansible inventory file that groups the managed VMs by role.

The inventory allows Ansible to run commands against all servers, or only specific groups such as `web`, `app`, or `db`.

### Evidence

#### Screenshot 10 — `inventory.ini` showing the `web`, `app`, and `db` groups

[inv](./screenshots/AS2T5SS10.png)!

---

#### Screenshot 11 — Output of `ansible-inventory -i inventory.ini --graph`

[inv](./screenshots/AS2T5SS11.png)!

---

### Notes

Created a custom Ansible inventory file for the three managed Azure VMs. The servers were organized by their roles using the `web`, `app`, and `db` inventory groups.

Configured friendly host aliases (`web1`, `app1`, and `db1`) with their corresponding public IP addresses through the `ansible_host` setting. Added the Azure SSH username `azureuser` and the controller private-key path `~/.ssh/id_ed25519` under `[all:vars]`.

Created a local `ansible.cfg` file with `host_key_checking = False` to prevent SSH fingerprint prompts during this temporary lab.

Validated the inventory with `ansible-inventory -i inventory.ini --graph`. The output confirmed that all three managed servers appear in the correct role-based groups.

---

# Task 6 — Run Ansible Ad-Hoc Commands

## Goal

Run Ansible ad-hoc commands from the controller to verify connectivity, check server information, and manage packages and services across inventory groups.

This task proves that the inventory is working and that Ansible can control multiple managed VMs without writing a playbook.

### Evidence

#### Screenshot 12 — Output of `ansible all -i inventory.ini -m ping`

[ansible](./screenshots/AS2T6SS12.png)!

---

#### Screenshot 13 — Output of `ansible all -i inventory.ini -m command -a "uptime"`

[ansible](./screenshots/AS2T6SS13.png)!

---

#### Screenshot 14 — Output of `ansible web -i inventory.ini -m apt -a "name=nginx state=present update_cache=yes" --become`

[ansible](./screenshots/AS2T6SS14.png)!

---

#### Screenshot 15 — Output of `ansible web -i inventory.ini -m service -a "name=nginx state=started enabled=yes" --become`

[ansible](./screenshots/AS2T6SS15.png)!

---

#### Screenshot 16 — Output of `ansible all -i inventory.ini -m apt -a "name=htop state=present update_cache=yes" --become`

[ansible](./screenshots/AS2T6SS15.png)!

---

#### Screenshot 17 — Output of `ansible web -i inventory.ini -m command -a "systemctl is-active nginx"`

[ansible](./screenshots/AS2T6SS16.png)!

---

### Notes

Used Ansible ad-hoc commands from the controller to manage and verify all three Azure Ubuntu virtual machines without creating an Ansible playbook.

Validated connectivity with the Ansible `ping` module. All managed servers (`web1`, `app1`, and `db1`) returned `SUCCESS` with `pong`, confirming that Ansible could connect through SSH and execute Python modules. The `whoami` command confirmed that connections used the `azureuser` account.

Ran the `uptime` command across all hosts to verify that each server was online and returning system information.

Installed Nginx on the `web` group only, which contains `web1`. Then used the Ansible service module with `--become` to ensure that the Nginx service was started and enabled at boot. The Nginx status check returned `active`.

Installed `htop` across all managed hosts using the Ansible `apt` module and `--become`. This demonstrated how Ansible can target a role-specific group, such as `web`, or the complete inventory using `all`.

The task demonstrated that Ansible ad-hoc commands are useful for quick connectivity checks, system-information checks, package installation, and service management across multiple servers.

---

# LinkedIn Post Required

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://lnkd.in/p/dCQnh2aq

---

#### Screenshot — Published LinkedIn post

[linkedin](./screenshots/AS2_LINKEDIN.png)!

---

# Assignment Questions

Answer the following in your own words:

**1. What is the purpose of an Ansible inventory file?**

An Ansible inventory file tells Ansible which servers it should manage and how to reach them. It can store host names, IP addresses, SSH settings, and groups of related servers.

---

**2. What is the difference between the `web`, `app`, and `db` groups in your inventory?**

The groups organize servers according to their role. The web group contains the web server that runs Nginx, the app group contains the application server, and the db group contains the database server. Grouping lets me run a command only on the servers that need it.

---

**3. What does the Ansible `ping` module verify?**

The Ansible ping module verifies that Ansible can connect to a managed server through SSH, run Python on that server, and receive a response. It is not the same as a normal network ICMP ping.

---

**4. Why do package installation commands require `--become`?**

Installing packages changes the operating system and requires administrator permissions. The --become option tells Ansible to use elevated privileges, similar to using sudo in a Linux terminal.

---

**5. When would you use an ad-hoc command instead of a playbook?**

I would use an ad-hoc command for a quick, one-time task such as checking uptime, checking disk space, testing connectivity, restarting a service, or installing a package on a few servers. A playbook is better when the task must be repeated consistently or has several steps.

---

**6. What is one challenge you faced while setting up SSH or inventory, and how did you fix it?**

One challenge was that my Ansible controller project was not in the default ~/ansible-onboarding location. It was located in ~/DMI/ansible-onboarding. I corrected the command paths, then created the inventory with the correct public IP address, azureuser SSH username, and private-key path. The Ansible ping test confirmed that all three servers were reachable.

---

# Required Files

Confirm that the following files are included in your assignment workspace:

- [ ] `ansible-adhoc-lab/README.md`
- [ ] `ansible-adhoc-lab/terraform/providers.tf`
- [ ] `ansible-adhoc-lab/terraform/main.tf`
- [ ] `ansible-adhoc-lab/terraform/variables.tf`
- [ ] `ansible-adhoc-lab/terraform/outputs.tf`
- [ ] `ansible-adhoc-lab/ansible/inventory.ini`
- [ ] Updated `.gitignore`

---

# Submission Instructions

- Add all required screenshots from the tasks.
- Full Name must be visible in required screenshots.
- Mention whether you used Azure or AWS.
- Mention whether you used the three-VM option or four-VM option.
- Add the public IP addresses of the VMs, redacted if preferred.
- Add your `inventory.ini` proof.
- Add a short explanation of what you learned.
- Answer all assignment questions clearly in your own words.
- Add your LinkedIn post URL.
- Do not expose SSH private keys, Terraform state files, cloud credentials, passwords, access keys, secret keys, account IDs, or subscription IDs.
- Submit only one Google Doc link.

---

# Completion Checklist

- [ ] Task 1: `ansible-adhoc-lab` project structure created
- [ ] Task 1: `.gitignore` updated for Terraform files
- [ ] Task 2: Terraform configuration created
- [ ] Task 2: Server roles defined for either three or four VMs
- [ ] Task 2: `count` or `for_each` used
- [ ] Task 2: SSH restricted to the controller public IP
- [ ] Task 2: HTTP allowed only for web hosts
- [ ] Task 2: Terraform output maps roles to public IPs
- [ ] Task 3: Terraform initialized successfully
- [ ] Task 3: Terraform configuration validated
- [ ] Task 3: Terraform apply completed successfully
- [ ] Task 3: All selected VMs are running
- [ ] Task 4: SSH key-based access works for every VM
- [ ] Task 5: `inventory.ini` contains `web`, `app`, and `db` groups
- [ ] Task 5: `ansible-inventory -i inventory.ini --graph` shows the correct groups
- [ ] Task 6: `ansible all -i inventory.ini -m ping` returns `SUCCESS`
- [ ] Task 6: Ad-hoc commands run successfully
- [ ] Task 6: `--become` was used for package and service tasks
- [ ] Task 6: Nginx is active on the `web` group
- [ ] Screenshots 1–17 are included
- [ ] Assignment questions are answered
- [ ] LinkedIn post published
- [ ] LinkedIn post URL added
- [ ] No sensitive information is exposed
- [ ] Google Doc is accessible

---

## About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra and The CloudAdvisory, focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## Resources

- DMI Official Website: [https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme](https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme)
- University: [https://university.pravinmishra.com?utm_source=github&utm_medium=readme](https://university.pravinmishra.com?utm_source=github&utm_medium=readme)
- Discord Community: [https://discord.pravinmishra.com?utm_source=github&utm_medium=readme](https://discord.pravinmishra.com?utm_source=github&utm_medium=readme)
- Blog: [https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme](https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme)
- YouTube Playlist: [https://www.youtube.com/playlist?list=PLFeSNDtI4Cho](https://www.youtube.com/playlist?list=PLFeSNDtI4Cho)
- Pravin Mishra LinkedIn: [https://www.linkedin.com/in/pravin-mishra-aws-trainer/](https://www.linkedin.com/in/pravin-mishra-aws-trainer/)
- CloudAdvisory LinkedIn: [https://www.linkedin.com/company/thecloudadvisory/](https://www.linkedin.com/company/thecloudadvisory/)

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*