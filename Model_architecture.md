CNN 模型架構介紹
## 方法與技術
首先我去研究了LeNet-5架構 發現他是由:

Input: 1 x 28 x 28 (灰階影像)

→ Conv1: 6 filters, 5x5      => 6 x 24 x 24→ Activation: ReLU

→ AvgPool (2x2, stride 2)    => 6 x 12 x 12

→ Conv2: 16 filters, 5x5     => 16 x 8 x 8→ Activation: ReLU

→ AvgPool (2x2, stride 2)    => 16 x 4 x 4

→ Flatten                    => 16*4*4 = 256

→ FC1: 256 -> 120
→ Activation: ReLU

→ FC2: 120 -> 84
→ Activation: ReLU

→ FC3: 84 -> 10 (output logits)

<img width="800" height="239" alt="image" src="https://github.com/user-attachments/assets/eeb0f281-8bbb-4b4f-9fe5-5ef7665bb4cd" />

圖片來源：Y. LeCun, L. Bottou, Y. Bengio, P. Haffner, “Gradient-Based Learning Applied to Document Recognition”, Proc. IEEE, 1998.

在卷積神經網路（CNN）中，主要層次與功能可分為三個部分：

---

## 卷積層（Convolutional Layer, Conv Layer）

**用途：**  
- 提取輸入影像中的「局部特徵」，例如邊緣、角度、紋理等。  
- 每個卷積核（Filter）會掃描整張圖片，生成特徵圖（Feature Map）。  
- 可學習層次化特徵：淺層捕捉低階特徵，深層捕捉高階特徵。

---

## 池化層（Pooling Layer）

**用途：**  
- 將特徵圖縮小，保留主要資訊、去除細微噪音。  
- 幫助模型理解空間概念，使得影像位置或比例改變，模型依舊能辨識。

**常見方法：**
- **最大池化（Max Pooling）**：取區域內最大值，強調最明顯的特徵。  
- **平均池化（Average Pooling）**：取區域平均值，使特徵更平滑。

---

## 線性層（Fully Connected Layer, Linear Layer）

**用途：**  
- 將前面卷積與池化所提取的特徵整合起來，用於最終的分類或回歸任務。  
- 每個輸入節點都與每個輸出節點相連，模擬高維特徵的組合。

---

## 非線性激活函數（Non-linear Activation Function）

**用途：**  
- 打破線性限制，使模型能夠學習更複雜的輸入與輸出關係。  
- 常見函數包括：
  - **ReLU**：保留正值，負值置零，收斂快，隱藏層常用。  
  - **Sigmoid**：輸出 (0,1)，常用於二分類輸出。  
  - **tanh**：輸出 (-1,1)，中心化輸出，梯度消失問題較輕。





