---
layout: default
title: BTL2 - Mở rộng: Tự viết train loop YOLO
---

[← BTL2](./) | [← Trang Chủ](../)

# 5. Mở rộng: Tự viết train loop YOLO (không dùng của Ultralytics)

Trong notebook `pascal_voc.ipynb`, nhóm triển khai **custom training loop** cho YOLOv8 nhằm kiểm soát chi tiết quá trình backprop và quan sát từng thành phần loss. Điều này giúp linh hoạt hơn khi nghiên cứu tác động của loss, optimizer và augmentation.

<div class="toc">
  <strong>Mục lục</strong>
  <ul>
    <li><a href="#motivation">5.1 Động cơ & khác biệt so với Ultralytics</a></li>
    <li><a href="#loss">5.2 Hàm loss và chuẩn bị target</a></li>
    <li><a href="#training">5.3 Thông số huấn luyện & lịch sử loss</a></li>
    <li><a href="#extensions">5.4 Gợi ý mở rộng</a></li>
  </ul>
</div>

## 5.1 Động cơ & khác biệt

- **Ultralytics** cung cấp `.train()` với pipeline tối ưu, nhưng khó can thiệp sâu vào từng thành phần loss.
- **Custom loop** cho phép tùy chỉnh optimizer, chiến lược log, và quan sát riêng từng loss: `box_loss`, `cls_loss`, `dfl_loss`.

## 5.2 Hàm loss và chuẩn bị target

- Sử dụng `v8DetectionLoss` từ `ultralytics.utils.loss`.
- Target phải chuyển về format phù hợp với YOLOv8 (center + size, chuẩn hóa).
- Custom pipeline hỗ trợ theo dõi loss theo epoch để phân tích hội tụ.

## 5.3 Thông số huấn luyện & lịch sử loss

Thiết lập baseline trong notebook:

- `train_yolo_baseline(epochs=3, batch_size=16, lr=1e-3)`
- Optimizer: **AdamW** (`weight_decay=1e-4`)
- Trích log các thành phần loss sau mỗi epoch.

Bảng lịch sử loss (trích từ `yolo_history.json`, 5 epochs):

| Epoch | Train Loss | Box Loss | Cls Loss | DFL Loss |
| ----- | ---------- | -------- | -------- | -------- |
| 1     | 645.409    | 2.815    | 4.291    | 3.048    |
| 2     | 589.090    | 2.483    | 3.978    | 2.810    |
| 3     | 557.616    | 2.332    | 3.793    | 2.646    |
| 4     | 531.648    | 2.218    | 3.634    | 2.516    |
| 5     | 508.049    | 2.124    | 3.479    | 2.394    |

<div class="callout">
  <strong>Nhận xét:</strong> Loss giảm đều theo epoch, xác nhận custom loop hoạt động ổn định. Tuy nhiên cần bổ sung validation mAP để so sánh trực tiếp với Ultralytics.
</div>

## 5.4 Gợi ý mở rộng

1. Thử thay **optimizer** (SGD + momentum) hoặc schedule (cosine/one-cycle).
2. So sánh **mosaic ON/OFF** để đánh giá ảnh hưởng tới object nhỏ.
3. Thử **imgsz=640** vs **imgsz=512** để kiểm tra trade-off tốc độ và mAP.
4. Thêm log validation mAP để đối chiếu trực tiếp với Ultralytics.

---
[← BTL2](./) | [← Trang Chủ](../)
