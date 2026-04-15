# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600252
**Name:** Phạm Anh Quân
**Date:** 03/04/2004

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Agent: Based on my data, the best choice is Laptop at $1200." | 9/10 | Chính xác tìm ra sản phẩm electronics có giá cao nhất |
| Garbage Data (`garbage_data.csv`) | Error hoặc kết quả sai lệch (không thể xử lý price="ten dollars") | 2/10 | Không xử lý được dữ liệu bị hỏng, không thể so sánh giá |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Có 5 vấn đề chính trong dữ liệu "garbage":

1. **Duplicate IDs**: ID "1" xuất hiện 2 lần (Laptop và Banana). Khi agent tìm kiếm, nó sẽ gặp confusion hoặc chỉ trả về một bản ghi, dẫn đến kết quả không đầy đủ.

2. **Sai kiểu dữ liệu**: Cột price có "ten dollars" thay vì số. Agent không thể so sánh `price` để tìm sản phẩm tốt nhất, gây ra lỗi hoặc kết quả sai.

3. **Outliers**: Nuclear Reactor có giá 999999 - rõ ràng không hợp lý. Nếu agent dùng logic "giá cao nhất = tốt nhất", nó sẽ recommend sản phẩm này thay vì Laptop.

4. **Null values**: Dòng cuối có ID trống, category không rõ. Agent sẽ gặp lỗi khi xử lý hoặc bỏ qua dòng này mà không warnings.

5. **Không nhất quán**: Category "electronics" và "fruit" được viết khác nhau. Tìm kiếm "electronic" có thể miss dữ liệu.

Kết quả: Agent không thể trả lời chính xác vì dữ liệu bị hỏng, dù prompt có tốt thế nào đi nữa.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** **CÓ, hoàn toàn đồng ý.**

Kết luận: Dữ liệu sạch là nền tảng. Một agent tốt nhất cũng không thể cứu vãn dữ liệu bị hỏng. Pipeline ETL + Data Validation là bước đầu tiên không thể thiếu trước khi AI xử lý. "Garbage in, garbage out" - nguyên lý vàng của data science.
