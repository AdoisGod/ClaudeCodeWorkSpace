# 同步報告 - {{timestamp}}

## 變更來源

- {{source_description}}

## Excel 變更

### 新增 ({{excel_create_count}}筆)

{{#excel_creates}}
- [{{sheet}}] Row {{row}}: {{address}} - {{content}}
{{/excel_creates}}

### 更新 ({{excel_update_count}}筆)

{{#excel_updates}}
- [{{sheet}}] Row {{row}}: {{change_description}}
{{/excel_updates}}

### 刪除 ({{excel_delete_count}}筆)

{{#excel_deletes}}
- [{{sheet}}] Row {{row}}: {{address}} - {{content}}
{{/excel_deletes}}

## Markdown 變更

{{#markdown_files}}
### {{filename}}

{{#changes}}
- {{action}}: {{description}}
{{/changes}}
{{/markdown_files}}

## 統計

- 總變更: {{total_changes}} 筆
- Excel: {{excel_total}} 筆
- Markdown: {{markdown_total}} 處

---

報告生成時間: {{generation_time}}
