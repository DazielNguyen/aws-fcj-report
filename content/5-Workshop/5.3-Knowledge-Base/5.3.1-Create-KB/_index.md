---
title: "Initialize Knowledge Base"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

#### Goal

We will use the Amazon Bedrock Wizard to set up the entire RAG architecture. This process will connect the S3 data source, the Embedding model, and automatically initialize the Vector storage (OpenSearch Serverless).

#### Implementation Steps

1.  Log in to the **AWS Management Console** and access the **Amazon Bedrock** service.
2.  In the left-hand menu, select **Knowledge bases**.
3.  Click the **Create knowledge base** button in the top right corner of the screen.

> ![Image illustrating Create Knowledge Base button on Bedrock interface](link_anh_create_kb_button)

**Step 1: Configure Knowledge Base**

On the first configuration screen:

1.  **Knowledge base name:** Enter a name for the knowledge base (E.g., `kb-workshop-<your-name>`).
2.  **IAM permissions:** Select the option **Create and use a new service role**.
3.  **Service role name:** Keep the default value suggested by AWS (starting with `AmazonBedrockExecutionRoleForKnowledgeBase_...`).
4.  Click **Next**.

> ![Image illustrating Step 1: Enter KB name and select IAM Role](link_anh_step1_details)

**Step 2: Configure Data Source**

Connect to the S3 Bucket containing the documents:

1.  **Data source name:** Enter a data source name (E.g., `s3-datasource`).
2.  **S3 URI:**
    - Click the **Browse S3** button.
    - In the pop-up window, select the bucket `rag-workshop-<your-name>` you created in the previous section.
    - Click **Choose**.
3.  Click **Next**.

> ![Image illustrating Step 2: Select S3 Bucket as data source](link_anh_step2_datasource)

**Step 3: Storage & Processing**

This is the most critical step to define the AI model and vector storage location:

1.  **Embeddings model:**
    - Click **Select model**.
    - Select model: **Titan Embeddings G1 - Text v2**.
2.  **Vector database:**
    - Select option: **Quick create a new vector store - Recommended**.
    - _Note:_ This option allows AWS to automatically create an **Amazon OpenSearch Serverless** cluster to store data, saving you from manual infrastructure management.
3.  Click **Next**.

> ![Image illustrating Step 3: Select Titan Embeddings v2 and Quick Create Vector Store](link_anh_step3_storage)

**Step 4: Review and Create Knowledge Base**

1.  Review all configuration information on the Review page.
2.  Ensure the S3 URI and Model items are correct.
3.  Scroll to the bottom of the page and click the **Create knowledge base** button.

> ![Image illustrating Step 4: Review screen and Create button](link_anh_step4_review)

**Step 5: Wait for Initialization**

After clicking Create, the system will begin the background infrastructure initialization process for the Vector Store.

- **Wait time:** Approximately **2 - 5 minutes**.
- **Note:** Please do not close the browser during this time.
- **Success:** When the screen displays a green notification **"Knowledge base created successfully"**, you have completed this step and are ready for the next section.

> ![Image illustrating green success notification screen](link_anh_step5_success)