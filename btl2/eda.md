---
layout: default
title: BTL2 - EDA Pascal VOC 2012
---

[← BTL2](./) | [← Trang Chủ](../)

# 1. EDA: Pascal VOC 2012

Phần EDA tập trung vào việc hiểu cấu trúc dữ liệu, phân bố lớp, đặc trưng bounding box và các yếu tố ảnh hưởng đến huấn luyện/đánh giá mô hình.

<div class="report-grid">
  <div class="kpi">
    <div class="label">Total images</div>
    <div class="value">17,125</div>
  </div>
  <div class="kpi">
    <div class="label">Bounding boxes</div>
    <div class="value">40,138</div>
  </div>
  <div class="kpi">
    <div class="label">Classes</div>
    <div class="value">20</div>
  </div>
  <div class="kpi">
    <div class="label">Objects / image</div>
    <div class="value">2.34</div>
  </div>
  <div class="kpi">
    <div class="label">Difficult</div>
    <div class="value">11.1%</div>
  </div>
  <div class="kpi">
    <div class="label">Truncated</div>
    <div class="value">43.8%</div>
  </div>
</div>

<div class="toc">
  <strong>Mục lục</strong>
  <ul>
    <li><a href="#phan-bo-lop">1.1 Phân bố lớp</a></li>
    <li><a href="#bbox-stats">1.2 Đặc trưng bounding box</a></li>
    <li><a href="#phan-bo-vi-tri">1.3 Phân bố vị trí & số object/ảnh</a></li>
    <li><a href="#properties">1.4 Đặc điểm ảnh</a></li>
    <li><a href="#mau-sac">1.5 Phân bố màu</a></li>
    <li><a href="#cooccurrence">1.6 Đồng xuất hiện lớp</a></li>
  </ul>
</div>

<div class="callout">
  <strong>Insight nhanh:</strong> Lớp <code>person</code> chiếm ~43.4% tổng object, imbalance ~25x (max/min). Điều này tác động trực tiếp đến per-class mAP và cần cân nhắc khi so sánh mô hình.
</div>

## 1.1 Phân bố lớp

<div class="two-col">
  <figure class="figure">
    <img src="./huybui/fig_class_counts.png" alt="Class distribution">
    <figcaption>Phân bố số lượng object theo lớp (trainval).</figcaption>
  </figure>
  <figure class="figure">
    <img src="./huybui/fig_train_val_split.png" alt="Train/val split per class">
    <figcaption>Phân bố object theo train/val cho từng lớp.</figcaption>
  </figure>
</div>

<figure class="figure">
  <img src="./huybui/fig_imbalance_cumulative.png" alt="Class imbalance cumulative">
  <figcaption>Pareto chart thể hiện mức độ mất cân bằng lớp và coverage tích lũy.</figcaption>
</figure>

## 1.2 Đặc trưng bounding box

<div class="two-col">
  <figure class="figure">
    <img src="./huybui/fig_bbox_width.png" alt="BBox width distribution">
    <figcaption>Phân bố chiều rộng bounding box (px).</figcaption>
  </figure>
  <figure class="figure">
    <img src="./huybui/fig_bbox_height.png" alt="BBox height distribution">
    <figcaption>Phân bố chiều cao bounding box (px).</figcaption>
  </figure>
</div>

<div class="two-col">
  <figure class="figure">
    <img src="./huybui/fig_aspect_ratio.png" alt="BBox aspect ratio">
    <figcaption>Tỷ lệ W/H (cắt ngưỡng 5) cho thấy nhiều object rộng hơn cao.</figcaption>
  </figure>
  <figure class="figure">
    <img src="./huybui/fig_bbox_area_per_class.png" alt="Median relative area per class">
    <figcaption>Median diện tích bbox theo lớp, gợi ý sizing anchor/feature map.</figcaption>
  </figure>
</div>

## 1.3 Phân bố vị trí & số object/ảnh

<div class="two-col">
  <figure class="figure">
    <img src="./huybui/fig_center_heatmap.png" alt="BBox center heatmap">
    <figcaption>Heatmap vị trí tâm bbox (chuẩn hóa 0-1).</figcaption>
  </figure>
  <figure class="figure">
    <img src="./huybui/fig_objs_per_image.png" alt="Objects per image distribution">
    <figcaption>Đa số ảnh có &lt; 5 object, một số ảnh đông người có tới 50+ object.</figcaption>
  </figure>
</div>

## 1.4 Đặc điểm ảnh

<div class="two-col">
  <figure class="figure">
    <img src="./huybui/fig_resolution.png" alt="Image resolution distribution">
    <figcaption>Độ phân giải ảnh tập trung quanh các kích thước 500×375 và 375×500.</figcaption>
  </figure>
  <figure class="figure">
    <img src="./huybui/fig_wh_scatter.png" alt="Image width vs height scatter">
    <figcaption>Ảnh có cả hướng ngang và dọc, cần resize/pad ổn định.</figcaption>
  </figure>
</div>

## 1.5 Phân bố màu

<div class="two-col">
  <figure class="figure">
    <img src="./huybui/fig_channel_R.png" alt="Red channel distribution">
    <figcaption>Kênh R: phân bố pixel gần chuẩn ImageNet.</figcaption>
  </figure>
  <figure class="figure">
    <img src="./huybui/fig_channel_G.png" alt="Green channel distribution">
    <figcaption>Kênh G: phù hợp với ImageNet normalization.</figcaption>
  </figure>
</div>

<figure class="figure">
  <img src="./huybui/fig_channel_B.png" alt="Blue channel distribution">
  <figcaption>Kênh B: trung bình thấp hơn R/G, vẫn phù hợp dùng ImageNet mean/std.</figcaption>
</figure>

## 1.6 Đồng xuất hiện lớp

<div class="two-col">
  <figure class="figure">
    <img src="./huybui/fig_cooccurrence_count.png" alt="Co-occurrence count">
    <figcaption>Ma trận đếm đồng xuất hiện, lớp <code>person</code> nổi bật.</figcaption>
  </figure>
  <figure class="figure">
    <img src="./huybui/fig_cooccurrence_prob.png" alt="Conditional co-occurrence">
    <figcaption>Xác suất có điều kiện P(j | i) cho thấy các cặp dễ nhầm.</figcaption>
  </figure>
</div>

<div class="callout">
  <strong>Gợi ý phân tích lỗi:</strong> Các cặp như <code>chair</code> ↔ <code>diningtable</code> và <code>person</code> ↔ <code>bottle</code> thường đồng xuất hiện, nên ưu tiên kiểm tra confusion matrix theo các cặp này.
</div>

---
[← BTL2](./) | [← Trang Chủ](../)
