---
name: project-coordinator
description: "Cross-skill coordination and sync system. Bridges skills to check consistency between work logs, documents, troubleshooting cases. Triggers (CN): 檢查同步、今天該更新什麼、工作有沒有遺漏、整合資訊、週報、月報、進度檢查. Triggers (EN): sync check, what to update, missing work, weekly report, progress check. Connects: engineering-log, equipment-doc-manager, motion-control-troubleshooting, technical-presentation."
---

# Project Coordinator

跨 Skill 協調與同步系統。

## 核心職責

```
1. 資訊路由    - 判斷資訊該通知哪些 skill
2. 同步檢查    - 比對多個 skill 的資料一致性
3. 遺漏偵測    - 從規格反查工作是否完成
4. 報告整合    - 彙整多 skill 產出週報/月報
```

---

## 已註冊 Skills

| Skill | 提供 | 接收 | 狀態 |
|-------|------|------|------|
| engineering-log | 工作紀錄、待辦事項、故障處理 | - | ✅ |
| equipment-doc-manager | 文件規格、層級定義、變動規則 | 工作紀錄 | ✅ |
| motion-control-troubleshooting | 故障案例、診斷流程 | 工作紀錄（新案例）| ✅ |
| technical-presentation | 簡報範本、結構指引 | 工作紀錄、文件規格 | ✅ |

### 新增 Skill 註冊方式

```markdown
在此表格新增一行：
| [skill-name] | [它提供什麼] | [它需要什麼] | ✅ |
```

---

## 功能 1：每日同步檢查

### 觸發詞
- 「檢查今天的同步狀態」
- 「今天該更新什麼文件」
- 「工作紀錄和文件同步嗎」

### 執行流程

```
1. 讀取今日/近期工作紀錄
   ↓
2. 提取關鍵變動
   - 新增硬體（軸、感測器、致動器）
   - 修改參數（DM/MR 位址、數值）
   - 解決問題（故障排除）
   - 完成測試（驗證紀錄）
   ↓
3. 比對文件規格（依 equipment-doc-manager 層級）
   - 20 層：硬體規格是否更新？
   - 30 層：序列是否反映變動？
   - 50 層：記憶體映射是否同步？
   - 80 層：異常代碼是否補充？
   ↓
4. 輸出同步報告
```

### 輸出格式

```markdown
## 同步檢查報告 - YYYY-MM-DD

### 📋 今日工作摘要
[從工作紀錄提取的關鍵項目]

### 📄 文件同步狀態

| 變動項目 | 影響文件 | 狀態 | 建議動作 |
|---------|---------|------|---------|
| 新增 HLight_Z2 軸 | 20-axes-specs.md | ⚠️ 待更新 | 補充軸規格 |
| 新增 HLight_Z2 軸 | 50-plc-memory-map.md | ⚠️ 待更新 | 分配 DM/MR |
| 解決 Conv_Y1 問題 | - | ✅ 無需更新 | - |

### ⏳ 建議優先處理
1. 更新 20-axes-specs.md（新增 HLight_Z2）
2. 更新 50-plc-memory-map.md（分配位址）

### ✅ 已同步項目
- 工作紀錄已記錄 Conv_Y1 故障排除
```

---

## 功能 2：規格反查工作

### 觸發詞
- 「檢查工作有沒有遺漏」
- 「XX 功能做完了嗎」
- 「對照規格檢查進度」

### 執行流程

```
1. 讀取指定文件的規格要求
   - 從 equipment-doc-manager 取得文件內容
   - 提取待完成項目（功能、測試、驗證）
   ↓
2. 搜尋相關工作紀錄
   - 使用 engineering-log 搜尋功能
   - 關鍵字：功能名稱、元件名稱、序列編號
   ↓
3. 比對完成狀態
   ↓
4. 輸出檢查報告
```

### 輸出格式

```markdown
## 規格完成度檢查 - [文件/功能名稱]

### 規格來源
- 文件：40-interlock-rules.md
- 章節：HLight_Z2 互鎖規則

### 完成狀態

| 規格項目 | 工作紀錄 | 狀態 |
|---------|---------|------|
| 定義 HLight_Z2 互鎖條件 | 工作紀錄_20251210 | ✅ 已完成 |
| 測試互鎖功能 | 工作紀錄_20251211 | ✅ 已完成 |
| 更新 50-plc-memory-map.md | - | ❓ 無紀錄 |
| 驗證 10 次循環 | - | ⏳ 未完成 |

### 建議動作
1. 確認是否已更新 50-plc-memory-map.md
2. 執行並記錄 10 次循環驗證
```

