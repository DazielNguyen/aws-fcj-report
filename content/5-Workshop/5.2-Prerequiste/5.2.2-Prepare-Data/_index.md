---
title: "Prepare source data"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

#### Overview

Initialize an object storage (S3 Bucket) to hold original documents (PDF, Word, Text). This acts as the "Source of Truth" that the Knowledge Base will access to read, analyze, and synchronize knowledge for the AI.

#### Data Preparation

We will create an S3 Bucket to store original documents, acting as the knowledge source for the Chatbot.

**Step 1. Create S3 Bucket**

- Access the **S3** service from the search bar.
- Click **Create bucket**.
- Configure Bucket information:
  - **Bucket name:** Enter `rag-workshop-<your-name>` (Note: Lowercase, no accents, no spaces. Example: `rag-workshop-nam-2024`).
  - **AWS Region:** Select `N. Virginia us-east-1`.
  - **Object Ownership:** Keep default `ACLs disabled`.
  - **Block Public Access settings:** Keep default (Selected `Block all public access`).
- Scroll to the bottom of the page, Click **Create bucket**.

> ![Image illustrating S3 Bucket creation interface and Region selection](link_anh_create_bucket_o_day)

**Step 2. Upload sample documents**

- In the Buckets list, Click on the **bucket name** you just created.
- Click **Upload**.
- In the Upload interface:
  - Click **Add files**.
  - Select sample document files from your computer (PDF or Word files with text-heavy content are recommended).
- Scroll to the bottom of the page, Click **Upload**.
- When you see the green "Upload succeeded" notification, Click **Close**.

> ![Image illustrating successful file upload interface](link_anh_upload_file_o_day)