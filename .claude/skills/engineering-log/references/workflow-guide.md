# Workflow Guide
# 工作流程指南

This guide provides detailed workflows for integrating the engineering log system into daily work.

---

## Daily Engineering Workflow / 每日工程工作流程

### 🌅 Morning Routine (8:00-8:30 AM) - SEARCH Mode

**Objective**: Review yesterday, plan today
**目標**: 回顧昨天，規劃今天

#### Step-by-Step Workflow

**1. Open Claude and Start Review**
```
Trigger phrase: "看一下昨天的工作紀錄"
Alternative: "昨天有什麼待辦事項？"
```

**2. Claude Actions**:
- Calculates yesterday's date
- Searches for `工作紀錄_[YYYYMMDD]`
- Extracts pending tasks
- Highlights unresolved issues
- Summarizes key achievements

**3. User Review**:
- Read through pending tasks
- Note any blockers
- Check if tasks still relevant
- Identify priorities for today

**4. Plan Today's Work**:
```
Follow-up query: "之前有沒有做過類似的X？"
```
- Check if similar work done before
- Learn from past approaches
- Avoid repeating mistakes

**5. Set Daily Goals**:
- List top 3 priorities
- Note any dependencies
- Flag items needing coordination

**Time Investment**: 15-30 minutes
**Value**: Starts day with clear direction and context

---

### 🔧 During Work - MIXED Mode

**Objective**: Solve problems efficiently using history
**目標**: 利用歷史高效解決問題

#### Scenario 1: Problem Occurs

**Step 1: SEARCH Historical Solutions** (5 minutes)
```
Query: "之前有沒有處理過 [module] [symptom] 的問題？"
Example: "之前有沒有處理過 HLight_Z1 響應慢的問題？"
```

**Claude will**:
- Search past work logs
- Find similar symptoms
- Extract previous solutions
- Show verification results

**Step 2: Evaluate Historical Solutions** (2-5 minutes)
- Is problem exactly the same?
- Was solution effective?
- Are conditions similar?
- Can solution be applied directly?

**Step 3: Apply or Adapt Solution** (varies)

**If solution applies directly**:
```
Trigger phrase: "記錄今天套用了 [date] 的解決方案到 [problem]"
```
- Apply solution
- Verify with same test method
- Document outcome

**If solution needs adaptation**:
```
Trigger phrase: "記錄今天的故障排除：[problem]，參考了 [date] 的方法但需要調整..."
```
- Document why adaptation needed
- Record modified approach
- Note differences from original

**If no similar case found**:
- Proceed with systematic diagnosis (see below)

---

#### Scenario 2: New Problem (No Historical Solution)

**Step 1: Immediate Documentation** (3-5 minutes)
```
Trigger phrase: "記錄故障排除：[problem title]"
```
- Record symptoms while fresh
- Note exact time and conditions
- Take photos if helpful
- Document error codes

**Step 2: Systematic Diagnosis** (varies)

**Use structured approach**:
```markdown
1. List possible causes (hypotheses)
2. For each hypothesis:
   - How to test?
   - What would confirm/reject?
   - Test it
   - Document result
3. Continue until root cause found
```

**Real-time Documentation**:
- Record each test attempt
- Note unexpected findings
- Document dead ends (saves time for others)

**Step 3: Solution Implementation**

**While implementing**:
- Document each step
- Record parameter changes with addresses
- Note any deviations from plan
- Capture before/after values

**Step 4: Verification Testing**

**Don't declare "fixed" prematurely**:
```
Minimum tests:
- Simple issues: 10-20 cycles
- Intermittent: 50+ cycles or 24 hours
- Critical: 1 week monitoring
```

**Step 5: Complete Documentation**
```
Trigger phrase: "補充完整的故障排除記錄：[problem]"
```
- Add prevention measures
- Include lessons learned
- Add searchable keywords
- Specify generic terminology

**Total Time**: Varies, but documentation adds only 10-15% overhead

