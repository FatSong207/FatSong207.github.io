---
title: "EC2 計費"
weight: 6
date: 2025-07-22
description: "Amazon EC2 定價模式比較，包含隨需、預留、Spot 等不同計費方式的優缺點。"
toc: true
---

# Amazon EC2 定價模式比較

## 定價模式總覽

| 定價模式 | 適用場景 | 成本節省 | 靈活性 | 風險 |
|---------|---------|---------|--------|------|
| **隨需執行個體** | 短期、不可預測的工作負載 | 無折扣 | 最高 | 無 |
| **預留執行個體** | 長期、穩定的工作負載 | 最多 72% | 中等 | 低 |
| **Savings Plans** | 需要靈活性的長期工作負載 | 最多 72% | 高 | 低 |
| **Spot 執行個體** | 可中斷的背景任務 | 最多 90% | 低 | 高 |
| **專用主機** | 需要專用硬體或授權合規 | 無折扣 | 低 | 無 |

---

## 詳細說明

### 1. 隨需執行個體 (On-Demand Instances)

**適用場景：**
- 不可中斷的短期不定期工作負載
- 開發和測試應用程式
- 使用模式無法預測的應用程式

**特點：**
- 無需預付成本或最低合約
- 持續執行直至主動停止
- 按使用的運算時間付費
- **不適合**持續一年或以上的工作負載

---

### 2. 預留執行個體 (Reserved Instances)

**類型：**
- **標準預留執行個體**：適合穩定狀態應用程式
- **可轉換預留執行個體**：適合需要靈活性的場景

**特點：**
- 1 年或 3 年期合約（3 年期節省更多）
- 需要指定執行個體類型和大小
- 可選擇指定可用區域獲得容量預留
- 期限結束後可繼續使用，但需支付隨需費率

**適用場景：**
- 知道穩定狀態應用程式所需的 EC2 執行個體類型和大小
- 計劃在特定 AWS 區域執行
- 需要容量保證

**限制：**
- 綁定特定執行個體類型和大小
- 無法輕易更改規格
- 如果需求變化，可能造成浪費

---

### 3. EC2 執行個體 Savings Plans

**特點：**
- 1 年期或 3 年期每小時支出承諾
- 最多可節省 72% 費用
- 無需事先指定執行個體類型和大小
- 在所選區域的執行個體系列中靈活使用
- 不包含容量預留選項

**適用場景：**
- 需要在承諾期限內擁有靈活性
- 不確定具體的執行個體類型和大小
- 希望獲得類似預留執行個體的折扣

**優勢：**
- 可在同一執行個體系列內自由切換
- 可更改執行個體大小
- 可更改作業系統
- 可在不同可用區域間移動

---

### 4. Spot 執行個體

**特點：**
- 利用未使用的 Amazon EC2 運算容量
- 最多可節省 90% 成本
- 可能被中斷（當容量不足或需求增加時）
- 適合可承受中斷的工作負載

**適用場景：**
- 背景處理任務
- 資料處理任務
- 啟動和結束時間較彈性的工作負載
- **不適合**需要穩定性的應用程式

---

### 5. 專用主機 (Dedicated Hosts)

**特點：**
- 完全專供您使用的實體伺服器
- 可使用現有的軟體授權
- 協助維持授權合規
- 在所有 EC2 選項中價格最高

**適用場景：**
- 需要專用硬體
- 需要維持軟體授權合規
- 對硬體隔離有特殊要求

---

## 選擇建議

1. **短期測試/開發** → 隨需執行個體
2. **長期穩定工作負載** → 預留執行個體
3. **需要靈活性的長期工作負載** → Savings Plans
4. **可中斷的背景任務** → Spot 執行個體
5. **需要專用硬體或授權合規** → 專用主機

---

## 預留執行個體 vs Savings Plans 詳細比較

### 實際例子

**預留執行個體場景：**
```
您購買了 m5.xlarge Linux 預留執行個體
↓
只能使用 m5.xlarge Linux 執行個體
↓
如果需要 m5.2xlarge 或 Windows 執行個體
↓
需要額外購買或支付隨需費用
```

**Savings Plans 場景：**
```
您購買了 M5 系列 Savings Plans
↓
可以使用任何 M5 系列執行個體：
- m5.small, m5.large, m5.xlarge, m5.2xlarge
- Linux 或 Windows
- 任何可用區域
↓
完全靈活，無需額外費用
```

### 選擇建議

**選擇預留執行個體當：**
- 您非常確定未來1-3年的需求
- 需要容量保證（避免資源不足）
- 工作負載非常穩定

**選擇 Savings Plans 當：**
- 需求可能會有變化
- 希望保持靈活性
- 不想被特定規格綁定
- 不確定具體需要什麼類型的執行個體

**總結：** Savings Plans 是預留執行個體的「升級版」，提供了相同的成本節省，但大大增加了靈活性。除非您特別需要容量預留功能，否則 Savings Plans 通常是更好的選擇。