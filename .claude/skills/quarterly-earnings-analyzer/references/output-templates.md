[output-templates.md](https://github.com/user-attachments/files/24169340/output-templates.md)
# Output Templates Reference

Detailed specifications for Markdown and Excel output formats.

## Markdown Summary Structure

```markdown
---
quarter: Q[N]
year: [YYYY]
analysis_date: [YYYY-MM-DD]
companies_analyzed: [count]
data_sources:
  earnings_transcripts: [count]
  news_articles: [count]
  financial_data: [count]
---

# Q[N] [YEAR] 季度投資要點

## 🎯 執行摘要（3 句話總結）
1. [Most important finding with metrics]
2. [Second key finding]
3. [Third key finding or outlook]

## 📊 產業趨勢總覽

### 關鍵主題提及率
| 主題 | 公司數 | 覆蓋率 | QoQ 變化 |
|------|--------|--------|----------|
| AI 相關 | 24/35 | 68.6% | +15% ↑ |
| Growth | 21/35 | 60.0% | +5% ↑ |
| [...]  | [...] | [...] | [...] |

### 新興主題（本季首次出現）
- **[Theme Name]** ([N] companies): [Brief description]

### 消失主題（本季不再提及）
- **[Theme Name]**: Previously mentioned by [N] companies in Q[N-1]

## 💰 財務表現方向

### Revenue Growth
- **正向**: [N] 家 ([percentage]%) - [Company list]
- **負向**: [N] 家 ([percentage]%) - [Company list]
- **方向性**: [✅ 全面正向 / ⚠️ 分化加劇 / ❌ 普遍疲軟]

### Margin Trend
- **Expansion**: [N] 家 - [Company list]
- **Pressure**: [N] 家 - [Company list]
- **方向性**: [Assessment]

### Guidance
- **上調**: [N] 家 ([percentage]%) - [Company list]
- **下調**: [N] 家 - [Company list]
- **方向性**: [Assessment]

## 🏆 重點公司表現

### ⭐ 超預期（Beat Expectations）
**[TICKER] - [Company Name]**
- [Key metric]: [Value] ([change])
- 關鍵事件: [Major developments]
- 🔑 驅動因素: [Primary drivers]

### ⚠️ 需追蹤（Concerns）
**[TICKER] - [Company Name]**
- ❗ [Primary concern]
- 🔍 下季關注: [What to watch]

### 📈 持續強勁
**[TICKER] - [Company Name]**
- [Performance summary]

## 🌐 產業聚類分析

### [Cluster Name]（[N] 家）
**成員**: [Ticker list]
**共同特徵**: [Common themes, metrics]
**內部分化**: [If applicable, sub-groups]

## 🔍 獨特洞察（非共識觀點）

### 洞察 1: [Insight Title]
**來源**: [Data sources]
**發現**: [What was discovered]
**相關公司**: [Companies involved]
**投資含義**: [What this means for investors]

## 📰 重要外部事件

### 產業事件
- **[Event Name]** ([Date]): [Impact description]
  - 相關公司: [Affected companies]

### 政策/法規
- **[Policy Change]**: [Description and impact]

### 競爭動態
- **[Competitive Development]**: [Analysis]

## 📌 下季追蹤清單

### 關鍵問題
- [ ] [Question 1 to answer next quarter]
- [ ] [Question 2]

### 值得關注的公司
- [ ] **[TICKER]**: [Why tracking]

### 產業催化劑
- [ ] [Upcoming event or data point]

---

**分析完成日期**: [YYYY-MM-DD]
**下次更新**: [Next quarter date]
```

## Excel Dashboard Structure

### Sheet 1: Overview
- Cell A1: "季度分析 Dashboard"
- Cell A3: "分析季度:" B3: "Q[N] [YEAR]"
- Cell A4: "公司數量:" B4: [count]
- Cell A6: "公司 Ticker 列表" (then list in column A starting row 7)

### Sheet 2: Keyword Heatmap
- Row 1: Headers - A1: "關鍵字", B1+: Company tickers
- Column A: Keywords (starting row 2)
- Cells: Count of mentions
- Color coding:
  - Red (>10 mentions): High frequency
  - Orange (5-10): Medium
  - Yellow (1-4): Low
  - White (0): Not mentioned

### Sheet 3: Financial Metrics
- Column A: Metric names (Revenue Growth, Margin Trend, Guidance)
- Column B: Positive count
- Column C: Negative count
- Column D: Positive percentage
- Include bar charts

### Sheet 4: Industry Clusters
- Column A: Cluster name
- Column B: Company tickers (comma-separated)
- Column C: Company count
- Column D: Coverage percentage

### Sheet 5: QoQ Trends (if previous quarter available)
- Column A: Metric
- Column B: Previous quarter value
- Column C: Current quarter value
- Column D: Change (absolute)
- Column E: Change (percentage)
- Include trend sparklines or line charts

## Company Tracking File Structure

```markdown
---
company: [Company Name]
ticker: [TICKER]
sector: [Sector]
last_updated: [YYYY-MM-DD]
---

# [TICKER] 歷史追蹤

## 📊 季度表現軌跡

### Q[N] [YEAR]
- **業績**: [⭐ 超預期 / ✓ 符合 / ⚠️ 低於]
- **Revenue**: [amount] ([YoY change])
- **關鍵事件**: [Events]
- **主題**: [Themes mentioned]
- **評價**: [🟢 看好 / 🟡 中性 / 🔴 謹慎]

[Repeat for each quarter]

## 🎯 長期追蹤指標

| 季度 | Revenue | YoY Growth | Key Metric | Margin | Guidance |
|------|---------|------------|------------|--------|----------|
| [...] | [...] | [...] | [...] | [...] | [...] |

## 💡 投資論點演變

### 當前論點（Q[N] [YEAR]）
1. [Thesis point 1]
2. [Thesis point 2]

### 風險因素
1. [Risk 1]
2. [Risk 2]

## 📝 管理層關鍵言論

### Q[N] [YEAR] Earnings Call
> "[Quote]"  
> — [Name], [Title]
```

## Customization Options

Tell Claude to modify output:
- "不要生成 Excel，只要 Markdown"
- "公司表現區塊要更詳細，加入財務數據表"
- "新增一個區塊追蹤供應鏈關係"
- "執行摘要改成 5 點，並加入量化指標"
