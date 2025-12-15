---
name: quarterly-earnings-analyzer
description: "Analyze quarterly earnings across multiple companies to identify trends, patterns, and investment insights. Use when: (1) Analyzing earnings transcripts (JSON/PDF) from multiple companies, (2) Finding cross-company trends and themes, (3) Comparing current quarter with historical data from Project Knowledge, (4) Generating investment summaries with financial metrics directionality (Revenue/Margin/Guidance), (5) Tracking company evolution over quarters"
---

# Quarterly Earnings Analyzer

## Overview

Analyze earnings data across companies, identify trends, generate structured summaries, and maintain historical tracking through Project Knowledge integration.

## Workflow

### 1. Data Collection
Accept data from:
- JSON earnings transcripts (`*_Processed_*.json` from `/mnt/project` or uploads)
- News articles (PDF uploads, or text provided by user)
- Financial data (Excel/CSV files)
- User notes (Markdown/text)

**Note**: If `web_fetch` tool is available, can also accept news article URLs directly.

### 2. Analysis Process

```python
# Extract keywords (filter stopwords)
keywords = extract_high_frequency_keywords(all_text, min_length=3, top_n=50)

# Calculate theme prevalence
themes = {
    'AI': ['ai', 'machine learning', 'neural', 'llm'],
    'Cloud/SaaS': ['cloud', 'saas', 'subscription', 'arr'],
    'Automation': ['automation', 'robotic', 'autonomous'],
    'Semiconductor': ['chip', 'semiconductor', 'wafer', 'foundry'],
    # See references/theme-keywords.md for complete list
}
coverage = {theme: count_companies_mentioning(keywords) for theme in themes}

# Financial metrics directionality
metrics = analyze_sentiment(positive_points, challenges, {
    'revenue': (['growth', 'strong', 'increase'], ['decline', 'weak']),
    'margin': (['expansion', 'improve'], ['pressure', 'compression']),
    'guidance': (['raise', 'optimistic'], ['lower', 'cautious'])
})

# Cluster companies by themes
clusters = group_by_common_themes(companies, themes)
```

### 3. Historical Comparison (Automatic)

Search Project Knowledge for previous quarter:
```python
previous = project_knowledge_search(f"Q{quarter-1} {year} Summary")
if previous:
    qoq_changes = calculate_changes(current, previous)
    # Include in output: AI coverage Q2 68% → Q3 75% (+6.4%)
```

### 4. Output Generation

**Markdown Summary** (primary - optimized for Project Knowledge search):
```markdown
---
quarter: Q3
year: 2025
companies_analyzed: 15
---

# Q3 2025 季度投資要點

## 🎯 執行摘要 (3 takeaways)
## 📊 產業趨勢 (theme coverage rates, QoQ changes)
## 💰 財務表現 (Revenue/Margin/Guidance directionality)
## 🏆 重點公司 (Beat/Miss/Concerns)
## 🌐 產業聚類 (cluster by themes)
## 🔍 獨特洞察 (mentioned by ≤2 companies)
## 📰 外部事件 (from news/web sources)
## 📌 下季追蹤 (watchlist for next quarter)
```

**Excel Dashboard** (optional, if `openpyxl` available):
- Sheet 1: Overview (company count, quarter info)
- Sheet 2: Keyword Heatmap (companies × keywords, color-coded by frequency)
- Sheet 3: Financial Metrics (positive/negative counts, charts)
- Sheet 4: Industry Clusters (grouped companies)
- Sheet 5: QoQ Trends (if previous quarter found)

## Quick Start Examples

**Basic analysis:**
```
User: "分析 Q3 2025，我的 project 有 15 個財報 JSON"
→ Load files, analyze, generate summary + Excel
```

**Add news context:**
```
User: "整合這篇新聞內容: [user pastes article text]"
→ Extract insights, add to "外部事件" section
```
*If web_fetch tool is available, can also provide URL directly.

**Historical comparison:**
```
User: "分析 Q4 2025 並與 Q3 比較"
→ Auto-search Q3 from Project Knowledge, calculate QoQ
```

**Company tracking:**
```
User: "CDNS 過去三季表現？"
→ Search Project Knowledge for quarterly summaries mentioning CDNS
```

## Technical Details

**Required tools:**
- `bash_tool` - file operations
- `view` - read project files
- `create_file` - generate outputs
- `project_knowledge_search` - retrieve historical data

**Optional tools (if available in environment):**
- `web_fetch` - fetch news articles from URLs (gracefully degrade if not available)
- `str_replace` - update tracking files (can use create_file as fallback)

**Python libraries:**
- `json`, `os`, `re`, `collections` - core processing
- `openpyxl` - Excel generation (gracefully skipped if unavailable)

**Key functions:**
```python
def load_earnings_data(directory):
    """Load all *_Processed_*.json files"""
    
def extract_keywords(text, stopwords, min_length=3):
    """Extract high-frequency keywords"""
    
def analyze_themes(companies, theme_definitions):
    """Calculate theme coverage: {theme: {rate, companies}}"""
    
def analyze_financial_metrics(companies):
    """Determine Revenue/Margin/Guidance direction"""
    
def get_previous_quarter(quarter, year):
    """Search Project Knowledge for previous quarter summary"""
    
def generate_summary(data, previous_data=None):
    """Create Markdown quarterly summary with optional QoQ"""
```

## Resources

### references/

**theme-keywords.md** - Complete keyword definitions for all themes (AI, Cloud, Automation, Semiconductor, Healthcare Tech, Edge Computing, Margin Pressure, Growth indicators). Load when customizing theme detection.

**output-templates.md** - Detailed Markdown and Excel structure specifications. Load when user wants to customize output format.

### scripts/

*(Optional - not included by default. Add if deterministic processing needed.)*

Example use cases:
- `calculate_metrics.py` - Pre-compute financial ratios
- `export_to_csv.py` - Convert JSON to tabular format

## Configuration

Customizable via in-context instructions (no separate config file needed):

**Adjust themes:**
```
"除了預設主題，也追蹤 'Robotics' 和 'Energy Efficiency'"
```

**Filter companies:**
```
"只分析市值 >$10B 的公司"
```

**Change output:**
```
"不要生成 Excel，只要 Markdown"
```

## Best Practices

1. **Naming convention**: Save summaries as `YYYY_Q[N]_Summary.md` in Project Knowledge for easy retrieval
2. **Incremental building**: Start with one quarter, add more for trend analysis
3. **Consistent structure**: Use standard section headers for reliable search
4. **Company tracking**: Optionally create separate `{TICKER}_History.md` files for per-company evolution

## Limitations

- Keyword-based sentiment (not advanced NLP)
- Clustering is rule-based (not ML)
- Excel requires `openpyxl` (gracefully degraded if missing)
- Large datasets (>200 companies) may need batching

