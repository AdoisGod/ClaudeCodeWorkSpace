# Search Mode Detailed Guide
# 搜尋模式詳細指南

## Advanced Search Strategies / 進階搜尋策略

### Time-Based Search / 基於時間的搜尋

**Specific date queries**:
- "昨天" → Calculate date and search `工作紀錄_[YYYYMMDD]`
- "12月2日" → Search `工作紀錄_20251202`
- "上週三" → Calculate specific weekday date

**Date range queries**:
- "上週" → Last 7 days, search multiple logs
- "11月" → All logs with `工作紀錄_202511*`
- "最近" → Most recent 5-10 logs

**Relative time**:
- "前天" → 2 days ago
- "這個月" → Current month logs
- "上個月" → Previous month logs

### Topic-Based Search / 基於主題的搜尋

**Problem-specific**:
```
Query: "HLight_Z1 響應慢"
Search in: 工作紀錄 files only
Look for: "HLight_Z1" AND ("響應" OR "慢" OR "延遲")
Focus on: ## 問題排除 sections
```

**Feature development**:
```
Query: "碰撞檢查開發進度"
Search in: 工作紀錄 files
Look for: "碰撞" OR "collision"
Focus on: ## 今日完成項目 and ## 待辦事項 sections
```

**Parameter adjustment history**:
```
Query: "SLOT_Z 參數調整"
Search in: 工作紀錄 files
Look for: "SLOT_Z" in ## 參數調整 sections
Extract: Parameter table data
```

### Search Query Construction Best Practices

**✅ Good queries**:
- Specific module names: "HLight_Z1", "DCheck_R2"
- Problem keywords: "響應慢", "定位精度", "通訊干擾"
- Action verbs: "調整", "測試", "驗證"
- Time indicators: "昨天", "上週", "11月"

**❌ Poor queries**:
- Too generic: "設備", "問題", "測試"
- Too broad: "PLC", "軸", "參數"
- Vague: "那個", "這個", "東西"

## Detailed Search Examples / 詳細搜尋範例

### Example 1: Morning Routine - Yesterday's Log

**User query**: "看一下昨天的工作紀錄，有什麼待辦事項"

**Step-by-step process**:
1. **Calculate date**: Today is 2025-12-03, yesterday is 2025-12-02
2. **Construct search**: `工作紀錄_20251202`
3. **Execute search**: Use `project_knowledge_search` with query "工作紀錄_20251202"
4. **Extract relevant sections**: Focus on "## 待辦事項"
5. **Format output**: Clean list without technical details

**Expected output**:
```markdown
## 昨天的待辦事項 (2025-12-02)

**優先級 🔴 Urgent**:
- [ ] 完成 Platform 2 測試功能開發
- [ ] 解決 SD13/SD8 通訊干擾問題

**優先級 🟡 Important**:
- [ ] 調整 SLOT_Z 速度參數優化
- [ ] 驗證 DCheck_R2 定位精度

**優先級 🟢 Normal**:
- [ ] 更新技術文件 40-interlock-rules.md

**備註**: 昨天已完成 Platform 1 全部測試功能
```

### Example 2: Problem Investigation - Historical Solution

**User query**: "之前有沒有處理過 HLight_Z1 響應慢的問題？"

**Step-by-step process**:
1. **Extract keywords**: "HLight_Z1", "響應", "慢"
2. **Construct search**: `HLight_Z1 響應 慢` OR `HLight_Z1 延遲`
3. **Filter files**: Search only in `工作紀錄_*` files
4. **Focus sections**: "## 問題排除" or "## 故障排除"
5. **Extract information**: Date, problem, solution, verification status

