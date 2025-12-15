# Terminology Guide and Checklists
# 術語指南與檢查清單

This file contains terminology mappings and detailed checklists.

---

## Equipment Terminology Mapping / 設備術語對應

### Why Use Generic Terms / 為何使用通用術語

**Benefits / 優點**:
1. **Reusability**: Cases apply across projects
2. **Knowledge Transfer**: Easier to understand for new team members
3. **Pattern Recognition**: Similar problems identified across equipment
4. **Documentation Value**: Increases long-term usefulness

**Format / 格式**:
Always include both in documentation:
```markdown
**設備背景**:
- 模組: HLight_Z1
  (通用術語: Vertical servo axis for high-intensity light source positioning)
```

---

### PD20 Equipment Terminology Table / PD20 設備術語對照表

| Equipment-Specific<br>設備特定名稱 | Generic Term<br>通用術語 | English Keywords<br>英文關鍵字 | Function<br>功能 |
|----------------------------------|------------------------|------------------------------|----------------|
| **Platform 1 / 平台1** ||||
| HLight_Z1 | High-light vertical axis<br>高光源垂直軸 | Vertical Servo Axis, Light Source Lift | High-intensity illumination positioning |
| Clamp_X | Clamp X axis<br>夾爪X軸 | Linear Clamp Axis (X) | Horizontal clamping position |
| Clamp_Z | Clamp Z axis<br>夾爪Z軸 | Linear Clamp Axis (Z) | Vertical clamping position |
| Conv_R1 | Stage rotary axis 1<br>載台旋轉軸1 | DD Motor Rotary Stage, Rotary Positioning Axis | Workpiece rotation for inspection |
| **Platform 2 / 平台2** ||||
| Conv_R2 | Stage rotary axis 2<br>載台旋轉軸2 | DD Motor Rotary Stage, Rotary Positioning Axis | Workpiece rotation for inspection |
| LLight_Z2 | Low-light vertical axis<br>低光源垂直軸 | Vertical Servo Axis, Light Source Lift | Low-intensity illumination positioning |
| **Door Module / 門模組** ||||
| DCheck_R2 | Door check rotary axis<br>門檢查旋轉軸 | Rotary Inspection Axis, DD Motor | Door surface rotation for inspection |
| Door_X | Door X axis<br>門X軸 | Linear Door Transfer Axis (X) | Door horizontal transfer |
| Door_Z | Door Z axis<br>門Z軸 | Linear Door Transfer Axis (Z) | Door vertical transfer |
| **Material Handling / 物料搬運** ||||
| SLOT_Z | Slot vertical axis<br>槽位垂直軸 | Vertical Linear Axis, Slot Access | FOUP slot access |
| **Measurement / 量測系統** ||||
| SD8 | Laser sensor 8<br>雷射感測器8 | Laser Distance Sensor, Height Measurement | Surface height detection |
| SD13 | Laser sensor 13<br>雷射感測器13 | Laser Distance Sensor, Height Measurement | Surface height detection |
| GT2 | Height sensor 2<br>高度感測器2 | Capacitive Height Sensor | Precise height measurement |

### General Motion System Components / 通用運動系統元件

| PD20 Specific | Generic Term | Description |
|--------------|--------------|-------------|
| KV-XL | Industrial PLC | Main controller |
| Yaskawa Σ-7 | AC Servo Drive | Servo motor driver |
| Panasonic MINAS A6 | AC Servo Drive | Servo motor driver |
| Oriental Motor AZD | Integrated Stepper | Stepper motor with driver |
| Keyence KV-L5 | Digital I/O Module | I/O expansion |

---

## Status Indicators Guide / 狀態指標指南

### When to Use Each Indicator / 何時使用各指標

#### Task/Problem Status

