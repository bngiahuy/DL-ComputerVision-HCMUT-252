# Báo cáo Exercise - DL in CV

## Thông Tin Nhóm
- **Giảng viên hướng dẫn:** TS. Lê Thành Sách
- **Nhóm**: group6
- **Thành viên:**

  - Bùi Nguyễn Gia Huy (MSHV: 2570201)
  - Lê Ngọc Minh Thư (MSHV: 2570331)
  - Phạm Minh Quang (MSHV: 2570302)
  - Nguyễn Ngọc Minh (MSHV: 2570111)

---

## Mục tiêu
Folder này bao gồm **5 phần bài tập thực hành** nhằm xây dựng kỹ năng cơ bản trong Deep Learning:

- Xây dựng và so sánh các mô hình phân loại ảnh từ đơn giản đến phức tạp: softmax
regression, MLP, CNN, Vision Transformer (ViT), và mô hình dựa trên LSTM/GRU.

- Tự viết vòng lặp huấn luyện (training loop) bằng PyTorch, sử dụng backward có sẵn
để tính đạo hàm, thay vì chỉ gọi API cấp cao.

- Hiểu cấu trúc bên trong Transformer qua việc tự hiện thực khối TransformerEncoder
từ các phép toán cơ bản.

- Khám phá các cách thiết kế kiến trúc khác nhau: kết hợp CNN–Transformer, các cách
tokenize/embed ảnh khác nhau, và biểu diễn ảnh thành chuỗi cho RNN

Toàn bộ bài tập sử dụng dataset **CIFAR-10** để thực hành trên dữ liệu chuẩn hoá.

---

## Cấu trúc bài tập

### **Phần 1-2:  Xây dựng các mô hình phân loại và Huấn luyện, đánh giá và so sánh**
[Notebook: Part1_2.ipynb](./Part1_2.ipynb)

---

### **Phần 3: Tự hiện thực TransformerEncoder và ViT**
[Notebook: Part3.ipynb](./Part3.ipynb)

---

### **Phần 4: Các kiến trúc kết hợp và cách embed ảnh khác nhau**
[Notebook: Part4.ipynb](./Part4.ipynb)

### **Phần 5: Phân loại ảnh với RNN (LSTM/GRU)**
[Notebook: Part5.ipynb](./Part5.ipynb)

---

## Dữ liệu (Data)

Sử dụng dataset **CIFAR-10** với 60,000 ảnh RGB kích thước 32x32 thuộc 10 lớp khác nhau. Dataset này được chia thành 50,000 ảnh huấn luyện và 10,000 ảnh kiểm tra. Các notebook sẽ tự động download dataset nếu chưa có.

---

## Yêu cầu

**Môi trường**: chỉ Linux có GPU (khuyến khích) hoặc CPU (chạy chậm hơn). Có thể sử dụng Google Colab T4, Kaggle T4, thuê máy ảo GPU, hoặc chạy trên máy cá nhân nếu có GPU.

**Ngôn ngữ:** Python 3.12

**Thư viện:**
- PyTorch
- Torchvision
- NumPy
- Pandas
- Seaborn
- Matplotlib
- Scikit-learn
- tqdm

---

## Hướng dẫn sử dụng

### Chạy từng phần:

1. **Mở Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```

2. **Hoặc dùng VS Code:**
   - Mở file `.ipynb` trong VS Code
   - Chạy từng cell bằng phím `Shift+Enter`

---

## Cấu trúc thư mục

```
exercise/
├── Part1_2.ipynb       # Phần 1-2
├── Part3.ipynb         # Phần 3
├── Part4.ipynb         # Phần 4
├── Part5.ipynb         # Phần 5
├── README.md           # README hướng dẫn
├── *.png/jpg/jpeg               # Hình ảnh minh họa kết quả
```

---

## Lưu ý

- Lần chạy đầu tiên sẽ mất vài phút để tải CIFAR-10 nếu chưa có
- Khuyến khích dùng GPU cho toàn bộ bài tập để tiết kiệm thời gian
- Có thể điều chỉnh `batch_size`, `epochs`,... tùy theo cấu hình của bạn.
- **Thời gian huấn luyện** có thể khác với kết quả của nhóm do phần cứng khác nhau.

---

## Tham khảo

- CIFAR-10 Dataset: https://www.cs.toronto.edu/~kriz/cifar.html
- PyTorch Documentation: https://pytorch.org/docs/
