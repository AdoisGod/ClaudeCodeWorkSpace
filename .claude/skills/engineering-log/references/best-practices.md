# Documentation Best Practices
# 文件最佳實踐

## Core Principles / 核心原則

### 1. Write Symptoms, Not Diagnoses / 寫症狀，而非診斷

**Why this matters / 為何重要**:
- Symptoms are objective facts
- Diagnoses can be wrong
- Others need to verify your thinking
- Pattern recognition requires symptom data

**Examples / 範例**:

❌ **Wrong - Writing Diagnosis**:
```
Problem: "編碼器電池沒電了"
(Encoder battery is dead)
```
**Issue**: This is your conclusion, not observation. If wrong, misleads others.

✅ **Right - Writing Symptoms**:
```
Symptoms:
- 原點復歸時有時成功(約60%)，有時失敗
- 失敗時錯誤代碼 E0023 (絕對位置資料異常)
- PLC 重啟後首次原點復歸必定失敗
- 手動模式下重複執行，成功率隨溫度上升而改善
- 錯誤發生無明顯規律性，但偏向早晨剛開機時

Through diagnosis: Measured encoder battery voltage 1.8V (standard >2.5V)
Root cause: Encoder battery insufficient voltage causing absolute position data loss
```

### 2. Document Diagnostic Logic / 記錄診斷邏輯

**Why this matters / 為何重要**:
- Shows your thinking process
- Helps others learn
- Proves thoroughness
- Valuable for similar future problems

**Structure / 結構**:
```markdown
## 診斷過程

### 假設 1: [Your hypothesis]
**為什麼懷疑這個 (Why suspected)**: [Reasoning]
**如何驗證 (How verified)**: [Test method]
**預期結果 (Expected)**: [What should happen if correct]
**實際結果 (Actual)**: [What happened]
**結論 (Conclusion)**: ✅ Confirmed / ❌ Rejected

### 假設 2: [Next hypothesis]
[Same structure]
```

**Example / 範例**:
```markdown
### 假設 1: EtherCAT 通訊問題
**為什麼懷疑**: HLight_Z1 響應慢，可能是通訊延遲
**如何驗證**: 
1. 檢查 EtherCAT 診斷資訊
2. 測量 cycle time
3. 檢查 frame error count

**預期結果**: 如果是通訊問題，應看到：
- Cycle time 不穩定
- Frame errors 存在
- Delayed frames 計數器增加

**實際結果**:
- Cycle time 穩定在 4ms
- No frame errors
- No delayed frames
- 但 4ms 對高速應用來說較慢

**結論**: ⚠️ 部分相關
通訊本身穩定，但 4ms 週期過長。調整為 2ms 後響應改善。

### 假設 2: 伺服驅動器參數設定
**為什麼懷疑**: Cycle time 調整後仍有偶發延遲
**如何驗證**: 檢查濾波器和響應參數設定
**實際結果**: 低通濾波器設定 500Hz，偏保守
**結論**: ✅ Confirmed - 調整為 1000Hz 後問題解決
```

### 3. Make Solutions Actionable / 使解決方案可操作

**Why this matters / 為何重要**:
- Anyone can replicate your solution
- Reduces troubleshooting time
- Enables knowledge transfer
- Ensures consistency

**Required Elements / 必要元素**:
1. **Specific parameters** / 具體參數
2. **Memory addresses** / 記憶體位址
3. **Step-by-step instructions** / 逐步說明
4. **Before/After values** / 前後值
5. **Tools needed** / 需要的工具

**Examples / 範例**:

❌ **Wrong - Vague**:
```
Solution: "調整了伺服參數"
(Adjusted servo parameters)
```

