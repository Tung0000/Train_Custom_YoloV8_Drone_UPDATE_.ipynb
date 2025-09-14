# Train_Custom_YoloV8_Drone_UPDATE_.ipynb
#เป้าหมาย / Overview

โปรเจกต์นี้เป็นการฝึก (training) โมเดล YOLOv8 สำหรับตรวจจับโดรน (drone detection) ด้วยชุดข้อมูลที่ปรับแต่งเอง (custom dataset) โดยใช้ Ultralytics YOLO รุ่น 8.x บน environment ที่รองรับ GPU — เพื่อให้ได้โมเดลที่สามารถตรวจจับโดรนได้แม่นยำ

โครงสร้างไฟล์ใน repo

#ไฟล์ที่สำคัญ มีดังนี้:

ชื่อไฟล์รายละเอียด


Train_Custom_YoloV8_Drone_update.ipynb หรือไฟล์ notebook	โค้ดหลัก — ตั้งค่าการฝึก, ทำ augmentation, ประเมินผล, inference
best.pt	โมเดลที่ดีที่สุด (weights) หลังจากฝึกเสร็จ
best_int8.tflite	โมเดลที่แปลงเป็น TFLite แบบ 8-bit (quantized)
results.png / results01.csv	กราฟหรือผลลัพธ์ เช่น precision, recall, mAP ฯลฯ
test.mp4	วิดีโอที่ใช้ทดสอบ inference ของโมเดลบนคลิปจริง
README.md	คำอธิบายโดยรวมของโปรเจกต์











#Validating /content/runs/detect/train/weights/best.pt...
#Ultralytics 8.3.199 🚀 Python-3.12.11 torch-2.8.0+cu126 CUDA:0 (Tesla T4, 15095MiB)
#Model summary (fused): 72 layers, 11,125,971 parameters, 0 gradients, 28.4 GFLOPs
                 Class     Images  Instances      Box(P          R      mAP50  mAP50-95): 100% ━━━━━━━━━━━━ 24/24 3.9it/s 6.1s
                   all        745        868      0.933       0.91       0.95      0.548
