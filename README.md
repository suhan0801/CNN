# CNN 模型研究專案

模型連結:https://colab.research.google.com/drive/1Jc3DdWGzWf7t-5b9wdv8FqewTxERR3_f?usp=sharing

這個專案主要進行 **CNN 模型相關研究**，重點包含：

- 利用 **LeNet-5** 研究模型架構  
- 嘗試修改模型架構與層數  
- **Saliency Map**（像素梯度分析）  
- **Grad-CAM**（卷積層特徵視覺化）  
- 使用 Python 與 **Mediapipe** 進行資料處理

---

## CNN 模型架構介紹

研究 LeNet-5 架構後，模型設計如下：

**輸入影像**: 1 x 28 x 28 (灰階影像)
Input: 1 x 28 x 28

→ Conv1: 6 filters, 5x5 → 6 x 24 x 24
Activation: ReLU

→ AvgPool (2x2, stride 2) → 6 x 12 x 12

→ Conv2: 16 filters, 5x5 → 16 x 8 x 8
Activation: ReLU

→ AvgPool (2x2, stride 2) → 16 x 4 x 4

→ Flatten → 1644 = 256

→ FC1: 256 → 120
Activation: ReLU

→ FC2: 120 → 84
Activation: ReLU

→ FC3: 84 → 10 (output logits)


<img width="800" height="239" alt="LeNet-5 Architecture" src="https://github.com/user-attachments/assets/eeb0f281-8bbb-4b4f-9fe5-5ef7665bb4cd" />

**圖片來源**：Y. LeCun, L. Bottou, Y. Bengio, P. Haffner, “Gradient-Based Learning Applied to Document Recognition”, Proc. IEEE, 1998.

---

## CNN 層次介紹

### 卷積層（Convolutional Layer, Conv Layer）

**用途：**  
- 提取輸入影像中的「局部特徵」，例如邊緣、角度、紋理等。  
- 每個卷積核（Filter）會掃描整張圖片，生成特徵圖（Feature Map）。  
- 可學習層次化特徵：淺層捕捉低階特徵，深層捕捉高階特徵。

---

### 池化層（Pooling Layer）

**用途：**  
- 將特徵圖縮小，保留主要資訊、去除細微噪音。  
- 幫助模型理解空間概念，使得影像位置或比例改變，模型依舊能辨識。

**常見方法：**
- **最大池化（Max Pooling）**：取區域內最大值，強調最明顯的特徵。  
- **平均池化（Average Pooling）**：取區域平均值，使特徵更平滑。

---

### 線性層（Fully Connected Layer, Linear Layer）

**用途：**  
- 將前面卷積與池化所提取的特徵整合，用於最終的分類或回歸任務。  
- 每個輸入節點都與每個輸出節點相連，模擬高維特徵的組合。

---

### 非線性激活函數（Non-linear Activation Function）

**用途：**  
- 打破線性限制，使模型能夠學習更複雜的輸入與輸出關係。  

**常見函數：**
- **ReLU**：保留正值，負值置零，收斂快，隱藏層常用。  
- **Sigmoid**：輸出 (0,1)，常用於二分類輸出。  
- **tanh**：輸出 (-1,1)，中心化輸出，梯度消失問題較輕。

---

## 視覺化分析方法

理解模型如何「看」影像非常重要，本專案使用 **Saliency Map** 與 **Grad-CAM** 兩種方法來視覺化模型對影像的關注點。

---

### Saliency Map（像素梯度分析）

**用途：**  
- 顯示輸入影像中哪些像素對模型預測最重要。

**原理：**  
- 對模型輸出對應類別的分數，計算對每個輸入像素的梯度大小。  
- 梯度越大表示該像素對預測影響越大。

**特點：**  
- 可快速檢視模型對細節的敏感程度。  
- 適合全局分析輸入層至輸出層。

**示意圖：**  
<img width="389" height="411" alt="Saliency Map" src="https://github.com/user-attachments/assets/49b821df-4213-475f-9df2-793e3f7e4dd0" />

---

### Grad-CAM（Gradient-weighted Class Activation Mapping）

**用途：**  
- 視覺化卷積層對特定類別預測的貢獻。

**原理：**  
- 利用卷積層的輸出特徵圖與該類別對應的梯度加權，生成熱力圖，標示模型「關注」的區域。

**特點：**  
- 可觀察模型在高階特徵層面的注意區域。  
- 比 Saliency Map 更容易理解模型如何決定分類結果，尤其是物體或手寫數字的形狀。

**示意圖：**  
<img width="389" height="389" alt="Grad-CAM Overlay" src="https://github.com/user-attachments/assets/05203814-f57c-4358-88f2-a132f47bfb8b" />

---

## 資料處理與工具

- **Python**：主要程式語言  
- **PyTorch**：模型建立與訓練  
- **Mediapipe**：手部或姿勢關鍵點資料處理  
- **Matplotlib / Seaborn**：視覺化分析  
- **Numpy / Pandas**：資料整理與計算

