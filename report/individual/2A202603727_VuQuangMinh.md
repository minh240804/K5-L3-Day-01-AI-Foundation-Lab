# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:2A202603727**
- **Họ và tên:Vu Quang Minh**
- **SEED** (in ở ô đầu notebook):

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | x |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính

               precision  recall  F1 (test)  F1 (SUB 40)  \
1. BoW + LogReg (tự code)            0.976   0.804      0.882        0.974   
2. BoW + MLP (deep learning)         0.969   0.922      0.945        1.000   
3a. Encoder (MiniLM) + kNN           0.810   0.961      0.879        1.000   
3b. Encoder (MiniLM) + LogReg        0.933   0.951      0.942        1.000   
3c. Encoder (MiniLM) + MLP head      0.942   0.951      0.946        1.000   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)            2.461      44099.860       0.054   
2. BoW + MLP (deep learning)         4.589      46738.683       0.151   
3a. Encoder (MiniLM) + kNN          90.525         12.748      55.678   
3b. Encoder (MiniLM) + LogReg       90.973         43.874      28.183   
3c. Encoder (MiniLM) + MLP head     91.502         40.566      31.566   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.072           0.0  
2. BoW + MLP (deep learning)          0.173           0.0  
3a. Encoder (MiniLM) + kNN           69.886           0.0  
3b. Encoder (MiniLM) + LogReg        40.746           0.0  
3c. Encoder (MiniLM) + MLP head      52.796           0.0  
• Hàng LLM chỉ đo trên SUB (40 tin) → so sánh chất lượng công bằng bằng cột 'F1 (SUB 40)'.
• SUB chỉ 40 tin: 1 tin sai đổi F1 vài điểm. Chênh < ~0.05 F1 coi như HOÀ — đừng xếp hạng theo số lẻ.
• Inference đo TỪ VĂN BẢN THÔ → NHÃN (gồm cả vectorize / encode). p50/p95 = gọi từng tin một, như một request thật.
• train (s) của 3a/3b/3c = thời gian encoder MiniLM encode tập train (+ train đầu LogReg / MLP); LLM = 0 vì không train. Số đo phụ thuộc CPU/GPU của Colab.

## 3. Dự đoán và thực tế

predict("ml_f1", "f1 ~75%, precision cao hơn recall và lượng")
Precission cao hơn nhưng chưa giải thích. F1 lền đến 98%

predict("ml_lr", "l0.001 khih bước nhảy này quá thấp sẽ khiên model bị đứng yên ở 1 đoạn đồng thời các bước ngắn cũng không thể hiện đươc độ tương phản, đối với lr=50 bước nhảy lớn sẽ khiến 1 số kết quả bị giao động mạnh nhảy qua các điêm quan trọng")  
Đự đoán đúng với các biểu đồ

predict("dl_curve", "val loss không giảm mãi vì không thể chắc chắn các batch sẽ đúng và cải thiện loss,  MLP sẽ hơn ")
Dự đoán đúng với mô hình overfit


## 4. Phân tích 50 case khó


## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