**Expected output**:
```markdown
## HLight_Z1 響應慢問題 - 歷史紀錄

### 📅 2025-11-15 - 工作紀錄_20251115

**問題描述**:
HLight_Z1 在自動模式下響應時間超過 300ms，手動模式正常

**診斷過程**:
1. 檢查伺服驅動器參數 → 正常
2. 檢查 EtherCAT 通訊週期 → 發現設定為 4ms（過大）
3. 測試不同 cycle time → 2ms 時響應時間降至 150ms

**根本原因**:
EtherCAT 通訊週期設定不當，導致命令更新頻率不足

**解決方案**:
調整 EtherCAT cycle time: 4ms → 2ms
位址: EtherCAT Master 設定

**驗證結果**: ✅ Verified
- 測試次數: 50 次循環
- 響應時間: 穩定在 140-160ms
- 持續監控: 24 小時無異常

**預防措施**:
- 所有高速軸 EtherCAT cycle time 標準化為 2ms
- 更新設備規格文件
- 定期監控通訊性能

---

### 📅 2025-11-08 - 工作紀錄_20251108

**問題描述**:
HLight_Z1 偶發性響應延遲，約 10% 機率發生

**診斷過程**:
1. 檢查 EtherCAT 通訊 → 正常
2. 檢查伺服驅動器濾波器設定 → 發現低通濾波器頻率過低
3. 調整濾波器參數後改善

**根本原因**:
伺服驅動器低通濾波器設定過於保守

**解決方案**:
調整濾波器頻率: 500Hz → 1000Hz
位址: Servo Parameter Pr2.15

**驗證結果**: ✅ Verified
- 測試次數: 100 次循環
- 無延遲發生

**關聯性分析**:
此問題與 11/15 的問題不同，是伺服驅動器參數問題，非 EtherCAT 通訊問題
```

### Example 3: Weekly Review - Time Range Search

**User query**: "彙整本週（11/25-12/01）的工作紀錄，重點是碰撞檢查和參數調整"

**Step-by-step process**:
1. **Identify time range**: 2025-11-25 to 2025-12-01 (7 days)
2. **List target files**:
   - 工作紀錄_20251125
   - 工作紀錄_20251126
   - 工作紀錄_20251127
   - 工作紀錄_20251128
   - 工作紀錄_20251129
   - 工作紀錄_20251130
   - 工作紀錄_20251201
3. **Search all files**: Use `project_knowledge_search` with query "工作紀錄 202511 202512 碰撞 參數"
4. **Focus topics**: "碰撞" related content and "參數調整" sections
5. **Analyze patterns**: Identify recurring issues, parameter trends
6. **Synthesize**: Create structured summary

