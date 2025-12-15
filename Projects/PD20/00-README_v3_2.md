[00-README_v3_2.md](https://github.com/user-attachments/files/24169658/00-README_v3_2.md)
# PD20 設備技術知識庫

## 文件總覽

本知識庫包含 PD20 自動化檢測設備的完整技術文件，採用分層架構設計。

---

## 文件架構

### 00-09：總覽與導航
- `00-README.md` - 本文件（知識庫導航）
- `01-equipment-overview.md` - 設備概述

### 10-19：設備基本定義
- `11-equipment-states.md` - 設備狀態定義（WatchDog/OperationMode/HomeReturnCompleted/Alarm）
- `12-operation-modes.md` - 操作模式行為差異（維修/非作業/作業）

### 20-29：硬體規格
- `20-axes-specs.md` - 軸規格定義
- `22-sensors-specs.md` - 感測器規格
- `23-actuators-specs.md` - 致動器規格
- `24-door-opening-module.md` - 開門模組

### 30-39：動作定義
- `30-motion-primitives.md` - 基本動作元件
- `31-motion-sequences-common.md` - 通用流程（原點復歸/進出料/搬運/開關門）
- `32-motion-sequences-stage1.md` - 載台1 檢測序列（9 個序列）
- `33-motion-sequences-stage2.md` - 載台2 檢測序列（3 個序列）
- `34-motion-sequences-door.md` - 開門模組檢測序列（2 個序列）
- `35-actuator-control-reference.md` - 氣缸控制快速參考表（9 組）

### 40-49：安全與互鎖
- `40-interlock-rules.md` - 互鎖規則（含維修模式放寬條件）
- `41-safety-circuits.md` - 安全電路
- `42-light-curtain-mute.md` - 光柵遮蔽機制

### 50-59：介面定義（依工作分類）
- `50-plc-memory-map.md` - PLC 記憶體映射總表
- `52-pc1-data-buffer-framework.md` - 視覺資料緩衝區
- `53-photo-handshake-protocol.md` - 視覺拍照握手協議
- `55-operation-interface.md` - PC-PLC 控制介面（進料/出料/命令）
- `56-pc1-status-monitor.md` - PC1 狀態監控
- `57-secs-state-mapping.md` - SECS 狀態映射（PM/IDLE/Run/Down）

### 80-89：異常管理
- `80-alarm-management.md` - 異常代碼與處理流程（待建立）

---

## 文件架構設計理念

### 分層原則

**核心思想**：
- 每個文件專注於自己的職責
- 定義「是什麼」與「怎麼做」分離
- 高內聚、低耦合
- 避免內容重複

**範例說明**：

```
狀態管理分層：

11-equipment-states.md（狀態定義）
├─ 定義狀態「是什麼」
├─ WatchDog = TRUE/FALSE 的意義
├─ OperationMode = 0/1/2 的意義
├─ HomeReturnCompleted = TRUE/FALSE 的意義
└─ 提供記憶體位址對照

12-operation-modes.md（行為差異）
├─ 定義各模式「行為差異」
├─ 維修模式：可做/不可做什麼
├─ 非作業模式：可做/不可做什麼
└─ 作業模式：可做/不可做什麼

31~34.md（流程實現）
├─ SEQ-000：原點復歸序列
├─ SEQ-001~006：進出料/搬運序列
├─ SEQ-101~108：載台1 檢測序列
├─ SEQ-201~203：載台2 檢測序列
└─ SEQ-301~304：開門模組序列

55-operation-interface.md（控制介面）
├─ 進料控制訊號握手
├─ 出料完成訊號
├─ 模式切換訊號
└─ START/STOP/RESET 命令

57-secs-state-mapping.md（狀態映射）
├─ 內部狀態 → SECS 狀態映射邏輯
├─ PM/IDLE/Run/Down 判定條件
└─ EMO/ESTOP 定義

80-alarm-management.md（異常管理）
├─ 異常代碼對照表
├─ 異常處理流程
├─ RESET 邏輯
└─ 哪些異常 → Down
```

---

### 30 層動作序列拆分架構

**v3.0 重構設計**：將原單一文件拆分為模組化結構

```
30-motion-primitives.md（基本動作元件）
└─ 軸的基本動作定義（Move/Home/Stop...）

31-motion-sequences-common.md（通用流程）
├─ SEQ-000：原點復歸
├─ SEQ-001：入料流程
├─ SEQ-002：出料流程
├─ SEQ-003：天車搬運
├─ SEQ-004：單雷射量測
├─ SEQ-005：Clamp 雷射量測
├─ SEQ-006：退料流程
├─ SEQ-301：開門流程
└─ SEQ-302：關門流程

32-motion-sequences-stage1.md（載台1 檢測）
├─ SEQ-101：左手把拍照（180°）
├─ SEQ-102：右手把拍照（0°）
├─ SEQ-103：鑰匙孔拍照（90°）
├─ SEQ-104-1：前氣閥拍照
├─ SEQ-104-2：後氣閥拍照
├─ SEQ-105：裂痕拍照
├─ SEQ-106：前氣閥 GT2 量測（90°）
├─ SEQ-107：後氣閥 GT2 量測（270°）
└─ SEQ-108：Y52 雷射厚度量測

33-motion-sequences-stage2.md（載台2 檢測）
├─ SEQ-201：Slot LineScan 拍照
├─ SEQ-202：Foup 內部拍照
└─ SEQ-203：Inner 雷射量測

34-motion-sequences-door.md（開門模組檢測）
├─ SEQ-303：膠條拍照
└─ SEQ-304：Latch 拍照

35-actuator-control-reference.md（氣缸快速參考）
├─ 9 組氣缸控制邏輯
├─ 真空控制系統
├─ 光柵控制系統
└─ 警示燈號系統
```

---

### 50 層介面分類原則

**依工作功能分類，不依 PC 編號**：

```
52-vision-data-buffer.md        ← 視覺資料緩衝（不限 PC1/PC2）
53-vision-photo-handshake.md    ← 視覺拍照握手（不限 PC1）
55-operation-interface.md       ← 控制介面（給所有 PC 用）
56-pc1-status-monitor.md        ← PC1 監控（專屬）
57-secs-state-mapping.md        ← SECS 映射（專屬）

設計理念：
├─ 功能職責優先，避免「該放 PC1 還是 PC2？」的困擾
└─ 容易擴充新功能
```

---

## 快速查詢指南

### 查詢設備狀態邏輯

| 問題 | 查哪個文件 |
|------|-----------|
| OperationMode 是什麼意思？ | 11.md |
| 維修模式能做什麼？ | 12.md |
| SECS 狀態怎麼判定？ | 57.md |
| PC1 監控邏輯？ | 56.md |
| 哪些異常會 Down？ | 80.md（待建） |

---

### 查詢動作流程

| 問題 | 查哪個文件 |
|------|-----------|
| 原點復歸怎麼做？ | 31.md（SEQ-000） |
| 進料流程是什麼？ | 31.md（SEQ-001） |
| 出料流程是什麼？ | 31.md（SEQ-002） |
| 天車搬運流程？ | 31.md（SEQ-003） |
| 開門/關門流程？ | 31.md（SEQ-301/302） |
| 載台1 檢測序列？ | 32.md（SEQ-101~108） |
| 載台2 檢測序列？ | 33.md（SEQ-201~203） |
| 開門模組檢測？ | 34.md（SEQ-303/304） |
| 基本動作怎麼定義？ | 30.md |
| 氣缸控制怎麼做？ | 35.md |

---

### 查詢安全與互鎖

| 問題 | 查哪個文件 |
|------|-----------|
| 軸之間的互鎖規則？ | 40.md |
| 維修模式互鎖放寬？ | 40.md |
| 安全電路定義？ | 41.md |
| 光柵遮蔽條件？ | 42.md |
| EMO/ESTOP 差異？ | 57.md |

---

### 查詢 PC-PLC 介面

| 問題 | 查哪個文件 |
|------|-----------|
| 進料控制訊號？ | 55.md |
| 出料完成訊號？ | 55.md |
| 視覺拍照握手？ | 53.md |
| LineScan 4 訊號握手？ | 53.md |
| PC1 狀態監控？ | 56.md |
| SECS 狀態上報？ | 57.md |
| 記憶體位址對照？ | 50.md |
| 資料緩衝區定義？ | 52.md |

---

### 查詢硬體規格

| 問題 | 查哪個文件 |
|------|-----------|
| 軸規格與行程？ | 20.md |
| 感測器清單？ | 22.md |
| 氣缸規格？ | 23.md |
| 氣缸控制快速查詢？ | 35.md |
| 開門模組規格？ | 24.md |

---

## 文件關係圖

### 狀態管理關係

```
11-equipment-states.md（內部狀態）
    ├─ 引用自 → 57.md（SECS 映射時使用）
    ├─ 引用自 → 31.md（原點復歸設定 HomeReturnCompleted）
    └─ 引用自 → 80.md（異常設定 EquipmentAlarm）

12-operation-modes.md（模式行為）
    ├─ 引用 → 11.md（OperationMode 值定義）
    ├─ 引用 → 31.md（進料/出料序列）
    ├─ 引用 → 40.md（維修模式互鎖放寬）
    ├─ 引用 → 42.md（光柵遮蔽機制）
    └─ 引用 → 55.md（控制介面）

57-secs-state-mapping.md（SECS 狀態）
    ├─ 引用 → 11.md（讀取內部狀態）
    ├─ 引用 → 56.md（PC1 監控判定 Down）
    └─ 引用 → 80.md（異常判定 Down）

56-pc1-status-monitor.md（PC1 監控）
    ├─ 引用 → 53.md（視覺拍照握手）
    ├─ 引用 → 57.md（觸發 Down 狀態）
    └─ 引用 → 80.md（異常代碼）
```

---

### 動作序列關係

```
30-motion-primitives.md（基本動作）
    └─ 被引用 → 31/32/33/34.md（所有序列文件）

31-motion-sequences-common.md（通用流程）
    ├─ 被引用 → 32/33/34.md（檢測序列前後流程）
    ├─ 引用 → 35.md（氣缸控制）
    └─ 引用 → 53.md（拍照握手）

32-motion-sequences-stage1.md（載台1）
    ├─ 引用 → 31.md（SEQ-001 入料前置）
    ├─ 引用 → 35.md（定位氣缸控制）
    └─ 引用 → 53.md（視覺拍照握手）

33-motion-sequences-stage2.md（載台2）
    ├─ 引用 → 31.md（SEQ-002 出料/SEQ-301 開門）
    ├─ 引用 → 35.md（定位氣缸控制）
    └─ 引用 → 53.md（LineScan 4 訊號握手）

34-motion-sequences-door.md（開門模組）
    ├─ 引用 → 31.md（SEQ-301/302 開關門流程）
    ├─ 引用 → 35.md（開蓋平台氣缸）
    └─ 引用 → 53.md（拍照握手）

35-actuator-control-reference.md（氣缸參考）
    ├─ 來源 → 23.md（執行器規格）
    └─ 來源 → 30.md（動作原語）
```

---

## 記憶體位址管理

### 位址分配原則

**已使用範圍**（需避開）：
```
DM100~273     : 各軸運動參數（29軸×6參數）
DM5000~6199   : 量測結果存放
DM6200~6315   : 各軸當前狀態
DM20000~20999 : 料號參數工作區

MR1000~1007   : 數據讀取位置控制
MR1100~1307   : 檢測序列握手訊號
MR5000~5506   : 各軸極限與原點訊號
MR5600~5603   : SECS 狀態（PM/IDLE/Run/Down）
```

**建議分配範圍**：
```
DM0~99        : 通用狀態與控制
DM2000~2999   : PC1 監控相關
MR2000~2999   : PC1 監控相關
MR5604~5699   : SECS 相關擴充
In0~99        : 通用輸入訊號
```

**完整映射** → 參考 `50-plc-memory-map.md`

---

## PLC 職責範圍

### PLC 負責
- ✅ 軸運動控制
- ✅ 序列流程管理
- ✅ 安全互鎖檢查
- ✅ 內部狀態管理（OperationMode/HomeReturnCompleted/Alarm）
- ✅ PC1 監控（WatchDog/超時檢測）
- ✅ SECS 狀態映射（PM/IDLE/Run/Down）
- ✅ 資料寫入記憶體
- ✅ 訊號握手管理

### PC1 負責
- ✅ 視覺檢測運算
- ✅ 主動讀取 PLC 記憶體
- ✅ 檢測結果寫入 Buffer
- ✅ 拍照握手回應

### PC2 負責
- ✅ HMI 顯示
- ✅ 操作介面
- ✅ SECS 通訊（讀取 PLC 狀態並上報）
- ✅ 資料記錄

### SECS 負責
- ✅ 接收設備狀態（PM/IDLE/Run/Down）
- ✅ 生產管理整合

---

## 文件維護原則

### 分工原則

1. **11.md**：只定義狀態「是什麼」，不寫「怎麼做」
2. **12.md**：只寫模式「行為差異」，不寫流程細節
3. **31~34.md**：寫動作序列「怎麼做」，不重複定義狀態
4. **35.md**：氣缸控制快速參考，詳細規格查 23.md
5. **55.md**：寫控制訊號「握手協議」，不寫序列細節
6. **80.md**：寫異常「處理流程」，不重複定義狀態

### 避免重複

- ❌ 不在多處定義同一件事
- ❌ 不在狀態文件寫流程
- ❌ 不在流程文件寫狀態定義
- ✅ 使用「參考 XX.md」指向正確文件

### 更新流程

1. 確認要修改的內容屬於哪一層
2. 只修改該層文件
3. 更新相關引用（如有必要）
4. 避免多處修改同一概念

---

## 待辦事項

### 待建立文件
- [ ] `80-alarm-management.md` - 異常代碼管理
- [ ] `55-operation-interface.md` - PC-PLC 控制介面（補充完整）

### 待補充內容
- [ ] `40-interlock-rules.md` - 維修模式條件互鎖放寬明細

### 待填寫位址
- [ ] 填寫 EXCEL 記憶體位址（18 個待填）
- [ ] 更新 `50-plc-memory-map.md`

---

## 版本記錄

| 版本 | 日期 | 修改內容 | 修改人 |
|------|------|---------|--------|
| v3.2 | 2025-12-11 | 更新 30 層架構：反映 31→35 拆分結構；更新快速查詢指南；新增動作序列關係圖；更新待辦事項 | Yao |
| v3.1 | 2025-12-09 | 更新架構說明：11.md/12.md 合併基本定義但保持分離；強化分層原則說明；更新文件關係圖；明確各文件職責邊界 | Yao |
| v3.0 | 2025-12-09 | 新增：狀態管理分層架構說明；PC1 監控獨立；50 層介面分類原則；文件關係圖 | Yao |
| v2.0 | 2025-12-07 | 新增：光柵遮蔽文件；調整操作模式定義 | Yao |
| v1.0 | 2025-12-07 | 初始版本 | Yao |

---

**最後更新**: 2025-12-11  
**維護者**: Yao
