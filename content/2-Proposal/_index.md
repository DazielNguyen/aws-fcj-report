---
title: "Proposal"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Personal Finance Management App

### 1. Executive Summary

The Personal Finance Management App project aims to provide an intelligent, modern, and highly automated personal financial management platform. The application allows users to record income and expenses, create and manage multiple money jars for different purposes, create spending plans, receive smart alerts, and generate visual analytical reports.

The application is built with a microservices architecture on .NET and FastAPI platform, deployed on AWS Cloud, ensuring flexibility, scalability, and data security. The development process follows the Agile/Scrum model (2 weeks/sprint), with MVP completion time within 2 months.

### 2. Problem Statement

#### What’s the Problem?

Current weather stations require manual data collection, becoming unmanageable with multiple units. There is no centralized system for real-time data or analytics, and third-party platforms are costly and overly complex.

**Solution**  
The solution uses AWS Cloud combined with microservices architecture to build an automated personal financial management platform, integrating AI in voice processing and bill recognition. The system is deployed on AWS ECS Fargate for backend services (.NET), FastAPI for AI processing, and Next.js for frontend. Compared to popular financial platforms like Money Lover or Misa Money Keeper, this application focuses on complete automation of financial data entry through detailed Vietnamese AI voice-to-text and bill scanning, helping reduce manual operations and errors. The system is suitable for individual users and small groups, and can be expanded when needed for enterprise scale or digital banking applications.

**Benefits and Return on Investment (ROI)**  
The solution brings many practical benefits both technically and in business value:

- Data Entry Automation: Reduces over 70% manual operations through AI voice and bill recognition.
- Increased Accuracy: Limits input errors, ensures financial data integrity (>90% accuracy).
- Improved User Performance: Record and categorize transactions in just seconds, optimizing user experience.
- Cost Savings: Low infrastructure costs thanks to AWS Free Tier utilization until 2026; only estimated ~$60 USD/month for AWS and ~$30 USD for AI compute.
- Fast ROI: Expected payback in 6–12 months, thanks to time savings in data entry and increased operational efficiency.
- Scalability & Integration: Microservices architecture on AWS allows easy addition of features (mobile app, advanced analytics, banking integration).

### 3. Solution Architecture

The system is built on a **microservices architecture** hosted on **AWS Cloud**, combining serverless components, containerized services, and managed databases for scalability and performance.

![Personal Finance Management App Sofware Architecture](/images/2-Proposal/development_architecture.drawio.png)

Users access the **Next.js** web application through **Amazon CloudFront**, with static content hosted in **Amazon S3** and routed via **Amazon Route 53**.
The first layer of security is provided by **AWS WAF**, which protects the system from common web attacks such as SQL injection and XSS.

When users log in, authentication is handled by **Amazon Cognito**, which issues access tokens used by the frontend to call APIs through **Amazon API Gateway**.
The API Gateway routes requests to an **Application Load Balancer (ALB)** via **AWS PrivateLink**, and the ALB forwards them to **Amazon ECS (Fargate)** — where the backend containers are deployed, including:

- **Backend Service**: Handles the core business logic of the system.
- **AI Service (FastAPI)**: Handles invoice processing, voice recognition, and other AI tasks.

The **AI Service** can access files from **Amazon S3** for data processing, then return the results to the **Backend Service** through internal APIs.

Container images are stored in **Amazon ECR**, and the deployment process is fully automated using **GitLab CI/CD pipelines** — including build, push to ECR, and ECS task definition updates.

All logs, metrics, and alerts from ECS, API Gateway, and ALB are collected in **Amazon CloudWatch** for centralized monitoring, while **Amazon SNS** is configured to send automatic notifications when incidents occur.

![Personal Finance Management App Cloud Architecture](/images/2-Proposal/cloud_architecture.drawio.png)

_AWS Services Used_

- _Amazon Route 53_: Domain name and DNS management.
- _AWS WAF_: Protects the system from common web attacks.
- _Amazon CloudFront_: Global content delivery and frontend acceleration.
- _Amazon S3_: Stores static website content and user files (invoices, audio files).
- _Amazon Cognito_: User authentication and access management.
- _Amazon API Gateway_: Entry point for frontend requests, routing traffic to backend services.
- _AWS PrivateLink_: Provides secure, private connectivity between API Gateway and ALB within the VPC.
- _Application Load Balancer (ALB)_: Distributes traffic across backend containers on ECS.
- _Amazon ECS (Fargate)_: Runs containerized backend and FastAPI (AI) services.
- _Amazon ECR_: Container image registry for ECS deployment.
- _Amazon CloudWatch_: Centralized logging, monitoring, and alerting.
- _Amazon SNS_: Sends alerts and notifications during incidents.
- _GitLab CI/CD_: Automates the container build, push, and deploy pipeline to ECS.

### 4. Technical Deployment

_Implementation Phases_

1. _Research and Architecture Design_: Study microservices models and design the overall architecture on AWS (including CloudFront, ECS Fargate, RDS, S3, API Gateway, Cognito) — (January).
2. _Cost Estimation and Optimization_: Use AWS Pricing Calculator to estimate cost and optimize service selection for affordability and ease of deployment — (January–February).
3. _Development, Testing, and Deployment_: Build frontend (Next.js), backend (.NET), and AI service (FastAPI); perform microservice integration testing; deploy the system to AWS via ECS Fargate; and set up monitoring with CloudWatch — (February–March).

_Technical Requirements_

