# 🪙 YOLO-Coin-Detector

This project applies **YOLOv11s** for object detection of Brazilian coins, with a pipeline for **K-Fold cross-validation training** and a **coin counting & valuation system** that sums the monetary value of detected coins in images and videos.

---

## 📂 Project Structure

- **Dataset Preparation**
  - Dataset labeled with **Label-Studio** (YOLO format).  
  - `images/` and `labels/` folders with all samples.  
  - `classes.txt` containing the list of coin classes.  
  - Automated split into **5 folds** using `scikit-learn` KFold.  
  - **Dataset source:** [Download here](https://drive.google.com/file/d/1LbcCQmxfR5IaBjUuQdXB7rPJCJIrE7_l/view?usp=sharing)  

- **Training (K-Fold with YOLOv11s)**
  - Each fold gets its own `data.yaml` and `hyp.yaml`.  
  - Custom data augmentation (mosaic, mixup, horizontal flips, rotations, scaling).  
  - Model trained for **50 epochs** per fold.  
  - Metrics collected: **mAP50**, **mAP50-95**, precision, recall.  
  - Best fold selected automatically based on validation **mAP50-95**.  
  - Export of the best model to **ONNX** for deployment.  

- **Inference & Coin Value Calculation**
  - Load the best trained YOLO model (`best.pt`).  
  - Run detection on images from the `test_images/` folder.  
  - Bounding boxes and class labels drawn with **OpenCV**.  
  - Each coin class mapped to its monetary value (BRL).  
  - Results saved in a **CSV report** (`relatorio_moedas.csv`) with:
    - Filename  
    - Detected coins  
    - Total monetary value  

- **Video Inference**
  - Load videos from a `test_videos/` folder.  
  - Process each frame with the YOLO model.  
  - Draw bounding boxes and class labels on frames.  
  - Calculate total coin value per video or per frame.  
  - Save processed videos with annotated frames for visualization.  

- **Evaluation & Reporting**
  - Training metrics averaged across folds.  
  - Final CSV report of coin detections per image/video.  
  - Visualizations with detected bounding boxes and coin totals.  

---
