---
title: "Week 3 Worklog"
date: "2025-09-22"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

- Understand comprehensive knowledge of **virtual server (Compute VM)** services on AWS.
- Focus on the core service **Amazon EC2**, including configuration selection (**Instance Types**), storage types (**EBS, Instance Store**), and automation **(User data, Auto Scaling)**.
- Learn about related services such as **Amazon Lightsail** (low-cost service), shared file storage solutions **(EFS for Linux and FSx for Windows/Linux)**, and the **AWS MGN** application migration service to migrate servers to AWS or build **Disaster Recovery**.

### Tasks to be carried out this week:

| Day 	| Task 	| Start Date 	| Completion Date 	| Reference Material 	|
|---	|---	|---	|---	|---	|
| 2 	| **Amazon Elastic Compute Cloud (EC2)**<br>- Learn about the architecture of Amazon EC2, a flexible virtual server service with fast boot capabilities and powerful resource scaling.<br>- Understand the technique of selecting server configurations through EC2 Instance Types, which determine factors like CPU, Memory, Network, and Storage.<br>- Learn how to use AMI (Amazon Machine Image) to provision one or more EC2 Instances and use Key Pairs (public and private key) to encrypt login information.<br>- Understand the EBS (Elastic Block Store) block storage technique, which operates independently, replicates data (3x) to ensure high availability, and connects to EC2 over the network.<br>- Differentiate EBS from Instance Store, which is an extremely high-speed NVME disk area but whose data is completely erased when the EC2 instance is stopped.<br>- Learn about the User Data automation technique, a script (bash shell or powershell) that runs once when an EC2 instance is launched.<br>- Understand Meta Data, information related to the EC2 instance (like IP, Hostname) that can be accessed from the server itself, often used for automation.<br>- Understand the EC2 Auto Scaling technique to automatically increase (scale-out) or decrease (scale-in) the number of EC2 Instances based on conditions (scaling policy).<br>- Learn about EC2 Pricing Options (On-demand, Reserved Instance, Saving Plans, Spot Instance) to optimize costs. 	| 22/09/2025 	| 22/09/2025 	| [Module 03](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md) 	|
| 3 	| **Amazon Lightsail**<br>- Learn about the Amazon Lightsail service, a low-cost virtual server solution (starting at $3.5/month) suitable for light workloads, test/dev environments.<br>- Understand the technique for connecting Lightsail (located in a special VPC) with a regular VPC via VPC Peering (with just 1 click).<br><br>**Amazon EFS/FSx**<br>- Learn about EFS (Elastic File System), a network file storage service (NFSv4) that allows multiple EC2 Instances (Linux only) to mount simultaneously, charging based on storage used.<br>- Learn about Amazon FSx, a service that allows creating NTFS volumes (SMB protocol) to attach to multiple EC2 Instances (supports Windows and Linux).<br>- Understand the deduplication technique of FSx, which helps reduce data duplication and lower storage costs.<br><br>**AWS Application Migration Service (MGN)**<br>- Learn about the AWS MGN service used to migrate and replicate servers (physical or virtual) from on-premise to the AWS environment.<br>- Understand the replication technique of MGN used for building a Disaster Recovery Site at a low cost (using low-configuration staging machines). 	| 23/09/2025 	| 23/09/2025 	| [Module 03](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md)	|
| 4 	| **Lab: 000004 - Basic EC2 Operations.**<br>- Create an EC2 Instance<br>- Take an EC2 Instance snapshot<br>- Install an application on EC2<br><br>**Lab: 000027 - Resource Management with Tags and Resource Groups**<br>- Use Tags<br>- Use Resource Groups 	| 24/09/2025 	| 24/09/2025 	| [Module 03](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md) 	|
| 5 	| **Lab: 000008 - Resource Management with Amazon CloudWatch**<br>- CloudWatch Agent<br>- Create CloudWatch Dashboard<br><br>**Lab: 000006 - Deploying an Autoscaling Group**<br>- Create Launch Template<br>- Create Target Group<br>- Create Load Balancer<br>- Create Auto Scaling Group<br>- Verify the results. 	| 25/09/2025 	| 25/09/2025 	| [Module 03](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md)	|
| 6 	| **Lab: 000045 - Getting Started with Amazon Lightsail**<br><br>- Preparation<br>- Test the application on Lightsail<br>- Use Lightsail Load Balancer<br>- Use RDS<br>- Migrate to EC2.<br><br>**[Supplemental Research] - Microsoft Workloads on AWS**<br><br>- A series of supplemental labs for running Microsoft servers and applications on AWS<br>- Supplement knowledge about operating systems<br>- Supplement knowledge about the Linux operating system such as LBI1, LBI2<br>- Supplement knowledge about the Windows operating system, learn more about the Bundo management system. Refer to the lab series 	| 26/09/2025 	| 26/09/2025 	| [Module 03](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_03/Take_notes_module_03.md) <br> [Research Link](https://www.youtube.com/playlist?list=PLhr1KZpdzukdJ\|IxuIUM7pMB7aJ2_FfTP)	|

### Week 3 Achievements:

- **EC2 Service:** Clearly understand that **EC2** is the core virtual server service of AWS.
- **EC2 Configuration Techniques:** Know how to select **Instance Type** (CPU, RAM, Network configuration) and use **AMI** to provision the operating system for the server.
- **EC2 Security Techniques:** Understand how to use **Key Pair** (public/private key) to encrypt login information, instead of using passwords.
- **Storage Service (Storage):** Clearly differentiate the 2 main disk storage types for EC2:
    + **EBS (Elastic Block Store):** Is a network drive, operates independently, data is replicated 3x within 1 AZ (99.999% availability), can be backed up using snapshots.
    + **Instance Store:** Is a physical drive (NVME) with extremely high speed, but the data is temporary (will be erased when EC2 is stopped), often used for cache/buffer or swap.
- **Automation Techniques (Automation):**
    + Know how to use **User Data** to run a script once when the server boots up (e.g., install a web server).
    + Understand what **Meta Data** is and how to use it to retrieve information (IP, hostname) about the server from within itself, used for automation scripts.
- **Scaling Techniques (Scaling):** Master the concept of **EC2 Auto Scaling** to automatically increase (scale-out) or decrease (scale-in) the number of servers based on load (e.g., when ActiveConnectionCount is high or low).
- **Cost Optimization Techniques (Pricing):** Recognize the 4 EC2 pricing models: **On-demand** (per hour/second, most expensive), **Reserved Instance** (1-3 year commitment), **Saving Plans** (1-3 year commitment, more flexible), and **Spot Instance** (low price, utilizes surplus resources but can be reclaimed).
- **Lightsail Service:** Understand **Amazon Lightsail** is a low-cost, simplified VM service, suitable for light workloads, and know how to peer it with a VPC.
- **File Storage Service (File Storage):** Differentiate between the 2 shared file storage services for multiple servers:
    + **EFS (Elastic File System):** Used for **Linux** (NFSv4 protocol), charges based on storage used.
    + **FSx:** Used for **Windows/Linux** (SMB protocol), supports deduplication feature to reduce costs.
- **Migration Service (Migration):** Understand **AWS MGN** is a service to migrate servers from on-premise to AWS or to build a low-cost **Disaster Recovery (DR)** system via a staging area.
- **Hands-on:** Understand the basic hands-on steps with EC2 (create, snapshot), deploy a complete Auto Scaling Group (with Load Balancer), and get familiar with Lightsail.
