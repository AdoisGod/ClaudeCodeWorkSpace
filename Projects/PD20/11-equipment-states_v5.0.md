# 設備狀態定義

## 概述

本文件定義 PD20 設備的**內部核心狀態**，僅定義狀態「是什麼」，不涉及「怎麼做」。

**設計原則**：
- 專注於狀態定義
- 提供記憶體位址對照
- 不涉及流程實現
- 不涉及控制邏輯

**文件定位**：
```
本文件（11.md）：定義狀態「是什麼」
├─ WatchDog 連線狀態的意義
├─ OperationMode 的值定義
├─ HomeReturnCompleted 旗標的意義
└─ EquipmentAlarm 旗標的意義

其他文件：定義「怎麼做」
├─ 12.md → 各模式的行為差異
├─ 31.md → 原點復歸序列實現
├─ 55.md → PC-PLC 控制介面
├─ 57.md → SECS 狀態映射
└─ 80.md → 異常處理流程
```

---

## WatchDog 連線狀態

### 狀態定義

**記憶體位址**：
```
MR_____ : BOOL;  // WatchDog_Connected
                 // [待填寫] → 填入 EXCEL
```

**狀態意義**：

| 狀態值 | 意義 | 說明 |
|--------|------|------|
| TRUE | 連線正常 | PLC 與 PC 通訊正常 |
| FALSE | 連線中斷 | PLC 與 PC 通訊異常 |

**設計意義**：
- WatchDog 監控 PLC 與 PC 之間的通訊健康度
- 連線狀態影響 PC 是否能讀取資料與發送命令
- PLC 可獨立於 PC 運作（即使 WatchDog = FALSE）

**相關文件**：
- WatchDog 實現機制 → 參考 `56-pc1-status-monitor.md`

---

## 操作模式（OperationMode）

### 模式定義

**記憶體位址**：
```
DM_____ : INT;  // OperationMode (0/1/2)
                // [待填寫] → 填入 EXCEL
```

**模式值定義**：

| 模式值 | 模式名稱 | 說明 |
|--------|---------|------|
| 0 | 維修模式（Maintenance） | 設備維護、調試、測試 |
| 1 | 非作業模式（Non-operation） | 設備待命，不執行檢測 |
| 2 | 作業模式（Operation） | 正常生產作業 |

**設計意義**：
- 操作模式決定設備的運作範圍
- 影響安全防護等級（門檢、光柵、軸互鎖）
- 影響可執行的動作類型

**相關文件**：
- 各模式詳細行為 → 參考 `12-operation-modes.md`
- SECS 狀態映射 → 參考 `57-secs-state-mapping.md`

---

### 模式切換控制

**硬體輸入位址**：
```
In_____ : INT;  // ModeSwitchInput (三切按鈕位置 0/1/2)
                // [待填寫] → 填入 EXCEL
```

**切換方式**：
- 透過操作面板三切按鈕物理切換
- 硬體直接控制（不經過 PC）

**相關文件**：
- 模式切換訊號介面 → 參考 `55-operation-interface.md`
- 切換前置檢查邏輯 → 參考 `12-operation-modes.md`

---

## 原點復歸完成旗標

### 旗標定義

**記憶體位址**：
```
MR_____ : BOOL;  // HomeReturnCompleted
                 // [待填寫] → 填入 EXCEL
```

**旗標意義**：

| 狀態值 | 意義 | 說明 |
|--------|------|------|
| TRUE | 已完成原點復歸 | 所有關鍵軸已回原點並移至安全位置 |
| FALSE | 未完成原點復歸 | 設備位置未確認，不可進入作業模式 |

**設計意義**：
- 確保設備位置正確，避免撞機
- 進入作業模式的必要條件
- 嚴重異常後可能需要重新原點復歸

**設定時機**：
- TRUE：所有關鍵軸完成原點復歸序列
- FALSE：上電、嚴重異常、位置可能偏移

**相關文件**：
- 原點復歸序列實現 → 參考 `31-motion-sequences.md`
- 前置檢查邏輯 → 參考 `57-secs-state-mapping.md`

---

## 異常旗標

### 旗標定義

**記憶體位址**：
```
MR_____ : BOOL;  // EquipmentAlarm (異常旗標)
                 // [待填寫] → 填入 EXCEL

DM_____ : INT;   // AlarmCode (異常代碼，0 = 正常)
                 // [待填寫] → 填入 EXCEL
```

**旗標意義**：

| 旗標 | 值 | 意義 |
|------|-----|------|
| EquipmentAlarm | TRUE | 設備有異常 |
| EquipmentAlarm | FALSE | 設備正常 |
| AlarmCode | 0 | 無異常 |
| AlarmCode | >0 | 具體異常代碼 |

