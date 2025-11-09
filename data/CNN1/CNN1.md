## 模型分析


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

整體而言，LeNet-5 模型在本次訓練中表現穩定，Loss 隨著 Epoch 明顯下降，模型收斂良好，最終測試正確率達 99%。
在特徵層部分，fc1 至 fc3 的分佈逐漸由雜亂轉為集中，可看出模型在高維空間中成功區分不同類別，特別是 fc3 已呈現出明確的線性分類邊界。

從 Saliency Map Overlay 可觀察到，模型已能聚焦於數字形狀的主要輪廓區域。例如在辨識數字「9」時，模型對關鍵筆劃處（彎曲與垂直區）展現較高梯度反應，顯示模型確實「學會」了視覺辨識的重點。
Grad-CAM Overlay 進一步顯示模型在卷積層中提取特徵的能力，熱力區域集中於數字主要結構位置，僅有右下角出現局部異常反應，可能反映輸入影像的邊界干擾或局部過擬合現象。
