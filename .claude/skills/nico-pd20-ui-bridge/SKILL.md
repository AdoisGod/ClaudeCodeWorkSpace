---
name: nico-pd20-ui-bridge
description: Manages bidirectional synchronization between PD20_Automaton_PLC交握表.xlsx (PC UI development interface specification) and 50-layer markdown documentation (PLC memory mapping). Use when (1) Syncing signals from work logs to Excel and markdown, (2) Detecting conflicts in memory address allocation, (3) Checking consistency between Excel and markdown, (4) Updating Excel based on markdown changes, (5) Updating markdown based on Excel changes, (6) Any task involving PD20 PLC memory mapping management, signal definition updates, or PC-PLC interface synchronization. This skill manages CRUD operations on both Excel and markdown files, with emphasis on conflict detection and semi-automated workflows requiring user confirmation.
---

# NICO PD20 UI Bridge

PC UI 與 PLC 文檔雙向同步管理工具。

## Quick Start

### 最常用：從工作紀錄同步

**觸發詞**：「同步工作紀錄」「從工作紀錄更新」「同步到 Excel」

**流程**：
1. 讀取最新工作紀錄
2. 提取訊號定義（參考 `references/log-parser-patterns.md`）
3. 執行衝突檢查
4. 顯示變更清單給使用者確認
5. 執行同步並生成報告

### 文件位置

- **Excel**: `/mnt/project/PD20_Automaton_PLC交握表_vol1_12012.xlsx`
- **Markdown**: `/mnt/project/50-*.md` ~ `59-*.md`
- **工作紀錄**: `/mnt/project/工作紀錄_*.md`

## Core Workflows

### Workflow 1: 從工作紀錄同步（雙向）⭐ 主要使用

**Phase 1: 讀取與解析**

1. 識別最新工作紀錄
2. 提取訊號定義（參考 `references/log-parser-patterns.md`）
3. 讀取現有 Excel（動態識別工作表）

**Phase 2: 衝突檢查**

執行四類檢查（詳見 `references/conflict-resolution.md`）：
1. 位址重複
2. 位址範圍重疊  
3. 命名不一致
4. 資料型態不一致

**如有衝突 → 立即停止並詢問使用者**

**Phase 3: 顯示變更清單**

**Phase 4: 執行同步**（使用者確認後）

**Phase 5: 生成報告**（使用 `assets/change-report-template.md`）

**完整流程參見**: `references/sync-workflows.md` Section 1

### Workflow 2: 衝突檢查與完整性驗證

**觸發詞**：「檢查衝突」「驗證一致性」

在任何同步操作前必須執行。詳見 `references/conflict-resolution.md`

### Workflow 3: Excel → Markdown 單向同步

**觸發詞**：「Excel 更新到文檔」

### Workflow 4: Markdown → Excel 反向同步

**觸發詞**：「文檔更新到 Excel」

## Excel 工作表動態識別

使用**混合識別策略**，自動適應 Excel 結構變化。

### 識別流程

**步驟 1: 配置檔過濾**

使用 `references/excel-config.yaml` 中的正則表達式排除無關工作表。

**步驟 2: 結構驗證**

檢查工作表結構特徵：必要欄位 Address/DataType/Content

**步驟 3: 彙總與報告**

### 自動適應範例

| 變化 | 結果 |
|------|------|
| 工作表改名 | ✅ 自動識別 |
| 新增工作表 | ✅ 自動納入 |
| 刪除工作表 | ✅ 自動忽略 |
| 順序調整 | ✅ 完全不影響 |

## Excel 結構

### 欄位映射

| 欄位 | 列 | 說明 |
|------|---|------|
| Address | A | MR/DM 位址 |
| R/W | B | 讀寫權限 |
| ActionType | C | PC UI 用 (A/B/C/None) |
| DataType | D | Bit/Word |
| PT | E | None/Uint/float/Int |
| Content | F | 訊號名稱 |

### 資料型態轉換

| Excel | Markdown | DM 佔用 |
|-------|---------|---------|
| Bit + None | BOOL | - |
| Word + float | REAL32 | 2 DM |
| Word + Uint | UINT16 | 1 DM |
| Word + Int | INT16 | 1 DM |

## Markdown 文件對應

| 文件 | 負責內容 |
|------|---------|
| 50.md | 記憶體映射總表 |
| 51.md | 視覺拍照交握 |
| 52.md | 量測數據緩衝 |
| 53.md | 設備狀態介面 |
| 54.md | 生產流程控制 |
| 55.md | 設備命令控制 |
| 56.md | 運動參數調整 |
| 57.md | 模式切換介面 |
| 58.md | 序列監控介面 |
| 59.md | 料號管理框架 |

## 工作紀錄解析

參見 `references/log-parser-patterns.md` 獲取完整模式清單。

常見格式：
1. 直接定義: MR1120: SEQ-105_Trigger
2. 新增語句: 新增 MR1120 SEQ-105_Trigger
3. 範圍定義: DM5200~5219: 裂紋檢測結果
4. 表格形式: | MR1120 | Bit | SEQ-105_Trigger |

信心度閾值：>= 0.8 自動接受，< 0.8 需使用者確認

## 使用者確認流程

所有同步操作都需要使用者確認：
1. 檢測階段：自動執行
2. 變更清單：顯示並等待確認
3. 執行階段：僅在明確確認後執行
4. 報告階段：自動生成

## 衝突處理策略

**原則**: 發現衝突 → 立即停止 → 詢問使用者

不進行任何自動衝突解決。詳見 `references/conflict-resolution.md`

## 變更報告

每次同步後自動生成，使用模板 `assets/change-report-template.md`。

## 位址分配規則

參見 `references/address-allocation.md`。

快速參考：
- MR1000~1099: 資料緩衝握手
- MR1100~1399: 視覺拍照握手
- MR2000~2999: 軸控制
- DM5000~6199: Zone 緩衝
- DM20000~40999: 料號參數

## 配置更新

如需更新 Excel 結構配置：
```bash
view /mnt/skills/user/nico-pd20-ui-bridge/references/excel-config.yaml
```

## 注意事項

1. **無備份機制**: 不自動備份，但會生成變更紀錄
2. **半自動化**: 所有變更需要使用者確認
3. **衝突停止**: 發現衝突立即停止等待決策
4. **ActionType**: PC UI 專用，不寫入 50-59.md
5. **工作表名稱**: 使用動態識別，改名不影響

## Troubleshooting

### Excel 讀取失敗
- 確認檔案路徑與格式

### 工作表識別錯誤
- 檢查第一行是否包含 Address/DataType/Content
- 檢查 `excel-config.yaml` 排除規則

### 衝突檢測誤報
- 檢查 `references/conflict-resolution.md` 閾值設定

### 工作紀錄解析失敗
- 確認格式符合 `references/log-parser-patterns.md`