| Indicator | Meaning | When to Use | Example |
|-----------|---------|-------------|---------|
| ✅ | Completed / Resolved / Pass | Task finished, problem solved, test passed | ✅ HLight_Z1 問題已解決 |
| ❌ | Failed / Unresolved / Fail | Task not completed, problem persists, test failed | ❌ Conv_R2 定位仍不穩定 |
| ⚠️ | Warning / Partial / Needs Attention | Partially complete, works but with issues | ⚠️ 定位精度改善但未達標 |
| ⏳ | In Progress / Pending / Monitoring | Currently working on, waiting, or monitoring | ⏳ 持續監控參數穩定性 |

#### Priority Indicators

| Indicator | Priority Level | When to Use | Response Time |
|-----------|---------------|-------------|---------------|
| 🔴 | Urgent / Critical | Must fix immediately, blocks production | Within hours |
| 🟡 | High / Important | Should fix soon, impacts efficiency | Within 1-2 days |
| 🟢 | Normal / Low | Fix when convenient, minor issues | Within 1 week |

#### Verification Status

| Indicator | Status | Test Requirements | Example |
|-----------|--------|-------------------|---------|
| ✅ Verified | Fully verified | Met minimum test cycles, monitored adequate time | ✅ 50次循環測試無異常 |
| ⚠️ Monitoring | Appears OK but monitoring | Initial tests pass, long-term monitoring ongoing | ⚠️ 10次測試通過，持續觀察 |
| ❌ Incomplete | Not yet verified | Insufficient testing or verification failed | ❌ 僅測試3次，需更多驗證 |

### Emoji Usage Rules / 表情符號使用規則

**✅ ALLOWED (Status indicators only) / 允許使用（僅狀態指標）**:
- ✅ ❌ ⚠️ ⏳ (Status)
- 🔴 🟡 🟢 (Priority)

**❌ NOT ALLOWED (Decorative emojis) / 不允許使用（裝飾性表情）**:
- 🎉 🎊 ⭐ ✨ 💪 🔥 💡 👍 🚀
- Any emojis not in allowed list
- Excessive use even of allowed emojis

**Examples / 範例**:

❌ **Wrong**:
```markdown
🎉 今天超棒的！完成了很多工作！💪
✨ HLight_Z1 終於修好了！🚀
⭐ 測試全過！讚！👍
```

✅ **Right**:
```markdown
## 今日完成項目

### HLight_Z1 響應優化
**狀態**: ✅ Completed
**驗證**: 50 次測試通過
**下一步**: ⏳ 持續監控 48 小時
```

---

## Detailed Checklists / 詳細檢查清單

### Morning Review Checklist / 早晨回顧檢查清單

**Time**: 8:00-8:30 AM  
**Duration**: 15-30 minutes

- [ ] **Open Claude and query yesterday's log**
  - Query: "看一下昨天的工作紀錄"
  
- [ ] **Review completed tasks**
  - What was accomplished?
  - Any unexpected results?
  - Lessons learned?

- [ ] **Check pending tasks**
  - Which tasks carried over?
  - Are they still relevant?
  - Any new dependencies?

- [ ] **Note unresolved issues**
  - What problems remain?
  - Blocking progress?
  - Need escalation?

- [ ] **Check for similar past work**
  - Query: "之前有沒有做過類似的X？"
  - Learn from past approaches
  - Avoid repeating mistakes

- [ ] **Set today's priorities**
  - Top 3 must-do items
  - Important but not urgent items
  - Nice-to-have tasks

- [ ] **Identify dependencies**
  - What do I need from others?
  - Who needs something from me?
  - Any coordination required?

- [ ] **Plan time allocation**
  - How much time per task?
  - Buffer time for unexpected issues?
  - Meeting/coordination time?

---

### Problem-Solving Checklist / 解決問題檢查清單

**When**: Problem occurs  
**Duration**: Varies by complexity

#### Phase 1: Initial Response (First 5-10 minutes)

- [ ] **Stop and document symptoms immediately**
  - What exactly happened?
  - When did it occur?
  - What were you doing?
  
- [ ] **Record environmental conditions**
  - Temperature, humidity
  - System load
  - Recent changes

