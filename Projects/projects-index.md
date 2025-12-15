# 專案索引 (Projects Index)

本索引提供工作區內所有專案的快速導航。

---

## 專案清單

| 專案代號 | 名稱 | 類型 | 狀態 | 說明 |
|---------|------|------|------|------|
| PD20 | 自動化視覺檢測設備 | 設備開發 | 開發中 | 半導體 Foup 門板視覺檢測設備 |

---

## PD20 - 自動化視覺檢測設備

### 基本資訊
- **設備類型**: 半導體 Foup 門板視覺檢測設備
- **檢測對象**: FOUP (Front Opening Unified Pod) 門板
- **控制架構**: PLC (Keyence KV-XL) + PC1 (視覺處理) + PC2 (HMI)

### 硬體規模
- **軸數**: 27 軸（伺服 15 + DD 2 + 步進 11）
- **氣缸**: 8 組
- **檢測序列**: 14 個

### 文件架構

```
PD20/
├── 00-09  總覽與導航
│   ├── 00-README_v3_2.md        ← 知識庫導航
│   └── 01-equipment-overview.md ← 設備概述
│
├── 10-19  設備基本定義
│   ├── 11-equipment-states.md   ← 設備狀態定義
│   └── 12-operation-modes.md    ← 操作模式行為
│
├── 20-29  硬體規格
│   ├── 20-axes-specs.md         ← 軸規格
│   ├── 22-sensors-specs.md      ← 感測器規格
│   ├── 23-actuators-specs.md    ← 致動器規格
│   └── 24-door-opening-module.md← 開門模組
│
├── 30-39  動作定義
│   ├── 30-motion-primitives.md  ← 基本動作元件
│   ├── 31-motion-sequences-common.md ← 通用流程
│   ├── 32-motion-sequences-stage1.md ← 載台1檢測
│   ├── 33-motion-sequences-stage2.md ← 載台2檢測
│   ├── 34-motion-sequences-door.md   ← 開門模組檢測
│   ├── 35-actuator-control-reference.md ← 氣缸控制參考
│   └── 36-single-product-discharge.md ← 單一產品排料
│
├── 40-49  安全與互鎖
│   ├── 40-interlock-rules.md    ← 互鎖規則
│   ├── 41-safety-circuits.md    ← 安全電路
│   └── 42-light-curtain-mute.md ← 光柵遮蔽機制
│
├── 50-59  介面定義
│   ├── 50-plc-memory-map.md     ← PLC 記憶體映射
│   ├── 51-vision-photo-handshake.md ← 視覺拍照握手
│   ├── 52-data-buffer-zone.md   ← 資料緩衝區
│   ├── 53-equipment-status.md   ← 設備狀態
│   ├── 54-production-flow-control.md ← 生產流程控制
│   ├── 55-equipment-command.md  ← 設備命令
│   ├── 56-motion-parameter.md   ← 運動參數
│   ├── 57-mode-switch.md        ← 模式切換
│   ├── 58-sequence-monitor.md   ← 序列監控
│   ├── 59-recipe-management.md  ← 料號參數管理
│   └── 60-ui-plc-handshake.md   ← UI-PLC 交握
│
└── 80-89  異常管理
    └── 80-alarm-management.md   ← 異常代碼與處理
```

### 快速查詢

| 想知道... | 查哪個文件 |
|-----------|-----------|
| 設備整體架構？ | 01-equipment-overview.md |
| 文件怎麼找？ | 00-README_v3_2.md |
| 軸規格與行程？ | 20-axes-specs.md |
| 檢測序列流程？ | 31~34-motion-sequences-*.md |
| PC-PLC 介面？ | 50~60-*.md |
| 安全互鎖規則？ | 40-interlock-rules.md |

---

## 相關 Skills

以下 Skills 可協助專案開發：

| Skill | 用途 | 觸發詞 |
|-------|------|--------|
| engineering-log | 工作紀錄管理 | 工作紀錄、記錄工作、查詢紀錄 |
| equipment-documentation-manager | 文件架構管理 | 文件架構、這該放哪、改了要更新哪些 |
| motion-control-troubleshooting | 運動控制故障排除 | 故障診斷、馬達問題、原點復歸失敗 |
| project-coordinator | 跨 Skill 協調 | 檢查同步、週報、進度檢查 |

---

## 版本記錄

| 版本 | 日期 | 變更 |
|------|------|------|
| v1.0 | 2025-12-15 | 初始版本，建立 PD20 專案索引 |
