## 模型分析


### LeNet-5 模型架構與輸出尺寸

LeNet5Pooling(

  ├─ conv1: Conv2d(1, 6, kernel_size=(5, 5), stride=(1, 1))
  
  ├─ conv2: Conv2d(6, 16, kernel_size=(5, 5), stride=(1, 1))
  
  ├─ pool:  AvgPool2d(kernel_size=2, stride=2, padding=0)
  
  ├─ fc1:   Linear(in_features=64, out_features=120, bias=True)
  
  ├─ fc2:   Linear(in_features=120, out_features=84, bias=True)
  
  └─ fc3:   Linear(in_features=84, out_features=10, bias=True)
  
)

**訓練參數：**
- 優化器：Adam  
- 學習率：0.01  
- 訓練 Epoch：20  

**測試結果：**
- Average loss: 0.0000809
- Accuracy: 9843/10000 (98%)

---

### 模型訓練曲線
#### 正確率與 Loss
<img width="1189" height="490" alt="下載 (5)" src="https://github.com/user-attachments/assets/96983ea4-9cb2-43fd-aaf2-91c1d12bf8f1" />




---

### 特徵圖可視化

#### fc1
<img width="526" height="435" alt="fc1" src="https://github.com/user-attachments/assets/6075e213-e904-49fa-a40e-7f6f9d1a1aa9" />



#### fc2
<img width="526" height="435" alt="fc2" src="https://github.com/user-attachments/assets/06973116-bee4-4018-9dd1-9782c5cb0295" />


#### fc3
<img width="526" height="435" alt="fc3" src="https://github.com/user-attachments/assets/a64d9c20-96d1-405a-8ca2-2589ccf8c990" />

---
### Saliency Map Overlay
<img width="389" height="411" alt="下載 (1)" src="https://github.com/user-attachments/assets/266c3e37-c6c0-4c1c-8c7d-f245d64214d4" />
<img width="389" height="411" alt="下載 (2)" src="https://github.com/user-attachments/assets/9b34dd00-e6ef-4bfb-959f-baeda0d50c5f" />

---

### Grad-CAM Overlay
<img width="389" height="389" alt="下載 (3)" src="https://github.com/user-attachments/assets/c6761ac1-ac2f-4665-9e40-7b852eab86ca" />

---

### 觀察與分析

這次實驗的主要變化是在 LeNet-5 架構中加入 Pooling 層，以觀察其對訓練表現與特徵分佈的影響。

從結果來看，整體準確率略低於未使用 Pooling 的版本（約下降 1%），但仍維持在高水準。模型的收斂速度穩定，顯示 Pooling 對訓練並未造成不良影響。

然而在特徵圖的部分可以觀察到明顯差異：

1.特徵值分佈更分散且範圍收縮明顯（從 80～30 壓縮至約 50～−10）。

2.各維度間的數值差距拉大，代表 Pooling 的平均化使得特徵之間不再緊密相似。

推測原因可能包括：

1.Pooling 的平滑化導致細節特徵被弱化。

2.資訊壓縮造成部分關鍵像素失真。

雖能降低過擬合與運算成本，但在此任務中犧牲了一些精度與細節學習能力。

整體來看，這次實驗說明了 Pooling 對模型的「穩定性提升」與「細節喪失」之間的權衡。