- [ ] **Take photos/videos**
  - Error messages
  - Physical condition
  - Unusual indicators

- [ ] **Note error codes**
  - PLC error codes
  - Drive alarms
  - System messages

- [ ] **Quick safety check**
  - Any safety hazards?
  - Need to stop equipment?
  - Inform others?

#### Phase 2: Search Historical Solutions (5-10 minutes)

- [ ] **Query past logs**
  - Query: "之前有沒有處理過 [module] [symptom]？"
  
- [ ] **Evaluate found solutions**
  - Same symptoms?
  - Same conditions?
  - Was it effective?

- [ ] **Decision point**
  - [ ] Apply historical solution → Go to Phase 4
  - [ ] No match found → Go to Phase 3

#### Phase 3: Systematic Diagnosis (Varies)

- [ ] **List possible causes**
  - Hypothesis 1: [   ] Likelihood: High/Med/Low
  - Hypothesis 2: [   ] Likelihood: High/Med/Low
  - Hypothesis 3: [   ] Likelihood: High/Med/Low

- [ ] **Plan diagnostic sequence**
  - Test highest likelihood first
  - Least invasive tests first
  - Consider test time/effort

- [ ] **For each hypothesis:**
  - [ ] Define test method
  - [ ] Predict expected result if hypothesis correct
  - [ ] Perform test
  - [ ] Document actual result
  - [ ] Conclusion: Confirmed / Rejected / Inconclusive
  - [ ] Record evidence

- [ ] **Continue until root cause found**
  - Don't stop at first plausible cause
  - Verify causation, not just correlation

#### Phase 4: Solution Implementation

- [ ] **Plan solution steps**
  - [ ] List required actions
  - [ ] Identify required tools/parts
  - [ ] Note safety precautions
  - [ ] Estimate time needed

- [ ] **Before making changes**
  - [ ] Record current parameters/settings
  - [ ] Backup relevant data
  - [ ] Note memory addresses
  - [ ] Take photos of current state

- [ ] **Implement solution step by step**
  - [ ] Document each action
  - [ ] Record parameter changes with values
  - [ ] Note any deviations from plan
  - [ ] Capture before/after comparisons

- [ ] **Code changes (if applicable)**
  - [ ] Comment changes in code
  - [ ] Test in safe mode first
  - [ ] Document logic changes

#### Phase 5: Verification (Critical - Don't Skip!)

- [ ] **Determine test requirements**
  - Simple issue: 10-20 cycles minimum
  - Intermittent issue: 50+ cycles minimum
  - Critical system: 100+ cycles + time monitoring

- [ ] **Prepare test environment**
  - [ ] Match original failure conditions
  - [ ] Prepare data collection method
  - [ ] Set up monitoring

- [ ] **Execute verification tests**
  - [ ] Run planned number of cycles
  - [ ] Document each test result
  - [ ] Note any anomalies
  - [ ] Record test conditions

- [ ] **Evaluate test results**
  - [ ] Success rate acceptable?
  - [ ] Any unexpected behaviors?
  - [ ] Need more testing?

- [ ] **Set monitoring plan (if needed)**
  - [ ] Duration: [X] hours/days
  - [ ] What to monitor
  - [ ] Alert conditions
  - [ ] Responsible person

#### Phase 6: Documentation and Prevention

- [ ] **Complete problem documentation**
  - [ ] Clear problem title
  - [ ] Equipment background with generic terms
  - [ ] Symptom description (not diagnosis)
  - [ ] Diagnostic logic shown
  - [ ] Root cause identified
  - [ ] Solution steps detailed
  - [ ] Verification results included

- [ ] **Add prevention measures**
  - [ ] Short-term prevention (immediate actions)
  - [ ] Long-term prevention (systematic improvements)
  - [ ] Documentation updates needed
  - [ ] Procedure changes required

