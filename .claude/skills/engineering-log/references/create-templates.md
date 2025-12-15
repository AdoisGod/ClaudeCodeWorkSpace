# Documentation Templates
# 文件範本

This file contains complete templates with field-by-field explanations and examples.

---

## Template 1: Daily Work Log (Complete)
## 範本 1：每日工作紀錄（完整版）

### When to Use / 使用時機
- End of work day
- Regular daily documentation
- General work summary

### Complete Template / 完整範本

```markdown
# 工作紀錄_YYYYMMDD

**日期 (Date)**: YYYY-MM-DD  
**專案 (Project)**: PD20  
**工程師 (Engineer)**: [Your Name]  
**工作時數 (Work Hours)**: [Hours]

---

## 今日完成項目 / Completed Tasks

### 1. [Task Name - Be Specific]

**目標 (Goal)**:
[What you aimed to achieve - one sentence]

**執行內容 (Actions Taken)**:
- [Specific action 1 with details]
- [Specific action 2 with details]
- [Specific action 3 with details]

**結果 (Result)**:
[Concrete outcome - what was achieved]

**驗證方式 (Verification Method)**:
[How you confirmed it works]

**耗時 (Time Spent)**: [Hours]

---

### 2. [Next Task Name]

[Same structure as above]

---

## 問題排除 / Troubleshooting

### [Problem Title - Clear and Searchable]

**設備背景 (Equipment Background)**:
- 專案 (Project): PD20
- 模組 (Module): [Specific name, e.g., HLight_Z1]
- 通用術語 (Generic Term): [e.g., Vertical servo axis for light source]
- 軸/元件 (Axis/Component): [Specific axis or component involved]

**症狀描述 (Symptom Description)**:
[Describe exactly what you observed - NO interpretation yet]

**發生條件 (Occurrence Conditions)**:
- 觸發時機 (When): [Specific conditions or timing]
- 發生頻率 (Frequency): [Always / Sometimes (XX%) / Rare]
- 影響範圍 (Impact): [What functions are affected]
- 環境因素 (Environment): [Temperature, load, etc. if relevant]

**診斷過程 (Diagnostic Process)**:
1. **假設 [Hypothesis 1]**:
   - 檢查內容 (What Checked): [Specific test or inspection]
   - 預期結果 (Expected): [What should happen if hypothesis correct]
   - 實際結果 (Actual): [What actually happened]
   - 結論 (Conclusion): ✅ Confirmed / ❌ Rejected

2. **假設 [Hypothesis 2]**:
   [Same structure]

3. **[Continue until root cause found]**

**根本原因 (Root Cause)**:
[The underlying cause based on diagnostic evidence]

**解決方案 (Solution)**:
**實施步驟 (Implementation Steps)**:
1. [Detailed step with parameters]
   - 參數名稱 (Parameter): [Name]
   - 變更內容 (Change): [Before → After]
   - 記憶體位址 (Address): [DM/MR address if applicable]
2. [Next step]

**程式碼變更 (Code Changes)** (if applicable):
```
[Relevant code snippets or logic changes]
```

**驗證測試 (Verification Test)**:
- 測試方法 (Test Method): [How you tested]
- 測試次數 (Test Cycles): [Number of cycles]
- 測試條件 (Test Conditions): [Environment, load, etc.]
- 測試結果 (Test Results): [Success rate, observations]
- 驗證狀態 (Verification Status): ✅ Verified / ⚠️ Needs Monitoring / ❌ Incomplete

**預防措施 (Prevention Measures)**:
**短期預防 (Immediate)**:
- [Quick action to prevent recurrence]

**長期改善 (Long-term)**:
- [Systematic improvement needed]
- [Documentation or specification updates]

**相關文件 (Related Documents)**:
- [Links to relevant technical specs or other logs]

**關鍵字 (Keywords)**: [Module], [Issue Type], [Solution Category]

**狀態 (Status)**: ✅ Resolved / ⏳ Monitoring / ❌ Unresolved

---

## 參數調整 / Parameter Adjustments

| 項目<br>Item | 設備/軸<br>Equipment | 參數名稱<br>Parameter | 原值<br>Original | 新值<br>New | 單位<br>Unit | 記憶體位址<br>Address | 調整原因<br>Reason | 結果<br>Result |
|------------|---------------------|---------------------|----------------|------------|------------|---------------------|---------------|---------------|
| 1 | HLight_Z1 | 最大速度 | 1000 | 1200 | mm/s | DM1000 | 提升效率 | ✅ 改善 |
| 2 | SLOT_Z | 加速度 | 1500 | 1800 | mm/s² | DM2050 | 減少震動 | ✅ 穩定 |

**參數調整備註**:
[Any important notes about parameter changes]

---

## 測試執行 / Tests Performed

### [Test Name]

**測試類型 (Test Type)**: 功能測試 / 性能測試 / 整合測試

**測試對象 (Test Target)**:
[Module or function being tested]

**測試結果 (Test Result)**: ✅ Pass / ❌ Fail / ⚠️ Partial

**詳細記錄 (Details)**:
[Brief summary or link to detailed test log]

---

## 待辦事項 / Pending Tasks

### 優先級 🔴 Urgent (明天必須完成)
- [ ] [Task with specific deliverable]
- [ ] [Task with deadline]

### 優先級 🟡 Important (本週內完成)
- [ ] [Important but not urgent task]
- [ ] [Task requiring coordination]

### 優先級 🟢 Normal (有空時處理)
- [ ] [Nice to have task]
- [ ] [Documentation update]

### 需要討論 / Need Discussion
- [ ] [Issue requiring team input with context]
- [ ] [Decision needed from management]

---

## 備註 / Notes

**重要發現 (Key Findings)**:
- [Any important insights or discoveries today]
- [Things that surprised you or worth noting]

**需要注意 (Cautions)**:
- [Warnings for tomorrow or future work]
- [Potential risks identified]

**下次改進 (Next Time Improvements)**:
- [What could be done better next time]
- [Lessons learned]

**工作環境 (Work Environment)** (if relevant):
- 溫度 (Temperature): [Value]
- 濕度 (Humidity): [Value]
- 其他 (Others): [Any environmental factors affecting work]

---

**記錄完成時間 (Log Completion Time)**: [HH:MM]
**明日計畫 (Tomorrow's Plan)**: [Brief overview of tomorrow's priorities]
```

