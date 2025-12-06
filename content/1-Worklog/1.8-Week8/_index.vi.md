---
title: "Worklog Tuần 8"
date: "2025-10-27"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Hoàn thành các khóa học về NLP (Natural Language Processing)
- Tìm hiểu thêm về FastAPI để chuẩn bị cho dự án sắp tới.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | Hoàn thành Module 01 - Xử lý ngôn ngữ tự nhiên với phân loại và không gian vectơ<br>- Week 01: Phân tích tình cảm với hồi quy logistic<br>- Week 02: Phân tích tình cảm với Naive Bayes<br>- Week 03: Mô hình không gian Vector<br>- Week 04: Dịch máy và Tìm kiếm tài liệu              | 27/10/2025   | 27/10/2025    | [Module 01 - Week 01](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2001/Lessons_Notes_Module_01/Week_01.md)<br>[Module 01 - Week 02](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2001/Lessons_Notes_Module_01/Week_02.md)<br>[Module 01 - Week 03](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2001/Lessons_Notes_Module_01/Week_03.md)<br>[Module 01 - Week 04](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2001/Lessons_Notes_Module_01/Week_04.md) |
| 3   | Hoàn thành Module 02 - Xử lý ngôn ngữ tự nhiên với mô hình xác suất<br>- Week 01: Tự động sửa lỗi và Khoảng cách chỉnh sửa tối thiểu<br>- Week 02: Gắn thẻ từ loại và mô hình Markov ẩn<br>- Week 03: Autocomplete and Language Models<br>- Week 04: Word Embeddings with Neural Network | 28/10/2025   | 28/10/2025    | [Module 02 - Week 01](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2002/Lessons_Notes_Module_02/Week_01.md)<br>[Module 02 - Week 02](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2002/Lessons_Notes_Module_02/Week_02.md)<br>[Module 02 - Week 03](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2002/Lessons_Notes_Module_02/Week_03.md)<br>[Module 02 - Week 04](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2002/Lessons_Notes_Module_02/Week_04.md) |
| 4   | Hoàn thành Module 03 - Xử lý ngôn ngữ tự nhiên với mô hình chuỗi<br>- Week 01: Recurrent Neural Network cho Language Modeling<br>- Week 02: LSTMs và Named Entity Recognition<br>- Week 03: Siamese Networks                                                                             | 29/10/2025   | 29/10/2025    | [Module 03 - Week 01](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2003/Lessons_Notes_Module_03/Week_01.md)<br>[Module 03 - Week 02](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2003/Lessons_Notes_Module_03/Week_02.md)<br>[Module 03 - Week 03](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2003/Lessons_Notes_Module_03/Week_03.md)                                                                                                                            |
| 5   | Hoàn thành Module 04 - Xử lý ngôn ngữ tự nhiên với các mô hình chú ý<br>- Week 01: Neural Machine Translation<br>- Week 02: Tóm tắt văn bản<br>- Week 03: Question Answering                                                                                                             | 30/10/2025   | 30/10/2025    | [Module 04 - Week 01](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2004/Lessons_Notes_Module_04/Week_01.md)<br>[Module 04 - Week 02](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2004/Lessons_Notes_Module_04/Week_02.md)<br>[Module 04 - Week 03](https://github.com/DazielNguyen/NLP301c/blob/main/Module%2004/Lessons_Notes_Module_04/Week_03.md)                                                                                                                            |
| 6   | - Học cách triển khai một một hình ML thành API<br>- Thử xây dựng một ứng dụng với CRUD dùng hoàn toàn bằng FastAPI                                                                                                                                                                      | 31/10/2025   | 31/10/2025    | [Machine_Learning_Model_AS_API](https://github.com/DazielNguyen/Machine_Learning_Model_AS_API)<br>[FastAPI_Built_Application_CRUD](https://github.com/DazielNguyen/FastAPI_Built_Application_CRUD/tree/main)                                                                                                                                                                                                                                                                                             |

### Kết quả đạt được tuần 8:

#### 1. Module 01 - Xử Lý Ngôn Ngữ Tự Nhiên với Phân Loại và Không Gian Vectơ

**Week 01: Phân Tích Tình Cảm với Hồi Quy Logistic**

- Hiểu về binary classification cho sentiment analysis
- Xây dựng model logistic regression từ đầu
- Feature extraction với Bag of Words
- Preprocessing: tokenization, stemming, stop words removal
- Đánh giá model với accuracy, precision, recall

**Week 02: Phân Tích Tình Cảm với Naive Bayes**

- Hiểu về Bayes' Theorem và conditional probability
- Xây dựng Naive Bayes classifier
- So sánh performance với Logistic Regression
- Hiểu về independence assumption
- Laplacian smoothing để xử lý zero probability

**Week 03: Mô Hình Không Gian Vector**

- Vector space models và word representations
- Cosine similarity để đo độ tương đồng
- PCA (Principal Component Analysis) để giảm chiều
- Visualize word embeddings
- Euclidean distance vs Cosine similarity

**Week 04: Dịch Máy và Tìm Kiếm Tài Liệu**

- Word alignment cho machine translation
- Hash tables và locality sensitive hashing
- Document search và information retrieval
- K-nearest neighbors trong NLP
- Transformation matrices cho word translation

#### 2. Module 02 - Xử Lý Ngôn Ngữ Tự Nhiên với Mô Hình Xác Suất

**Week 01: Tự Động Sửa Lỗi và Khoảng Cách Chỉnh Sửa Tối Thiểu**

- Edit distance (Levenshtein distance)
- Dynamic programming cho minimum edit distance
- Spelling correction algorithms
- Probability-based error correction
- N-gram models cho spell checking

**Week 02: Gắn Thẻ Từ Loại và Mô Hình Markov Ẩn**

- Part-of-Speech (POS) tagging
- Hidden Markov Models (HMMs)
- Viterbi algorithm cho sequence labeling
- Transition và emission probabilities
- Training HMMs với tagged corpus

**Week 03: Autocomplete và Language Models**

- N-gram language models (unigram, bigram, trigram)
- Perplexity để đánh giá language models
- Smoothing techniques (Laplace, Add-k)
- Backoff và interpolation
- Building autocomplete systems

**Week 04: Word Embeddings với Neural Networks**

- Continuous Bag of Words (CBOW)
- Skip-gram model
- Word2Vec architecture
- Training word embeddings
- Negative sampling
- Evaluating word embeddings

#### 3. Module 03 - Xử Lý Ngôn Ngữ Tự Nhiên với Mô Hình Chuỗi

**Week 01: Recurrent Neural Networks cho Language Modeling**

- RNN architecture và forward propagation
- Backpropagation through time (BPTT)
- Vanishing và exploding gradient problems
- Language modeling với RNNs
- Text generation với RNNs
- GRU (Gated Recurrent Units)

**Week 02: LSTMs và Named Entity Recognition**

- Long Short-Term Memory (LSTM) architecture
- Cell state, forget gate, input gate, output gate
- Named Entity Recognition (NER) task
- Bidirectional LSTMs
- Training LSTMs cho sequence labeling
- Evaluating NER systems

**Week 03: Siamese Networks**

- Siamese network architecture
- Triplet loss function
- One-shot learning
- Similarity learning
- Applications: question duplicate detection, semantic similarity
- Cosine similarity trong neural networks

#### 4. Module 04 - Xử Lý Ngôn Ngữ Tự Nhiên với Các Mô Hình Chú Ý

**Week 01: Neural Machine Translation**

- Sequence-to-sequence (Seq2Seq) models
- Encoder-decoder architecture
- Attention mechanism
- Teacher forcing
- BLEU score cho machine translation
- Beam search decoding

**Week 02: Tóm Tắt Văn Bản**

- Extractive vs Abstractive summarization
- Seq2Seq với attention cho summarization
- ROUGE scores (ROUGE-1, ROUGE-2, ROUGE-L)
- Coverage mechanism
- Pointer-generator networks
- Handling long documents

**Week 03: Question Answering**

- Question answering systems
- Context-based QA
- Attention mechanisms cho QA
- SQuAD dataset
- Extractive QA models
- End-to-end trainable QA systems

#### 5. FastAPI và Triển Khai Machine Learning Models

**Machine Learning Model as API:**

- Setup FastAPI project structure
- Load và serve ML models
- Request/Response schemas với Pydantic
- Input validation và error handling
- Preprocessing pipelines trong API
- Testing API endpoints
- Dockerize ML API

**FastAPI CRUD Application:**

- RESTful API design principles
- CRUD operations (Create, Read, Update, Delete)
- Database integration (SQLAlchemy)
- Async/await operations
- Authentication và authorization
- API documentation với Swagger/OpenAPI
- Dependency injection trong FastAPI
- File structure best practices:
  - `app/main.py`: Entry point
  - `app/routers/`: API routes
  - `app/models/`: Database models
  - `app/schemas/`: Pydantic schemas
  - `app/crud/`: Database operations
  - `app/db/`: Database configuration

**FastAPI Key Features Mastered:**

- Path parameters và query parameters
- Request body validation
- Response models
- Background tasks
- Middleware
- CORS configuration
- Environment variables
- Testing với pytest

**Tổng kết:** Tuần 8 đã hoàn thành toàn bộ chương trình học về NLP từ cơ bản đến nâng cao, bao gồm 4 modules với các chủ đề từ classification, probabilistic models, sequence models đến attention mechanisms. Nắm vững các kỹ thuật từ traditional methods (Naive Bayes, HMM) đến modern deep learning approaches (RNN, LSTM, Attention). Đồng thời thành thạo FastAPI framework để triển khai ML models thành production-ready APIs với đầy đủ CRUD operations, validation, và best practices. Đã sẵn sàng áp dụng kiến thức NLP và FastAPI vào dự án thực tế.
