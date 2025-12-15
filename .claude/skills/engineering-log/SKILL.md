---
name: engineering-log
description: "Work log management for equipment development. Handles SEARCH (retrieve past logs) and CREATE (document new work) modes. Triggers (CN): 工作紀錄、待辦事項、記錄工作、查詢紀錄、昨天做了什麼、故障排除、參數調整. Triggers (EN): work log, daily log, record work, search log, troubleshooting. Coordinated by: project-coordinator."
---

# Engineering Work Log Management
# 工程工作紀錄管理系統

## 快速判斷：SEARCH or CREATE？

```
使用者意圖判斷：

搜尋/查詢/找/看一下/昨天/上週/之前  → SEARCH Mode
記錄/寫/建立/今天做了/完成了        → CREATE Mode
兩者都有（如：看昨天的然後繼續記錄） → SEARCH → CREATE
```

---

## SEARCH Mode

### 觸發詞
- 搜尋、查詢、找、看一下
- 昨天的、上週的、之前有沒有
- 回顧、檢視

### 檔案命名規則
```
工作紀錄_YYYYMMDD.md
例：工作紀錄_20251212.md
```

### 搜尋策略

| 使用者說 | 搜尋方式 |
|---------|---------|
| 「昨天的工作紀錄」| 計算昨天日期 → 搜尋對應檔案 |
| 「上週的紀錄」| 過去 7 天 → 搜尋多個檔案 |
| 「之前處理過 X 嗎」| 關鍵字 X → 搜尋所有紀錄 |
| 「11 月的待辦」| 11 月日期範圍 → 提取待辦章節 |

### 輸出格式

```markdown
## 搜尋結果

**查詢範圍**: [時間或主題]

### 📅 YYYY-MM-DD
**相關內容**:
[僅提取回答問題的部分]

**待辦事項** (如有):
- [ ] ...
```

---

## CREATE Mode

### 觸發詞
- 記錄、寫、建立、新增
- 今天做了、完成了
- 文件化這個問題

### 範本選擇

| 情境 | 範本 |
|------|------|
| 每日結束總結 | Daily Work Log |
| 故障排除紀錄 | Troubleshooting Log |
| 測試結果紀錄 | Test Results Log |

### Daily Work Log 結構

```markdown
# 工作紀錄_YYYYMMDD

## 今日完成項目
[完成的工作，含目標與結果]

## 問題排除
[解決的問題，含症狀、診斷、解法]

## 參數調整
| 項目 | 原值 | 新值 | 原因 |
|------|------|------|------|

## 待辦事項
- [ ] 🔴 [高優先]
- [ ] 🟡 [中優先]
- [ ] 🟢 [低優先]
```

### Troubleshooting Log 結構

```markdown
# 故障排除 - [問題標題]

## 問題概述
[症狀描述，不含診斷猜測]

## 診斷邏輯
[逐步推理過程]

## 解決方案
[具體步驟]

## 驗證測試
[測試結果，至少 10 次循環]

## 預防措施
[避免再發生的方法]
```

---

## 寫作原則

### ✅ DO
- 寫症狀：「原點復歸時 60% 成功，40% 失敗」
- 寫具體參數：「加速度 1000 → 1500 mm/s²（DM1000）」
- 寫驗證次數：「測試 15 次，全部成功」

### ❌ DON'T
- 寫猜測：「應該是編碼器沒電」
- 寫模糊：「調整了參數」
- 寫過早結論：「測試 2 次 OK，問題解決」

---

## 每日工作流程

```
🌅 早上
   └─ SEARCH：看昨天的待辦 → 規劃今天

🔧 工作中
   └─ MIXED：遇到問題 → 搜尋之前有沒有 → 立即記錄新發現

🌙 下班前
   └─ CREATE：記錄今天完成項目 → 列出明天待辦
```

---

## 與 project-coordinator 協作

本 skill 可被 `project-coordinator` 協調。

### 提供給 coordinator
- 工作紀錄內容（完成項目、問題處理、參數調整）
- 待辦事項清單
- 故障排除案例

### 協作情境

| coordinator 請求 | 本 skill 提供 |
|-----------------|--------------|
| 「今天的工作有什麼變動？」| 今日工作紀錄摘要 |
| 「本週完成了什麼？」| 一週紀錄彙整 |
| 「這個問題有紀錄嗎？」| 搜尋相關故障排除 |

### 協作觸發
當使用者說「檢查同步」「週報」「月報」時，由 `project-coordinator` 主導，本 skill 提供工作紀錄資料。

---

## 詳細參考

需要更詳細的範本或指引時，查看：
- `references/search-guide.md` - 搜尋策略詳解
- `references/create-templates.md` - 完整範本
- `references/best-practices.md` - 寫作最佳實踐

---

## 版本記錄

| 版本 | 日期 | 變更 |
|------|------|------|
| v4.0 | 2025-12-12 | 精簡主文件、加入 project-coordinator 協作 |
| v3.1 | 2025-12-03 | Progressive Disclosure 架構 |
