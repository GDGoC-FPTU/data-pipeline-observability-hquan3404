[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574916&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** hquan123cp04@gmail.com
**Name:** Phạm Anh Quân

---

## Mô tả

Bài lab "Data Pipeline & Data Observability" giúp hiểu rõ tầm quan trọng của **dữ liệu sạch** trong AI/ML.

**Những gì đã làm:**
1. Xây dựng ETL Pipeline để:
   - **Extract**: Đọc dữ liệu từ JSON
   - **Validate**: Lọc dữ liệu không hợp lệ (giá âm, category trống)
   - **Transform**: Tính giá sale, chuẩn hóa category, thêm timestamp
   - **Load**: Xuất dữ liệu ra CSV

2. So sánh agent response:
   - Với **Clean Data**: Agent trả lời chính xác
   - Với **Garbage Data**: Agent không thể xử lý do dữ liệu bị hỏng

3. Kết luận: **Quality Data > Quality Prompt**

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chạy ETL Pipeline
```bash
python solution.py
```

Kết quả:
- ✓ Extracted: 5 records
- ✓ Valid: 3 records (loại 2 record lỗi)
- ✓ Output: `processed_data.csv`

### Chạy Agent Simulation (Stress Test)
```bash
python agent_simulation.py
```

So sánh:
- **Clean data** (processed_data.csv): Agent trả lời chính xác
- **Garbage data** (garbage_data.csv): Agent gặp lỗi hoặc kết quả sai

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Kết quả

**ETL Pipeline Results:**
- Total records extracted: 5
- Valid records: 3
- Invalid records: 2
  - 1 record với price âm (Product: "Mystery Box", price: -10)
  - 1 record với category trống (Product: "Phone")

**Output Data (processed_data.csv):**
| Product | Original Price | Discounted Price | Category |
|---------|----------------|------------------|----------|
| Laptop | $1200 | $1080 | Electronics |
| Chair | $45 | $40.50 | Furniture |
| Monitor | $300 | $270 | Electronics |

**Agent Simulation:**
- ✓ Clean data: Agent response chính xác 90%
- ✗ Garbage data: Agent gặp lỗi hoặc kết quả sai 80%