---

#### Scenario 3: Parameter Adjustment

**Before Adjustment**:
```
Query: "查詢 [axis/module] 的參數調整歷史"
```
- Review past adjustments
- Check trends
- Learn from previous attempts
- Understand constraints

**During Adjustment**:
- Record original value
- Document reason for change
- Note memory address
- Record new value

**After Adjustment**:
```
Trigger phrase: "記錄參數調整：[module] [parameter] 從 [old] 改為 [new]"
```
- Verify with testing
- Document result
- Note any side effects
- Update if needed

---

### 🌙 End of Day (5:00-5:30 PM) - CREATE Mode

**Objective**: Document today's work comprehensively
**目標**: 全面記錄今天的工作

#### Step-by-Step Workflow

**1. Prepare Information** (5 minutes)
Before calling Claude, gather:
- Completed tasks list
- Problems solved
- Parameters changed
- Test results
- Tomorrow's pending items

**2. Create Work Log** (10-20 minutes)
```
Trigger phrase: "記錄今天的工作：
- 完成了 [task 1]
- 解決了 [problem]
- 調整了 [parameters]
- 明天需要 [pending items]"
```

**Claude will**:
- Use appropriate template
- Structure information
- Add necessary sections
- Request clarifications if needed

**3. Review and Refine** (5 minutes)
Check generated log for:
- [ ] All tasks documented
- [ ] Problems have solutions
- [ ] Parameters have details (addresses, values)
- [ ] Verification results included
- [ ] Prevention measures added
- [ ] Generic terminology used
- [ ] Tomorrow's tasks clear

**4. Save and Close**
- Confirm file name: `工作紀錄_YYYYMMDD.md`
- Save to project directory
- Quick mental review for completeness

**Total Time**: 20-30 minutes
**Value**: Complete knowledge capture, ready for tomorrow's morning review

---

### 📅 Weekly Review (Friday PM or Monday AM) - SEARCH Mode

**Objective**: Identify patterns and plan ahead
**目標**: 識別模式並預先規劃

#### Workflow

**1. Gather Week's Logs** (2-3 minutes)
```
Query: "彙整本週（MM/DD - MM/DD）的工作紀錄"
```

**2. Claude Analyzes** (processed automatically):
- Extracts completed tasks
- Lists problems solved
- Tracks parameter changes
- Identifies recurring issues
- Notes pending items

**3. Pattern Analysis** (10-15 minutes)
Review Claude's summary for:
- **Recurring problems**: Same issue multiple times?
- **Parameter trends**: Drifting parameters?
- **Time sinks**: What took most time?
- **Successes**: What went well?
- **Blockers**: What prevents progress?

**4. Planning Actions** (10 minutes):

**For recurring problems**:
```
Follow-up query: "這個 [problem] 出現幾次了？每次的解決方案是什麼？"
```
- Root cause analysis
- Permanent solution needed?
- Documentation update required?

**For parameter trends**:
```
Query: "查詢 [parameter] 的調整歷史和趨勢"
```
- Is parameter stabilizing?
- Need standardization?
- Hardware issue?

**For time sinks**:
- Can be automated?
- Need better process?
- Training needed?

**5. Next Week Planning**:
- Prioritize based on patterns
- Allocate time for systemic improvements
- Schedule preventive actions

**Total Time**: 30-45 minutes
**Value**: Strategic oversight, continuous improvement

---

## Integration with Other Skills / 與其他技能整合

### With motion-control-troubleshooting Skill

**Workflow**:
```
Daily logs (engineering-log)
    ↓ Structured problem records
motion-control-troubleshooting skill
    ↓ Diagnostic procedures + Solutions
Reusable case database
```

**When to use together**:
1. **During troubleshooting**:
   - Engineering-log: Document specific instance
   - Motion-control: Guide systematic diagnosis

2. **When building knowledge base**:
   - Engineering-log: Capture real cases
   - Motion-control: Extract patterns and create procedures

