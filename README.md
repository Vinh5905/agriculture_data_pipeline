/agriculture_data_pipeline/
|
├── 📂 data/
|   ├── 📂 raw/
|   |   └── 📄 original_document.pdf
|   ├── 📂 processed/
|   |   └── 📄 chunks.json
|   └── 📂 extracted_graph/
|       └── 📄 graph_data_1.json
|
├── 📂 src/
|   ├── 📂 components/
|   |   ├── 📄 1_chunking.py
|   |   ├── 📄 2_graph_extractor.py
|   |   └── 📄 3_graph_importer.py
|   ├── 📂 core/
|   |   ├── 📄 graph_db.py
|   |   └── 📄 llm_client.py
|   ├── 📂 agent/
|   |   ├── 📄 chain.py
|   |   └── 📄 agent_server.py
|   └── 📄 config.py
|
├── 📂 notebooks/
|   └── 📄 01_test_extraction_prompt.ipynb
|
├── 📄 .env
├── 📄 docker-compose.yml
├── 📄 requirements.txt
└── 📄 README.md

* **`data/`** : Chứa toàn bộ dữ liệu của dự án.
* **`raw/`** : Để lưu trữ các file tài liệu gốc (PDF, DOCX...).
* **`processed/`** : Chứa dữ liệu đã qua xử lý, ví dụ file `chunks.json` sau khi bạn đã tách văn bản.
* **`extracted_graph/`** : Lưu các file JSON chứa cấu trúc đồ thị (nodes, relationships) được trích xuất bởi LLM.
* **`src/`** : Chứa toàn bộ mã nguồn chính của ứng dụng.
* **`components/`** : Gồm các script xử lý theo từng bước (pipeline).
  * `1_chunking.py`: (Bạn đã làm rồi) Script để đọc file PDF và chunking dữ liệu.
  * `2_graph_extractor.py`: Script đọc các chunks, gọi LLM để trích xuất ra cấu trúc graph và lưu thành file JSON.
  * `3_graph_importer.py`: Script đọc các file JSON chứa cấu trúc graph và nạp (import) vào database Neo4j.
* **`core/`** : Chứa các module cốt lõi, kết nối tới dịch vụ bên ngoài.
  * `graph_db.py`: Thiết lập và quản lý kết nối tới Neo4j.
  * `llm_client.py`: Thiết lập và quản lý kết nối tới API của LLM (OpenAI, Gemini...).
* **`agent/`** : Chứa logic của RAG Agent.
  * `chain.py`: Nơi định nghĩa chuỗi xử lý (chain) của LangChain/LlamaIndex, chuyển câu hỏi người dùng thành truy vấn Cypher và sinh câu trả lời.
  * `agent_server.py`: Tạo một API endpoint (sử dụng FastAPI) để có thể "giao tiếp" với agent.
* `config.py`: Đọc các biến môi trường và cấu hình chung cho dự án (API keys, DB credentials).
* **`notebooks/`** : Dành cho các file Jupyter Notebook để thử nghiệm, phân tích, và tinh chỉnh (ví dụ: thử nghiệm prompt).
* **`.env`** : **(Rất quan trọng)** File này chứa các thông tin nhạy cảm như API keys, mật khẩu database. **Không bao giờ đưa file này lên Git.**
* **`docker-compose.yml`** : Định nghĩa các dịch vụ cần thiết (ở đây là database Neo4j) để chạy bằng Docker.
* **`requirements.txt`** : Liệt kê tất cả các thư viện Python cần thiết cho dự án.
* **`README.md`** : Mô tả về dự án, cách cài đặt và sử dụng.
