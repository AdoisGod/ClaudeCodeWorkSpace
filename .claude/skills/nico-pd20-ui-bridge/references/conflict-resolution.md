# 衝突解決策略

## 衝突類型

### Type 1: 位址重複

**定義**: 同一位址被多個訊號使用

**檢測**:
```python
if address in used_addresses:
    conflict = "address_duplicate"
```

**處理**:
1. 顯示衝突訊息
2. 建議替代位址（同區域下一個可用）
3. 等待使用者決策

**範例**:
```
⚠️ 位址重複衝突
- 位址: MR1120
- 現有: SEQ-104_Trigger (門板鑰匙孔拍照)
- 新增: SEQ-105_Trigger (左手把裂紋拍照)
- 建議: 使用 MR1124
```

### Type 2: 位址範圍重疊

**定義**: DM 範圍定義有重疊

**檢測**:
```python
if start1 <= end2 and start2 <= end1:
    conflict = "range_overlap"
```

**處理**:
1. 顯示重疊範圍
2. 建議調整起始位址
3. 等待使用者決策

### Type 3: 命名不一致

**定義**: 同位址在 Excel 和 Markdown 中名稱不同

**處理**:
1. 顯示兩個名稱
2. 詢問使用者使用哪個
3. 統一更新

### Type 4: 資料型態不一致

**定義**: 同位址資料型態定義不同

**處理**:
1. 顯示兩個型態
2. 詢問使用者使用哪個
3. 更新不一致的來源

## 建議位址算法

```python
def suggest_alternative_address(address, used_addresses):
    # 解析位址
    addr_type = 'MR' if address.startswith('MR') else 'DM'
    addr_num = int(address[2:])
    
    # 在同區域搜尋可用位址
    candidate = addr_num + 1
    while f"{addr_type}{candidate}" in used_addresses:
        candidate += 1
    
    return f"{addr_type}{candidate}"
```
