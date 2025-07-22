---
title: "EC2 安全群組設定"
date: 2025-07-22
weight: 2
---

# EC2 安全群組設定

## 什麼是安全群組？

安全群組作為虛擬防火牆，控制 EC2 實例的入站和出站流量。

## 基本原則

### 預設設定
- **入站規則**: 預設拒絕所有流量
- **出站規則**: 預設允許所有流量

### 常見設定

```bash
# SSH 存取 (22 port)
Type: SSH
Protocol: TCP
Port: 22
Source: My IP (你的 IP 位址)

# HTTP 存取 (80 port)
Type: HTTP
Protocol: TCP
Port: 80
Source: 0.0.0.0/0 (所有 IP)

# HTTPS 存取 (443 port)
Type: HTTPS
Protocol: TCP
Port: 443
Source: 0.0.0.0/0 (所有 IP)
```

## 最佳實務

1. **最小權限原則** - 只開放必要的 port
2. **限制來源 IP** - 避免使用 0.0.0.0/0 除非必要
3. **定期檢視規則** - 移除不需要的規則
4. **使用描述** - 為每個規則添加說明

## 常見問題

### 無法 SSH 連線
檢查安全群組是否開放 22 port，並確認來源 IP 設定正確。

### 網站無法存取
確認已開放 80 (HTTP) 或 443 (HTTPS) port。