- [ ] **Include lessons learned**
  - [ ] What worked well
  - [ ] What could be better
  - [ ] New knowledge gained
  - [ ] Applicable to other modules?

- [ ] **Add searchable keywords**
  - [ ] Module name
  - [ ] Problem type
  - [ ] Solution category
  - [ ] Relevant technical terms

- [ ] **Update related documents**
  - [ ] Technical specifications
  - [ ] Operating procedures
  - [ ] Maintenance checklists
  - [ ] Training materials

---

### After Solution Checklist / 解決後檢查清單

**When**: Problem has been "solved"  
**Before**: Declaring it "fixed"

- [ ] **Verification is complete**
  - Met minimum test cycles for problem type?
  - Tested under various conditions?
  - No anomalies observed?

- [ ] **Documentation is thorough**
  - All required sections filled?
  - Specific parameters and addresses included?
  - Generic terminology used?
  - Solution is actionable?

- [ ] **Prevention measures included**
  - Short-term actions defined?
  - Long-term improvements identified?
  - Responsibility assigned?
  - Timeline set?

- [ ] **Knowledge capture complete**
  - Lessons learned documented?
  - Applicable to other cases?
  - Keywords added for searchability?
  - Cross-references made?

- [ ] **Communicate as needed**
  - Team members informed?
  - Management updated if significant?
  - Related personnel notified?

- [ ] **Follow-up plan set**
  - Monitoring plan defined?
  - Review date scheduled?
  - Responsible person assigned?

---

### End of Day Checklist / 每日結束檢查清單

**Time**: 5:00-5:30 PM  
**Duration**: 20-30 minutes

#### Information Gathering (5 minutes)

- [ ] **List completed tasks**
  - What was finished today?
  - What were the results?
  - How long did each take?

- [ ] **Note problems solved**
  - What issues were resolved?
  - What were the solutions?
  - Verification status?

- [ ] **Record parameter changes**
  - What parameters changed?
  - Original and new values?
  - Memory addresses?
  - Reasons for changes?

- [ ] **Collect test results**
  - What tests were performed?
  - Pass/fail status?
  - Any interesting findings?

- [ ] **Identify pending items**
  - What's not finished?
  - What needs follow-up?
  - Priority level?
  - Blockers?

#### Log Creation (10-15 minutes)

- [ ] **Prepare summary for Claude**
  - Organize information
  - Have specific details ready
  - Clear about what needs documentation

- [ ] **Create work log**
  - Query: "記錄今天的工作：[summary]"
  - Provide detailed information when asked
  - Review generated content

- [ ] **Quality check generated log**
  - [ ] All tasks documented?
  - [ ] Problems have complete solutions?
  - [ ] Parameters include addresses and values?
  - [ ] Verification results included?
  - [ ] Prevention measures added where applicable?
  - [ ] Generic terminology used?
  - [ ] Tomorrow's tasks clear and prioritized?

- [ ] **Make necessary corrections**
  - Add missing information
  - Clarify unclear points
  - Fix any errors

- [ ] **Add personal notes**
  - Anything not covered?
  - Personal reflections?
  - Ideas for improvement?

#### Preparation for Tomorrow (5 minutes)

- [ ] **Review tomorrow's pending tasks**
  - Clear understanding of priorities?
  - Any preparation needed tonight?
  - Dependencies identified?

- [ ] **Mental preparation**
  - Rough plan for tomorrow?
  - Potential challenges identified?
  - Resources needed?

- [ ] **Save and close**
  - File name correct: `工作紀錄_YYYYMMDD.md`?
  - Saved to project directory?
  - Quick mental review done?

---

### Weekly Review Checklist / 週回顧檢查清單

**Time**: Friday PM (4:00-5:00) or Monday AM (8:00-9:00)  
**Duration**: 45-60 minutes

#### Week Summary (10-15 minutes)

- [ ] **Generate week summary**
  - Query: "彙整本週（MM/DD - MM/DD）的工作紀錄"
  
