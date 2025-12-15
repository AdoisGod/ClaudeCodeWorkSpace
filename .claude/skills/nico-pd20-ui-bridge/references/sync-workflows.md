# 同步工作流程詳細說明

## Workflow 1: 從工作紀錄同步

### Phase 1: 讀取與解析

```python
import glob
import re

# 1. 識別最新工作紀錄
logs = sorted(glob.glob("/mnt/project/工作紀錄_*.md"))
latest_log = logs[-1]

# 2. 讀取內容
with open(latest_log, 'r', encoding='utf-8') as f:
    content = f.read()

# 3. 提取訊號（使用 log-parser-patterns.md 中的模式）
patterns = {
    'direct': r'(MR|DM)\d+\s*[:：]\s*(.+)',
    'new': r'新增\s*(訊號)?\s*(MR|DM)\d+\s+(.+)',
    'range': r'(MR|DM)(\d+)~(MR|DM)?(\d+)\s*[:：]\s*(.+)',
}

extracted_signals = []
for line in content.split('\n'):
    for pattern_name, pattern in patterns.items():
        match = re.search(pattern, line)
        if match:
            # 提取並儲存
            signal = {
                'address': match.group(1) + match.group(2),  # 依pattern調整
                'content': match.group(...),
                'confidence': calculate_confidence(...),
                'source_line': line
            }
            extracted_signals.append(signal)
```

### Phase 2: 讀取現有 Excel

```python
import openpyxl
import yaml

# 載入配置
with open('/mnt/skills/user/nico-pd20-ui-bridge/references/excel-config.yaml') as f:
    config = yaml.safe_load(f)

# 載入 Excel
wb = openpyxl.load_workbook('/mnt/project/PD20_Automaton_PLC交握表_vol1_12012.xlsx')

# 動態識別工作表
def should_exclude(sheet_name, patterns):
    import re
    for pattern in patterns:
        if re.match(pattern, sheet_name):
            return True
    return False

def identify_sheet_role(sheet):
    headers = [cell.value for cell in sheet[1]]
    has_required = all(col in headers for col in ['Address', 'DataType', 'Content'])
    if has_required:
        return 'signal_definition'
    if headers[0] in ['Errcode', '料號清單'] or headers.count(None) > len(headers) * 0.5:
        return 'exclude'
    return 'unknown'

signal_sheets = []
for sheet_name in wb.sheetnames:
    if should_exclude(sheet_name, config['exclude_patterns']):
        continue
    sheet = wb[sheet_name]
    if identify_sheet_role(sheet) == 'signal_definition':
        signal_sheets.append(sheet_name)

# 提取現有訊號
existing_signals = {}
for sheet_name in signal_sheets:
    sheet = wb[sheet_name]
    for row_idx in range(2, sheet.max_row + 1):
        address = sheet[f'A{row_idx}'].value
        content = sheet[f'F{row_idx}'].value
        if address and content:
            existing_signals[address] = {
                'sheet': sheet_name,
                'row': row_idx,
                'content': content
            }
```

### Phase 3: 衝突檢查

```python
conflicts = []

# 檢查位址重複
for signal in extracted_signals:
    addr = signal['address']
    if addr in existing_signals:
        conflicts.append({
            'type': 'address_duplicate',
            'address': addr,
            'existing': existing_signals[addr],
            'new': signal
        })

if conflicts:
    print(f"⚠️ 發現 {len(conflicts)} 個衝突")
    for conf in conflicts:
        print(f"- {conf['address']}: {conf['existing']['content']} vs {conf['new']['content']}")
    # 停止並詢問使用者
    return
```

### Phase 4: 生成變更清單

```python
changes = {
    'excel': {'create': [], 'update': [], 'delete': []},
    'markdown': {}
}

# 判斷訊號應插入哪個工作表
def determine_target_sheet(signal):
    # 根據 Content 判斷
    content = signal['content']
    if 'Trigger' in content or 'Done' in content:
        # 拍照握手 → 找對應的工作表
        # 需要進一步判斷或詢問使用者
        pass
    # ... 其他邏輯
    return target_sheet

for signal in extracted_signals:
    if signal['address'] not in existing_signals:
        target_sheet = determine_target_sheet(signal)
        changes['excel']['create'].append({
            'sheet': target_sheet,
            'signal': signal
        })
```

### Phase 5: 執行同步

```python
# Excel 更新
for create in changes['excel']['create']:
    sheet = wb[create['sheet']]
    new_row = sheet.max_row + 1
    
    signal = create['signal']
    sheet[f'A{new_row}'] = signal['address']
    sheet[f'D{new_row}'] = signal['data_type']  # 需推斷
    sheet[f'E{new_row}'] = signal['pt']
    sheet[f'F{new_row}'] = signal['content']

wb.save('/mnt/project/PD20_Automaton_PLC交握表_vol1_12012.xlsx')

# Markdown 更新
# ... 類似邏輯
```

### Phase 6: 生成報告

使用 `assets/change-report-template.md`