✅ **Right - Actionable**:
```
Solution:
1. 使用 Keyence KV STUDIO 開啟 PLC 程式
2. 修改 HLight_Z1 最大速度參數：
   - 位址: DM1000
   - 原值: 1000 mm/s
   - 新值: 1200 mm/s
   - 修改原因: 提升生產效率
   
3. 調整加速度參數：
   - 位址: DM1001
   - 原值: 2000 mm/s²
   - 新值: 2500 mm/s²
   - 修改原因: 配合速度增加

4. 下載程式至 PLC 並重啟

5. 驗證方法：
   - 執行 50 次循環測試
   - 測量實際移動時間
   - 確認無過沖或震動
```

### 4. Verify Thoroughly / 徹底驗證

**Why this matters / 為何重要**:
- One success doesn't mean "fixed"
- Intermittent problems need extensive testing
- Prevents premature closure
- Builds confidence

**Minimum Verification Standards / 最低驗證標準**:

| Problem Type | Minimum Tests | Duration | Why |
|-------------|---------------|----------|-----|
| Simple, consistent issues | 10-20 cycles | 1-2 hours | Ensure basic repeatability |
| Intermittent issues (10-30% rate) | 50+ cycles | 4-8 hours | Statistical significance |
| Rare intermittent (<10% rate) | 100+ cycles | 24+ hours | Catch rare occurrences |
| Critical systems | 200+ cycles | 1 week+ | Production confidence |

**Verification Documentation**:
```markdown
## 驗證結果

**測試方法**:
[Describe test procedure]

**測試條件**:
- 環境溫度: [Value]
- 負載條件: [Conditions]
- 測試時段: [Time period]

**測試結果**:
- 測試次數: [Count] cycles
- 成功次數: [Count]
- 失敗次數: [Count]
- 成功率: [Percentage]
- 測試期間: [Duration]

**異常觀察**:
[Any unexpected behaviors, even if minor]

**結論**: 
✅ Verified - Ready for production
⚠️ Needs More Testing - Observed [issue]
❌ Not Fixed - Problem still exists
```

### 5. Use Generic Terminology / 使用通用術語

**Why this matters / 為何重要**:
- Makes documentation reusable
- Helps with knowledge transfer
- Easier to find similar cases
- Valuable across projects

**How to Apply / 如何應用**:

**Always include both / 始終包含兩者**:
1. Equipment-specific name (for search)
2. Generic description (for understanding)

**Format / 格式**:
```markdown
**設備背景**:
- 模組: HLight_Z1
  (通用術語: Vertical servo axis for high-intensity light source positioning)
```

**Common Mappings / 常用對應**:

| Equipment-Specific | Generic Term | Use Case |
|-------------------|--------------|----------|
| HLight_Z1 | Vertical servo axis for light source | Positioning system |
| Clamp_X, Clamp_Z | Linear clamp axes (X/Z) | Material handling |
| Conv_R1, Conv_R2 | DD motor rotary stages | Rotational positioning |
| DCheck_R2 | Rotary inspection axis | Door checking |
| SLOT_Z | Vertical linear axis | Slot access |

**Example in Context / 實際應用範例**:
```markdown
## Problem: DCheck_R2 定位精度不足

**設備背景**:
- 專案: PD20
- 模組: DCheck_R2
- 通用術語: Rotary axis for door inspection (DD motor driven)
- 傳動方式: Direct drive with 1:5 harmonic reducer

**問題描述**:
旋轉定位精度 ±0.2°，需求為 ±0.1°

**根本原因**:
齒輪背隙 (gear backlash) 造成反向運動時的定位誤差

**解決方案**:
實施單向接近法 (unidirectional approach)
- 所有定位動作統一從同一方向接近目標位置
- 設定最小移動距離 5°（小於此值時先後退再前進）

**通用性說明**:
此方案適用於所有使用減速機的旋轉軸，包括：
- Conv_R1/R2 (同樣使用 DD motor + reducer)
- 其他專案中類似的旋轉定位系統
```

### 6. Always Include Prevention / 始終包含預防措施

**Why this matters / 為何重要**:
- Prevents recurrence
- Shows complete thinking
- Helps with continuous improvement
- Reduces long-term maintenance