---

## 功能 3：跨 Skill 資訊整合

### 觸發詞
- 「整理 XX 功能的所有資訊」
- 「XX 的完整狀態」
- 「彙整 XX 相關內容」

### 執行流程

```
1. 識別目標主題/功能
   ↓
2. 從各 skill 收集資訊
   - engineering-log：相關工作紀錄
   - equipment-doc-manager：技術規格
   - motion-control-troubleshooting：相關故障案例
   ↓
3. 整合輸出
```

### 輸出格式

```markdown
## [主題] 完整資訊彙整

### 📐 技術規格（from equipment-doc-manager）
- 文件：20-axes-specs.md
- 規格摘要：...

### 📋 工作紀錄（from engineering-log）
| 日期 | 內容摘要 |
|------|---------|
| 2025-12-10 | 安裝完成 |
| 2025-12-11 | 參數調整 |

### 🔧 相關故障案例（from motion-control-troubleshooting）
- Case 007：[相關案例摘要]

### 📊 狀態總結
- 規格定義：✅ 完成
- 安裝測試：✅ 完成
- 文件同步：⚠️ 部分待更新
```

---

## 功能 4：週報/月報生成

### 觸發詞
- 「生成本週報告」
- 「整理本月進度」
- 「週報」「月報」

### 執行流程

```
1. 彙整指定期間工作紀錄
   ↓
2. 分類統計
   - 完成項目
   - 解決問題
   - 參數調整
   - 待辦事項
   ↓
3. 比對文件變更
   ↓
4. 輸出結構化報告
```

### 輸出格式

```markdown
## 週報 - YYYY-MM-DD ~ YYYY-MM-DD

### 📈 本週成果
- 完成項目：X 項
- 解決問題：X 項
- 文件更新：X 份

### 📋 完成項目
1. [項目 1]
2. [項目 2]

### 🔧 問題處理
| 問題 | 狀態 | 解決方案 |
|------|------|---------|
| ... | ✅ 已解決 | ... |

### ⏳ 進行中
- [進行中項目]

### 📅 下週計畫
- [計畫項目]

### 📄 文件同步狀態
- 已更新：X 份
- 待更新：X 份
```

---

## 功能 5：新案例轉移

### 觸發詞
- 「這個問題要加到案例庫嗎」
- 「轉成故障案例」

### 執行流程

```
1. 從工作紀錄提取故障排除內容
   ↓
2. 檢查是否符合案例庫標準
   - 有明確症狀描述
   - 有診斷過程
   - 有驗證結果
   - 有通用性（不只適用於單一設備）
   ↓
3. 建議是否加入 motion-control-troubleshooting
```

---

## 快速指令對照

| 使用者說 | 執行功能 |
|---------|---------|
| 「今天該更新什麼」| 功能 1：每日同步檢查 |
| 「工作有沒有遺漏」| 功能 2：規格反查工作 |
| 「整理 XX 的資訊」| 功能 3：跨 Skill 整合 |
| 「週報」| 功能 4：週報生成 |
| 「這問題要加案例庫嗎」| 功能 5：新案例轉移 |

---

## 設計原則

### 協調而非控制

```
project-coordinator 的角色：

✅ 橋接各 skill 的輸出入
✅ 檢查資訊一致性
✅ 提供整合視圖

❌ 不取代各 skill 的功能
❌ 不直接修改文件（建議而非執行）
❌ 不改變各 skill 的觸發邏輯
```

### 各 Skill 保持獨立

```
engineering-log          → 獨立處理工作紀錄
equipment-doc-manager    → 獨立處理文件架構
motion-control-trouble   → 獨立處理故障診斷
technical-presentation   → 獨立處理簡報製作

project-coordinator      → 只在需要「跨 skill」時介入
```

### 擴充方式

新 skill 加入時：
1. 在「已註冊 Skills」表格新增一行
2. 定義「提供什麼」和「接收什麼」
3. 其他 skill 完全不用改

---

## 版本記錄

| 版本 | 日期 | 變更 |
|------|------|------|
| v1.0 | 2025-12-12 | 初始版本，支援 4 個 skill 協調 |