**Expected output**:
```markdown
## 本週工作彙整 (11/25 - 12/01)

### 📊 整體進度概況

**完成率**: 85% (17/20 計畫項目)

**主要里程碑**:
- ✅ Platform 1 全站測試功能開發完成
- ✅ 碰撞檢查邏輯實作並驗證
- ✅ SD13/SD8 通訊干擾問題解決
- ⏳ Platform 2 測試功能開發中 (60%)

---

### 🎯 碰撞檢查開發進度

**11/25 - 基礎架構**:
- 設計碰撞檢查邏輯框架
- 定義軸位置檢查規則
- 實作基本的目標位置預檢

**11/27 - Platform 1 實作**:
- 完成 Clamp_X, Clamp_Z 與 HLight_Z1 碰撞檢查
- 實作三軸同動的碰撞偵測
- 測試驗證: 50 次循環無誤觸發

**11/29 - 優化與除錯**:
- 修正 DCheck_R2 旋轉範圍判斷邏輯
- 調整碰撞檢查觸發時機
- 增加詳細錯誤訊息

**12/01 - 整合測試**:
- Platform 1 全流程碰撞檢查測試
- 驗證各種異常情境
- 確認無誤報和漏報

**狀態**: ✅ Platform 1 完成, ⏳ Platform 2 待開發

**技術要點**:
- 使用主動預防式檢查（檢查目標位置）
- 優於被動偵測式（檢查當前位置）
- 程式碼可讀性高，易於維護

---

### ⚙️ 參數調整統計

**本週參數調整次數**: 12 次

**主要調整項目**:

| 日期 | 軸/模組 | 參數項目 | 原值 | 新值 | 原因 | 結果 |
|------|---------|---------|------|------|------|------|
| 11/25 | SLOT_Z | 最大速度 | 800 | 600 | 機械限制 | ✅ 穩定 |
| 11/26 | HLight_Z1 | 加速度 | 1000 | 1500 | 提升效率 | ✅ 改善 |
| 11/27 | DCheck_R2 | 定位帶 | ±0.1° | ±0.05° | 精度要求 | ⚠️ 需觀察 |
| 11/28 | Clamp_X | EtherCAT週期 | 4ms | 2ms | 響應速度 | ✅ 顯著改善 |
| 11/29 | SD13 | PWM頻率 | 20kHz | 10kHz | 降低干擾 | ✅ 解決 |

**參數調整趨勢分析**:
1. **速度優化**: 多數參數調整目標為提升系統效率
2. **精度提升**: DCheck_R2 定位精度持續優化中
3. **干擾解決**: 通訊相關參數調整有效

**需要注意**:
- DCheck_R2 定位帶縮小後需長期監控
- SLOT_Z 速度降低影響 cycle time (+0.5s)

---

### 🔧 解決的技術問題

#### 1. SD13/SD8 通訊干擾 (Critical)
**問題**: Modbus RTU 通訊不穩定，約 30% 機率讀取失敗

**解決方案**:
- 分離 SD13 和 SD8 線路路徑
- 安裝磁珠濾波器 (Ferrite Core)
- 降低 PWM 載波頻率: 20kHz → 10kHz

**驗證**: ✅ 100 次通訊測試全部成功

**投入時間**: 4 工時

---

#### 2. DCheck_R2 定位精度不足
**問題**: 定位精度 ±0.2°，需求為 ±0.1°

**解決方案**:
- 實施單向接近法（避免齒輪背隙）
- 調整定位帶參數
- 增加最小移動距離限制 (5°)

**驗證**: ⚠️ 改善至 ±0.12°，仍需優化

**投入時間**: 6 工時

---

#### 3. HLight_Z1 響應延遲
**問題**: 自動模式響應時間 >300ms

**解決方案**:
- 調整 EtherCAT cycle time: 4ms → 2ms
- 優化伺服驅動器參數

**驗證**: ✅ 響應時間降至 150ms

**投入時間**: 3 工時

---

### 📋 本週待辦事項完成率

**已完成** (12 項):
- ✅ Platform 1 碰撞檢查實作
- ✅ SD13/SD8 通訊干擾解決
- ✅ HLight_Z1 響應優化
- ✅ Clamp 系統參數調整
- ✅ EtherCAT 通訊優化
- [... 其他項目]

**未完成** (3 項):
- ❌ Platform 2 測試功能開發（延至下週，因碰撞檢查需優先完成）
- ❌ Door 模組整合測試（硬體未到位）
- ❌ 系統性能基準測試（等待所有站點完成）

---

### 🔄 重複出現的議題

1. **定位精度問題**:
   - DCheck_R2, Conv_R1 皆出現定位精度不足
   - 建議: 系統性檢查所有旋轉軸齒輪背隙
   - 計畫: 下週進行全面檢查

2. **EtherCAT 參數標準化**:
   - 不同軸使用不同 cycle time
   - 建議: 建立標準化參數表
   - 計畫: 下週完成參數標準化文件

3. **通訊干擾**:
   - SD13/SD8 解決後，需預防其他通訊介面
   - 建議: 所有通訊線路安裝磁珠
   - 計畫: 採購足夠磁珠備用

---

### 📅 下週計畫 (12/02 - 12/08)

**優先級 🔴 Urgent**:
1. Platform 2 測試功能開發
2. 全軸定位精度系統性檢查
3. EtherCAT 參數標準化

**優先級 🟡 Important**:
1. Door 模組整合測試（硬體到位後）
2. 碰撞檢查邏輯文件化
3. 通訊線路磁珠安裝

**優先級 🟢 Normal**:
1. 系統性能基準測試
2. 技術文件更新
3. 備品清單整理

---

### 💡 本週關鍵學習

1. **碰撞檢查設計**:
   - 主動預防優於被動偵測
   - 程式可讀性是長期維護關鍵

2. **機械背隙補償**:
   - 小於 5° 的移動可能因齒輪背隙無效
   - 單向接近法是有效解決方案

3. **通訊干擾處理**:
   - 線路物理分離最有效
   - 磁珠 + 參數調整雙管齊下

4. **參數調整策略**:
   - 需要系統性方法，非個案處理
   - 標準化參數表很重要
```

### Example 4: Parameter History - Specific Module