**Two Types of Prevention / 兩種預防類型**:

**Short-term / 短期預防**:
- Quick actions
- Immediate implementation
- Prevent immediate recurrence

**Long-term / 長期預防**:
- Systematic improvements
- Design changes
- Process improvements

**Template / 範本**:
```markdown
## 預防措施

### 短期預防 (Immediate):
1. [Quick action 1]
   - 實施方式: [How]
   - 責任人: [Who]
   - 完成時間: [When]

2. [Quick action 2]
   [Same structure]

### 長期預防 (Long-term):
1. [Systematic improvement 1]
   - 改善目標: [Goal]
   - 實施計畫: [Plan]
   - 預估時間/成本: [Estimate]
   - 預期效益: [Expected benefit]

2. [Systematic improvement 2]
   [Same structure]

### 文件更新:
- [ ] 更新技術規格: [Which docs]
- [ ] 更新操作程序: [Which procedures]
- [ ] 更新檢查清單: [Which checklists]
- [ ] 新增訓練教材: [What content]

### 標準化:
[How to prevent similar issues in other modules/projects]
```

---

## Common Mistakes to Avoid / 常見錯誤避免

### ❌ Mistake 1: Over-Use of Emojis

**Problem**:
```markdown
🎉 今天完成了超棒的工作！ 💪
✨ HLight_Z1 問題終於解決了！ 🎊
⭐ 測試全部通過！ 🔥
```

**Why it's bad**:
- Unprofessional
- Distracting
- Reduces searchability
- Makes document look childish

**Correct approach**:
```markdown
## 今日完成項目

### HLight_Z1 響應延遲問題

**狀態**: ✅ Resolved
**驗證**: 50 次循環測試全部通過
**結果**: 響應時間從 300ms 降至 150ms
```

**Allowed emojis (status indicators only)**:
- ✅ Completed/Pass
- ❌ Failed
- ⚠️ Warning/Partial
- ⏳ In Progress
- 🔴🟡🟢 Priority indicators

### ❌ Mistake 2: Excessive Nested Bullets

**Problem**:
```markdown
## 問題排除
- 問題
  - 症狀
    - 發生時機
      - 早上
        - 溫度低時
          - 特別是在 15°C 以下
            - 而且濕度高的時候
```

**Why it's bad**:
- Hard to read
- Lost in nested levels
- Makes simple things complex
- Reduces clarity

**Correct approach**:
```markdown
## 問題排除

**症狀**: HLight_Z1 原點復歸失敗

**發生條件**:
- 時機: 早晨剛開機時
- 環境: 溫度 <15°C 且濕度 >70%
- 頻率: 約 60% 機率發生

[Continue with flat, clear structure]
```

**Rule**: Maximum 2 levels of bullets

### ❌ Mistake 3: Vague Descriptions

**Problem**:
```markdown
## 今天的工作
- 調整了一些參數
- 修了一些問題
- 測試了幾個功能
```

**Why it's bad**:
- Useless for future reference
- Can't replicate
- Can't search
- No knowledge transfer

**Correct approach**:
```markdown
## 今日完成項目

### 1. HLight_Z1 參數優化
**調整內容**:
- 最大速度: 1000 → 1200 mm/s (DM1000)
- 加速度: 2000 → 2500 mm/s² (DM1001)
**原因**: 提升生產效率 8%
**驗證**: 50 次循環測試，無過沖
```

### ❌ Mistake 4: Premature "Fixed" Declaration

**Problem**:
```markdown
問題: HLight_Z1 偶發性延遲
解決: 調整了參數
結果: 測試 3 次都正常了！✅ Fixed!
```

**Why it's bad**:
- 3 tests not enough for intermittent issue
- Problem might return
- Wastes time when it recurs
- Damages credibility

**Correct approach**:
```markdown
問題: HLight_Z1 偶發性延遲 (約 10% 發生率)

解決方案: [Details]

驗證測試:
- 測試次數: 100 cycles
- 測試時間: 8 hours
- 失敗次數: 0
- 監控狀態: ⏳ Continuing monitoring for 1 week

狀態: ⚠️ Solution appears effective, monitoring ongoing
```

