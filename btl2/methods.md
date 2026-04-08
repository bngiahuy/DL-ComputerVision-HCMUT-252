---
layout: default
title: BTL2 - Xây dựng, huấn luyện & đánh giá
---

[← BTL2](./)

# 3. Xây dựng, huấn luyện, đánh giá & so sánh

Phần này mô tả hai pipeline chính: **YOLOv8 Nano (Ultralytics)** và **Faster R-CNN (ResNet50 FPN)**. Mỗi pipeline được trình bày theo 4 bước: cấu hình, huấn luyện, đánh giá, và phân tích.

<div class="toc">
  <strong>Mục lục</strong>
  <ul>
    <li><a href="#yolov8">3.1 YOLOv8 Nano (Ultralytics)</a></li>
    <li><a href="#frcnn">3.2 Faster R-CNN (ResNet50 FPN)</a></li>
    <li><a href="#compare">3.3 So sánh kiến trúc & thiết lập</a></li>
  </ul>
</div>

## 3.1 YOLOv8 Nano (Ultralytics)

**Cấu hình chính:**

- Model khởi tạo từ `yolov8n.pt` (pretrained COCO).
- Dataset cấu hình qua `voc_data.yaml` (20 classes).
- Huấn luyện 20 epochs, `imgsz=512`, `batch=32`, `seed=42`.
- Sử dụng `cos_lr=True`, cache dữ liệu theo `disk` để tăng tốc.

**Đánh giá:**

- Ultralytics tự động tính mAP và xuất log theo epoch.
- Kết quả tốt nhất ở cuối epoch: **mAP50 ≈ 0.746**, **mAP50-95 ≈ 0.555**.

## 3.2 Faster R-CNN (ResNet50 FPN)

**Cấu hình chính:**

- Model khởi tạo từ `fasterrcnn_resnet50_fpn(pretrained=True)`.
- **num_classes = 21** (20 lớp + background).
- Label offset: `labels = labels + 1`.

**Training settings:**

- Epochs: 20, batch size: 8.
- Optimizer: `SGD(lr=0.005, momentum=0.9, weight_decay=5e-4)`.
- Scheduler: `StepLR(step_size=5, gamma=0.5)`.
- Transform: resize + pad 512x512, normalize `[0,1]` (không dùng ImageNet mean/std).

**Đánh giá:**

- Tính mAP bằng `torchmetrics.detection.MeanAveragePrecision`.
- Kết quả: **mAP50 = 0.758**, **mAP50-95 = 0.508**.

## 3.3 So sánh kiến trúc & thiết lập

| Tiêu chí   | YOLOv8 Nano                | Faster R-CNN                          |
| ---------- | -------------------------- | ------------------------------------- |
| Kiến trúc  | 1-stage, anchor-free       | 2-stage (RPN + RoI Head)              |
| Backbone   | CSPDarknet                 | ResNet50 + FPN                        |
| Tham số    | ~3.0M                      | ~41M                                  |
| Cách label | YOLO format (cx, cy, w, h) | VOC absolute (xmin, ymin, xmax, ymax) |
| Ưu điểm    | Nhanh, nhẹ                 | mAP50 cao hơn                         |
| Nhược điểm | Khó với object nhỏ         | Chậm, tốn VRAM                        |

<div class="callout">
  <strong>Kết luận nhanh:</strong> YOLOv8 Nano phù hợp real-time nhờ tốc độ cao và tham số nhỏ. Faster R-CNN đạt mAP50 tốt hơn nhưng chi phí tính toán lớn.
</div>

---
[← BTL2](./)