- [ ] **Review completed work**
  - What major items were finished?
  - Progress vs. planned?
  - Unexpected achievements?

- [ ] **Review problems solved**
  - What issues were resolved?
  - Time spent per issue?
  - Effectiveness of solutions?

- [ ] **Review parameter changes**
  - What parameters adjusted?
  - Trends visible?
  - Stability achieved?

#### Pattern Analysis (15-20 minutes)

- [ ] **Identify recurring problems**
  - Same issue multiple times?
  - Query: "[Problem] 發生幾次了？"
  - Pattern in occurrence?
  - Common root cause?

- [ ] **Analyze parameter trends**
  - Parameters drifting?
  - Query: "[Module] 參數調整歷史"
  - Converging to stable values?
  - Need standardization?

- [ ] **Review time allocation**
  - What took most time?
  - Efficient use of time?
  - Unexpected time sinks?
  - Better approaches available?

- [ ] **Check achievement rate**
  - Tasks completed vs. planned?
  - Reasons for delays?
  - Estimation accuracy?

#### Action Planning (15-20 minutes)

- [ ] **For recurring problems**
  - [ ] Need root cause analysis?
  - [ ] Permanent solution possible?
  - [ ] Specification update required?
  - [ ] Training needed?

- [ ] **For parameter trends**
  - [ ] Create standard values?
  - [ ] Document optimal settings?
  - [ ] Hardware issues indicated?
  - [ ] Procedure updates needed?

- [ ] **For time management**
  - [ ] Process improvements possible?
  - [ ] Automation opportunities?
  - [ ] Training beneficial?
  - [ ] Resource allocation optimal?

- [ ] **For knowledge gaps**
  - [ ] Documentation insufficient?
  - [ ] Need external expertise?
  - [ ] Training required?
  - [ ] Better tools needed?

#### Next Week Planning (10-15 minutes)

- [ ] **Set priorities based on analysis**
  - [ ] Critical issues first
  - [ ] Prevention measures
  - [ ] Improvement projects
  - [ ] Routine tasks

- [ ] **Allocate time strategically**
  - [ ] Known tasks
  - [ ] Buffer for unknowns (30-40%)
  - [ ] Improvement time (10-20%)
  - [ ] Coordination time

- [ ] **Prepare for known challenges**
  - [ ] Difficult tasks identified?
  - [ ] Resources prepared?
  - [ ] Help arranged if needed?

- [ ] **Document weekly review**
  - [ ] Key insights captured?
  - [ ] Actions assigned?
  - [ ] Timeline set?

---

## File Naming Convention Checklist / 檔案命名規範檢查清單

### Before Saving Any Log File

- [ ] **Check file type and use correct format**
  - Daily work log: `工作紀錄_YYYYMMDD.md`
  - Troubleshooting: `故障排除_[Module]_YYYYMMDD.md`
  - Test results: `測試紀錄_[Module]_[TestType]_YYYYMMDD.md`

- [ ] **Verify date format**
  - Year: 4 digits (YYYY)
  - Month: 2 digits (MM) with leading zero
  - Day: 2 digits (DD) with leading zero
  - No separators in date (20251203, not 2025-12-03)

- [ ] **Check module name (if applicable)**
  - Use actual equipment name, not generic
  - Consistent spelling and capitalization
  - No spaces (use underscore if needed)

- [ ] **Verify file extension**
  - Always `.md` for markdown
  - Lowercase extension

- [ ] **Examples of correct names**
  - ✅ `工作紀錄_20251203.md`
  - ✅ `故障排除_HLight_Z1_20251203.md`
  - ✅ `測試紀錄_Platform1_功能測試_20251203.md`

- [ ] **Examples of incorrect names**
  - ❌ `工作紀錄12-03.md` (incomplete date)
  - ❌ `Work Log 2025-12-03.md` (English, wrong format)
  - ❌ `HLight Z1 troubleshooting.md` (spaces, no date)

---

**End of Terminology Guide and Checklists**
