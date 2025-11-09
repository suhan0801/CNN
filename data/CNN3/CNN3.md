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
- 學習率：0.05  
- 訓練 Epoch：20  

**測試結果：**
- Average loss: 0.0023064  
- Accuracy: 1135/10000 (11%)

---

### 模型訓練曲線
#### 正確率與 Loss
<img width="1189" height="490" alt="下載" src="https://github.com/user-attachments/assets/70b1450e-5f2e-47e0-90a5-73b8289b4533" />


---

### 特徵圖可視化

#### fc1
<img width="510" height="453" alt="fc1" src="https://github.com/user-attachments/assets/0afd4cf6-8e8d-4e62-87d1-c76ca55b6583" />



#### fc2
<img width="519" height="453" alt="fc2" src="https://github.com/user-attachments/assets/f1638d59-8c31-46c8-884a-caff4dbcf083" />


#### fc3
<img width="539" height="453" alt="fc3" src="https://github.com/user-attachments/assets/3219d94a-495e-4d0a-bf79-18c7eee61b48" />

---
### Saliency Map Overlay
<img width="389" height="411" alt="下載 (2)" src="https://github.com/user-attachments/assets/f04719fd-2750-47f7-a4b9-627a97130cac" />
<img width="389" height="411" alt="下載 (3)" src="https://github.com/user-attachments/assets/06b6bf8e-1598-4753-ad28-4679c8587873" />

---

### Grad-CAM Overlay
<img width="389" height="389" alt="下載 (4)" src="https://github.com/user-attachments/assets/5a80fcbd-8c57-4a1e-a4ee-f1a45de060e6" />

---

### 觀察與分析

這次實驗主要是將學習率調高，結果導致模型無法正常收斂。從訓練曲線可以明顯看到損失值呈現劇烈震盪，準確率也無法穩定上升，整體訓練過程幾乎沒有形成有效的學習趨勢。

在特徵視覺化部分，fc 層的特徵圖呈現出極度雜亂的狀態，無法辨識出任何明顯的群集或結構。進一步觀察 Saliency Map Overlay 與 Grad-CAM Overlay，可以發現模型幾乎沒有成功聚焦於影像的關鍵區域，整張圖呈現出模糊且無規律的熱度分佈。

整體而言，本次實驗結果清楚地顯示：學習率是模型穩定訓練的關鍵超參數之一。過高的學習率會使模型無法學習到任何有意義的特徵，最終導致視覺化與分類結果全面失效。
