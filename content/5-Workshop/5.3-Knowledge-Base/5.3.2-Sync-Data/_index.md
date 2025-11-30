---
title: "Check Vector Store and Data Synchronization"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---

#### Goal

Before the AI can answer, data must be ingested into the vector storage (Vector Store). We will perform a "Before and After" check to clearly see how Bedrock automatically encodes and stores data into OpenSearch.

#### Implementation Steps

**Step 1: Check Vector Store (Empty State)**

We will directly access Amazon OpenSearch Serverless to confirm that no data exists yet.

1.  In the AWS Console search bar, type `OpenSearch` and select **Amazon OpenSearch Service**.
2.  In the left menu, under **Serverless**, select **Collections**.
3.  Click on the Collection name newly created by Bedrock (usually named like `bedrock-knowledge-base-...`).

> ![Image illustrating Collections list in OpenSearch](link_anh_opensearch_collections)

4.  On the Collection details page, click the **Open Dashboard** button (located at the top right of the screen).
    - _Note:_ If asked to log in, use your current AWS credentials.

> ![Image illustrating Open Dashboard button on Collection details page](link_anh_open_dashboard_btn)

5.  In the OpenSearch Dashboard interface:
    - Click the **Menu (3 horizontal lines)** icon in the top left corner.
    - Select **Dev Tools** (usually located at the bottom of the menu list).

> ![Image illustrating Dev Tools selection menu in Dashboard](link_anh_menu_devtools)

6.  In the **Console** pane (on the left), enter the following command to check data:
    ```
    GET _search
    {
      "query": {
        "match_all": {}
      }
    }
    ```
7.  Click the **Play (Run)** button (small triangle next to the command line).
8.  **Result:** Observe the right pane, `hits` -> `total` -> `value` is **0**.

> ![Image illustrating Dev Tools result returning 0 value](link_anh_devtools_empty)

**Step 2: Sync Data**

Now we will trigger Bedrock to read files from S3 and load them into OpenSearch.

1.  Return to the **Amazon Bedrock** tab on the browser.
2.  Select **Knowledge bases** in the left menu and click on the KB name you just created.
3.  Scroll down to the **Data source** section, check the box (tick) next to the data source name (`s3-datasource`).
4.  Click the **Sync** button (Orange).

> ![Image illustrating selecting Data Source and clicking Sync button](link_anh_click_sync_btn)

5.  **Wait:**
    - This process will take **5 - 10 minutes** depending on the sample document size.
    - Wait until the **Sync status** column changes from `Syncing` to `Available`.

> ![Image illustrating successful Sync status Available](link_anh_sync_status_available)

**Step 3: Re-check Vector Store (Populated)**

After Bedrock reports Sync completion, we return to the repository to verify the data has been successfully ingested.

1.  Switch to the **OpenSearch Dashboard** tab (still open from Step 1).
2.  In **Dev Tools**, click the **Play (Run)** button again with the old command:
    ```
    GET _search
    {
      "query": {
        "match_all": {}
      }
    }
    ```
3.  **Result:**
    - The `hits` -> `total` -> `value` section will be greater than **0** (e.g., 10, 20... depending on the number of text chunks).
    - You will see details of the vectors (number arrays) and text content stored in the `_source` field.

> ![Image illustrating Dev Tools result showing synced data](link_anh_devtools_populated)

**Congratulations!** You have completed building the "brain" for the AI. The data has been encoded and sits safely in the Vector Database, ready for retrieval.