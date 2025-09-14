# Train_Custom_YoloV8_Drone_UPDATE_

## เป้าหมาย / Overview
โปรเจกต์นี้เป็นการฝึก (training) โมเดล **YOLOv8** สำหรับตรวจจับโดรน (drone detection) ด้วยชุดข้อมูลที่ปรับแต่งเอง (**custom dataset**) โดยใช้ **Ultralytics YOLO รุ่น 8.x** บน environment ที่รองรับ GPU — เพื่อให้ได้โมเดลที่สามารถตรวจจับโดรนได้แม่นยำ

---

## โครงสร้างไฟล์ใน repo

### ไฟล์ที่สำคัญ มีดังนี้:

| ชื่อไฟล์ | รายละเอียด |
|---|---|
| Train_Custom_YoloV8_Drone_update.ipynb หรือไฟล์ notebook | โค้ดหลัก — ตั้งค่าการฝึก, ทำ augmentation, ประเมินผล, inference |
| best.pt | โมเดลที่ดีที่สุด (weights) หลังจากฝึกเสร็จ |
| best_int8.tflite | โมเดลที่แปลงเป็น TFLite แบบ 8-bit (quantized) |
| results.png / results01.csv | กราฟหรือผลลัพธ์ เช่น precision, recall, mAP ฯลฯ |
| test.mp4 | วิดีโอที่ใช้ทดสอบ inference ของโมเดลบนคลิปจริง |
| README.md | คำอธิบายโดยรวมของโปรเจกต์ |

---

## ขั้นตอนการใช้งาน (Workflow)

1. **เตรียม dataset**  
   - รูปภาพของโดรน + annotation (bounding box)  
   - แบ่งเป็นชุด `train` และ `val`  
   - ใช้ format YOLOv8: `.txt` ระบุ class + bounding box (center_x, center_y, width, height)  

2. **ตั้งค่า config / hyperparameters**  
   - ขนาดภาพ (`imgsz`)  
   - batch size  
   - จำนวน epochs  
   - ปรับแต่ง augmentation, learning rate, optimizer ฯลฯ  

3. **ฝึกโมเดล (Training)**  
   - ใช้ **Ultralytics YOLOv8**  
   - ดู progress: loss, precision, recall, mAP  
   - บันทึกโมเดลที่ดีที่สุด (`best.pt`)  

4. **ประเมินผล (Evaluation)**  
   - วิเคราะห์ผลบนชุด validation  
   - ดู Precision-Recall, mAP@0.5, mAP@0.5-0.95  
   - เปรียบเทียบระหว่าง epoch  

5. **Inference / ทดสอบ**  
   - ใช้โมเดลที่ดีที่สุด ตรวจจับในรูปภาพหรือวิดีโอ (`test.mp4`)  
   - แสดงผล bounding box / class  
   - บันทึกผลลัพธ์หรือคลิปที่ตีกรอบโดรน  

6. **Export / Deployment**  
   - แปลงโมเดลเป็น **TFLite แบบ quantized (int8)** หรือ ONNX  
   - ใช้งานบนอุปกรณ์ edge / มือถือ  

---

## ผลการประเมินโมเดล
Validating /content/runs/detect/train/weights/best.pt...
Ultralytics 8.3.199 🚀 Python-3.12.11 torch-2.8.0+cu126 CUDA:0 (Tesla T4, 15095MiB)
Model summary (fused): 72 layers, 11,125,971 parameters, 0 gradients, 28.4 GFLOPs
Class Images Instances Box(P R mAP50 mAP50-95):
all 745 868 0.933 0.91 0.95 0.548




#ข้อดี / จุดแข็ง

#ใช้ YOLOv8 รุ่นใหม่ที่ performance สูง

#มีการ quantize โมเดลเป็น int8 สำหรับการใช้งานจริง (ลดขนาด / เร่ง inference บนอุปกรณ์เบา)

#มีตัวอย่าง test วิดีโอเพื่อดูผลลัพธ์จริง

#ผลลัพธ์ค่อนข้างดี — mAP50 สูงมาก



#ข้อจำกัด / สิ่งที่ควรปรับปรุง

#mAP@0.5-0.95 อยู่ที่ ~0.548 — ยังมีช่องว่างถ้าต้องการความแม่นยำสูงในทุกช่วง IoU

#Dataset อาจมีจำนวนรูป/instances ยังไม่เยอะมาก — ข้อมูลเพิ่มจะช่วย generalize ดีขึ้น

#ถ้าใช้บนเครื่อง resource จำกัด อาจต้องลด batch size หรือปรับขนาดภาพ

#ควรมี test set แยกต่างหาก เพื่อวัดความ generalization นอกตัวชุด validation
