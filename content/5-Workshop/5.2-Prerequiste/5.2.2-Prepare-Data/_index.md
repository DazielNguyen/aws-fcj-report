---
title: "Prepare source data"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

#### Overview

Initialize an object storage (S3 Bucket) to hold original documents (PDF, Word, Text). This acts as the "Source of Truth" that the Knowledge Base will access to read, analyze, and synchronize knowledge for the AI. You can store knowledge related to your field to use in creating your own personal assistant or Chatbot.

#### Data Preparation

We will create an S3 Bucket to store original documents, acting as the knowledge source for the Chatbot.

**Step 1. Create S3 Bucket**

- Access the [S3](https://us-east-1.console.aws.amazon.com/s3/get-started?region=us-east-1) service from the search bar.
- **AWS Region:** Select `United States (N. Virginia us-east-1)`.

> ![Access S3](/images/5-Workshop/5.2-Prerequisite/04_S3.jpg)

- Click **Create bucket**.

> ![Create S3 Bucket](/images/5-Workshop/5.2-Prerequisite/05_S3_Create_Bucket.jpg)

- Configure Bucket information:
    - **Bucket Type:** Click `General purpose`
    - **Bucket name:** Enter `rag-workshop-demo`
    - **Object Ownership:** Keep default `ACLs disabled`.
    - **Block Public Access settings:** Keep default (Selected `Block all public access`).

> ![Configure S3 Bucket](/images/5-Workshop/5.2-Prerequisite/06_Configure_S3_Bucket.jpg)

- Scroll to the bottom of the page, Click **Create bucket**.

> ![Image illustrating S3 Bucket creation interface and Region selection](/images/5-Workshop/5.2-Prerequisite/07_Finished_Create_bucket.jpg)

- Check that the S3 Bucket has been created successfully.

> ![Create S3 Bucket Successful](/images/5-Workshop/5.2-Prerequisite/08_Create_S3_Successful.jpg)


**Step 2. Upload sample documents**

- In the Buckets list, Click on the **bucket name** you just created.
- Click **Upload**.
- In the Upload interface:
  - Click **Add files**.
  - Select sample document files from your computer (PDF or Word files with text-heavy content are recommended).
- Scroll to the bottom of the page, Click **Upload**.
- When you see the green "Upload succeeded" notification, Click **Close**.

> ![Image illustrating successful file upload interface](link_anh_upload_file_o_day)