### Field Explanations / 欄位說明

**症狀描述 vs 根本原因**:
- ❌ 症狀: "編碼器電池沒電" (This is diagnosis, not symptom)
- ✅ 症狀: "原點復歸時有時成功(60%)但隨機失敗，錯誤代碼 E0023"
- ✅ 根本原因: "編碼器絕對位置資料遺失，經檢查為電池電壓不足(1.8V < 2.5V 標準值)"

**診斷過程**:
- Show your thinking, not just final answer
- Include rejected hypotheses (what you checked but wasn't the cause)
- This helps others understand the problem better

**驗證測試**:
- Don't declare "fixed" after 1-2 tests
- Simple issues: 10-20 cycles minimum
- Intermittent issues: 50+ cycles or 24+ hours
- Document test conditions

---

## Template 2: Troubleshooting Log (Focused)
## 範本 2：專注故障排除紀錄

### When to Use / 使用時機
- Significant problem that needs detailed documentation
- Complex troubleshooting requiring multiple steps
- Problem that might recur and needs reference

### Complete Template / 完整範本

```markdown
# 故障排除 - [Clear Problem Title]

**日期時間 (Date/Time)**: YYYY-MM-DD HH:MM  
**專案 (Project)**: PD20  
**模組 (Module)**: [Specific name]  
**通用術語 (Generic Term)**: [Generic description for reusability]  
**影響程度 (Impact Level)**: 🔴 Critical / 🟡 High / 🟢 Medium / ⚪ Low

---

## 問題概述 / Problem Overview

**問題標題 (Problem Title)**:
[One sentence description]

**症狀 (Symptoms)**:
[Exact observations - what you see, hear, measure]
- [Symptom 1]
- [Symptom 2]
- [Symptom 3]

**初次發現 (First Occurrence)**:
- 日期時間 (Date/Time): [When first noticed]
- 發生情境 (Context): [What was happening at the time]

**影響分析 (Impact Analysis)**:
- 生產影響 (Production): ✅ No Impact / ⚠️ Partial / ❌ Complete Stop
- 功能影響 (Functionality): [What functions don't work]
- 安全影響 (Safety): [Any safety concerns]
- 預估停機時間 (Estimated Downtime): [If applicable]

---

## 設備背景 / Equipment Background

**硬體資訊 (Hardware Information)**:
- 軸/模組 (Axis/Module): [Specific name]
- 驅動器 (Driver): [Model, version]
- 馬達 (Motor): [Model, specifications]
- 編碼器 (Encoder): [Type, resolution]
- 相關元件 (Related Components): [Other parts involved]

**軟體資訊 (Software Information)**:
- PLC 程式版本 (PLC Version): [Version]
- 相關 FB/Function: [Relevant function blocks]
- 最近變更 (Recent Changes): [Any recent code or parameter changes]

**操作條件 (Operating Conditions)**:
- 負載 (Load): [Current load]
- 速度 (Speed): [Operating speed]
- 環境 (Environment): [Temperature, humidity, etc.]

---

## 診斷邏輯 / Diagnostic Logic

### 初步分析 (Initial Analysis)

**可能原因列表 (Possible Causes List)**:
1. [Hypothesis 1] - 可能性 (Likelihood): High / Medium / Low
2. [Hypothesis 2] - 可能性 (Likelihood): High / Medium / Low
3. [Hypothesis 3] - 可能性 (Likelihood): High / Medium / Low

**診斷策略 (Diagnostic Strategy)**:
[Explain your approach - which hypotheses to test first and why]

---

### 診斷步驟 (Diagnostic Steps)

#### 步驟 1: [Test Description]

**假設 (Hypothesis)**: [What you're testing]

**測試方法 (Test Method)**:
[Detailed description of what you did]

**預期結果 (Expected Result)**:
[What should happen if hypothesis is correct]

**實際結果 (Actual Result)**:
[What actually happened]

**觀察資料 (Observed Data)**:
- [Measurement 1]: [Value]
- [Measurement 2]: [Value]

**結論 (Conclusion)**: ✅ Hypothesis Confirmed / ❌ Hypothesis Rejected / ⚠️ Inconclusive

**證據 (Evidence)**:
[What supports your conclusion]

---

#### 步驟 2: [Next Test]

[Same structure as Step 1]

---

[Continue until root cause identified]

---

## 根本原因分析 / Root Cause Analysis

**確認的根本原因 (Confirmed Root Cause)**:
[The underlying cause based on diagnostic evidence]

**因果關係 (Cause-Effect Relationship)**:
[Explain how the root cause leads to observed symptoms]

**為什麼之前沒發現 (Why Not Detected Earlier)**:
[If applicable, why this wasn't caught sooner]

**5-Why Analysis** (if complex problem):
1. Why did the problem occur? [Answer]
2. Why [answer to #1]? [Answer]
3. Why [answer to #2]? [Answer]
4. Why [answer to #3]? [Answer]
5. Why [answer to #4]? [Root cause]

---

## 解決方案 / Solution

### 方案選擇 (Solution Selection)

**考慮的方案 (Considered Solutions)**:

| 方案<br>Solution | 優點<br>Pros | 缺點<br>Cons | 實施難度<br>Difficulty | 成本<br>Cost | 選擇<br>Selected |
|-----------------|-------------|-------------|---------------------|------------|----------------|
| 方案 A | [Pros] | [Cons] | High/Med/Low | [Cost] | ✅ / ❌ |
| 方案 B | [Pros] | [Cons] | High/Med/Low | [Cost] | ✅ / ❌ |

**選擇理由 (Selection Rationale)**:
[Why chosen solution was selected]

---

### 實施步驟 (Implementation Steps)

**準備工作 (Preparation)**:
- [ ] [Required tools]
- [ ] [Required parts]
- [ ] [Safety measures]
- [ ] [Backup plans]

**實施程序 (Implementation Procedure)**:

**步驟 1**: [Detailed step]
- 具體操作 (Specific Action): [Exact action]
- 參數設定 (Parameter Setting): [If applicable]
- 記憶體位址 (Address): [DM/MR address]
- 預期結果 (Expected Result): [What should happen]
- 實際結果 (Actual Result): [What happened]

**步驟 2**: [Next step]
[Same structure]

[Continue for all steps]

**實施時間 (Implementation Time)**: [Duration]

---

### 程式碼變更 (Code Changes) (if applicable)

**變更前 (Before)**:
```
[Original code]
```

**變更後 (After)**:
```
[Modified code]
```

**變更說明 (Change Explanation)**:
[Why code was changed this way]

---

### 參數變更 (Parameter Changes)

| 項目<br>Item | 參數名稱<br>Parameter | 變更前<br>Before | 變更後<br>After | 單位<br>Unit | 位址<br>Address | 變更原因<br>Reason |
|------------|---------------------|----------------|---------------|------------|----------------|---------------|
| 1 | [Param] | [Value] | [Value] | [Unit] | [DM/MR] | [Why] |

---

## 驗證測試 / Verification Test

### 測試計畫 (Test Plan)

**測試目標 (Test Objective)**:
[What needs to be verified]

**測試條件 (Test Conditions)**:
- 環境 (Environment): [Conditions]
- 負載 (Load): [Test load]
- 速度 (Speed): [Test speed]
- 其他 (Others): [Other relevant conditions]

**測試程序 (Test Procedure)**:
1. [Test step 1]
2. [Test step 2]
3. [Test step 3]

**接受標準 (Acceptance Criteria)**:
- [Criterion 1]
- [Criterion 2]

---

### 測試結果 (Test Results)

**測試執行 (Test Execution)**:
- 測試開始時間 (Start Time): [DateTime]
- 測試結束時間 (End Time): [DateTime]
- 測試次數 (Number of Cycles): [Count]
- 測試人員 (Tested By): [Name]

**測試資料 (Test Data)**:

| 測試項目<br>Test Item | 目標值<br>Target | 實測值<br>Measured | 單位<br>Unit | 結果<br>Result | 備註<br>Notes |
|---------------------|----------------|------------------|------------|---------------|--------------|
| [Item 1] | [Target] | [Measured] | [Unit] | ✅/❌ | [Comments] |
| [Item 2] | [Target] | [Measured] | [Unit] | ✅/❌ | [Comments] |

**異常情況 (Anomalies)**:
[Any unexpected behaviors or observations]

**整體結果 (Overall Result)**: ✅ Pass / ❌ Fail / ⚠️ Conditional Pass

---

### 長期監控計畫 (Long-term Monitoring Plan)

**監控項目 (Monitoring Items)**:
- [What to monitor]
- [Frequency]
- [Alert conditions]

**監控期限 (Monitoring Duration)**:
[How long to monitor before considering fully resolved]

**監控負責人 (Monitoring Owner)**:
[Who is responsible]

---

## 預防與改善 / Prevention & Improvement

### 短期預防措施 (Immediate Prevention)

**操作程序變更 (Procedure Changes)**:
- [Change 1]
- [Change 2]

**警告標示 (Warning Labels)**:
- [What warnings to add and where]

**檢查點增加 (Additional Checkpoints)**:
- [New inspection points]

---

### 長期改善措施 (Long-term Improvement)

**設計改善 (Design Improvements)**:
- [Fundamental design changes needed]
- [Estimated time/cost]

**文件更新 (Documentation Updates)**:
- [ ] 技術規格文件 (Technical Specs): [Which files]
- [ ] 操作程序 (Operating Procedures): [Which procedures]
- [ ] 維護手冊 (Maintenance Manual): [Which sections]
- [ ] 訓練教材 (Training Materials): [Which materials]

**標準化 (Standardization)**:
- [What should be standardized]
- [How to prevent similar issues in other modules]

**備品準備 (Spare Parts)**:
- [What spare parts should be kept in stock]

---

### 知識分享 (Knowledge Sharing)

**相關人員通知 (Notify Relevant Personnel)**:
- [ ] [Person/Team 1]
- [ ] [Person/Team 2]

**技術會議議題 (Technical Meeting Topic)**:
- [If this warrants discussion in tech meeting]

**案例庫更新 (Case Database Update)**:
- [How this case should be categorized and stored]

---

## 成本分析 / Cost Analysis (if significant)

**直接成本 (Direct Costs)**:
- 零件更換 (Parts): [Cost]
- 人力時間 (Labor): [Hours × Rate]
- 外部支援 (External Support): [Cost]

**間接成本 (Indirect Costs)**:
- 停機損失 (Downtime Loss): [Estimated]
- 品質影響 (Quality Impact): [If applicable]

**總成本 (Total Cost)**: [Sum]

---

## 附件 / Attachments

**照片 (Photos)**:
- [Description of photos taken]

**資料檔案 (Data Files)**:
- [Log files, oscilloscope data, etc.]

**相關文件 (Related Documents)**:
- [Links to technical specs, previous logs, etc.]

---

**關鍵字 (Keywords)**: [Module], [Problem Type], [Root Cause Category], [Solution Type]

**案例編號 (Case Number)**: [If using case tracking system]

**最終狀態 (Final Status)**: ✅ Resolved / ⏳ Monitoring / ❌ Unresolved

**文件完成時間 (Document Completion Time)**: YYYY-MM-DD HH:MM

---

**簽核 (Approval)** (if required):
- 記錄者 (Documented By): [Name] - [Date]
- 審核者 (Reviewed By): [Name] - [Date]
- 核准者 (Approved By): [Name] - [Date]
```

---

## Template 3: Test Results Log (Complete)
## 範本 3：測試結果紀錄（完整版）

### When to Use / 使用時機
- Formal test execution
- Verification of fixes
- Performance validation
- Integration testing
- Acceptance testing

### Complete Template / 完整範本

```markdown
# 測試紀錄 - [Test Name]

**日期 (Date)**: YYYY-MM-DD  
**測試類型 (Test Type)**: ☐ 功能測試 ☐ 性能測試 ☐ 整合測試 ☐ 驗收測試  
**測試階段 (Test Phase)**: ☐ 開發測試 ☐ 系統測試 ☐ 用戶測試  
**測試版本 (Test Version)**: [Software/Hardware version]

---

## 測試概述 / Test Overview

**測試目的 (Test Objective)**:
[What this test aims to verify - be specific]

**測試範圍 (Test Scope)**:
**包含 (Included)**:
- [Function/Module 1]
- [Function/Module 2]

**不包含 (Excluded)**:
- [What's not tested]
- [Why excluded]

**測試依據 (Test Basis)**:
- 需求文件 (Requirements): [Document reference]
- 設計規格 (Design Specs): [Document reference]
- 驗收標準 (Acceptance Criteria): [Criteria reference]

---

## 測試配置 / Test Configuration

### 硬體配置 (Hardware Configuration)

**PLC 系統 (PLC System)**:
- 型號 (Model): [PLC model]
- 版本 (Version): [Firmware version]
- 模組 (Modules): [I/O modules, etc.]

**測試設備 (Test Equipment)**:
- [Equipment 1]: [Model, specifications]
- [Equipment 2]: [Model, specifications]
- [Measurement tools]: [Details]

**被測模組 (Device Under Test)**:
- 模組名稱 (Module): [Name]
- 通用術語 (Generic Term): [Generic description]
- 硬體版本 (Hardware Version): [Version]
- 韌體版本 (Firmware Version): [Version]

---

### 軟體配置 (Software Configuration)

**PLC 程式 (PLC Program)**:
- 程式版本 (Program Version): [Version]
- 編譯時間 (Compile Time): [DateTime]
- 相關 FB/Function: [Relevant function blocks]
- 程式碼變更 (Code Changes): [Recent changes if any]

**PC 端軟體 (PC Software)** (if applicable):
- PC1 視覺系統 (Vision System): [Version]
- PC2 HMI: [Version]
- 其他軟體 (Others): [Details]

---

### 環境條件 (Environment Conditions)

**測試環境 (Test Environment)**:
- 地點 (Location): [Where test was conducted]
- 溫度 (Temperature): [Value] ±[Tolerance]
- 濕度 (Humidity): [Value] ±[Tolerance]
- 電源 (Power Supply): [Voltage, stability]

**負載條件 (Load Conditions)**:
- 負載類型 (Load Type): [Type of load]
- 負載值 (Load Value): [Measurement]
- 其他條件 (Other Conditions): [Any other relevant factors]

---

## 測試程序 / Test Procedure

### 測試前準備 (Pre-test Preparation)

**檢查清單 (Checklist)**:
- [ ] 硬體連接確認
- [ ] 軟體版本確認
- [ ] 安全措施確認
- [ ] 測試工具校驗
- [ ] 環境條件檢查
- [ ] 備份資料

**初始狀態設定 (Initial State Setup)**:
[Describe initial system state before testing]

---

### 測試步驟 (Test Steps)

#### 測試案例 1: [Test Case Name]

**測試案例 ID (Test Case ID)**: TC-001

**測試目標 (Test Goal)**:
[What this specific test case verifies]

**前置條件 (Preconditions)**:
- [Condition 1]
- [Condition 2]

**測試步驟 (Steps)**:

**步驟 1.1**: [Detailed action]
- 操作 (Operation): [What to do]
- 預期結果 (Expected): [What should happen]
- 實際結果 (Actual): [What happened]
- 觀測資料 (Observed Data): [Measurements]
- 狀態 (Status): ✅ Pass / ❌ Fail / ⚠️ Partial
- 備註 (Notes): [Any observations]

**步驟 1.2**: [Next action]
[Same structure]

**測試案例結果 (Test Case Result)**: ✅ Pass / ❌ Fail / ⚠️ Partial

**失敗原因 (Failure Reason)** (if failed):
[Detailed explanation]

---

#### 測試案例 2: [Next Test Case]

[Same structure as Test Case 1]

---

[Continue for all test cases]

---

## 測試資料 / Test Data

### 功能測試資料 (Functional Test Data)

| TC ID | 測試項目<br>Test Item | 輸入<br>Input | 預期輸出<br>Expected | 實際輸出<br>Actual | 結果<br>Result | 備註<br>Notes |
|-------|---------------------|--------------|-------------------|------------------|---------------|--------------|
| TC-001 | [Item] | [Input] | [Expected] | [Actual] | ✅/❌ | [Notes] |
| TC-002 | [Item] | [Input] | [Expected] | [Actual] | ✅/❌ | [Notes] |

---

### 性能測試資料 (Performance Test Data) (if applicable)

| 測試項目<br>Test Item | 目標值<br>Target | 實測值<br>Measured | 單位<br>Unit | 偏差<br>Deviation | 結果<br>Result | 備註<br>Notes |
|---------------------|----------------|------------------|------------|-----------------|---------------|--------------|
| 響應時間 | <200 | 150 | ms | -25% | ✅ | [Notes] |
| 定位精度 | ±0.1 | ±0.08 | mm | -20% | ✅ | [Notes] |
| 循環時間 | <30 | 28 | s | -6.7% | ✅ | [Notes] |

---

### 壓力測試資料 (Stress Test Data) (if applicable)

**測試條件 (Test Conditions)**:
- 測試時長 (Duration): [Hours]
- 循環次數 (Cycles): [Count]
- 負載條件 (Load): [Maximum load]

**測試結果 (Results)**:
- 成功次數 (Successful Cycles): [Count]
- 失敗次數 (Failed Cycles): [Count]
- 成功率 (Success Rate): [Percentage]
- 觀察到的問題 (Issues Observed): [List]

---

## 測試結果分析 / Test Results Analysis

### 整體結果 (Overall Results)

**測試統計 (Test Statistics)**:
- 總測試案例數 (Total Test Cases): [Count]
- 通過案例數 (Passed): [Count] ([Percentage]%)
- 失敗案例數 (Failed): [Count] ([Percentage]%)
- 部分通過案例數 (Partial): [Count] ([Percentage]%)

**整體評估 (Overall Assessment)**: ✅ Pass / ❌ Fail / ⚠️ Conditional Pass

**是否符合驗收標準 (Meets Acceptance Criteria)**: ☐ Yes ☐ No ☐ Partially

---

### 發現的問題 (Issues Found)

#### 問題 1: [Issue Title]

**嚴重程度 (Severity)**: 🔴 Critical / 🟡 High / 🟢 Medium / ⚪ Low

**問題描述 (Description)**:
[Detailed description]

**重現步驟 (Reproduction Steps)**:
1. [Step 1]
2. [Step 2]

**預期行為 (Expected Behavior)**:
[What should happen]

**實際行為 (Actual Behavior)**:
[What happened]

**影響範圍 (Impact)**:
[What is affected]

**建議解決方案 (Suggested Solution)**:
[Proposed fix]

**優先級 (Priority)**: 🔴 Must Fix / 🟡 Should Fix / 🟢 Nice to Fix

---

#### 問題 2: [Next Issue]

[Same structure]

---

### 性能分析 (Performance Analysis) (if applicable)

**性能指標總結 (Performance Metrics Summary)**:
- 平均響應時間 (Avg Response Time): [Value]
- 最大響應時間 (Max Response Time): [Value]
- 平均循環時間 (Avg Cycle Time): [Value]
- 系統穩定性 (System Stability): [Assessment]

**性能瓶頸 (Performance Bottlenecks)**:
[Identified bottlenecks and analysis]

**優化建議 (Optimization Suggestions)**:
[Recommendations for improvement]

---

## 後續行動 / Follow-up Actions

### 立即行動項目 (Immediate Actions)

**必須修正 (Must Fix)**:
- [ ] [Issue 1] - 負責人: [Name] - 期限: [Date]
- [ ] [Issue 2] - 負責人: [Name] - 期限: [Date]

**建議修正 (Should Fix)**:
- [ ] [Issue 3] - 負責人: [Name] - 期限: [Date]

---

### 重測計畫 (Retest Plan)

**需要重測的項目 (Items Requiring Retest)**:
- [Test case 1] - 原因: [Why retest needed]
- [Test case 2] - 原因: [Why retest needed]

**重測時機 (Retest Timing)**:
[When to retest]

**重測負責人 (Retest Owner)**:
[Who will conduct retest]

---

### 文件更新 (Documentation Updates)

**需要更新的文件 (Documents Requiring Update)**:
- [ ] 技術規格 (Technical Specs): [Which sections]
- [ ] 使用手冊 (User Manual): [Which sections]
- [ ] 維護程序 (Maintenance Procedures): [Which procedures]
- [ ] 訓練教材 (Training Materials): [Which materials]

---

## 測試結論 / Test Conclusion

**測試目標達成度 (Objective Achievement)**:
☐ 完全達成 (Fully Achieved)  
☐ 部分達成 (Partially Achieved)  
☐ 未達成 (Not Achieved)

**建議 (Recommendations)**:
☐ 通過驗收，可進入下階段 (Approve for next phase)  
☐ 需修正後重測 (Requires fixes and retest)  
☐ 需重新設計 (Requires redesign)

**特別說明 (Special Notes)**:
[Any important notes or caveats]

---

## 附件 / Attachments

**測試照片 (Test Photos)**:
- [Description of photos]

**測試影片 (Test Videos)**:
- [Description of videos]

**Log 檔案 (Log Files)**:
- [File names and descriptions]

**測試資料原始檔 (Raw Data Files)**:
- [File names and locations]

---

**測試執行人員 (Test Performed By)**:
- 主要測試 (Primary): [Name] - [Signature] - [Date]
- 協助測試 (Assisted): [Names]

**測試審核 (Test Reviewed By)**:
- 技術審核 (Technical Review): [Name] - [Signature] - [Date]
- 品質審核 (Quality Review): [Name] - [Signature] - [Date]

**測試核准 (Test Approved By)**:
- 專案經理 (Project Manager): [Name] - [Signature] - [Date]

---

**測試報告編號 (Test Report Number)**: TR-YYYYMMDD-001

**報告版本 (Report Version)**: v1.0

**報告完成時間 (Report Completion Time)**: YYYY-MM-DD HH:MM
```

---

## Tips for Using Templates / 使用範本技巧

### 1. Choose the Right Template
- **Daily log**: Regular end-of-day documentation
- **Troubleshooting**: Significant problems needing detail
- **Test log**: Formal testing and verification

### 2. Don't Fill Every Field
- Use fields relevant to your situation
- Empty sections can be deleted
- Focus on important information

### 3. Be Consistent
- Use same template structure across team
- Maintain consistent terminology
- Follow same naming conventions

### 4. Adapt as Needed
- Templates are starting points, not rigid rules
- Adjust based on project needs
- Add custom sections if necessary

### 5. Review Before Saving
- Check for completeness
- Verify all key information present
- Ensure searchable keywords included
- Confirm generic terminology used

---

**End of Templates Reference**