### With equipment-documentation-manager Skill

**Workflow**:
```
Daily work logs (engineering-log)
    ↓ Accumulate knowledge
Technical specifications (equipment-doc-manager)
    ↓ Formal documentation
Customer deliverables
```

**When to use together**:
1. **Specification updates**:
   - Engineering-log: Track actual changes
   - Equipment-doc-manager: Update formal specs

2. **Knowledge transfer**:
   - Engineering-log: Detailed work history
   - Equipment-doc-manager: Create training materials

### With technical-presentation Skill

**Workflow**:
```
Work logs (engineering-log)
    ↓ Raw data and achievements
Extract and structure (technical-presentation)
    ↓ Professional slides
Management briefings / Customer presentations
```

**When to use together**:
```
Query: "從本月的工作紀錄中提取重點，製作進度報告簡報"
```
- Engineering-log provides content
- Technical-presentation formats for audience

---

## Common Workflows / 常見工作流程

### Workflow 1: Starting New Feature Development

**Day 1**:
```
Morning: "這個功能之前有沒有類似的開發經驗？"
→ Search for similar features
→ Learn from past approaches

Evening: "記錄今天開始開發 [feature]，設計了 [approach]"
→ Document initial design
→ Note design decisions
```

**During Development**:
- Daily end-of-day logging
- Problem documentation as they occur
- Parameter tracking

**Feature Complete**:
```
Query: "彙整 [feature] 的開發歷程"
→ Summary for documentation
→ Lessons learned capture
```

---

### Workflow 2: Commissioning New Module

**Pre-commissioning**:
```
Query: "類似模組的調機經驗？"
→ Review past commissioning
→ Prepare checklist
→ Anticipate issues
```

**During Commissioning**:
```
Real-time: "記錄 [module] 調機過程"
→ Document each adjustment
→ Track parameter evolution
→ Note unexpected behaviors
```

**Post-commissioning**:
```
Query: "彙整 [module] 調機記錄，建立標準程序"
→ Create procedure document
→ Capture optimal parameters
→ Document lessons learned
```

---

### Workflow 3: Recurring Problem Management

**Problem Identified as Recurring**:
```
Query: "[Problem] 發生幾次了？趨勢如何？"
→ Get occurrence history
→ Analyze pattern
→ Check if solutions working
```

**Root Cause Investigation**:
```
Review all instances:
- What's common?
- What's different?
- Is "fix" temporary?
- What's real root cause?
```

**Permanent Solution**:
```
Document: "建立 [problem] 的根本解決方案和預防措施"
→ Implement systematic fix
→ Update specifications
→ Create prevention procedure
→ Monitor long-term
```

---

## Time Management / 時間管理

### Recommended Time Allocation

**Daily Documentation**:
- Morning review: 15-30 min
- Real-time notes: ~5% work time
- End-of-day log: 20-30 min
- **Total: ~45-60 min/day**

**Weekly Activities**:
- Weekly review: 30-45 min
- Pattern analysis: 15-30 min
- **Total: ~1 hour/week**

**Return on Investment**:
- Faster problem solving (30-50% time savings)
- Reduced repeated mistakes
- Better knowledge transfer
- Improved decision making

**Net benefit**: 2-3x time invested

---

## Efficiency Tips / 效率技巧

### 1. Document While Working
- Don't wait until end of day
- Capture symptoms immediately
- Record steps as you go
- Photos/videos in the moment

### 2. Use Voice Notes (then type)
- Speak observations during work
- Type up later in proper format
- Don't lose real-time insights

### 3. Template Customization
- Create personal shortcuts
- Pre-fill common sections
- Adapt templates to your style

### 4. Batch Similar Tasks
- Review multiple logs together
- Update related documents
 at once
- Plan similar future tasks together

### 5. Use Claude Effectively
- Specific queries get better results
- Provide context when needed
- Review and refine outputs
- Build on previous conversations

---

**End of Workflow Guide**
