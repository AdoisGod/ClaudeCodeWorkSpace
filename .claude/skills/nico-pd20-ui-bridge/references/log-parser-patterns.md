# 工作紀錄解析模式

## 支援的格式

### 格式 1: 直接定義

**模式**: `(MR|DM)\d+\s*[:：]\s*(.+)`

**範例**:
```
MR1120: SEQ-105_Trigger
DM5200: 裂紋檢測結果起始位址
```

**提取**:
- Address: MR1120
- Content: SEQ-105_Trigger

### 格式 2: 新增語句

**模式**: `新增\s*(訊號)?\s*(MR|DM)\d+\s+(.+)`

**範例**:
```
新增 MR1120 SEQ-105_Trigger
新增訊號 DM5200 裂紋檢測結果
```

### 格式 3: 範圍定義

**模式**: `(MR|DM)(\d+)~(MR|DM)?(\d+)\s*[:：]\s*(.+)`

**範例**:
```
DM5200~5219: 裂紋檢測結果緩衝區
MR1120~1121: SEQ-105 握手訊號
```

### 格式 4: 表格形式

**模式**: `\|\s*(MR|DM)\d+\s*\|.*\|.*\|`

**範例**:
```markdown
| Address | DataType | Content |
|---------|----------|---------|
| MR1120  | Bit      | SEQ-105_Trigger |
| MR1121  | Bit      | SEQ-105_Done |
```

## 信心度計算

- 完全匹配正則表達式: 1.0
- 部分匹配: 0.6~0.9
- 需要額外驗證: < 0.8

## 使用範例

```python
import re

patterns = {
    'direct': r'(MR|DM)\d+\s*[:：]\s*(.+)',
    'new': r'新增\s*(訊號)?\s*(MR|DM)\d+\s+(.+)',
    'range': r'(MR|DM)(\d+)~(MR|DM)?(\d+)\s*[:：]\s*(.+)',
    'table': r'\|\s*(MR|DM)\d+\s*\|'
}

for line in log_lines:
    for pattern_name, pattern in patterns.items():
        match = re.search(pattern, line)
        if match:
            # 提取訊號
            break
```
