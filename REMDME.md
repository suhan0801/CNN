# CNN 模型研究專案

這個專案主要是進行 **CNN 模型相關研究**，重點包含：

- 利用 **LeNet-5** 研究模型架構  
- 聲音模型的 CNN 分析  
- 嘗試修改模型架構與層數  
- **Saliency Map**（像素梯度分析）  
- **Grad-CAM**（卷積層特徵視覺化）  
- 使用 Python 與 **Mediapipe** 進行資料處理

---

## 1️⃣ 視覺化分析

在本專案中，我們透過 **Saliency Map** 和 **Grad-CAM** 來理解模型的內部運作：

### Saliency Map
- 根據輸入影像對模型輸出影響的梯度，找出重要像素。  
- 可觀察模型對哪個區域最敏感，幫助理解模型的決策依據。

### Grad-CAM
- 使用卷積層的特徵圖與梯度計算，生成輸出結果對應的熱力圖。  
- 可視化模型對不同區域的關注程度，更直觀地呈現模型特徵。



## 2️⃣ 模型分析

本專案包含不同模型及修改實驗，以下為 **LeNet-5** 分析結果。

### LeNet-5 模型架構與輸出尺寸

| 層名稱 | 輸出形狀 |
|--------|-----------|
| conv1  | torch.Size([1000, 6, 24, 24]) |
| conv2  | torch.Size([1000, 16, 8, 8]) |
| fc1    | torch.Size([1000, 120]) |
| fc2    | torch.Size([1000, 84]) |
| fc3    | torch.Size([1000, 10]) |

**訓練參數：**
- 優化器：Adam  
- 學習率：0.01  
- 訓練 Epoch：20  

**測試結果：**
- Average loss: 0.0000667  
- Accuracy: 9887/10000 (99%)

---

### 模型訓練曲線
#### 正確率與 Loss
<img width="1189" height="490" alt="Accuracy & Loss" src="https://github.com/user-attachments/assets/7a5762cb-bae9-4b4f-b8d3-84c1f2e5114a" />

---

### 特徵圖可視化

#### fc1
<img width="526" height="435" alt="fc1 Features" src="https://github.com/user-attachments/assets/f2e75463-69c5-48cd-9ea7-c80ebf4481f4" />

#### fc2
<img width="526" height="435" alt="fc2 Features" src="https://github.com/user-attachments/assets/969cd7cc-4017-46c2-ae32-9f78aba686e9" />

#### fc3
<img width="526" height="435" alt="fc3 Features" src="https://github.com/user-attachments/assets/6132d234-9fa5-4dfb-bbf9-c4562381058c" />

---

### Saliency Map Overlay
<img width="389" height="411" alt="Saliency Map" src="https://github.com/user-attachments/assets/49b821df-4213-475f-9df2-793e3f7e4dd0" />
<img width="389" height="411" alt="Saliency Map1" src="https://github.com/user-attachments/assets/95efd82c-6f82-47e7-8118-339c7cbc1e4b" />

---

### Grad-CAM Overlay
<img width="389" height="389" alt="Grad-CAM Overlay" src="https://github.com/user-attachments/assets/05203814-f57c-4358-88f2-a132f47bfb8b" />

---

### 觀察與分析
> 先保留
---

## 3️⃣ 資料處理與工具

- **Python**：主要程式語言  
- **PyTorch**：模型建立與訓練  
- **Mediapipe**：手部或姿勢關鍵點資料處理  
- **Matplotlib / Seaborn**：視覺化分析  
- **Numpy / Pandas**：資料整理與計算

---

📌 **小結**
本專案透過 CNN 模型架構、視覺化分析與實驗修改，深入理解模型內部運作與特徵學習能力，並提供手寫數字與聲音辨識的實作範例。