- _Frontend_:
  The **Next.js** web application is hosted on **Amazon S3** and distributed via **CloudFront**, communicating securely with the backend through **API Gateway**.
  User authentication and session management are handled by **Amazon Cognito**, which provides tokens for secured API calls.
- _Backend_:
  Developed in **.NET** (or a similar framework) and deployed on **ECS Fargate**.
  Handles business operations, user interactions, and service orchestration.
  Container images are stored in **ECR** and automatically deployed via **GitLab CI/CD**.
  Load balancing between backend containers is managed by **ALB**.
- _AI Service_:
  Developed in **FastAPI**, responsible for processing invoice images and voice inputs.
  Accesses raw data from **S3**, performs AI inference, and returns results to the **Backend Service** via internal APIs.
- _Cloud Infrastructure_:
  Runs inside a **multi-AZ Amazon VPC**, using **Application Load Balancer** for traffic distribution and **CloudWatch** for observability.
  Containers are stored in **ECR** and deployed through **ECS Fargate**.
  The deployment pipeline is automated using **GitLab CI/CD**.
- _Security_:
  User authentication managed by **Amazon Cognito**.
  Access permissions defined through **IAM Roles** for ECS, S3, CloudWatch, and API Gateway.
  **Security Groups** are tightly configured between ECS, ALB, and other services.
  **AWS WAF** provides web-layer protection against common exploits.

### 5. Timeline & Milestones

- **Pre-internship (Month 0)**: 1 month for planning.
- **Internship (Month 1–3)**:
  - Month 1: Learn AWS and upgrade programming skills.
  - Month 2: Design and adjust architecture.
  - Month 3: Implement, test, and deploy.
- **Post-deployment**: Research mobile development and deploy after month 4.

### 6. Budget Estimation

You can view costs on [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=2f4e6708ef12a3310b2d3955aaf1d4563932d165).

| Service              |                          In Free Tier |                         After Free Tier |
| -------------------- | ------------------------------------: | --------------------------------------: |
| Amazon ECS (Fargate) |                         $0.00 / month |                           $8.00 / month |
| Amazon API Gateway   |                         $0.00 / month |                           $2.00 / month |
| Amazon S3            |                         $0.00 / month |                           $1.00 / month |
| Amazon CloudWatch    |                         $0.00 / month |                           $2.00 / month |
| Amazon Cognito       |                         $0.00 / month |                           $0.00 / month |
| Amazon ECR           |                         $0.00 / month |                           $0.20 / month |
| Amazon Route 53      |                         $1.00 / month |                           $1.00 / month |
| AWS WAF              |                         $0.00 / month |                           $1.00 / month |
| Amazon SNS           |                         $0.00 / month |                           $0.50 / month |
| GitLab CI/CD         |                         $0.00 / month |                           $2.00 / month |
| **Estimated Total**  | **≈ $1.00 / month** (≈ $12.00 / year) | **≈ $17.70 / month** (≈ $212.40 / year) |

### 7. Risk Assessment

**Risk Matrix**

- AI model misrecognition (voice/bill): Medium impact, medium probability.
- AWS connection loss or regional service errors: High impact, low probability.
- Exceeding AWS usage budget: Medium impact, low probability.
- Data synchronization errors between microservices: Medium impact, medium probability.
- User information leakage (Cognito/Database): High impact, low probability.

**Mitigation Strategies**

- **AI**: Improve OCR and voice-to-text models through additional training, regular testing with real data.
- **AWS Region**: Set up multi-AZ deployment and regular RDS database backup.
- **Cost**: Configure **AWS Budget Alert** and optimize ECS, S3 based on actual usage.
- **Microservices**: Use **SQS/RabbitMQ** to ensure asynchronous processing and retry on errors.
- **Security**: Data encryption (AES-256, HTTPS), IAM control following "Least Privilege" principle.

**Contingency Plans**

- If AWS encounters issues: Temporarily switch to local transaction data storage and sync after recovery.
- Restore infrastructure using **AWS CloudFormation** or pre-saved **IaC (Infrastructure as Code)**.
- Keep regular database copies (RDS snapshots) for data loss recovery.

### 8. Expected results of the project

- **Automated financial data entry:** The application helps users avoid manual entry, just take a photo of the invoice or record a voice for the system to automatically classify spending.
- **Intuitive financial management:** Users can view spending charts, monthly reports, and receive savings suggestions based on consumer behavior.
- **Minimal user experience:** Friendly web interface, modern design, optimized for mobile devices and suitable for people new to financial management.
- **Stable, scalable system:** Microservices architecture makes it easy to add new features such as spending reminders, AI predictive analysis, or expand to a mobile app.
- **Low operating costs:** Take advantage of Free Tier AWS and the serverless model to maintain the system at an average cost of < 50 USD/month.
- **Improving development team skills:** Project members have practical access to DevOps processes, CI/CD implementation, and cloud-based application optimization.

### 9. Project limitations

- **Vietnamese AI model is still limited:** The ability to recognize regional voices or handwritten invoices has not yet achieved high accuracy.
- **No separate mobile application:** The MVP version only supports the web platform, there is no native mobile app.
- **User limit:** The current architecture is only optimized for 50–100 active users; when expanding the scale, the infrastructure needs to be restructured.
- **Internet connection dependent:** All processing and storage operations are via the cloud, cannot operate offline.
- **Advanced security system has not been deployed:** Only stops at Cognito authentication and basic encryption, no MFA (Multi-Factor Authentication) or in-depth security logs.