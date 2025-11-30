---
title: "Client Application Integration (Optional)"
date: "2025-09-09"
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Target

Many people think that working with Cloud is just about dry command-line screens. In this section, we will prove the opposite.

You will turn a few lines of Python code into a professional **Chatbot Web Interface (GUI)**, friendly to end-users (similar to the ChatGPT interface) in just a few minutes.

We will use:

- **Backend:** AWS CloudShell.
- **Frontend:** Streamlit.
- **AI Model:** **Claude 3.5 Sonnet**.

#### Implementation Steps

**Step 1: Start CloudShell**

1.  On the top menu bar of the AWS Console, click the **CloudShell** icon `>_`.
2.  Wait for the terminal to start.

> ![Image illustrating CloudShell icon location on the menu bar](link_anh_cloudshell_icon)

**Step 2: Install libraries and prepare code**

1. Install libraries: `pip install streamlit boto3`
1. Create file: `nano app.py`
1. Paste the following code (Remember to replace your `KB_ID`):

```python
import streamlit as st
import boto3

# --- CONFIGURATION ---
# TODO: Replace the ID below with your Knowledge Base ID
KB_ID = "REPLACE_WITH_YOUR_ID"
MODEL_ARN = "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-5-sonnet-20240620-v1:0"

# Initialize Client to connect to AWS
client = boto3.client(service_name='bedrock-agent-runtime', region_name='ap-southeast-1')

st.set_page_config(page_title="Enterprise AI Assistant")
st.title("🤖 Chat with Private Documents")

# Initialize chat history
if "messages" not in st.session_state:
    st.session_state.messages = []

# Display chat history on screen
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# Handle user input
if prompt := st.chat_input("Ask something about your documents..."):
    # 1. Display user question
    st.chat_message("user").markdown(prompt)
    st.session_state.messages.append({"role": "user", "content": prompt})

    # 2. Call AI to process
    with st.chat_message("assistant"):
        message_placeholder = st.empty()
        message_placeholder.markdown("⏳ Reading documents...")

        try:
            # Call Bedrock's RetrieveAndGenerate API
            response = client.retrieve_and_generate(
                input={'text': prompt},
                retrieveAndGenerateConfiguration={
                    'type': 'KNOWLEDGE_BASE',
                    'knowledgeBaseConfiguration': {
                        'knowledgeBaseId': KB_ID,
                        'modelArn': MODEL_ARN
                    }
                }
            )

            # Get the returned result
            answer = response['output']['text']

            # (Optional) Display
```

**Step 3: Update Knowledge Base ID:**:

1. Move the cursor to the line `KB_ID = "...".`
2. Delete the old content and enter your ID (Get it from the Bedrock Console).
3. Save file (Ctrl+O -> Enter) and Exit (Ctrl+X).

**Step 4: Open Web Interface**

This is the step to switch from the console screen to the web interface.

1. At the command line, run the server: `streamlit run app.py --server.port 8080`
2. Look at the top right corner of the CloudShell frame, select the Actions button (square icon).
3. Select Preview Web App.
4. Enter port `8080`.
5. Click Preview.