**設計意義**：
- 標示設備當前是否有異常
- AlarmCode 指示具體異常類型
- 部分異常會觸發 Down 狀態（由 57.md 判定）

**相關文件**：
- 異常代碼對照表 → 參考 `80-alarm-management.md`
- 異常處理流程 → 參考 `80-alarm-management.md`
- Down 狀態判定 → 參考 `57-secs-state-mapping.md`

---

## 控制命令

### 命令定義

**記憶體位址**：
```
MR_____ : BOOL;  // CMD_Reset (異常復位命令)
                 // [待填寫] → 填入 EXCEL

MR_____ : BOOL;  // StateChanged (狀態變更旗標)
                 // [待填寫] → 填入 EXCEL
```

**命令意義**：

| 命令 | 意義 | 說明 |
|------|------|------|
| CMD_Reset | 異常復位 | 清除異常旗標，恢復正常狀態 |
| StateChanged | 狀態變更通知 | 通知 PC 設備狀態已變更 |

**設計意義**：
- CMD_Reset 用於異常復原後清除異常旗標
- StateChanged 減少 PC 不必要的輪詢

**相關文件**：
- 異常復位流程 → 參考 `80-alarm-management.md`
- PC 控制介面 → 參考 `55-operation-interface.md`

---

## 記憶體位址彙總

**[待填寫] → 全部填入 EXCEL**

```
[WatchDog 連線]
MR_____ : BOOL;  // WatchDog_Connected

[操作模式]
DM_____ : INT;   // OperationMode (0/1/2)
In_____ : INT;   // ModeSwitchInput (三切按鈕 0/1/2)

[原點復歸]
MR_____ : BOOL;  // HomeReturnCompleted

[異常旗標]
MR_____ : BOOL;  // EquipmentAlarm
DM_____ : INT;   // AlarmCode

[控制命令]
MR_____ : BOOL;  // CMD_Reset
MR_____ : BOOL;  // StateChanged
```

---

## 狀態關係圖

### 基本關係

```
OperationMode (操作模式)
    ├─ 0 (維修) → 詳見 12.md
    ├─ 1 (非作業) → 詳見 12.md
    └─ 2 (作業) → 詳見 12.md
        └─ 前提：HomeReturnCompleted = TRUE

HomeReturnCompleted (原點復歸完成)
    ├─ TRUE → 可切換至作業模式
    └─ FALSE → 拒絕切換至作業模式
        └─ 需執行原點復歸序列 (參考 31.md)

EquipmentAlarm (異常旗標)
    ├─ FALSE → 正常
    └─ TRUE → 異常
        ├─ AlarmCode → 異常代碼 (參考 80.md)
        └─ 可能觸發 Down 狀態 (參考 57.md)

WatchDog_Connected (連線狀態)
    ├─ TRUE → PC 可通訊
    └─ FALSE → PC 無法通訊
        └─ PLC 繼續運作
```

---

## 相關文件索引

### 狀態行為與流程
- `12-operation-modes.md` - 各操作模式詳細行為
- `31-motion-sequences.md` - 原點復歸序列實現
- `57-secs-state-mapping.md` - SECS 狀態映射
- `80-alarm-management.md` - 異常處理流程

### 介面定義
- `50-plc-memory-map.md` - 記憶體映射總表
- `55-operation-interface.md` - PC-PLC 控制介面
- `56-pc1-status-monitor.md` - PC1 狀態監控

---

## 待填寫項目清單

請將以下資訊填入 EXCEL，完成後回傳：

### 記憶體位址（8 個）
```
[ ] WatchDog_Connected - MR 位址
[ ] OperationMode (0/1/2) - DM 位址
[ ] ModeSwitchInput (三切按鈕 0/1/2) - In 位址
[ ] HomeReturnCompleted - MR 位址
[ ] EquipmentAlarm - MR 位址
[ ] AlarmCode - DM 位址
[ ] CMD_Reset - MR 位址
[ ] StateChanged - MR 位址
```

---

## 版本記錄

| 版本 | 日期 | 修改內容 | 修改人 |
|------|------|---------|--------|
| v5.0 | 2025-12-09 | 重大精簡：合併 12.md 基本定義；移除所有流程實現；專注於狀態「是什麼」；嚴格遵守分層原則；大幅減少內容重複 | Yao |
| v4.0 | 2025-12-09 | 重大重構：回歸內部狀態管理；移除 SECS/GEM 相關內容 | Yao |
| v3.0 | 2025-12-07 | 全新架構：新增 WatchDog 連線狀態 | Yao |

---

**文件類型**: 設備狀態定義（核心狀態）  
**最後更新**: 2025-12-09  
**維護者**: Yao  
**適用範圍**: 所有需要引用設備狀態的文件
