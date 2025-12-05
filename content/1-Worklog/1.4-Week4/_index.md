---
title: "Week 4 Worklog"
date: "2025-09-29"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

- Learn comprehensive knowledge about the diverse storage services on AWS.
- Focus deeply on the core service **Amazon S3** (Simple Storage Service), an object storage service, including its characteristics (like 11 nines durability, replication across 3 AZs), and Storage Classes.
- Learn about important features like **Lifecycle Management**, **Versioning**, and **Static Website Hosting**.
- Large-scale data migration solutions (the **Snow Family**), hybrid storage solutions connecting on-premise with the cloud (Storage Gateway), the centralized backup management service (**AWS Backup**), and the basic concepts and strategies for **Disaster Recovery (DR)**.

### Tasks to be carried out this week:

| Day 	| Task 	| Start Date 	| Completion Date 	| Reference Material 	|
|---	|---	|---	|---	|---	|
| 2 	| **Amazon Simple Storage Service - S3**<br><br>- Learn about the architecture of **Amazon S3**, an **object** storage service, suitable for Write-Once-Read-Many (WORM) data.<br>- Understand the technique of automatic data replication across **3 AZs** within 1 Region to ensure high availability.<br>- Learn about the **durability** of S3, designed for up to 99.999999999% (11 nines).<br>- Understand the technique of uploading (HTTP PUT) and accessing (HTTP GET) S3 data via **REST API**.<br>- Learn about the architecture of **Storage Classes**, including S3 Standard, S3 Standard-IA, S3 Intelligent-Tiering, S3 One Zone-IA, and Amazon Glacier/Deep Archive.<br>- Understand the **Object Life Cycle Management** technique to automatically move objects between storage classes over time.<br>- Understand the technique for hosting a **Static Website** (suitable for Single Page Applications) and configuring **CORS** (Cross-origin resource sharing).<br>- Understand access control techniques using **S3 Access Control List (ACL)** (attached to buckets/objects) and **S3 Bucket Policy** (easier to manage).<br>- Learn about the architecture of **S3 Endpoints**, which allow access to S3 buckets over the AWS private network without needing the Internet.<br>- Understand the **Versioning** technique to recover objects after accidental deletion or overwrite, and to support protection against ransomware.<br>- Understand the S3 performance optimization technique by using **random prefixes** for object keys, helping S3 store objects across multiple partitions.<br>- Learn about the architecture of **S3 Glacier**, a low-cost, long-term archival service that requires data to be **retrieved** (Expedited, Standard, Bulk) to an S3 Bucket before use. 	| 29/09/2025 	| 29/09/2025 	| [Module 04](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md) 	|
| 3 	| **Snow Family**<br><br>- Learn about the **Snow Family** services (Snowball, Snowball Edge, Snowmobile) used to migrate PetaByte (PB) to Exabyte (EB) scale data from on-premise to AWS (S3 or Glacier).<br>- Understand the technique of **Snowball Edge**, which is a special device with available compute resources to process data locally.<br><br>**Amazon Storage Gateway**<br><br>- Learn about the architecture of **AWS Storage Gateway**, a **Hybrid** storage solution that combines storage capacity on AWS with on-premise.<br>- Understand the techniques of the three types of gateways:<br>    + **File Gateway:** Allows storing files on S3 via NFS and SMB protocols.<br>    + **Volume Gateway:** Provides block storage via iSCSI, with data stored on S3.<br>    + **Tape Gateway:** Provides a virtual tape library (VTL) iSCSI, storing virtual tape data in S3 or Glacier. 	| 30/09/2025 	| 30/09/2025 	| [Module 04](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md)  	|
| 4 	| **Disaster Recovery on AWS**<br><br>- Understand the technique... for designing Disaster Recovery (DR) based on two key metrics:<br>    + **RTO (Recovery Time Objective):** The time required to restore service.<br>    + **RPO (Recovery Point Objective):** The maximum period of time during which data might be lost.<br>- Learn about the 4 DR strategies on AWS: Backup and Restore, Pilot Light, Low Capacity Active-Active, and Full Capacity Active-Active.<br><br>**AWS Backup**<br>- Learn about the **AWS Backup** service, a centralized management service that allows configuring and scheduling, and setting retention policies for backing up multiple AWS resources (EBS, EC2, RDS, EFS, Storage Gateway...). 	| 01/10/2025 	| 01/10/2025 	| [Module 04](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md)  	|
| 5 	| **Lab: 000057 - Getting Started with Amazon S3**<br>- Create S3 Bucket<br>- Upload data to S3<br>- Host static website on S3<br><br>**Lab: 000013 - AWS Backup**<br>- Prepare infrastructure<br>- Create Backup Plan<br>- Set up Notification<br>- Verify operation<br><br>**Lab: 000014 - AWS Import/Export**<br>- Prepare virtual machine<br>- Import virtual machine to AWS<br>- Export virtual machine from AWS 	| 02/10/2025 	| 02/10/2025 	| [Module 04](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md)  	|
| 6 	| **Lab: 000024 - Storage Gateway**<br>- Create Storage Gateway<br>- Create File Sharing<br>- Connect the File Share to the machine<br><br>**Lab: 000025 - FSx**<br>- AWS Managed MS AD<br>- Deploy Instance<br>- Set up and use FSx<br><br>**[Supplemental Research] - AWS Skill Builder**<br><br>- A series of in-depth theory lessons for storage specialists on AWS.<br>- Storage Learning Plan: Block Storage<br>- Storage Learning Plan: Object Storage 	| 03/10/2025 	| 03/10/2025 	| [Module 04](https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_04/Take_notes_module_04.md) <br> [Research Link](https://explore.skillbuilder.aws/) 	|

### Week 4 Achievements:

- **S3 Service (Basics):** Clearly understand that **Amazon S3** is an object storage service, not block storage, operating on a WORM (Write Once, Read Many) model.
- **Lesson on Durability:** Know that S3 is designed for 11 nines (99.999999999%) of durability by automatically replicating data across 3 Availability Zones (AZs).
- **S3 Cost Optimization Techniques:** Differentiate between Storage Classes such as **S3 Standard** (frequent access), **S3 Standard-IA** (infrequent access), and **S3 Glacier** (long-term, low-cost archival, requires retrieval).
- **S3 Automation Techniques:**
    + Know how to use **Object Life Cycle Management** to automatically transition data to cheaper tiers (e.g., from Standard to Glacier) over time.
    + Understand **Trigger Events** (e.g., triggering a serverless function upon file upload).
- **S3 Security Techniques:** Differentiate between two access control mechanisms: **S3 ACL** (legacy mechanism) and **S3 Bucket Policy** (easier to define access permissions).
- **Lesson on Data Protection (S3):** Clearly understand the **Versioning** feature, which allows restoring previous versions of a file, helping to protect against accidental deletion or ransomware attacks.
- **S3 Networking Techniques:**
    + Know how to use an **S3 Endpoint** to access S3 from within a VPC over the AWS private network without needing the Internet.
    + Know how to host a **Static Website** on S3 and configure **CORS**.
- **Data Migration Service (Migration):** Recognize the **Snow Family** (Snowball, Snowmobile) as the *physical* solution for large-scale (Petabyte, Exabyte) data migration from on-premise.
- **Hybrid Storage Service:** Understand **Storage Gateway** as a hybrid storage solution, allowing on-premise applications to use protocols (NFS, SMB, iSCSI) to store data on S3/Glacier.
- **Lesson on Disaster Recovery (DR):** Understand the 2 basic concepts for designing DR: **RTO** (recovery time) and **RPO** (acceptable data loss).
- **Backup Service (Backup):** Know that **AWS Backup** is a centralized management service that helps automate backups (schedule, retention) for multiple AWS resources (EBS, RDS, EFS...).
- **Hands-on:** Understand the practical steps to create an S3 bucket, host a static website, and configure AWS Backup.