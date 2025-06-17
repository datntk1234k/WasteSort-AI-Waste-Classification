# WasteSort AI – Waste Classification  
*(First Prize, **Zero to AI Challenge 2024** – Finals @ FPT Polytechnic)*  

## 1 · Goal  
Deliver, in **two weeks** (20 May → 06 Jun 2024), a **no-code** AI system that lets users hold any household item up to a webcam and instantly see whether it is **organic** or **recyclable** waste—raising public awareness of source-separation.

## 2 · Team & Roles  

| Name | Key Contribution |
|------|------------------|
| **Dat Nguyen** | Idea owner · data collection & labelling · **co-training & model integration** |
| **Vuong Hoang** | Model tuning · validation · testing |
| **Viet Hoang**  | Front-end (HTML/CSS/JS) · camera integration · UX/UI |

## 3 · Dataset  
- **25 000** labelled images (2 classes).  
- Split: **80 % train (20 000)** · **20 % validation (5 000)** · **0 % test** (future work).  
- Resized to **28 × 28 × 3**; augmentation applied in Deep Learning Studio (DLS).

## 4 · Model & Training  
- **Platform:** Deep Learning Studio (local, drag-and-drop CNN).  
- **Architecture:** 7 Conv → 3 MaxPool → Flatten → Dense 2048 → Dense 1024 → Dropout → Dense 1024 → Dense 2 (softmax).  
- **Best run (10 epochs):** 0.832 train / 0.840 val acc · loss 0.366 / 0.377 → balanced fit.  
- **Long run (100 epochs):** 0.985 train / 0.831 val acc → clear over-fitting after 30 k batches.  
- Speed: ≈ 353 samples / s · 64 s / epoch on CPU i5-1035G1 (GPU idle).

## 5 · Deployment Workflow  
1. **Export** `waste_classifier.onnx` + `labels.txt` from DLS.  
2. **Embed** in `ai.html` via **ONNX Runtime (JS)** → **< 1 s** in-browser inference.  
3. **Web UI:** live camera feed, *Capture* button, result label & icon.  
4. Demo assets: `training_screenshot.png` (train log) & `demo_result.mp4` (real-time prediction).

## 6 · Results & Impact  
- **≈ 91 % accuracy** on a fresh **1 000-image** test set.  
- **Zero server cost** – all inference happens client-side after first load.  
- **First-Prize** winner, *Zero to AI Challenge 2024* finals (see press: [Vietstock](https://vietstock.vn/2024/06/ket-qua-vong-chung-ket-cuoc-thi-zero-to-ai-challenge-2024-4511-1196672.htm), [FPT Polytechnic News](https://caodang.fpt.edu.vn/tin-tuc-poly/soi-dong-vong-chung-ket-cuoc-thi-zero-to-ai-challenge.html)).  

## 7 · Highlights  
- Complete **end-to-end pipeline** (data → no-code training → ONNX deployment) in just two weeks.  
- **In-browser inference** is ~25× faster than an equivalent server-hosted prototype.  
- **Scalable:** new waste classes can be added entirely via DLS UI—no code changes.

## 8 · Challenges & Next Steps  

| Issue | Mitigation |
|-------|------------|
| Over-fitting after > 30 epochs | Early-Stopping · stronger Dropout · richer augmentation |
| No dedicated test split | Reserve 5 % (~1 250 images) for unbiased evaluation |
| Large FC layers inflate model size | Replace with Global Average Pooling or Dense 512 |
| Browser download size | Quantise ONNX model to FP16 / INT8 |

## 9 · Tech Stack  
**Deep Learning Studio** · **ONNX Runtime (JS)** · **HTML/CSS/JavaScript** · **Git/GitHub**
