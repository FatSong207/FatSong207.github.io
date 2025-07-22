---
title: "Network Load Balancer 設定"
date: 2025-07-22
weight: 2
---

# Network Load Balancer (NLB) 設定

## 什麼是 NLB？

Network Load Balancer 工作在 OSI 第 4 層 (傳輸層)，提供極高效能的 TCP/UDP 流量分發。

## 主要特色

### 超高效能
- 每秒處理數百萬請求
- 極低延遲
- 靜態 IP 支援

### 協定支援
- TCP
- UDP
- TLS

## 適用場景

1. **高效能需求** - 需要極低延遲的應用
2. **靜態 IP** - 需要固定 IP 位址的場景
3. **非 HTTP 協定** - TCP/UDP 應用程式
4. **極大流量** - 每秒數百萬連線

## 設定注意事項

### 健康檢查
```
TCP 健康檢查: 檢查 TCP 連線是否成功
HTTP 健康檢查: 可選，提供更詳細的健康狀態
```

### 目標類型
- **實例** - EC2 實例
- **IP** - 特定 IP 地址 (可跨 VPC)
- **Lambda** - Lambda 函數

## 與 ALB 的比較

| 功能 | NLB | ALB |
|------|-----|-----|
| OSI 層級 | Layer 4 | Layer 7 |
| 協定 | TCP/UDP/TLS | HTTP/HTTPS |
| 效能 | 極高 | 高 |
| 路由能力 | 基礎 | 進階 |
| 成本 | 較低 | 較高 |

## 最佳實務

1. **選擇合適的目標類型**
2. **配置適當的健康檢查**
3. **考慮跨區域負載平衡**
4. **監控連線指標**