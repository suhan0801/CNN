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
- 學習率：0.005  
- 訓練 Epoch：20  

**測試結果：**
- Average loss: 0.0000549  
- Accuracy: 9875/10000 (99%)

---

### 模型訓練曲線
#### 正確率與 Loss
<img width="1189" height="490" alt="loss" src="https://github.com/user-attachments/assets/3e431fab-c043-4f74-abc1-136562c1d5cf" />


---

### 特徵圖可視化

#### fc1
<img width="526" height="435" alt="fc1" src="https://github.com/user-attachments/assets/418f3d16-f88d-40b7-8109-1cda796cbf8e" />


#### fc2
<img width="526" height="435" alt="fc2" src="https://github.com/user-attachments/assets/b3485d16-5885-4b72-980f-264bf8617bf1" />


#### fc3
<img width="526" height="435" alt="fc3" src="https://github.com/user-attachments/assets/49f306fb-dc2a-4e71-bc6f-9bf53e3747c7" />

---

### 觀察與分析

這次與前一次實驗不同，我將學習率調低。結果顯示，模型的學習曲線確實變得較為平緩，收斂速度下降，但最終的正確率仍維持在高水準。
不過，也能觀察到模型出現輕微的 overfitting 現象：訓練集表現極佳，但測試集的提升幅度相對有限。
比較特別的是，這次的特徵圖顯得相當雜亂，分類邊界不像前一版本那麼清晰，卻依然能達到近乎相同的準確度，顯示模型在高維特徵空間中仍具備強大的辨識能力。

推測原因

1.非線性激活函數的分離能力：ReLU 能夠在高維度特徵中創造多重非線性邊界，使模型即使在特徵雜訊較多時，也能維持有效的分類。

2.Adam 優化器的穩定性：在較低的學習率下，Adam 能根據梯度的歷史資訊自動調整每個參數的更新幅度，因此即使收斂較慢，仍能穩定逼近全域最小值。

3.卷積層的特徵冗餘：CNN 具有高度特徵重疊的特性，即使部分神經元學到的特徵不明顯，其他濾波器仍可能捕捉到足夠的資訊完成分類。