### ❌ Mistake 5: Missing Context

**Problem**:
```markdown
Changed DM1000 from 100 to 150
Result: Fixed!
```

**Why it's bad**:
- What is DM1000?
- What was the problem?
- Why 150?
- How to verify?

**Correct approach**:
```markdown
## HLight_Z1 響應延遲問題

**設備背景**:
- 模組: HLight_Z1 (High-light vertical servo axis)
- 驅動器: Yaskawa Σ-7

**問題**: 響應時間 >300ms, 需求 <200ms

**解決方案**:
調整 EtherCAT cycle time
- 參數: EtherCAT Master Cycle Time
- 位址: DM1000
- 原值: 4 ms (100 in DM units, 100×0.04ms)
- 新值: 2 ms (50 in DM units, 50×0.04ms)
- 原因: 4ms 週期對高速應用響應不足

**驗證**: 響應時間降至 150ms (50 次測試)
```

---

## Quality Checklist / 品質檢查清單

Before saving any work log, verify:

### Content Quality / 內容品質
- [ ] Symptoms described objectively (not just diagnoses)
- [ ] Diagnostic logic clearly shown
- [ ] Solutions are actionable with specific details
- [ ] Verification is thorough and documented
- [ ] Prevention measures included
- [ ] Generic terminology used where applicable

### Format Quality / 格式品質
- [ ] No excessive emojis (only status indicators)
- [ ] Maximum 2 levels of bullet nesting
- [ ] Clear section headers
- [ ] Tables used appropriately for parameter data
- [ ] Consistent terminology

### Completeness / 完整性
- [ ] All required sections filled
- [ ] Memory addresses specified where relevant
- [ ] Time/date information included
- [ ] Keywords added for searchability
- [ ] Status indicators used correctly

### Reusability / 可重用性
- [ ] Generic terms included
- [ ] Context sufficient for others to understand
- [ ] Problem patterns identifiable
- [ ] Solution can be replicated
- [ ] Lessons learned documented

---

## Writing Style Guide / 寫作風格指南

### Tone / 語氣
- Professional but not overly formal
- Factual and objective
- Concise and clear
- Technical but understandable

### Language / 語言
- Use active voice: "調整參數" not "參數被調整"
- Be specific: "1200 mm/s" not "比較快的速度"
- Use technical terms correctly
- Include units always

### Structure / 結構
- Start with most important information
- Use parallel structure in lists
- Group related information
- Separate facts from interpretations

---

## Advanced Tips / 進階技巧

### 1. Cross-Referencing
Link related logs and documents:
```markdown
**相關工作紀錄**:
- [工作紀錄_20251115](工作紀錄_20251115.md) - 類似問題
- [工作紀錄_20251120](工作紀錄_20251120.md) - 相關參數調整

**相關技術文件**:
- [20-axes-specs.md](20-axes-specs.md) - HLight_Z1 規格
- [40-interlock-rules.md](40-interlock-rules.md) - 安全聯鎖規則
```

### 2. Version Control Awareness
Document when things changed:
```markdown
**參數變更歷史**:
- v1.0 (2025-11-01): 初始設定 1000 mm/s
- v1.1 (2025-11-15): 調整為 1200 mm/s (效率優化)
- v1.2 (2025-11-25): 調降為 600 mm/s (機械限制)
```

### 3. Lessons Learned Section
Always reflect:
```markdown
## 本次學習

**技術層面**:
- 小於 5° 的旋轉移動因齒輪背隙可能無效
- 單向接近法是有效的背隙補償策略

**流程層面**:
- 應先查閱歷史紀錄再開始診斷
- 系統性方法比trial-and-error更有效

**下次改進**:
- 建立參數標準化表格
- 增加自動化測試腳本
```

---

**End of Best Practices Guide**