**User query**: "查詢 SLOT_Z 的所有參數調整歷史"

**Step-by-step process**:
1. **Extract module name**: "SLOT_Z"
2. **Construct search**: `SLOT_Z 參數` in 工作紀錄 files
3. **Focus sections**: "## 參數調整" tables
4. **Extract chronologically**: All parameter change records
5. **Analyze trends**: Why parameters changed, results

**Expected output**:
```markdown
## SLOT_Z 參數調整歷史

### 📊 調整統計
- 總調整次數: 8 次
- 時間跨度: 2025-10-15 至 2025-12-01
- 主要原因: 速度優化 (3次), 機械限制 (2次), 精度改善 (3次)

---

### 詳細調整記錄

#### 調整 #8 - 2025-12-01
**參數**: 最大加速度
**變更**: 2000 → 1800 mm/s²
**原因**: 減少震動，提升定位穩定性
**位址**: DM2050
**結果**: ✅ 震動減少 40%，定位時間增加 0.1s
**備註**: 可接受的 trade-off

#### 調整 #7 - 2025-11-25
**參數**: 最大速度
**變更**: 800 → 600 mm/s
**原因**: 機械限制，避免導軌磨損
**位址**: DM2048
**結果**: ✅ 穩定運行，無異常
**備註**: 此為最終設定值

#### 調整 #6 - 2025-11-20
**參數**: 定位完成帶
**變更**: ±0.5mm → ±0.2mm
**原因**: 提升定位精度要求
**位址**: DM2052
**結果**: ⚠️ 偶有定位逾時，需觀察
**備註**: 後續調整加速度解決

[... 繼續其他調整記錄]

---

### 趨勢分析

**速度參數演變**:
- 初始: 1000 mm/s (10/15)
- 優化: 1200 mm/s (10/20) - 提升效率
- 調降: 800 mm/s (11/10) - 發現震動
- 最終: 600 mm/s (11/25) - 機械限制確認

**結論**: 最大速度受限於機械系統，600 mm/s 為最佳設定

**精度參數演變**:
- 定位帶逐步縮小: ±1.0mm → ±0.2mm
- 伴隨加速度調整以確保穩定定位

**建議**:
- SLOT_Z 參數已趨於穩定
- 建議固化當前參數為標準值
- 定期（每月）驗證機械狀態
```

## Search Efficiency Tips / 搜尋效率技巧

### 1. Use Date Calculations Smartly
```python
# When user says "昨天"
today = datetime.now()
yesterday = today - timedelta(days=1)
search_query = f"工作紀錄_{yesterday.strftime('%Y%m%d')}"
```

### 2. Combine Keywords Intelligently
```
Good: "HLight_Z1 響應"
Better: "HLight_Z1 (響應 OR 延遲 OR 慢)"
Best: "HLight_Z1" AND ("響應" OR "延遲") in 問題排除 sections
```

### 3. Prioritize Recent Logs
When searching without specific time:
- Start with most recent logs (last 7 days)
- Expand search if not found
- Recent solutions more likely relevant

### 4. Extract Minimal Necessary Content
Don't return entire log files:
- Extract only sections answering the query
- Summarize if multiple logs contain relevant info
- Use bullet points for key findings

### 5. Handle "Not Found" Gracefully
```markdown
## 搜尋結果

**查詢內容**: [User's query]
**搜尋範圍**: [Time period or scope]

**結果**: 未找到直接相關的工作紀錄

**建議**:
1. 擴大搜尋時間範圍？
2. 使用不同關鍵字？
3. 這可能是新問題，需要創建新紀錄
```

---

## Advanced Filtering / 進階篩選

### By Section Type
- Problem solving: Search in "## 問題排除"
- Parameter changes: Search in "## 參數調整"
- Pending tasks: Search in "## 待辦事項"
- Completed work: Search in "## 今日完成項目"

### By Status
- Resolved issues: Look for ✅ status
- Ongoing issues: Look for ⏳ or ⚠️ status
- Failed attempts: Look for ❌ status

### By Priority
- Urgent items: Look for 🔴
- Important items: Look for 🟡
- Normal items: Look for 🟢

---

**End of Search Guide**
