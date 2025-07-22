---
title: "Application Load Balancer 設定"
date: 2025-07-22
weight: 1
---

# Application Load Balancer (ALB) 設定

## 什麼是 ALB？

Application Load Balancer 工作在 OSI 第 7 層 (應用層)，可以根據 HTTP/HTTPS 請求內容進行路由。

## 主要功能

### 路徑基礎路由
```
example.com/api/* → API 伺服器群組
example.com/web/* → Web 伺服器群組
```

### Host 基礎路由
```
api.example.com → API 伺服器群組
www.example.com → Web 伺服器群組
```

## 設定步驟

### 1. 建立目標群組 (Target Group)
```bash
# 透過 AWS CLI 建立目標群組
aws elbv2 create-target-group \
    --name my-app-targets \
    --protocol HTTP \
    --port 80 \
    --vpc-id vpc-12345678
```

### 2. 註冊目標實例
```bash
# 將 EC2 實例註冊到目標群組
aws elbv2 register-targets \
    --target-group-arn arn:aws:elasticloadbalancing:region:account:targetgroup/my-app-targets \
    --targets Id=i-1234567890abcdef0
```

### 3. 建立 Load Balancer
- 選擇子網路 (至少兩個 AZ)
- 配置安全群組
- 設定監聽器規則

## 健康檢查設定

```
健康檢查路徑: /health
檢查間隔: 30 秒
逾時時間: 5 秒
健康閾值: 2
不健康閾值: 5
```

## 最佳實務

1. **多 AZ 部署** - 至少兩個可用區域
2. **適當的健康檢查** - 確保檢查端點能反映應用狀態
3. **SSL 終止** - 在 ALB 層級處理 SSL
4. **監控設定** - 啟用 CloudWatch 指標