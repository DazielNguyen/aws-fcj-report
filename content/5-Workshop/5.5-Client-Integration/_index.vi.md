---
title: "Tích hợp ứng dụng Client (Tùy chọn)"
date: "2025-09-09"
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

#### Mục tiêu

Bạn sẽ biến dòng code Python thành một **Giao diện Web Chatbot (GUI)** chuyên nghiệp, thân thiện với người dùng cuối (tương tự như giao diện ChatGPT) chỉ trong vài phút.

Chúng ta sử dụng:

- **Backend:** AWS CloudShell.
- **Frontend:** Streamlit.
- **AI Model:** **Claude 3.5 Sonnet**.

#### Các bước thực hiện

**Bước 1: Khởi động CloudShell**

1.  Tại thanh menu trên cùng của AWS Console, click vào biểu tượng **CloudShell** `>_`.
2.  Đợi terminal khởi động.

> ![Ảnh minh họa vị trí nút CloudShell trên thanh menu](/images/5-Workshop/5.5-Client-Integration/01_CloudShell.jpg)

**Bước 2: Cài đặt thư viện và chuẩn bị code**

1. Cài đặt thư viện `pip install streamlit boto3`
1. Tạo file: `nano app.py`
1. Dán đoạn code sau (Nhớ thay `KB_ID` của bạn):

```python
import streamlit as st
import boto3

# --- CẤU HÌNH ---
# TODO: Thay thế ID bên dưới bằng Knowledge Base ID của bạn
KB_ID = "THAY_ID_CUA_BAN_VAO_DAY"
MODEL_ARN = "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-5-sonnet-20240620-v1:0"

# Khởi tạo Client kết nối AWS
client = boto3.client(service_name='bedrock-agent-runtime', region_name='ap-southeast-1')

st.set_page_config(page_title="Trợ lý AI Doanh Nghiệp")
st.title("Chat với Tài Liệu Riêng")

# Khởi tạo lịch sử chat
if "messages" not in st.session_state:
    st.session_state.messages = []

# Hiển thị lịch sử chat lên màn hình
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# Xử lý khi người dùng nhập câu hỏi
if prompt := st.chat_input("Hỏi gì đó về tài liệu của bạn..."):
    # 1. Hiển thị câu hỏi người dùng
    st.chat_message("user").markdown(prompt)
    st.session_state.messages.append({"role": "user", "content": prompt})

    # 2. Gọi AI xử lý
    with st.chat_message("assistant"):
        message_placeholder = st.empty()
        message_placeholder.markdown("⏳ Đang đọc tài liệu...")

        try:
            # Gọi API RetrieveAndGenerate của Bedrock
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

            # Lấy kết quả trả về
            answer = response['output']['text']

            # (Optional) Hiển thị nguồn trích dẫn
            citations = response['citations'][0]['retrievedReferences']
            if citations:
                doc_uri = citations[0]['location']['s3Location']['uri']
                doc_name = doc_uri.split('/')[-1]
                answer += f"\n\n---\n *Nguồn tham khảo: {doc_name}*"

            message_placeholder.markdown(answer)
            st.session_state.messages.append({"role": "assistant", "content": answer})

        except Exception as e:
            st.error(f"Lỗi: {str(e)}")
```

**Bước 3: Cập nhật Knowledge Base ID**:

1. Di chuyển con trỏ đến dòng `KB_ID = "..."`.
2. Xóa nội dung cũ và điền ID của bạn vào (Lấy trong Bedrock Console).
3. Lưu file (Ctrl+O -> Enter) và Thoát (Ctrl+X).

**Bước 4: Mở giao diện Web**

Đây là bước chuyển từ màn hình console sang giao diện web.

1. Tại dòng lệnh, chạy server: `streamlit run app.py --server.port 8080`
2. Nhìn lên góc phải khung CloudShell, chọn nút Actions (biểu tượng hình vuông).
3. Chọn Preview Web App.
4. Nhập port `8080`
5. Nhấn Preview.