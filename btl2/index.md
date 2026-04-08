---
layout: default
title: Báo cáo BTL2 - Pascal VOC 2012
---
[← Trang Chủ](../)

# Báo cáo Bài Tập Lớn 2: Phát Hiện Vật Thể (Pascal VOC 2012)

Mục tiêu của báo cáo này là trình bày toàn bộ pipeline phát hiện vật thể trên **Pascal VOC 2012**, từ EDA, chuẩn bị dữ liệu, xây dựng mô hình, đến đánh giá và so sánh hai phương pháp chính: **YOLOv8 Nano (Ultralytics)** và **Faster R-CNN (ResNet50 FPN)**.

## Dataset Summary

- **Total images:** 17,125  
- **Bounding boxes:** 40,138  
- **Classes:** 20  
- **Objects / image:** 2.34  

<div class="callout">
    <strong>Insight nhanh:</strong> Lớp <code>person</code> chiếm ~43% tổng object (imbalance ~25x). Phân bố tâm bbox tập trung ở vùng giữa ảnh, phù hợp với prior của các mô hình YOLO và Faster R-CNN.
</div>

<div class="toc">
    <strong>Mục lục</strong>
    <ul>
        <li><a href="./eda.html">1. EDA: Bài toán & Dataset</a></li>
        <li><a href="./data_pipeline.html">2. Dataset, DataLoader & Augmentation</a></li>
        <li><a href="./methods.html">3. Xây dựng, huấn luyện, đánh giá & so sánh mô hình</a></li>
        <li><a href="./experiments.html">4. Kết quả thực nghiệm & thảo luận</a></li>
        <li><a href="./extended.html">5. Mở rộng: tự viết train loop YOLO</a></li>
    </ul>
</div>

## Tóm tắt phương pháp

| Mô hình          | Kiến trúc                | Điểm mạnh                            | Hạn chế                                       |
| ---------------- | ------------------------ | ------------------------------------ | --------------------------------------------- |
| **YOLOv8 Nano**  | 1-stage, anchor-free     | Nhanh, ít tham số, phù hợp real-time | mAP thấp hơn với object nhỏ, khó cân bằng lớp |
| **Faster R-CNN** | 2-stage (RPN + RoI Head) | mAP50 cao hơn, định vị ổn định       | Chậm hơn, tốn VRAM                            |

## So sánh nhanh (Val set)

| Metric                 | YOLOv8 Nano   | Faster R-CNN |
| ---------------------- | ------------- | ------------ |
| **mAP50**              | 0.746         | **0.758**    |
| **mAP50-95**           | **0.555**     | 0.508        |
| **Tham số**            | ~3.0M         | ~41M         |

## Video Demo & Thuyết Trình
- **Video Demo:** [Link](https://youtu.be/QjHL0zFC1Gs)
- **YouTube Presentation:** [Link](https://youtu.be/AnbZ-kEVD78)
- **Source Code:** [GitHub Repo](https://github.com/bngiahuy/DL-ComputerVision-HCMUT-252/btl2)

---
[Quay lại Trang Chủ](../)
